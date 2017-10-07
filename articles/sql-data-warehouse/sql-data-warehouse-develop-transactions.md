---
title: "aaaTransactions w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące implementowania transakcji w magazynie danych SQL Azure związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a>Transakcje w usłudze SQL Data Warehouse
Jak można oczekiwać, Magazyn danych SQL obsługuje transakcje jako część obciążenia magazynu danych hello. Jednak tooensure hello wydajności usługi SQL Data Warehouse jest zachowywana na dużą skalę, niektóre funkcje są ograniczone, kiedy porównaniu tooSQL serwera. W tym artykule wyróżnia różnice hello i list hello innych użytkowników. 

## <a name="transaction-isolation-levels"></a>Poziom izolacji transakcji
Usługa SQL Data Warehouse implementuje transakcje ACID. Hello izolacji Obsługa transakcyjna hello jest jednak ograniczona zbyt`READ UNCOMMITTED` i nie można zmienić. Można zaimplementować wiele metod kodowania, które tooprevent zanieczyszczone odczytuje danych, jeśli jest to istotny. Witaj najpopularniejszych metod wykorzystać CTAS i przełączanie partycji tabeli (często określane jako hello wzorca przesuwanego okna) tooprevent użytkownikom wykonywanie zapytania na danych, który jest nadal przygotowany. Widoki danych filtr wstępny hello jest również popularnych podejście.  

## <a name="transaction-size"></a>Rozmiar transakcji
Rozmiar jest ograniczony transakcji modyfikacji danych. Hello limit dzisiaj jest stosowana "dystrybucji". W związku z tym hello całkowitej alokacji Oblicza iloczyn hello limit liczby dystrybucji hello. tooapproximate hello maksymalną liczbę wierszy w transakcji hello dzielenia zakończenia dystrybucji hello przez hello całkowity rozmiar każdego wiersza. Dla kolumn o zmiennej długości należy wziąć pod uwagę biorąc długość kolumny średni zamiast hello maksymalny rozmiar.

W tabeli hello poniżej hello zostały wprowadzone następujące założenia:

* Wystąpił nawet rozkład danych 
* Długość wiersza średni Hello jest 250 bajtów

| [JEDNOSTKA DWU][DWU] | Cap na dystrybucji (GiB) | Liczba dystrybucji | Maksymalny rozmiar transakcji (GiB) | # Wierszy na dystrybucji | Maksymalna liczba wierszy na transakcję |
| --- | --- | --- | --- | --- | --- |
| DW100 |1 |60 |60 |4,000,000 |240,000,000 |
| DW200 |1.5 |60 |90 |6 000 000 |360,000,000 |
| DW300 |2.25 |60 |135 |9,000,000 |540,000,000 |
| DW400 |3 |60 |180 |12,000,000 |720,000,000 |
| DW500 |3.75 |60 |225 |15,000,000 |900,000,000 |
| DW600 |4.5 |60 |270 |18,000,000 |1,080,000,000 |
| DW1000 |7.5 |60 |450 |30,000,000 |1,800,000,000 |
| DW1200 |9 |60 |540 |36,000,000 |2,160,000,000 |
| DW1500 |11.25 |60 |675 |45,000,000 |2,700,000,000 |
| DW2000 |15 |60 |900 |60,000,000 |3,600,000,000 |
| DW3000 |22.5 |60 |1,350 |90,000,000 |5,400,000,000 |
| DW6000 |45 |60 |2,700 |180,000,000 |10,800,000,000 |

limit rozmiaru transakcji Hello jest stosowane osobno do każdej operacji lub transakcji. Nie została zastosowana we wszystkich równoczesnych transakcji. W związku z tym każda transakcja jest dozwolone toowrite ilość danych toohello dziennika. 

toooptimize i zminimalizować ilość hello zapisanych dziennika toohello danych można znaleźć toohello [transakcji najlepsze rozwiązania] [ Transactions best practices] artykułu.

> [!WARNING]
> Maksymalny rozmiar transakcji można osiągnąć jedynie dla skrótu lub tabele ROUND_ROBIN rozproszonych gdzie hello rozprzestrzeniania się hello danych Hello jest parzysta. Jeśli transakcji hello zapisuje dane w sposób spowodowałoby zafałszowanie dystrybucje toohello następnie hello limit jest prawdopodobnie toobe osiągnął toohello poprzednich transakcji maksymalny rozmiar.
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a>Stan transakcji
Usługa SQL Data Warehouse używa hello XACT_STATE() funkcja tooreport transakcji nie powiodło się przy użyciu wartości hello -2. Oznacza to, że hello transakcji nie powiodło się i jest oznaczony do wycofania tylko

> [!NOTE]
> Witaj użyć-2 toodenote funkcja XACT_STATE hello nieudanych transakcji tooSQL inaczej reprezentuje serwera. Program SQL Server używa hello wartość -1 toorepresent której transakcji. SQL Server może tolerować błędy wewnątrz transakcji bez konieczności toobe oznaczony jako której. Na przykład `SELECT 1/0` może spowodować błąd, ale nie wymusić transakcji, w której stan. SQL Server umożliwia również odczytów w hello której transakcji. Jednak usługa SQL Data Warehouse nie zezwala na to zrobić. W przypadku wystąpienia błędu wewnątrz transakcji SQL Data Warehouse automatycznie wprowadzi stanu hello -2 i nie będą mogli toomake wszelkie dodatkowe wybierz instrukcje dopóki instrukcji hello została wycofana. Dlatego jest ważne toocheck czy toosee kodu aplikacji, gdy jest używana podczas XACT_STATE() może być konieczne toomake modyfikacji kodu.
> 
> 

Na przykład w programie SQL Server można napotkać transakcji, która wygląda następująco:

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Jeśli pozostanie kodu, ponieważ jest powyżej zostanie wyświetlony następujący komunikat o błędzie hello:

Msg 111233, poziom 16, stan 1 wiersz 1 111233; hello bieżąca transakcja została przerwana, a wszystkie oczekujące zmiany mają została wycofana. Przyczyna: W stanie tylko do wycofania transakcji nie zostało jawnie wycofane przed DDL i DML instrukcji SELECT.

Nie również otrzymasz dane wyjściowe hello hello ERROR_ * funkcji.

W usłudze SQL Data Warehouse kodu hello musi toobe nieco zmodyfikowany:

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Hello oczekuje się, że zachowanie jest teraz przestrzegane. Błąd Hello w transakcji hello jest zarządzana i hello ERROR_ * funkcji Podaj wartości, zgodnie z oczekiwaniami.

Zmieniono jest tym hello `ROLLBACK` z hello transakcji wcześniej toohappen hello odczytu informacji o błędach hello w hello `CATCH` bloku.

## <a name="errorline-function"></a>ERROR_LINE() — funkcja
Warto również zauważyć, że usługi SQL Data Warehouse wdrożenia lub nie obsługuje hello ERROR_LINE() — funkcja. Jeśli masz to w kodzie należy tooremove go toobe zgodne z usługą Magazyn danych SQL. W zamian użyj etykiet zapytania w kodzie tooimplement równoważne funkcje. Zobacz toohello [etykiety] [ LABEL] artykułu, aby uzyskać więcej informacji na temat tej funkcji.

## <a name="using-throw-and-raiserror"></a>Przy użyciu THROW i RAISERROR
THROW jest hello nowoczesną wykonania na występowanie wyjątków w usłudze SQL Data Warehouse, ale obsługiwana jest również RAISERROR. Istnieje kilka różnic, które warto płatności toohowever uwagi.

* Komunikaty o błędach cyfr nie może być w hello 150 000 100 000 zakres THROW zdefiniowane przez użytkownika
* Komunikaty o błędach RAISERROR są ustalone na poziomie 50 000
* Korzystanie z widoku sys.messages nie jest obsługiwane.

## <a name="limitiations"></a>Limitiations
Magazyn danych SQL ma kilka ograniczeń, które odnoszą się tootransactions.

Są one w następujący sposób:

* Nie transakcji rozproszonych
* Nie transakcji zagnieżdżonych dozwolone
* Bez zapisu punkty dozwolone
* Brak transakcji o nazwie
* Nie zaznaczonych transakcji
* Brak obsługi języka DDL, takie jak `CREATE TABLE` wewnątrz użytkownika zdefiniowanych transakcji

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat optymalizacji transakcji, zobacz [transakcji najlepsze rozwiązania][Transactions best practices].  toolearn dotyczące innych najlepszych rozwiązań usługi SQL Data Warehouse, zobacz [najlepsze rozwiązania w zakresie usługi SQL Data Warehouse][SQL Data Warehouse best practices].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
