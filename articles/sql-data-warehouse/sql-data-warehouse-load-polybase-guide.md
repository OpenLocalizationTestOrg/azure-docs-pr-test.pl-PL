---
title: "aaaGuide dla przy użyciu programu PolyBase w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wskazówki i zalecenia dotyczące przy użyciu programu PolyBase w scenariuszach SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a>Przewodnik dla przy użyciu programu PolyBase w usłudze SQL Data Warehouse
Ten przewodnik zawiera informacje praktyczne dla przy użyciu programu PolyBase w usłudze SQL Data Warehouse.

tooget pracę, zobacz hello [ładowanie danych przy użyciu programu PolyBase] [ Load data with PolyBase] samouczka.

## <a name="rotating-storage-keys"></a>Obracanie magazynu kluczy
Od czasu tootime można magazynu obiektów blob klucza tooyour toochange hello dostęp ze względów bezpieczeństwa.

Witaj najbardziej elegancki tooperform sposób, to zadanie jest toofollow w ramach procesu nazywanego "obracanie klucze hello". Można zauważyć ma dwa klucze magazynu dla konta magazynu obiektów blob. Jest to, aby można przejść

Obracanie klucze konta magazynu platformy Azure jest procesem prosty krok trzy

1. Utworzyć drugi poświadczeń o zakresie bazy danych na podstawie klucza dostępu do magazynu pomocniczego hello
2. Utworzyć drugi zewnętrznego źródła danych poza tym nowe poświadczenie
3. Usunąć i utworzyć tabel zewnętrznych hello wskazanie toohello nowego zewnętrznego źródła danych

Po dokonaniu migracji wszystkich tabel zewnętrznych toohello nowego zewnętrznego źródła danych, a następnie można wykonać hello wyczyścić zadań:

1. Usuń pierwszy zewnętrznego źródła danych
2. Poświadczeń, klucz dostępu do magazynu podstawowego hello w oparciu o zakresie pierwszy Porzuć bazę danych
3. Zaloguj się do platformy Azure i ponownie wygenerować klucza dostępu podstawowy hello gotowe do hello następnym

## <a name="query-azure-blob-storage-data"></a>Zapytania na danych magazynu obiektów blob platformy Azure
Zapytania dotyczące tabel zewnętrznych po prostu użyć nazwy tabeli hello tak, jakby był relacyjne tabeli.

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> Zapytania w tabeli zewnętrznej może zakończyć się niepowodzeniem z powodu błędu hello *"zapytanie zostało przerwane — podczas odczytu z zewnętrznego źródła Osiągnięto próg maksymalnej Odrzuć hello"*. Oznacza to, że dane zewnętrzne zawiera *zanieczyszczone* rekordów. Rekord danych jest uznawany za "zakłócone", jeśli hello rzeczywiste dane typy/liczba kolumn nie zgadzają hello definicje kolumn z tabeli zewnętrznej hello lub hello danych nie jest zgodna z toohello określonego zewnętrznego formatu pliku. toofix, sprawdź, czy poprawność tabeli zewnętrznej i definicje format pliku zewnętrznego, jak i dane zewnętrzne zgodne toothese definicje. W przypadku, gdy podzbiór rekordów danych zewnętrznych zostały zmienione, możesz wybrać tooreject te rekordy zapytań przy użyciu opcji Odrzuć hello utworzyć DDL tabeli zewnętrznej.
> 
> 

## <a name="load-data-from-azure-blob-storage"></a>Ładowanie danych usługi Azure Blob Storage
W tym przykładzie ładuje dane z bazy danych Data Warehouse tooSQL magazynu obiektów blob platformy Azure.

Zapisywanie danych bezpośrednio usuwa hello czas transferu danych zapytań. Przechowywanie danych z indeksem magazynu kolumn poprawia wydajność kwerendy analizy zapytań przez się too10x.

W tym przykładzie używane dane tooload instrukcji CREATE TABLE AS SELECT hello. Nowa tabela Hello dziedziczy hello kolumny o nazwie w zapytaniu hello. W definicji tabeli zewnętrznej hello dziedziczy hello typy danych tych kolumn.

CREATE TABLE AS SELECT jest wysokiej wydajności instrukcji języka Transact-SQL, która ładuje dane hello w hello równoległych tooall obliczeniowe węzłów magazynu danych SQL.  Pierwotnie został opracowany dla aparatu masowego przetwarzania równoległego (MPP) hello w Analytics Platform System, a jest teraz w usłudze SQL Data Warehouse.

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

Zobacz [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].

## <a name="create-statistics-on-newly-loaded-data"></a>Tworzenie statystyk na nowo załadowanych danych
Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.  W kolejności tooget hello najlepszą wydajność zapytań należy utworzyć statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu hello lub każdej istotnej zmianie występują w danych hello.  Aby uzyskać szczegółowy opis statystyk, zobacz hello [statystyki] [ Statistics] tematu w hello grupie artykułów dla programistów.  Poniżej przedstawiono sposób toocreate statystyk na powitania przedłożenia załadowany w tym przykładzie przedstawiono prosty przykład.

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a>Eksportowanie danych tooAzure obiektu blob magazynu
W tej sekcji przedstawiono, jak magazynu obiektów blob danych tooexport z tooAzure SQL Data Warehouse. W tym przykładzie użyto, tworzenie zewnętrznych TABLE AS SELECT czyli wysokiej wydajności języka Transact-SQL instrukcji tooexport hello danych równolegle z dowolnych węzłów obliczeniowych hello.

Witaj poniższy przykład tworzy tabelę zewnętrzną Weblogs2014 przy użyciu definicje kolumn i danych z dbo. Tabela dzienników sieci Web. definicji tabeli zewnętrznej hello są przechowywane w magazynie danych SQL i wyniki hello instrukcji SELECT hello są wyeksportowanego toohello określony przez źródło danych hello kontener obiektów blob hello do katalogu "/ archiwum/log2014 /". Witaj dane są eksportowane w formacie pliku hello określony tekst.

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a>Izolowanie podczas ładowania użytkowników
Brak często toohave potrzeba wielu użytkowników, które można załadować danych do magazynu danych SQL. Ponieważ hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] wymaga uprawnienia kontroli hello bazy danych, spowoduje utworzenie z wieloma użytkownikami z kontroli dostępu za pośrednictwem wszystkich schematów. toolimit, można użyć instrukcji sterowania ODMÓW hello.

Przykład: Należy wziąć pod uwagę schema_A schematów bazy danych dla działu A i schema_B dla działu B Let bazy danych użytkowników user_A i user_B można użytkowników dla ładowanie w Dział A i B, odpowiednio PolyBase. Oba przyznano uprawnienia kontroli bazy danych.
twórcy Hello schematu, A i B teraz zablokowanie ich schematów przy użyciu odmowy:

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 O tym, user_A i user_B powinna teraz zostać zablokowane z hello schematu innego działu.
 


## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat przenoszenia tooSQL danych magazynu danych, zobacz hello [Omówienie migracji danych][data migration overview].

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
