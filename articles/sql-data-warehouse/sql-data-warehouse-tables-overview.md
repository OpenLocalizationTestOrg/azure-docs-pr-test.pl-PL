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
# <a name="overview-of-tables-in-sql-data-warehouse"></a><span data-ttu-id="3a3b2-103">Przegląd tabel w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3a3b2-103">Overview of tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="3a3b2-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="3a3b2-105">[Typy danych][Data Types]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="3a3b2-106">[Dystrybuuj][Distribute]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="3a3b2-107">[Indeks][Index]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-107">[Index][Index]</span></span>
> * <span data-ttu-id="3a3b2-108">[Partycji][Partition]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="3a3b2-109">[Statystyki][Statistics]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="3a3b2-110">[Tymczasowe][Temporary]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="3a3b2-111">Wprowadzenie do tworzenia tabel w usłudze SQL Data Warehouse jest proste.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-111">Getting started with creating tables in SQL Data Warehouse is simple.</span></span>  <span data-ttu-id="3a3b2-112">podstawowe Hello [CREATE TABLE] [ CREATE TABLE] składni następuje hello składni wspólnej najprawdopodobniej już znasz Praca z innych baz danych.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-112">hello basic [CREATE TABLE][CREATE TABLE] syntax follows hello common syntax you are most likely already familiar with from working with other databases.</span></span>  <span data-ttu-id="3a3b2-113">toocreate tabelę, wystarczy tooname tabeli nazwy kolumn i definiowanie typów danych dla każdej kolumny.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-113">toocreate a table, you simply need tooname your table, name your columns and define data types for each column.</span></span>  <span data-ttu-id="3a3b2-114">Jeśli już tworzenie tabel w innych bazach danych, to powinno wyglądać bardzo znanych tooyou.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-114">If you've create tables in other databases, this should look very familiar tooyou.</span></span>

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

<span data-ttu-id="3a3b2-115">Witaj powyżej przykład tworzy tabeli o nazwie klientów z dwiema kolumnami, imię i nazwisko.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-115">hello above example creates a table named Customers with two columns, FirstName and LastName.</span></span>  <span data-ttu-id="3a3b2-116">Każda kolumna jest zdefiniowana z typem danych VARCHAR(25), co ogranicza hello danych too25 znaków.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-116">Each column is defined with a data type of VARCHAR(25), which limits hello data too25 characters.</span></span>  <span data-ttu-id="3a3b2-117">Te atrybuty podstawowych w tabeli, a także innych osób, przede wszystkim są hello jak w przypadku innych baz danych.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-117">These fundamental attributes of a table, as well as others, are mostly hello same as other databases.</span></span>  <span data-ttu-id="3a3b2-118">Typy danych są zdefiniowane dla każdej kolumny i zapewnienia hello integralność danych.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-118">Data types are defined for each column and ensure hello integrity of your data.</span></span>  <span data-ttu-id="3a3b2-119">Indeksy można dodać tooimprove wydajność dzięki zmniejszeniu we/wy.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-119">Indexes can be added tooimprove performance by reducing I/O.</span></span>  <span data-ttu-id="3a3b2-120">Partycjonowanie mogą być dodawane tooimprove wydajności podczas należy toomodify danych.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-120">Partitioning can be added tooimprove performance when you need toomodify data.</span></span>

<span data-ttu-id="3a3b2-121">[Zmiana nazwy] [ RENAME] tabeli SQL Data Warehouse wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="3a3b2-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span></span>

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a><span data-ttu-id="3a3b2-122">Rozproszone tabele</span><span class="sxs-lookup"><span data-stu-id="3a3b2-122">Distributed tables</span></span>
<span data-ttu-id="3a3b2-123">Nowy atrybut podstawowych wynikające z systemów rozproszonych, takich jak SQL Data Warehouse jest hello **kolumny dystrybucji**.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is hello **distribution column**.</span></span>  <span data-ttu-id="3a3b2-124">Kolumna dystrybucji Hello jest znacznie co wydaje się jak.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-124">hello distribution column is very much what it sounds like.</span></span>  <span data-ttu-id="3a3b2-125">Jest hello kolumny, która określa, jak toodistribute, lub dzielenia, dane w tle hello.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-125">It is hello column that determines how toodistribute, or divide, your data behind hello scenes.</span></span>  <span data-ttu-id="3a3b2-126">Po utworzeniu tabeli bez określania hello dystrybucji kolumny tabeli hello jest automatycznie dystrybuowany za pomocą **działanie okrężne**.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-126">When you create a table without specifying hello distribution column, hello table is automatically distributed using **round robin**.</span></span>  <span data-ttu-id="3a3b2-127">Działanie okrężne tabele mogą być wystarczające w niektórych scenariuszach, definiowania kolumn dystrybucji może znacznie zmniejszyć przenoszenia danych podczas wykonywania kwerend, w związku z tym optymalizacji wydajności.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span></span>  <span data-ttu-id="3a3b2-128">W sytuacjach, w przypadku małej ilości danych w tabeli, wybierając toocreate hello tabeli z hello **replikować** typ dystrybucji kopiuje węzeł obliczeniowy tooeach danych i zapisuje przenoszenia danych w czasie wykonywania zapytania.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-128">In situations where there is a small amount of data in a table, choosing toocreate hello table with hello **replicate** distribution type copies data tooeach compute node and saves data movement at query execution time.</span></span> <span data-ttu-id="3a3b2-129">Zobacz [Dystrybucja tabeli] [ Distribute] toolearn więcej informacji na temat tooselect kolumny dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-129">See [Distributing a Table][Distribute] toolearn more about how tooselect a distribution column.</span></span>

## <a name="indexing-and-partitioning-tables"></a><span data-ttu-id="3a3b2-130">Indeksowanie i Partycjonowanie tabel</span><span class="sxs-lookup"><span data-stu-id="3a3b2-130">Indexing and partitioning tables</span></span>
<span data-ttu-id="3a3b2-131">Staną się bardziej zaawansowane za pomocą usługi SQL Data Warehouse i mają toooptimize wydajności, należy toolearn dodatkowe informacje o projektowaniu tabel.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-131">As you become more advanced in using SQL Data Warehouse and want toooptimize performance, you'll want toolearn more about Table Design.</span></span>  <span data-ttu-id="3a3b2-132">toolearn więcej, zobacz artykuły hello na [typy danych tabeli][Data Types], [Dystrybucja tabeli][Distribute], [indeksowania tabeli] [ Index] i [partycjonowania tabeli][Partition].</span><span class="sxs-lookup"><span data-stu-id="3a3b2-132">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span></span>

## <a name="table-statistics"></a><span data-ttu-id="3a3b2-133">Statystyk tabeli</span><span class="sxs-lookup"><span data-stu-id="3a3b2-133">Table statistics</span></span>
<span data-ttu-id="3a3b2-134">Statystyki są bardzo ważne toogetting hello najlepszą wydajność poza usługą SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-134">Statistics are an extremely important toogetting hello best performance out of your SQL Data Warehouse.</span></span>  <span data-ttu-id="3a3b2-135">Ponieważ Magazyn danych SQL nie zostały jeszcze automatycznie utworzyć i Aktualizuj statystyki, takie jak pochodzić tooexpect w bazie danych SQL Azure, odczytywanie artykułem na [statystyki] [ Statistics] może być jednym z hello Najważniejsze artykuły odczytu tooensure otrzymasz hello najlepszą wydajność zapytań.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-135">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come tooexpect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of hello most important articles you read tooensure that you get hello best performance from your queries.</span></span>

## <a name="temporary-tables"></a><span data-ttu-id="3a3b2-136">Tabele tymczasowe</span><span class="sxs-lookup"><span data-stu-id="3a3b2-136">Temporary tables</span></span>
<span data-ttu-id="3a3b2-137">Tabele tymczasowe są tabele, które tylko istnieją na czas trwania hello logowania i nie są widoczne dla innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-137">Temporary tables are tables which only exist for hello duration of your logon and cannot be seen by other users.</span></span>  <span data-ttu-id="3a3b2-138">Tabele tymczasowe można innym tooprevent dobry sposób wyświetlania wyników tymczasowego i również zmniejszyć hello potrzebę oczyszczania.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-138">Temporary tables can be a good way tooprevent others from seeing temporary results and also reduce hello need for cleanup.</span></span>  <span data-ttu-id="3a3b2-139">Ponieważ tabele tymczasowe również korzystać z lokalnego magazynu, umożliwiając im szybsza dla niektórych operacji.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-139">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span></span>  <span data-ttu-id="3a3b2-140">Zobacz hello [tabeli tymczasowej] [ Temporary] artykuły, aby uzyskać więcej informacji o tabelach tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-140">See hello [Temporary Table][Temporary] articles for more details about temporary tables.</span></span>

## <a name="external-tables"></a><span data-ttu-id="3a3b2-141">Tabele zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="3a3b2-141">External tables</span></span>
<span data-ttu-id="3a3b2-142">Tabele zewnętrzne, znanej także jako Polybase tabele są tabel, które można wykonać zapytania z usługi SQL Data Warehouse, ale toodata punktu zewnętrzne z usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-142">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point toodata external from SQL Data Warehouse.</span></span>  <span data-ttu-id="3a3b2-143">Na przykład tworzenia tabeli zewnętrznej toofiles punktów, które na magazyn obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-143">For example, you can create an external table which points toofiles on Azure Blob Storage.</span></span>  <span data-ttu-id="3a3b2-144">Więcej informacji dotyczących sposobu toocreate i zapytania tabeli zewnętrznej, zobacz [ładowanie danych przy użyciu programu Polybase][Load data with Polybase].</span><span class="sxs-lookup"><span data-stu-id="3a3b2-144">For more details on how toocreate and query an external table, see [Load data with Polybase][Load data with Polybase].</span></span>  

## <a name="unsupported-table-features"></a><span data-ttu-id="3a3b2-145">Funkcje nieobsługiwane tabeli</span><span class="sxs-lookup"><span data-stu-id="3a3b2-145">Unsupported table features</span></span>
<span data-ttu-id="3a3b2-146">Gdy usługi SQL Data Warehouse zawiera wiele hello tej samej tabeli funkcje dostępne w innych bazach danych, brak niektórych funkcji, które nie są jeszcze obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-146">While SQL Data Warehouse contains many of hello same table features offered by other databases, there are some features which are not yet supported.</span></span>  <span data-ttu-id="3a3b2-147">Poniżej znajduje się lista niektórych hello funkcji tabeli, które nie są jeszcze obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-147">Below is a list of some of hello table features which are not yet supported.</span></span>

| <span data-ttu-id="3a3b2-148">Nieobsługiwane funkcje</span><span class="sxs-lookup"><span data-stu-id="3a3b2-148">Unsupported features</span></span> |
| --- |
| <span data-ttu-id="3a3b2-149">Klucz podstawowy, kluczy obcych unikatowych i wyboru [ograniczenia tabeli][Table Constraints]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span></span> |
| <span data-ttu-id="3a3b2-150">[Unikatowe indeksy][Unique Indexes]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-150">[Unique Indexes][Unique Indexes]</span></span> |
| <span data-ttu-id="3a3b2-151">[Kolumny obliczane][Computed Columns]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-151">[Computed Columns][Computed Columns]</span></span> |
| <span data-ttu-id="3a3b2-152">[Kolumny rozrzedzone][Sparse Columns]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-152">[Sparse Columns][Sparse Columns]</span></span> |
| <span data-ttu-id="3a3b2-153">[Typy definiowane przez użytkownika][User-Defined Types]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-153">[User-Defined Types][User-Defined Types]</span></span> |
| <span data-ttu-id="3a3b2-154">[Sekwencja][Sequence]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-154">[Sequence][Sequence]</span></span> |
| <span data-ttu-id="3a3b2-155">[Wyzwalacze][Triggers]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-155">[Triggers][Triggers]</span></span> |
| <span data-ttu-id="3a3b2-156">[Indeksowane widoki][Indexed Views]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-156">[Indexed Views][Indexed Views]</span></span> |
| <span data-ttu-id="3a3b2-157">[Synonimy][Synonyms]</span><span class="sxs-lookup"><span data-stu-id="3a3b2-157">[Synonyms][Synonyms]</span></span> |

## <a name="table-size-queries"></a><span data-ttu-id="3a3b2-158">Zapytania o rozmiar tabeli</span><span class="sxs-lookup"><span data-stu-id="3a3b2-158">Table size queries</span></span>
<span data-ttu-id="3a3b2-159">Jeden prosty sposób tooidentify miejsca i używane przez tabelę w każdym dystrybucje hello 60 wierszy jest toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span><span class="sxs-lookup"><span data-stu-id="3a3b2-159">One simple way tooidentify space and rows consumed by a table in each of hello 60 distributions, is toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span></span>

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="3a3b2-160">Jednak przy użyciu polecenia DBCC może być dość ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-160">However, using DBCC commands can be quite limiting.</span></span>  <span data-ttu-id="3a3b2-161">Dynamicznych widoków zarządzania (widoków DMV) umożliwi toosee bardziej szczegółowo opisano, jak również mieć znacznie większą kontrolę nad hello wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-161">Dynamic management views (DMVs) will allow you toosee much more detail as well as give you much greater control over hello query results.</span></span>  <span data-ttu-id="3a3b2-162">Rozpocznij od utworzenia wielu nasze przykłady tego widoku, który będzie tooby określonego w tym i innych artykułów.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-162">Start by creating this view, which will be referred tooby many of our examples in this and other articles.</span></span>

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

### <a name="table-space-summary"></a><span data-ttu-id="3a3b2-163">Podsumowanie obszaru tabel</span><span class="sxs-lookup"><span data-stu-id="3a3b2-163">Table space summary</span></span>
<span data-ttu-id="3a3b2-164">To zapytanie zwraca wiersze hello i miejsca przez tabelę.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-164">This query returns hello rows and space by table.</span></span>  <span data-ttu-id="3a3b2-165">Jest toosee dużą zapytania, tabel, które są największych tabel i czy są one okrężnego replikowane lub skrótu rozproszonych.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-165">It is a great query toosee which tables are your largest tables and whether they are round robin, replicated or hash distributed.</span></span>  <span data-ttu-id="3a3b2-166">Dla tablic skrótów rozproszonych zawiera także hello dystrybucji kolumny.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-166">For hash distributed tables it also shows hello distribution column.</span></span>  <span data-ttu-id="3a3b2-167">W większości przypadków największych tabel należy skrótu rozpowszechnianej za pomocą klastrowanego indeksu magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="3a3b2-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span></span>

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

### <a name="table-space-by-distribution-type"></a><span data-ttu-id="3a3b2-168">Obszar tabel według typu dystrybucji</span><span class="sxs-lookup"><span data-stu-id="3a3b2-168">Table space by distribution type</span></span>
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

### <a name="table-space-by-index-type"></a><span data-ttu-id="3a3b2-169">Obszar tabel według typu indeksu</span><span class="sxs-lookup"><span data-stu-id="3a3b2-169">Table space by index type</span></span>
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

### <a name="distribution-space-summary"></a><span data-ttu-id="3a3b2-170">Miejsce dystrybucji podsumowania</span><span class="sxs-lookup"><span data-stu-id="3a3b2-170">Distribution space summary</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="3a3b2-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3a3b2-171">Next steps</span></span>
<span data-ttu-id="3a3b2-172">toolearn więcej, zobacz artykuły hello na [typy danych tabeli][Data Types], [Dystrybucja tabeli][Distribute], [indeksowania tabeli] [ Index], [Partycjonowania tabeli][Partition], [utrzymania statystyk tabeli] [ Statistics] i [ Tabele tymczasowe][Temporary].</span><span class="sxs-lookup"><span data-stu-id="3a3b2-172">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="3a3b2-173">Aby uzyskać więcej informacji na temat najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="3a3b2-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
