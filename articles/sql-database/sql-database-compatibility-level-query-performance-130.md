---
title: "poziom zgodności aaaDatabase 130 — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule firma Microsoft Poznaj zalety hello systemem 130 na poziomie zgodności bazy danych SQL Azure i wykorzystanie zalet hello hello nowy Optymalizator zapytań i wyszukiwać funkcje procesora. Możemy także spełnić hello efekty uboczne na wydajność zapytań hello hello istniejących aplikacji SQL."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a>Zwiększona wydajność zapytań ze zgodnością 130 poziom w bazie danych SQL Azure
Baza danych SQL Azure działa niewidocznie setki tysięcy baz danych na wielu poziomach różnych zgodności, zachowania i gwarantujących hello zgodności z poprzednimi wersjami toohello odpowiednią wersję programu Microsoft SQL Server dla wszystkich klientów!

W tym artykule firma Microsoft Poznaj zalety hello uruchomiona z Databse SQL Azure na poziomie zgodności 130 i wykorzystanie zalet hello hello nowy Optymalizator zapytań i wyszukiwać funkcje procesora. Możemy także spełnić hello efekty uboczne na wydajność zapytań hello hello istniejących aplikacji SQL.

Dla przypomnienia historii wyrównanie hello poziomy zgodności toodefault wersji programu SQL są następujące:

* 100: w programie SQL Server 2008 i Azure SQL bazy danych V11.
* 110: w programie SQL Server 2012 i Azure SQL bazy danych V11.
* 120: w programie SQL Server 2014 i Azure SQL bazy danych w wersji 12.
* 130: w programie SQL Server 2016 i Azure SQL bazy danych w wersji 12.

> [!IMPORTANT]
> Począwszy od **środek czerwca 2016**, w bazie danych SQL Azure, hello domyślny poziom zgodności będzie 130 zamiast 120 dla **nowo utworzony** baz danych.
> 
> Bazy danych utworzone przed środek czerwca 2016 r. zostanie *nie* zmian i będzie utrzymywać ich bieżący poziom zgodności (100, 110 lub 120). Bazy danych, które są migrowane z bazy danych SQL Azure w wersji V11 tooV12 ma poziom zgodności 100 lub 110. 
> 

## <a name="about-compatibility-level-130"></a>O poziomie zgodności 130
Najpierw Jeśli chcesz tooknow hello bieżący poziom zgodności bazy danych, należy wykonać hello następującej instrukcji języka Transact-SQL.

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


Przed wprowadzeniem tej zmiany toolevel 130 odbywa się w **nowo** teraz utworzony baz danych, przejrzyj ta zmiana jest wszystko, za pośrednictwem przykładowe zapytanie bardzo proste, a Zobacz każdy korzyści z niej.

Przetwarzanie zapytań w relacyjnych baz danych może być bardzo skomplikowane i może prowadzić toolots komputera nauki i matematyce toounderstand hello związanego z używaniem decyzji projektowych i zachowania. W tym dokumencie hello zawartość została celowo uproszczona tooensure, że każda osoba mająca minimalne informacje techniczne zrozumienie wpływu zmiany poziomu zgodności hello hello i określić, jak też korzystać aplikacje.

Załóżmy ma poziom zgodności hello 130 łączy w tabeli hello krótki przegląd.  Można znaleźć więcej szczegółów na [zmienić poziom zgodności bazy danych (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), ale poniżej przedstawiono krótkie podsumowanie:

* Hello operacji wstawiania instrukcji Insert select może być wielowątkowych lub może mieć plan równoległy podczas przed jednowątkowe tej operacji.
* Pamięci tabela zoptymalizowana i tabeli Zmienne zapytania można teraz mieć równoległych planów podczas zanim ta operacja została również jednowątkowego.
* Statystyki dla tabel zoptymalizowanych pod kątem pamięci może być próbkowany i są aktualizowane automatycznie. Zobacz [What's New in aparatu bazy danych: OLTP w pamięci](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) więcej szczegółów.
* Zmiany trybu wiersza v trybu partii/s z indeksami magazynu kolumn
  * Sortuje w tabeli z indeksem magazynu kolumn są dostępne w trybie wsadowym.
  * Agreguje okien działał w trybie wsadowym, takie jak instrukcje TSQL opóźnienie/realizacji.
  * Zapytania w tabelach magazynu kolumn z wielu różnych klauzule działają w trybie wsadowym.
  * Zapytań wykonywanych w ramach DOP = 1 lub z planem serial również wykonać w trybie wsadowym.
* Ostatnio ulepszenia szacowania kardynalności faktycznie pochodzą z poziomem zgodności 120, ale dla osób, które z poziomu zgodności niższy (tj. 100 lub 110), hello przenoszenia toocompatibility poziom 130 również wywoła te ulepszenia i mogą również korzyści hello wydajność aplikacji.

## <a name="practicing-compatibility-level-130"></a>Ćwiczenie poziom zgodności 130
Pierwszy Załóż niektórych tabel, indeksy i losowe dane utworzone toopractice niektóre z nowych funkcji. Przykłady skryptów TSQL Hello mogą być wykonywane w ramach programu SQL Server 2016, lub baza danych SQL Azure. Jednak podczas tworzenia bazy danych Azure SQL, upewnij się, wybierz na powitania minimalna P2 bazy danych, ponieważ należy co najmniej kilka wielowątkowości tooallow rdzeni i w związku z tym korzystanie z tych funkcji.

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


Teraz załóżmy ma toosome wygląd, pochodzących z poziomem zgodności 130 funkcji przetwarzania zapytania hello.

## <a name="parallel-insert"></a>Wstaw równoległych
Wykonywanie instrukcji TSQL hello poniżej wykonuje hello operacja WSTAWIANIA w obszarze poziom zgodności 120 i 130, które odpowiednio wykonuje hello operacja WSTAWIANIA w jednym modelu wątków (120) i w modelu wielowątkowych (130).

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


Przez zażądanie planu zapytania rzeczywiste hello hello spojrzenie na jej reprezentację albo jej zawartość XML, można określić, które szacowania kardynalności funkcja znajduje się na play. Spojrzenie na powitania planów side-by-side na rysunku 1, firma Microsoft może wyraźnie Zobacz tego hello wykonywania Wstaw magazynu kolumn zawiera z serial w 120 tooparallel 130. Zauważ również, taka zmiana hello hello iteratora ikony w planie 130 hello przedstawiający dwa strzałki równoległe, pokazujący hello fakt, że teraz hello wykonywania iteratora jest w rzeczywistości równoległych. Jeśli masz dużą toocomplete operacji INSERT hello wykonywanie równoległe, połączonego toohello liczba rdzeni posiadanego Twojej dyspozycji hello bazy danych, będą działać lepiej; zapasowej tooa 100 razy szybsze w zależności od sytuacji!

*Rysunek 1: Wstaw operację zmiany z serial tooparallel o poziomie zgodności 130.*

![Rysunek 1.](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a>Tryb SERIAL partii
Podobnie przenoszenie poziom toocompatibility 130 podczas przetwarzania wierszy danych umożliwia przetwarzanie wsadowe tryb. Po pierwsze operacji w trybie wsadowym są dostępne tylko podczas ma indeks magazynu kolumn w miejscu. Po drugie, partii zazwyczaj reprezentuje ~ 900 wierszy i używa logiki kodu, zoptymalizowana pod kątem wielordzeniowych procesorów, wyższej przepustowości pamięci i bezpośrednio wykorzystanie hello skompresowane dane hello magazynu kolumn zawsze, gdy jest to możliwe. W tych warunkach SQL Server 2016 może przetwarzać ~ 900 wierszy jednocześnie, zamiast 1 wiersz w czasie hello, i w konsekwencji hello ogólne zmniejszenie kosztów operacji hello jest udostępniany przez całą partię hello, zmniejszenie hello ogólne koszty według wierszy. Udostępniony ilość połączonymi z kompresji magazynu kolumny hello zasadniczo zmniejsza opóźnienia hello związanego z operacją tryb Wybierz partii. Można znaleźć więcej informacji o magazynie kolumny hello i tryb w partii [przewodnik indeksy magazynu kolumn](https://msdn.microsoft.com/library/gg492088.aspx).

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Jako widoczny poniżej obserwując hello zapytania planów side-by-side na rysunku 2, zobaczysz, że tryb przetwarzania hello została zmieniona z poziomem zgodności hello, i w konsekwencji podczas wykonywania zapytania hello w obu poziom zgodności całkowicie, firma Microsoft można stwierdzić, że w większości przypadków przetwarzania hello jest przeznaczony na wiersz (86%) w porównaniu toohello partii tryb (14%), gdzie zostaną przetworzone partie 2. Zwiększ hello zestawu danych, hello korzyści zwiększy.

*Rysunek 2: Wybierz operację zmiany z trybu serial toobatch o poziomie zgodności 130.*

![Rysunek 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a>Trybie wsadowym na wykonanie sortowania
Podobne toohello powyżej, ale operacja sortowania tooa zastosowane, przejście powitania od wiersza (poziom zgodności 120) toobatch trybami (poziom zgodności 130) poprawia wydajność hello hello operacja sortowania dla hello przyczyny.

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Widoczne side-by-side na rysunku 3, zobaczysz, że operacja sortowania hello w trybie wierszowym reprezentuje 81% hello koszt podczas w trybie wsadowym hello tylko reprezentuje % 19 kosztu hello (odpowiednio 81% i % 56 sortowania hello, sam).

*Rysunek 3: Operacja sortowania zmienia tryb toobatch wiersza o poziomie zgodności 130.*

![Rysunek 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

Oczywiście te przykłady zawierają tylko dziesiątki tysięcy wierszy, które ma podczas przeglądania danych hello dostępne w większości serwerów SQL te dni. Tylko projektu są względem miliony wierszy zamiast tego, a to może dokonywać translacji za kilka minut wykonywania oszczędza codziennie oczekujących hello rodzaju obciążenia.

## <a name="cardinality-estimation-ce-improvements"></a>Ulepszenia (CE) szacowania kardynalności
Wszystkie bazy danych uruchomiony na poziomie zgodności 120 lub powyżej wprowadzonego w programie SQL Server 2014, będzie korzystać z nowych funkcji szacowania kardynalności hello. Zasadniczo szacowania kardynalności jest logiki hello używany jak programu SQL server będzie wykonywać zapytania na podstawie jej kosztu szacowany toodetermine. Szacowanie Hello jest obliczana przy użyciu danych wejściowych z statystyki związane z obiektami związanego z tej kwerendy. W praktyce, w wysokiego poziomu, funkcje szacowania kardynalności są wartościami szacunkowymi liczby wierszy wraz z informacjami o dystrybucji hello hello wartości liczby unikatowych wartości i liczby zduplikowane zawarte w hello tabele i obiekty, do których odwołuje się zapytanie hello. Uzyskiwanie szacunków błąd, może to prowadzić We/Wy dysku w toounnecessary powodu tooinsufficient przyznaje pamięci (tj. bazy danych TempDB wyciekami) lub tooa wybór wykonanie planu szeregowych, za pośrednictwem równoległego zaplanować wykonanie, tooname kilka. Zawarcia, niepoprawny szacuje może prowadzić tooan ogólną spadek wydajności hello wykonywania zapytania. Na powitania drugiej stronie lepiej szacuje, dokładniejsze szacuje, potencjalnych klientów toobetter zapytania wykonaniami!

Jak wspomniano wcześniej, optymalizację zapytania i szacuje są sprawy złożonych, ale ma więcej informacji na temat planów kwerend i narzędzia do szacowania kardynalności toolearn mogą odwoływać się dokumentu toohello [optymalizacji Your plany zapytań z hello programu SQL Server 2014 Narzędzia do szacowania kardynalności](https://msdn.microsoft.com/library/dn673537.aspx) dla bardziej zgłębić temat.

## <a name="which-cardinality-estimation-do-you-currently-use"></a>Które szacowania kardynalności obecnie używasz?
toodetermine, w których działają zapytań szacowania kardynalności, umożliwia po prostu użyj hello zapytania przykłady poniżej. Należy pamiętać, że w tym przykładzie pierwsze będą uruchamiane na poziomie zgodności 110, co oznacza użycie hello hello starego szacowania kardynalności funkcji.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Po zakończeniu wykonywania, kliknij łącze XML hello i przyjrzyj hello właściwości iteratora pierwszy hello, jak pokazano poniżej. Zanotuj nazwę właściwości hello o nazwie CardinalityEstimationModelVersion aktualnie ustawione na 70. Nie oznacza to, że poziom zgodności bazy danych hello jest ustawiona wersja programu SQL Server 7.0 toohello (jest ustawiona na 110 jako widoczny w instrukcjach języka TSQL hello powyżej), ale hello wartość 70 po prostu reprezentuje hello starszych szacowania kardynalności funkcje dostępne od SQL Serwer 7.0, który miał żadnych głównych poprawek do programu SQL Server 2014 (który pochodzi z poziomem zgodności 120).

*Rysunek 4: hello CardinalityEstimationModelVersion ustawiono too70 używając poziomie zgodności 110 lub poniżej.*

![Rysunek 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

Alternatywnie można zmienić too130 poziomu zgodności hello i wyłączyć hello korzystanie z nowej funkcji szacowania kardynalności hello przy użyciu hello LEGACY_CARDINALITY_ESTIMATION ustawić tooON z [ALTER konfiguracji bazy danych o zakresie](https://msdn.microsoft.com/library/mt629158.aspx). To będzie można dokładnie hello taki sam jak przy użyciu 110 z szacowania kardynalności funkcja punktu widzenia, używając najnowszej kwerendy hello przetwarzania poziom zgodności. Dzięki temu można korzystać z nowej kwerendy hello przetwarzania funkcje pochodzące z najnowszą hello poziom zgodności (tj. w trybie wsadowym), ale nadal zależne od hello starego szacowania kardynalności funkcji w razie potrzeby.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Po prostu przenoszenie poziom zgodności toohello 120 lub 130 umożliwia hello nowych funkcji szacowania kardynalności. W takim przypadku domyślnego hello CardinalityEstimationModelVersion zostanie ustawiona odpowiednio too120 lub 130 jako widoczna poniżej.

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


*Rysunek 5: hello CardinalityEstimationModelVersion ustawiono too130 korzystając z poziomu zgodności 130.*

![Rysunek 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a>Naocznych kontrolach hello szacowania kardynalności różnic
Teraz umożliwia uruchamianie nieco bardziej złożone zapytania dotyczące INNER JOIN z klauzuli WHERE, z niektórych predykaty i Przyjrzyjmy się szacowana liczba wierszy powitania od starego funkcja szacowania kardynalności hello najpierw.

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Wykonywanie tej kwerendy skutecznie zwraca 200,704 wierszy podczas szacowania wiersza hello z hello starego szacowania kardynalności funkcji oświadczeń 194,284 wierszy. Oczywiście jak już wspomniano, przed, te wyniki liczby wierszy również zależy od częstotliwości uruchomiono hello poprzedniej próbki, który wypełnia hello Przykładowe tabele wielokrotnie przy każdym uruchomieniu. Oczywiście predykaty hello kwerendy będą także mieć wpływ na rzeczywiste szacowania hello jako uzupełnienie hello tabeli kształtu, danych i jak te dane są faktycznie skorelowania ze sobą.

*Rysunek 6: hello wiersza liczba szacuje się, 194,284 lub 6000 wierszy poza hello wierszy 200,704 oczekiwano.*

![Rysunek 6.](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

W hello tak samo, umożliwia teraz wykonywanie hello samo zapytanie z nowych funkcji szacowania kardynalności hello.

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Spojrzenie na powitania poniżej, możemy teraz Zobacz tego hello wiersza szacuje się, że 202,877, lub znacznie ściślejszej i wyższe niż hello starego szacowania kardynalności.

*Rysunek 7: szacowana liczba wierszy hello jest teraz 202,877 zamiast 194,284.*

![Rysunek 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

W rzeczywistości hello zestaw wyników jest 200,704 wierszy (ale wszystkie zależy, jak często zostało uruchomione hello zapytań hello ich w poprzedniej próbki, ale co ważniejsze, ponieważ hello TSQL używa instrukcji RAND() hello, hello rzeczywiste wartości zwracane mogą się różnić od jednego toohello uruchomienia obok). W związku z tym w tym przykładzie hello nowego szacowania kardynalności oznacza lepsze zadania na szacowanie hello liczbę wierszy, ponieważ 202,877 jest znacznie bliżej too200, 704, niż 194,284! Ostatnia zmiana hello klauzuli WHERE predykaty tooequality (zamiast ">" dla wystąpienia), to może spowodować szacuje hello między hello starych i nowych funkcji Kardynalność jeszcze bardziej różne, w zależności od tego, ile dopasowań można uzyskać.

Oczywiście w tym przypadku jest wierszy ~ 6000 poza od rzeczywistej liczby nie reprezentuje dużą ilość danych w niektórych sytuacjach. Teraz, Przestaw tego toomillions wierszy w kilku tabel i bardziej złożonych kwerend i w czasie hello szacowania można wyłączyć przez miliony wierszy i w związku z tym hello ryzyka błędne plan wykonania lub żądanie za mało pamięci przyznaje wiodące hello pobrania w górę wyciekami tooTempDB i dlatego więcej operacji We/Wy są znacznie wyższa.

Jeśli masz możliwość hello ćwiczenie to porównanie z najbardziej typowych zapytania i zestawy danych i zobacz, przez ile niektóre hello szacuje stary i nowy jest narażony, gdy niektóre można tylko staną się bardziej off w rzeczywistości hello lub niektóre inne wystarczy po prostu bliżej toohello wiersza rzeczywistej liczby faktycznie zwracane w zestawach wyników hello. Wszystkie z nich zależy od kształtu hello zapytania, właściwości bazy danych Azure SQL hello, charakter hello i rozmiar hello zestawów danych i dostępne o nich statystyki hello. Jeśli właśnie utworzony z wystąpienie bazy danych SQL Azure, zapytania hello Optymalizator będzie mieć toobuild uruchamia jej wiedzy od początku zamiast ponowne używanie statystyki z hello poprzednie zapytanie. Tak szacuje hello są bardzo kontekstowe i prawie określonych tooevery sytuacji serwera i aplikacji. Jest istotnym elementem tookeep pamiętać!

## <a name="some-considerations-tootake-into-account"></a>Niektóre tootake uwagi pod uwagę
Mimo że większość obciążeń korzystałby z poziomu zgodności hello 130, przed przyjmowanie hello poziom zgodności dla środowiska produkcyjnego, masz zasadniczo 3 opcje:

1. Przenieś poziom toocompatibility 130 i zobacz, jak wykonać czynności. W przypadku można zauważyć pewne regresji, wystarczy po prostu ustawić tooits wstecz poziomu zgodności hello oryginalnego poziomu lub 130, a ich anulować tylko hello szacowania kardynalności wstecz toohello ze starszej wersji trybu (zgodnie z powyższymi wskazówkami, to samodzielnie można rozwiązać hello problem).
2. Należy dokładnie przetestować istniejących aplikacji pod obciążeniem produkcji podobne, dostrojenia i Zweryfikuj wydajność hello przed przejściem tooproduction. W przypadku problemów taki sam jak powyżej, możesz zawsze wrócić do poprzedniej strony toohello oryginalnego poziom zgodności, lub po prostu odwrócić hello szacowania kardynalności wstecz toohello ze starszej wersji trybu.
3. Jako ostatnia opcja i hello najnowszych tooaddress sposób te pytania, jest magazyn zapytań hello tooleverage. To zalecana opcja współczesnych! Analiza hello tooassist zapytań w obszarze zgodności poziomie 120 lub poniżej i 130, nie zachęcamy za mało toouse magazynu zapytań. Magazyn zapytań jest dostępne w najnowszej wersji bazy danych SQL Azure V12 hello i jest przeznaczona toohelp możesz z rozwiązywaniem problemów wydajności zapytania. Witaj magazynu zapytań można traktować jako rejestrator danych zbierania i prezentować szczegółowe informacje historyczne na temat wszystkich zapytań bazy danych. To znacznie upraszcza dowodowe wydajność dzięki zmniejszeniu hello czas toodiagnose i rozwiązać problemy. Więcej informacji można znaleźć [magazyn zapytań: Rejestrator danych dla bazy danych](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).

Na powitania wysokiego poziomu, jeśli już masz zestaw baz danych uruchomionych na poziomie zgodności 120 lub poniżej i Zaplanuj toomove niektóre z nich too130, lub ponieważ obciążenie automatycznie obsługi administracyjnej nowych baz danych, które będą wkrótce będzie można ustawić domyślnego too130, rozważ Witaj następujących wartości:

* Przed zmianą toohello nowy poziom zgodności w środowisku produkcyjnym, Włącz magazyn zapytań. Można odwoływać się za[zmienić hello trybu zgodności bazy danych i użyj hello magazynu zapytań](https://msdn.microsoft.com/library/bb895281.aspx) Aby uzyskać więcej informacji.
* Następnie przetestuj wszystkich krytycznych obciążeń przy użyciu danych reprezentatywnych i zapytań środowiska przypominającej środowisko produkcyjne, i porównaj hello wydajności wystąpił i jako zgłoszony przez Magazyn zapytań. Jeśli występują pewne regresji, można go zidentyfikować hello uwzględniona zapytania z hello magazyn zapytań i użyj planu hello wymuszania opcję magazynu zapytań (Planowanie alias przypinanie). W takim przypadku możesz ostatecznie pozostać o poziomie zgodności hello 130 i użyć planu zapytania wcześniejsze hello sugerowanej hello magazynu zapytań.
* Tooleverage nowe funkcje i możliwości usługi Azure SQL Database (na którym jest uruchomiony program SQL Server 2016), ale są toochanges poufnych przez 130, poziom zgodności hello w ostateczności można rozważyć wymuszania hello wstecz poziom zgodności poziom toohello pasujące obciążenia przy użyciu instrukcji ALTER DATABASE. Najpierw należy jednak pamiętać, że plan magazynu zapytań hello przypinanie opcji jest najlepszym wyjściem, ponieważ nie używa 130 przebywa zasadniczo na poziomie funkcjonalności hello w starszej wersji programu SQL Server.
* Jeśli masz wielodostępnych aplikacji obejmujących wiele baz danych, może być konieczne tooupdate hello inicjowania obsługi logiki tooensure Twojego baz danych poziom zgodności spójne dla wszystkich baz danych; stary i nowo aprowizowanej z nich. Na wydajność obciążenia aplikacji może być poufnych toohello fakt, że niektóre bazy danych są uruchomione na zgodność z różnych poziomach i w związku z tym spójności poziomu zgodności przez wszystkie bazy danych może być wymagane w porządku tooprovide hello takie same środowisko klientów tooyour wszystkie między hello tablicy. Należy pamiętać, że nie ma upoważnienia naprawdę jest zależna od wpływ hello poziom zgodności aplikacji.
* Ostatnio, dotyczące hello szacowania kardynalności oraz jak zmiana poziomu zgodności hello, przed kontynuowaniem w środowisku produkcyjnym, jest zalecane tootest obciążenie produkcji w obszarze hello nowe warunki toodetermine, jeśli aplikacja korzysta z ulepszenia szacowania kardynalności Hello.

## <a name="conclusion"></a>Podsumowanie
Za pomocą usługi Azure SQL Database toobenefit z wszystkie rozszerzenia SQL Server 2016 wyraźnie może zwiększyć Twojej wykonania zapytania. Podobnie jak-jest! Oczywiście takich jak nowa funkcja poprawna ocena muszą być konfigurowane toodetermine hello dokładne warunki na jakich obciążenie bazy danych działa hello najlepiej. Środowisko informuje, że większość obciążeń umożliwiają oczekiwanego tooat najmniej uruchamiana niewidocznie poziom zgodności 130, podczas korzystania z nowego zapytania przetwarzania, funkcje i nowego szacowania kardynalności. Będący powiedział realistycznie rzecz biorąc, są zawsze niektóre wyjątki i wykonując prawidłowego ukończenia starannością toodetermine oceny ważne, ile będzie można korzystać z tych rozszerzeń. I ponownie hello magazynu zapytań może być dużą pomocy w tym tę pracę!

W miarę rozwoju środowisko SQL Azure, można oczekiwać, że poziom zgodności 140 w hello przyszłych. Gdy czas jest odpowiednie, firma Microsoft rozpocznie się mówić co ten poziom zgodności w przyszłości 140 zostanie wyświetlone, tak samo, jak pokrótce omówiono tutaj 130 poziom zgodności jest Przywracanie dzisiaj.

Teraz załóżmy nie zapomnij, od czerwca 2016 r. bazy danych SQL Azure ulegnie zmianie hello domyślny poziom zgodności z too130 120 dla nowo utworzonej bazy danych. Należy pamiętać!

## <a name="references"></a>Dokumentacja
* [Nowości w aparacie bazy danych](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [Blog: Magazyn zapytań: Rejestrator danych dla bazy danych, przez Borko Novakovic, czerwca 2016 8](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [Poziom zgodności bazy danych zmiany (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)
* [ZMIANY W ZAKRESIE KONFIGURACJI BAZY DANYCH](https://msdn.microsoft.com/library/mt629158.aspx)
* [Poziom zgodności 130 bazy danych Azure SQL V12](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [Optymalizacja Your plany zapytań z programu SQL Server 2014 narzędzia do szacowania kardynalności hello](https://msdn.microsoft.com/library/dn673537.aspx)
* [Przewodnik indeksy magazynu kolumn](https://msdn.microsoft.com/library/gg492088.aspx)
* [Blog: Ulepszone zapytania wydajności o poziomie zgodności 130 w bazie danych Azure SQL, przez Alain Lissoir maj 2016 6](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
