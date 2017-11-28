---
title: "Przegląd tabel w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c16fef2f302dbc56f257eaf2f0d2b68b6a3c1852
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a><span data-ttu-id="ec463-103">Przegląd tabel w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ec463-103">Overview of tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="ec463-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="ec463-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="ec463-105">[Typy danych][Data Types]</span><span class="sxs-lookup"><span data-stu-id="ec463-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="ec463-106">[Dystrybuuj][Distribute]</span><span class="sxs-lookup"><span data-stu-id="ec463-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="ec463-107">[Indeks][Index]</span><span class="sxs-lookup"><span data-stu-id="ec463-107">[Index][Index]</span></span>
> * <span data-ttu-id="ec463-108">[Partycji][Partition]</span><span class="sxs-lookup"><span data-stu-id="ec463-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="ec463-109">[Statystyki][Statistics]</span><span class="sxs-lookup"><span data-stu-id="ec463-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="ec463-110">[Tymczasowe][Temporary]</span><span class="sxs-lookup"><span data-stu-id="ec463-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="ec463-111">Wprowadzenie do tworzenia tabel w usłudze SQL Data Warehouse jest proste.</span><span class="sxs-lookup"><span data-stu-id="ec463-111">Getting started with creating tables in SQL Data Warehouse is simple.</span></span>  <span data-ttu-id="ec463-112">Podstawowe [CREATE TABLE] [ CREATE TABLE] składni następuje wspólnej składni, najprawdopodobniej już znasz Praca z innych baz danych.</span><span class="sxs-lookup"><span data-stu-id="ec463-112">The basic [CREATE TABLE][CREATE TABLE] syntax follows the common syntax you are most likely already familiar with from working with other databases.</span></span>  <span data-ttu-id="ec463-113">Aby utworzyć tabelę, należy po prostu nazwę tabeli, nazwy kolumn i definiowanie typów danych dla każdej kolumny.</span><span class="sxs-lookup"><span data-stu-id="ec463-113">To create a table, you simply need to name your table, name your columns and define data types for each column.</span></span>  <span data-ttu-id="ec463-114">Jeśli już tworzenie tabel w innych bazach danych, to wygląda bardzo znane.</span><span class="sxs-lookup"><span data-stu-id="ec463-114">If you've create tables in other databases, this should look very familiar to you.</span></span>

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

<span data-ttu-id="ec463-115">Powyższy przykład tworzy tabeli o nazwie klientów z dwiema kolumnami, imię i nazwisko.</span><span class="sxs-lookup"><span data-stu-id="ec463-115">The above example creates a table named Customers with two columns, FirstName and LastName.</span></span>  <span data-ttu-id="ec463-116">Każda kolumna jest zdefiniowana z typem danych VARCHAR(25), co ogranicza dane do 25 znaków.</span><span class="sxs-lookup"><span data-stu-id="ec463-116">Each column is defined with a data type of VARCHAR(25), which limits the data to 25 characters.</span></span>  <span data-ttu-id="ec463-117">Te atrybuty podstawowych w tabeli, a także innych osób, przede wszystkim są takie same jak innych baz danych.</span><span class="sxs-lookup"><span data-stu-id="ec463-117">These fundamental attributes of a table, as well as others, are mostly the same as other databases.</span></span>  <span data-ttu-id="ec463-118">Typy danych są zdefiniowane dla każdej kolumny i zapewniania integralności danych.</span><span class="sxs-lookup"><span data-stu-id="ec463-118">Data types are defined for each column and ensure the integrity of your data.</span></span>  <span data-ttu-id="ec463-119">Aby zwiększyć wydajność przez zmniejszenie we/wy, można dodać indeksów.</span><span class="sxs-lookup"><span data-stu-id="ec463-119">Indexes can be added to improve performance by reducing I/O.</span></span>  <span data-ttu-id="ec463-120">Partycjonowanie można dodać do zwiększenia wydajności, gdy konieczna modyfikacja danych.</span><span class="sxs-lookup"><span data-stu-id="ec463-120">Partitioning can be added to improve performance when you need to modify data.</span></span>

<span data-ttu-id="ec463-121">[Zmiana nazwy] [ RENAME] tabeli SQL Data Warehouse wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="ec463-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span></span>

```sql  
RENAME OBJECT Customer TO CustomerOrig; 
 ```

## <a name="distributed-tables"></a><span data-ttu-id="ec463-122">Rozproszone tabele</span><span class="sxs-lookup"><span data-stu-id="ec463-122">Distributed tables</span></span>
<span data-ttu-id="ec463-123">Nowy atrybut podstawowych wynikające z systemów rozproszonych, takich jak SQL Data Warehouse jest **kolumny dystrybucji**.</span><span class="sxs-lookup"><span data-stu-id="ec463-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is the **distribution column**.</span></span>  <span data-ttu-id="ec463-124">Kolumny dystrybucji jest znacznie co wydaje się to np.</span><span class="sxs-lookup"><span data-stu-id="ec463-124">The distribution column is very much what it sounds like.</span></span>  <span data-ttu-id="ec463-125">Jest kolumna, która określa sposób dystrybucji lub podziału danych w tle.</span><span class="sxs-lookup"><span data-stu-id="ec463-125">It is the column that determines how to distribute, or divide, your data behind the scenes.</span></span>  <span data-ttu-id="ec463-126">Po utworzeniu tabeli bez określania dystrybucji kolumny tabeli jest automatycznie dystrybuowany za pomocą **działanie okrężne**.</span><span class="sxs-lookup"><span data-stu-id="ec463-126">When you create a table without specifying the distribution column, the table is automatically distributed using **round robin**.</span></span>  <span data-ttu-id="ec463-127">Działanie okrężne tabele mogą być wystarczające w niektórych scenariuszach, definiowania kolumn dystrybucji może znacznie zmniejszyć przenoszenia danych podczas wykonywania kwerend, w związku z tym optymalizacji wydajności.</span><span class="sxs-lookup"><span data-stu-id="ec463-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span></span>  <span data-ttu-id="ec463-128">W sytuacjach, w przypadku małej ilości danych w tabeli, wybierając opcję utworzenia tabeli z **replikować** typ dystrybucji kopiuje dane na każdy węzeł obliczeniowy i zapisuje przenoszenia danych w czasie wykonywania zapytania.</span><span class="sxs-lookup"><span data-stu-id="ec463-128">In situations where there is a small amount of data in a table, choosing to create the table with the **replicate** distribution type copies data to each compute node and saves data movement at query execution time.</span></span> <span data-ttu-id="ec463-129">Zobacz [Dystrybucja tabeli] [ Distribute] Aby dowiedzieć się więcej na temat sposobu wybierania kolumn dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="ec463-129">See [Distributing a Table][Distribute] to learn more about how to select a distribution column.</span></span>

## <a name="indexing-and-partitioning-tables"></a><span data-ttu-id="ec463-130">Indeksowanie i Partycjonowanie tabel</span><span class="sxs-lookup"><span data-stu-id="ec463-130">Indexing and partitioning tables</span></span>
<span data-ttu-id="ec463-131">Staną się bardziej zaawansowane za pomocą usługi SQL Data Warehouse i chcesz zoptymalizować wydajność, należy dowiedzieć się więcej o projektowaniu tabel.</span><span class="sxs-lookup"><span data-stu-id="ec463-131">As you become more advanced in using SQL Data Warehouse and want to optimize performance, you'll want to learn more about Table Design.</span></span>  <span data-ttu-id="ec463-132">Aby dowiedzieć się więcej, zobacz artykuły w [typy danych tabeli][Data Types], [Dystrybucja tabeli][Distribute], [indeksowania tabeli] [ Index] i [partycjonowania tabeli][Partition].</span><span class="sxs-lookup"><span data-stu-id="ec463-132">To learn more, see the articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span></span>

## <a name="table-statistics"></a><span data-ttu-id="ec463-133">Statystyk tabeli</span><span class="sxs-lookup"><span data-stu-id="ec463-133">Table statistics</span></span>
<span data-ttu-id="ec463-134">Statystyki są bardzo ważne dla pobierania najlepszą wydajność poza usługą SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ec463-134">Statistics are an extremely important to getting the best performance out of your SQL Data Warehouse.</span></span>  <span data-ttu-id="ec463-135">Ponieważ Magazyn danych SQL nie zostały jeszcze automatycznie utworzyć i Aktualizuj statystyki, takie jak mogą pochodzić można oczekiwać w bazie danych SQL Azure, odczytywanie artykułem na [statystyki] [ Statistics] może być jednym z najważniejszych artykułów odczytu Upewnij się, aby uzyskać najlepszą wydajność zapytań.</span><span class="sxs-lookup"><span data-stu-id="ec463-135">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come to expect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of the most important articles you read to ensure that you get the best performance from your queries.</span></span>

## <a name="temporary-tables"></a><span data-ttu-id="ec463-136">Tabele tymczasowe</span><span class="sxs-lookup"><span data-stu-id="ec463-136">Temporary tables</span></span>
<span data-ttu-id="ec463-137">Tabele tymczasowe są tabele, które tylko istnieją w czasie trwania logowania i nie są widoczne dla innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ec463-137">Temporary tables are tables which only exist for the duration of your logon and cannot be seen by other users.</span></span>  <span data-ttu-id="ec463-138">Tabele tymczasowe może być dobrym sposobem uniemożliwienia podglądu wyników tymczasowego i również ograniczyć potrzebę oczyszczania.</span><span class="sxs-lookup"><span data-stu-id="ec463-138">Temporary tables can be a good way to prevent others from seeing temporary results and also reduce the need for cleanup.</span></span>  <span data-ttu-id="ec463-139">Ponieważ tabele tymczasowe również korzystać z lokalnego magazynu, umożliwiając im szybsza dla niektórych operacji.</span><span class="sxs-lookup"><span data-stu-id="ec463-139">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span></span>  <span data-ttu-id="ec463-140">Zobacz [tabeli tymczasowej] [ Temporary] artykuły, aby uzyskać więcej informacji o tabelach tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="ec463-140">See the [Temporary Table][Temporary] articles for more details about temporary tables.</span></span>

## <a name="external-tables"></a><span data-ttu-id="ec463-141">Tabele zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="ec463-141">External tables</span></span>
<span data-ttu-id="ec463-142">Tabele zewnętrzne, znanej także jako Polybase tabele są tabele, które można wykonać zapytania z usługi SQL Data Warehouse, ale punkt, aby dane zewnętrzne z usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ec463-142">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point to data external from SQL Data Warehouse.</span></span>  <span data-ttu-id="ec463-143">Na przykład można utworzyć tabeli zewnętrznej wskazującą na plików w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="ec463-143">For example, you can create an external table which points to files on Azure Blob Storage.</span></span>  <span data-ttu-id="ec463-144">Aby uzyskać więcej informacji na temat sposobu tworzenia i przeszukiwania tabeli zewnętrznej, zobacz [ładowanie danych przy użyciu programu Polybase][Load data with Polybase].</span><span class="sxs-lookup"><span data-stu-id="ec463-144">For more details on how to create and query an external table, see [Load data with Polybase][Load data with Polybase].</span></span>  

## <a name="unsupported-table-features"></a><span data-ttu-id="ec463-145">Funkcje nieobsługiwane tabeli</span><span class="sxs-lookup"><span data-stu-id="ec463-145">Unsupported table features</span></span>
<span data-ttu-id="ec463-146">Gdy usługi SQL Data Warehouse zawiera wiele tej samej tabeli funkcji oferowanych przez innych baz danych, brak niektórych funkcji, które nie są jeszcze obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="ec463-146">While SQL Data Warehouse contains many of the same table features offered by other databases, there are some features which are not yet supported.</span></span>  <span data-ttu-id="ec463-147">Poniżej przedstawiono listę niektórych funkcji tabeli, które nie są jeszcze obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="ec463-147">Below is a list of some of the table features which are not yet supported.</span></span>

| <span data-ttu-id="ec463-148">Nieobsługiwane funkcje</span><span class="sxs-lookup"><span data-stu-id="ec463-148">Unsupported features</span></span> |
| --- |
| <span data-ttu-id="ec463-149">Klucz podstawowy, kluczy obcych unikatowych i wyboru [ograniczenia tabeli][Table Constraints]</span><span class="sxs-lookup"><span data-stu-id="ec463-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span></span> |
| <span data-ttu-id="ec463-150">[Unikatowe indeksy][Unique Indexes]</span><span class="sxs-lookup"><span data-stu-id="ec463-150">[Unique Indexes][Unique Indexes]</span></span> |
| <span data-ttu-id="ec463-151">[Kolumny obliczane][Computed Columns]</span><span class="sxs-lookup"><span data-stu-id="ec463-151">[Computed Columns][Computed Columns]</span></span> |
| <span data-ttu-id="ec463-152">[Kolumny rozrzedzone][Sparse Columns]</span><span class="sxs-lookup"><span data-stu-id="ec463-152">[Sparse Columns][Sparse Columns]</span></span> |
| <span data-ttu-id="ec463-153">[Typy definiowane przez użytkownika][User-Defined Types]</span><span class="sxs-lookup"><span data-stu-id="ec463-153">[User-Defined Types][User-Defined Types]</span></span> |
| <span data-ttu-id="ec463-154">[Sekwencja][Sequence]</span><span class="sxs-lookup"><span data-stu-id="ec463-154">[Sequence][Sequence]</span></span> |
| <span data-ttu-id="ec463-155">[Wyzwalacze][Triggers]</span><span class="sxs-lookup"><span data-stu-id="ec463-155">[Triggers][Triggers]</span></span> |
| <span data-ttu-id="ec463-156">[Indeksowane widoki][Indexed Views]</span><span class="sxs-lookup"><span data-stu-id="ec463-156">[Indexed Views][Indexed Views]</span></span> |
| <span data-ttu-id="ec463-157">[Synonimy][Synonyms]</span><span class="sxs-lookup"><span data-stu-id="ec463-157">[Synonyms][Synonyms]</span></span> |

## <a name="table-size-queries"></a><span data-ttu-id="ec463-158">Zapytania o rozmiar tabeli</span><span class="sxs-lookup"><span data-stu-id="ec463-158">Table size queries</span></span>
<span data-ttu-id="ec463-159">Prosty sposób identyfikacji miejsca i używane przez tabelę w każdym z 60 dystrybucje wierszy jest użycie [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span><span class="sxs-lookup"><span data-stu-id="ec463-159">One simple way to identify space and rows consumed by a table in each of the 60 distributions, is to use [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span></span>

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="ec463-160">Jednak przy użyciu polecenia DBCC może być dość ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="ec463-160">However, using DBCC commands can be quite limiting.</span></span>  <span data-ttu-id="ec463-161">Dynamicznych widoków zarządzania (widoków DMV) umożliwiają znacznie bardziej szczegółowo w temacie, a także zapewniają znacznie większą kontrolę nad wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="ec463-161">Dynamic management views (DMVs) will allow you to see much more detail as well as give you much greater control over the query results.</span></span>  <span data-ttu-id="ec463-162">Rozpocznij od utworzenia tego widoku, który będzie odwoływać się wiele nasze przykłady w tym i innych artykułów.</span><span class="sxs-lookup"><span data-stu-id="ec463-162">Start by creating this view, which will be referred to by many of our examples in this and other articles.</span></span>

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

### <a name="table-space-summary"></a><span data-ttu-id="ec463-163">Podsumowanie obszaru tabel</span><span class="sxs-lookup"><span data-stu-id="ec463-163">Table space summary</span></span>
<span data-ttu-id="ec463-164">To zapytanie zwraca wiersze i miejsca przez tabelę.</span><span class="sxs-lookup"><span data-stu-id="ec463-164">This query returns the rows and space by table.</span></span>  <span data-ttu-id="ec463-165">Jest bardzo zapytań do tabel, które są największych tabel i określa, czy mają one okrężnego replikowane lub rozpowszechniane skrót.</span><span class="sxs-lookup"><span data-stu-id="ec463-165">It is a great query to see which tables are your largest tables and whether they are round robin, replicated or hash distributed.</span></span>  <span data-ttu-id="ec463-166">Dla tablic skrótów rozproszonych zawiera także kolumny dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="ec463-166">For hash distributed tables it also shows the distribution column.</span></span>  <span data-ttu-id="ec463-167">W większości przypadków największych tabel należy skrótu rozpowszechnianej za pomocą klastrowanego indeksu magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="ec463-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span></span>

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

### <a name="table-space-by-distribution-type"></a><span data-ttu-id="ec463-168">Obszar tabel według typu dystrybucji</span><span class="sxs-lookup"><span data-stu-id="ec463-168">Table space by distribution type</span></span>
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

### <a name="table-space-by-index-type"></a><span data-ttu-id="ec463-169">Obszar tabel według typu indeksu</span><span class="sxs-lookup"><span data-stu-id="ec463-169">Table space by index type</span></span>
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

### <a name="distribution-space-summary"></a><span data-ttu-id="ec463-170">Miejsce dystrybucji podsumowania</span><span class="sxs-lookup"><span data-stu-id="ec463-170">Distribution space summary</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="ec463-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ec463-171">Next steps</span></span>
<span data-ttu-id="ec463-172">Aby dowiedzieć się więcej, zobacz artykuły w [typy danych tabeli][Data Types], [Dystrybucja tabeli][Distribute], [indeksowania tabeli][Index], [partycjonowania tabeli][Partition], [utrzymania statystyk tabeli] [ Statistics] i [tabel tymczasowych][Temporary].</span><span class="sxs-lookup"><span data-stu-id="ec463-172">To learn more, see the articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="ec463-173">Aby uzyskać więcej informacji na temat najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="ec463-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
