---
title: "procedury aaaStored w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące implementowania procedur przechowywanych w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a>Procedury składowane w usłudze SQL Data Warehouse
Magazyn danych SQL obsługuje wiele funkcji języka Transact-SQL hello dostępnych w programie SQL Server. Są ważniejsze skalowania w poziomie określonych funkcji, firma Microsoft będzie tooleverage toomaximize hello wydajność rozwiązania.

Toomaintain hello skalowalność i wydajność usługi SQL Data Warehouse są jednak także pewne funkcje i możliwości, mające różnice funkcjonalne i inne osoby, które nie są obsługiwane.

W tym artykule opisano, jak tooimplement przechowywanych procedur w usłudze SQL Data Warehouse.

## <a name="introducing-stored-procedures"></a>Wprowadzenie do procedury składowane
Procedury składowane są to dobry sposób na hermetyzując kodu SQL; przechowywanie ich danych zamknij tooyour w hello hurtowni danych. Hermetyzując hello kodu w jednostki zarządzane procedur składowanych pomóc deweloperom modularyzacji ich rozwiązań. ułatwianie większa ponownego wykorzystywania kodu. Każdej procedury składowanej także zaakceptować toomake parametry im bardziej elastyczne.

Magazyn danych SQL zawiera implementację uproszczony i zoptymalizowany procedury składowanej. Witaj największych różnicę w porównaniu tooSQL serwera jest który hello procedury składowanej nie jest wstępnie skompilowanego kodu. W hurtowni danych możemy dotyczy ogólnie mniej hello czas kompilacji. Jest większe znaczenie kodu procedury przechowywane hello poprawnie są zoptymalizowane podczas działania względem dużych ilości danych. Celem Hello jest toosave godziny, minuty i sekundy nie milisekund. Dlatego jest bardziej użyteczne toothink procedur składowanych jako kontenery logiki SQL.     

Gdy usługi SQL Data Warehouse wykonuje instrukcji SQL procedury składowanej hello są przeanalizować, translacji i zoptymalizowany w czasie wykonywania. W trakcie tego procesu każda instrukcja jest konwertowany na zapytań rozproszonych. Witaj kodu SQL, który faktycznie jest wykonywane względem danych hello jest kwerenda różnych toohello przesłane.

## <a name="nesting-stored-procedures"></a>Procedury przechowywane zagnieżdżenia
Jeśli procedury składowane wywołania innych procedur składowanych lub wykonać dynamicznej sql, a następnie procedurę składowaną wewnętrzny hello lub wywołanie kodu jest nazywany toobe zagnieżdżone.

Magazyn danych SQL obsługuje maksymalnie 8 poziomów zagnieżdżenia. Jest to tooSQL nieco inny serwer. poziom zagnieżdżania Hello w programie SQL Server to 32.

Wywołanie najwyższego poziomu procedury składowanej Hello oznacza toonest poziomu 1

```sql
EXEC prc_nesting
```
Jeśli hello przechowywane procedury powoduje EXEC innego wywołania, spowoduje to zwiększenie too2 poziomu zagnieżdżania hello

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
Jeśli drugiej procedury hello następnie wykonuje niektóre dynamiczne sql następnie zwiększy to too3 poziomu zagnieżdżania hello

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

Uwaga SQL Data Warehouse nie obsługuje obecnie@NESTLEVEL. Konieczne będzie tookeep ścieżką poziom zagnieżdżania samodzielnie. Jest mało prawdopodobne, nastąpi trafienie poziomu limit zagnieżdżania hello 8, ale jeśli użytkownik czy należy toore pracy kodu, a "spłaszczanie" go tak, aby zmieścił się w ten limit.

## <a name="insertexecute"></a>INSERT... WYKONANIE
Usługa SQL Data Warehouse pozwala tooconsume hello zestawu wyników procedury składowanej z instrukcji INSERT. Istnieje jednak alternatywne podejście, których można użyć.

Zobacz toohello poniższego artykułu [tabel tymczasowych] na przykład o tym, jak toodo to.

## <a name="limitations"></a>Ograniczenia
Brak niektórych aspektów procedury przechowywanej Transact-SQL, które nie są zaimplementowane w usłudze SQL Data Warehouse.

Są to:

* tymczasowych procedur składowanych
* numerowane procedury składowane
* rozszerzone procedury składowane
* Procedur składowanych CLR
* Opcja szyfrowania
* opcji replikacji
* Parametry przechowywanymi w tabeli
* Parametry tylko do odczytu
* domyślne parametry
* Kontekst wykonywania
* Return — instrukcja

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].

<!--Image references-->

<!--Article references-->
[tabel tymczasowych]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
