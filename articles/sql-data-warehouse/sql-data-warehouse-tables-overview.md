---
title: "aaaOverview tabel w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: Wprowadzenie do tabel magazynu danych SQL Azure.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 2114d9ad-c113-43da-859f-419d72604bdf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/29/2016
ms.author: shigu;jrj
ms.openlocfilehash: 4edabcb4b0754bf6c99c2b6b3f0c077749051d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a>Przegląd tabel w usłudze SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Omówienie][Overview]
> * [Typy danych][Data Types]
> * [Dystrybuuj][Distribute]
> * [Indeks][Index]
> * [Partycji][Partition]
> * [Statystyki][Statistics]
> * [Tymczasowe][Temporary]
> 
> 

Wprowadzenie do tworzenia tabel w usłudze SQL Data Warehouse jest proste.  podstawowe Hello [CREATE TABLE] [ CREATE TABLE] składni następuje hello składni wspólnej najprawdopodobniej już znasz Praca z innych baz danych.  toocreate tabelę, wystarczy tooname tabeli nazwy kolumn i definiowanie typów danych dla każdej kolumny.  Jeśli już tworzenie tabel w innych bazach danych, to powinno wyglądać bardzo znanych tooyou.

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

Witaj powyżej przykład tworzy tabeli o nazwie klientów z dwiema kolumnami, imię i nazwisko.  Każda kolumna jest zdefiniowana z typem danych VARCHAR(25), co ogranicza hello danych too25 znaków.  Te atrybuty podstawowych w tabeli, a także innych osób, przede wszystkim są hello jak w przypadku innych baz danych.  Typy danych są zdefiniowane dla każdej kolumny i zapewnienia hello integralność danych.  Indeksy można dodać tooimprove wydajność dzięki zmniejszeniu we/wy.  Partycjonowanie mogą być dodawane tooimprove wydajności podczas należy toomodify danych.

[Zmiana nazwy] [ RENAME] tabeli SQL Data Warehouse wygląda następująco:

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a>Rozproszone tabele
Nowy atrybut podstawowych wynikające z systemów rozproszonych, takich jak SQL Data Warehouse jest hello **kolumny dystrybucji**.  Kolumna dystrybucji Hello jest znacznie co wydaje się jak.  Jest hello kolumny, która określa, jak toodistribute, lub dzielenia, dane w tle hello.  Po utworzeniu tabeli bez określania hello dystrybucji kolumny tabeli hello jest automatycznie dystrybuowany za pomocą **działanie okrężne**.  Działanie okrężne tabele mogą być wystarczające w niektórych scenariuszach, definiowania kolumn dystrybucji może znacznie zmniejszyć przenoszenia danych podczas wykonywania kwerend, w związku z tym optymalizacji wydajności.  W sytuacjach, w przypadku małej ilości danych w tabeli, wybierając toocreate hello tabeli z hello **replikować** typ dystrybucji kopiuje węzeł obliczeniowy tooeach danych i zapisuje przenoszenia danych w czasie wykonywania zapytania. Zobacz [Dystrybucja tabeli] [ Distribute] toolearn więcej informacji na temat tooselect kolumny dystrybucji.

## <a name="indexing-and-partitioning-tables"></a>Indeksowanie i Partycjonowanie tabel
Staną się bardziej zaawansowane za pomocą usługi SQL Data Warehouse i mają toooptimize wydajności, należy toolearn dodatkowe informacje o projektowaniu tabel.  toolearn więcej, zobacz artykuły hello na [typy danych tabeli][Data Types], [Dystrybucja tabeli][Distribute], [indeksowania tabeli] [ Index] i [partycjonowania tabeli][Partition].

## <a name="table-statistics"></a>Statystyk tabeli
Statystyki są bardzo ważne toogetting hello najlepszą wydajność poza usługą SQL Data Warehouse.  Ponieważ Magazyn danych SQL nie zostały jeszcze automatycznie utworzyć i Aktualizuj statystyki, takie jak pochodzić tooexpect w bazie danych SQL Azure, odczytywanie artykułem na [statystyki] [ Statistics] może być jednym z hello Najważniejsze artykuły odczytu tooensure otrzymasz hello najlepszą wydajność zapytań.

## <a name="temporary-tables"></a>Tabele tymczasowe
Tabele tymczasowe są tabele, które tylko istnieją na czas trwania hello logowania i nie są widoczne dla innych użytkowników.  Tabele tymczasowe można innym tooprevent dobry sposób wyświetlania wyników tymczasowego i również zmniejszyć hello potrzebę oczyszczania.  Ponieważ tabele tymczasowe również korzystać z lokalnego magazynu, umożliwiając im szybsza dla niektórych operacji.  Zobacz hello [tabeli tymczasowej] [ Temporary] artykuły, aby uzyskać więcej informacji o tabelach tymczasowych.

## <a name="external-tables"></a>Tabele zewnętrzne
Tabele zewnętrzne, znanej także jako Polybase tabele są tabel, które można wykonać zapytania z usługi SQL Data Warehouse, ale toodata punktu zewnętrzne z usługi SQL Data Warehouse.  Na przykład tworzenia tabeli zewnętrznej toofiles punktów, które na magazyn obiektów Blob Azure.  Więcej informacji dotyczących sposobu toocreate i zapytania tabeli zewnętrznej, zobacz [ładowanie danych przy użyciu programu Polybase][Load data with Polybase].  

## <a name="unsupported-table-features"></a>Funkcje nieobsługiwane tabeli
Gdy usługi SQL Data Warehouse zawiera wiele hello tej samej tabeli funkcje dostępne w innych bazach danych, brak niektórych funkcji, które nie są jeszcze obsługiwane.  Poniżej znajduje się lista niektórych hello funkcji tabeli, które nie są jeszcze obsługiwane.

| Nieobsługiwane funkcje |
| --- |
| Klucz podstawowy, kluczy obcych unikatowych i wyboru [ograniczenia tabeli][Table Constraints] |
| [Unikatowe indeksy][Unique Indexes] |
| [Kolumny obliczane][Computed Columns] |
| [Kolumny rozrzedzone][Sparse Columns] |
| [Typy definiowane przez użytkownika][User-Defined Types] |
| [Sekwencja][Sequence] |
| [Wyzwalacze][Triggers] |
| [Indeksowane widoki][Indexed Views] |
| [Synonimy][Synonyms] |

## <a name="table-size-queries"></a>Zapytania o rozmiar tabeli
Jeden prosty sposób tooidentify miejsca i używane przez tabelę w każdym dystrybucje hello 60 wierszy jest toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

Jednak przy użyciu polecenia DBCC może być dość ograniczenie.  Dynamicznych widoków zarządzania (widoków DMV) umożliwi toosee bardziej szczegółowo opisano, jak również mieć znacznie większą kontrolę nad hello wyników zapytania.  Rozpocznij od utworzenia wielu nasze przykłady tego widoku, który będzie tooby określonego w tym i innych artykułów.

```sql
CREATE VIEW dbo.vTableSizes
AS
WITH base
AS
(
SELECT 
 GETDATE()                                                             AS  [execution_time]
, DB_NAME()                                                            AS  [database_name]
, s.name                                                               AS  [schema_name]
, t.name                                                               AS  [table_name]
, QUOTENAME(s.name)+'.'+QUOTENAME(t.name)                              AS  [two_part_name]
, nt.[name]                                                            AS  [node_table_name]
, ROW_NUMBER() OVER(PARTITION BY nt.[name] ORDER BY (SELECT NULL))     AS  [node_table_name_seq]
, tp.[distribution_policy_desc]                                        AS  [distribution_policy_name]
, c.[name]                                                             AS  [distribution_column]
, nt.[distribution_id]                                                 AS  [distribution_id]
, i.[type]                                                             AS  [index_type]
, i.[type_desc]                                                        AS  [index_type_desc]
, nt.[pdw_node_id]                                                     AS  [pdw_node_id]
, pn.[type]                                                            AS  [pdw_node_type]
, pn.[name]                                                            AS  [pdw_node_name]
, di.name                                                              AS  [dist_name]
, di.position                                                          AS  [dist_position]
, nps.[partition_number]                                               AS  [partition_nmbr]
, nps.[reserved_page_count]                                            AS  [reserved_space_page_count]
, nps.[reserved_page_count] - nps.[used_page_count]                    AS  [unused_space_page_count]
, nps.[in_row_data_page_count] 
    + nps.[row_overflow_used_page_count] 
    + nps.[lob_used_page_count]                                        AS  [data_space_page_count]
, nps.[reserved_page_count] 
 - (nps.[reserved_page_count] - nps.[used_page_count]) 
 - ([in_row_data_page_count] 
         + [row_overflow_used_page_count]+[lob_used_page_count])       AS  [index_space_page_count]
, nps.[row_count]                                                      AS  [row_count]
from 
    sys.schemas s
INNER JOIN sys.tables t
    ON s.[schema_id] = t.[schema_id]
INNER JOIN sys.indexes i
    ON  t.[object_id] = i.[object_id]
    AND i.[index_id] <= 1
INNER JOIN sys.pdw_table_distribution_properties tp
    ON t.[object_id] = tp.[object_id]
INNER JOIN sys.pdw_table_mappings tm
    ON t.[object_id] = tm.[object_id]
INNER JOIN sys.pdw_nodes_tables nt
    ON tm.[physical_name] = nt.[name]
INNER JOIN sys.dm_pdw_nodes pn
    ON  nt.[pdw_node_id] = pn.[pdw_node_id]
INNER JOIN sys.pdw_distributions di
    ON  nt.[distribution_id] = di.[distribution_id]
INNER JOIN sys.dm_pdw_nodes_db_partition_stats nps
    ON nt.[object_id] = nps.[object_id]
    AND nt.[pdw_node_id] = nps.[pdw_node_id]
    AND nt.[distribution_id] = nps.[distribution_id]
LEFT OUTER JOIN (select * from sys.pdw_column_distribution_properties where distribution_ordinal = 1) cdp
    ON t.[object_id] = cdp.[object_id]
LEFT OUTER JOIN sys.columns c
    ON cdp.[object_id] = c.[object_id]
    AND cdp.[column_id] = c.[column_id]
)
, size
AS
(
SELECT
   [execution_time]
,  [database_name]
,  [schema_name]
,  [table_name]
,  [two_part_name]
,  [node_table_name]
,  [node_table_name_seq]
,  [distribution_policy_name]
,  [distribution_column]
,  [distribution_id]
,  [index_type]
,  [index_type_desc]
,  [pdw_node_id]
,  [pdw_node_type]
,  [pdw_node_name]
,  [dist_name]
,  [dist_position]
,  [partition_nmbr]
,  [reserved_space_page_count]
,  [unused_space_page_count]
,  [data_space_page_count]
,  [index_space_page_count]
,  [row_count]
,  ([reserved_space_page_count] * 8.0)                                 AS [reserved_space_KB]
,  ([reserved_space_page_count] * 8.0)/1000                            AS [reserved_space_MB]
,  ([reserved_space_page_count] * 8.0)/1000000                         AS [reserved_space_GB]
,  ([reserved_space_page_count] * 8.0)/1000000000                      AS [reserved_space_TB]
,  ([unused_space_page_count]   * 8.0)                                 AS [unused_space_KB]
,  ([unused_space_page_count]   * 8.0)/1000                            AS [unused_space_MB]
,  ([unused_space_page_count]   * 8.0)/1000000                         AS [unused_space_GB]
,  ([unused_space_page_count]   * 8.0)/1000000000                      AS [unused_space_TB]
,  ([data_space_page_count]     * 8.0)                                 AS [data_space_KB]
,  ([data_space_page_count]     * 8.0)/1000                            AS [data_space_MB]
,  ([data_space_page_count]     * 8.0)/1000000                         AS [data_space_GB]
,  ([data_space_page_count]     * 8.0)/1000000000                      AS [data_space_TB]
,  ([index_space_page_count]  * 8.0)                                   AS [index_space_KB]
,  ([index_space_page_count]  * 8.0)/1000                              AS [index_space_MB]
,  ([index_space_page_count]  * 8.0)/1000000                           AS [index_space_GB]
,  ([index_space_page_count]  * 8.0)/1000000000                        AS [index_space_TB]
FROM base
)
SELECT * 
FROM size
;
```

### <a name="table-space-summary"></a>Podsumowanie obszaru tabel
To zapytanie zwraca wiersze hello i miejsca przez tabelę.  Jest toosee dużą zapytania, tabel, które są największych tabel i czy są one okrężnego replikowane lub skrótu rozproszonych.  Dla tablic skrótów rozproszonych zawiera także hello dystrybucji kolumny.  W większości przypadków największych tabel należy skrótu rozpowszechnianej za pomocą klastrowanego indeksu magazynu kolumn.

```sql
SELECT 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
,    COUNT(distinct partition_nmbr) as nbr_partitions
,    SUM(row_count)                 as table_row_count
,    SUM(reserved_space_GB)         as table_reserved_space_GB
,    SUM(data_space_GB)             as table_data_space_GB
,    SUM(index_space_GB)            as table_index_space_GB
,    SUM(unused_space_GB)           as table_unused_space_GB
FROM 
    dbo.vTableSizes
GROUP BY 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
ORDER BY
    table_reserved_space_GB desc
;
```

### <a name="table-space-by-distribution-type"></a>Obszar tabel według typu dystrybucji
```sql
SELECT 
     distribution_policy_name
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY distribution_policy_name
;
```

### <a name="table-space-by-index-type"></a>Obszar tabel według typu indeksu
```sql
SELECT 
     index_type_desc
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY index_type_desc
;
```

### <a name="distribution-space-summary"></a>Miejsce dystrybucji podsumowania
```sql
SELECT 
    distribution_id
,    SUM(row_count)                as total_node_distribution_row_count
,    SUM(reserved_space_MB)        as total_node_distribution_reserved_space_MB
,    SUM(data_space_MB)            as total_node_distribution_data_space_MB
,    SUM(index_space_MB)           as total_node_distribution_index_space_MB
,    SUM(unused_space_MB)          as total_node_distribution_unused_space_MB
FROM dbo.vTableSizes
GROUP BY     distribution_id
ORDER BY    distribution_id
;
```

## <a name="next-steps"></a>Następne kroki
toolearn więcej, zobacz artykuły hello na [typy danych tabeli][Data Types], [Dystrybucja tabeli][Distribute], [indeksowania tabeli] [ Index], [Partycjonowania tabeli][Partition], [utrzymania statystyk tabeli] [ Statistics] i [ Tabele tymczasowe][Temporary].  Aby uzyskać więcej informacji na temat najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Load data with Polybase]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md

<!--MSDN references-->
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx
[DBCC PDW_SHOWSPACEUSED]: https://msdn.microsoft.com/library/mt204028.aspx
[Table Constraints]: https://msdn.microsoft.com/library/ms188066.aspx
[Computed Columns]: https://msdn.microsoft.com/library/ms186241.aspx
[Sparse Columns]: https://msdn.microsoft.com/library/cc280604.aspx
[User-Defined Types]: https://msdn.microsoft.com/library/ms131694.aspx
[Sequence]: https://msdn.microsoft.com/library/ff878091.aspx
[Triggers]: https://msdn.microsoft.com/library/ms189799.aspx
[Indexed Views]: https://msdn.microsoft.com/library/ms191432.aspx
[Synonyms]: https://msdn.microsoft.com/library/ms177544.aspx
[Unique Indexes]: https://msdn.microsoft.com/library/ms188783.aspx

<!--Other Web references-->
