---
title: "tabele aaaPartitioning w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: Wprowadzenie do partycjonowania tabeli w magazynie danych SQL Azure.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="30a6d-103">Partycjonowanie tabel w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="30a6d-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="30a6d-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="30a6d-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="30a6d-105">[Typy danych][Data Types]</span><span class="sxs-lookup"><span data-stu-id="30a6d-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="30a6d-106">[Dystrybuuj][Distribute]</span><span class="sxs-lookup"><span data-stu-id="30a6d-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="30a6d-107">[Indeks][Index]</span><span class="sxs-lookup"><span data-stu-id="30a6d-107">[Index][Index]</span></span>
> * <span data-ttu-id="30a6d-108">[Partycji][Partition]</span><span class="sxs-lookup"><span data-stu-id="30a6d-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="30a6d-109">[Statystyki][Statistics]</span><span class="sxs-lookup"><span data-stu-id="30a6d-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="30a6d-110">[Tymczasowe][Temporary]</span><span class="sxs-lookup"><span data-stu-id="30a6d-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="30a6d-111">Partycjonowanie jest obsługiwana dla wszystkich typów tabeli SQL Data Warehouse; w tym klastrowanego magazynu kolumn, indeks klastrowany i stosu.</span><span class="sxs-lookup"><span data-stu-id="30a6d-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="30a6d-112">Partycjonowanie jest również obsługiwany na wszystkich typach dystrybucji, w tym zarówno skrótu lub działanie okrężne rozproszonych.</span><span class="sxs-lookup"><span data-stu-id="30a6d-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="30a6d-113">Partycjonowanie umożliwia toodivide, które dane na mniejsze grupy danych i w większości przypadków Partycjonowanie jest wykonywana na kolumnę dat.</span><span class="sxs-lookup"><span data-stu-id="30a6d-113">Partitioning enables you toodivide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="30a6d-114">Korzyści wynikające z partycjonowania</span><span class="sxs-lookup"><span data-stu-id="30a6d-114">Benefits of partitioning</span></span>
<span data-ttu-id="30a6d-115">Partycjonowanie mogą korzystać wydajność obsługi i zapytań danych.</span><span class="sxs-lookup"><span data-stu-id="30a6d-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="30a6d-116">Określa, czy przynosi korzyści zarówno lub jeden z nich jest zależna od jak załadować danych i czy hello tej samej kolumnie może służyć do obu celów, ponieważ Partycjonowanie jest możliwe tylko w jednej kolumnie.</span><span class="sxs-lookup"><span data-stu-id="30a6d-116">Whether it benefits both or just one is dependent on how data is loaded and whether hello same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-tooloads"></a><span data-ttu-id="30a6d-117">Tooloads korzyści</span><span class="sxs-lookup"><span data-stu-id="30a6d-117">Benefits tooloads</span></span>
<span data-ttu-id="30a6d-118">Hello główną zaletą partycjonowania w usłudze SQL Data Warehouse jest zwiększyć wydajność hello i wydajności podczas ładowania danych przy użyciu usunięcia partycji, przełączania i scalanie.</span><span class="sxs-lookup"><span data-stu-id="30a6d-118">hello primary benefit of partitioning in SQL Data Warehouse is improve hello efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="30a6d-119">W większości przypadków, w których dane są podzielone na partycje w dniu kolumny, która jest ściśle powiązana sekwencji toohello danych hello jest załadowany toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="30a6d-119">In most cases data is partitioned on a date column that is closely tied toohello sequence which hello data is loaded toohello database.</span></span>  <span data-ttu-id="30a6d-120">Jedną z największych zalet hello przy użyciu danych toomaintain partycje go hello unikania rejestrowanie transakcji.</span><span class="sxs-lookup"><span data-stu-id="30a6d-120">One of hello greatest benefits of using partitions toomaintain data it hello avoidance of transaction logging.</span></span>  <span data-ttu-id="30a6d-121">Po prostu Wstawianie, aktualizowanie lub usuwanie danych mogą być Najprostszym rozwiązaniem hello z niewielką ilością myśl i nakładu pracy, przy użyciu podziału na partycje podczas procesu obciążenia znacznie może poprawić wydajność.</span><span class="sxs-lookup"><span data-stu-id="30a6d-121">While simply inserting, updating or deleting data can be hello most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="30a6d-122">Przełączanie partycji można używane tooquickly Usuń lub Zamień sekcji tabeli.</span><span class="sxs-lookup"><span data-stu-id="30a6d-122">Partition switching can be used tooquickly remove or replace a section of a table.</span></span>  <span data-ttu-id="30a6d-123">Na przykład tabela faktów sprzedaży może zawierać tylko dane dla hello ostatnich miesięcy 36.</span><span class="sxs-lookup"><span data-stu-id="30a6d-123">For example, a sales fact table might contain just data for hello past 36 months.</span></span>  <span data-ttu-id="30a6d-124">Na końcu hello co miesiąc hello miesiąc najstarsze dane są usuwane z tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="30a6d-124">At hello end of every month, hello oldest month of sales data is deleted from hello table.</span></span>  <span data-ttu-id="30a6d-125">Można go usunąć te dane przy użyciu danych hello toodelete instrukcji delete dla hello najstarsze miesiąca.</span><span class="sxs-lookup"><span data-stu-id="30a6d-125">This data could be deleted by using a delete statement toodelete hello data for hello oldest month.</span></span>  <span data-ttu-id="30a6d-126">Jednak usunięcie dużych ilości danych wiersz po wierszu z instrukcji delete może zająć bardzo dużo czasu, a także spowodować ryzyko hello duże transakcje przyjmujących toorollback dużo czasu, jeśli jakaś nieprawidłowość.</span><span class="sxs-lookup"><span data-stu-id="30a6d-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create hello risk of large transactions which could take a long time toorollback if something goes wrong.</span></span>  <span data-ttu-id="30a6d-127">Więcej optymalne podejście jest toosimply upuszczania hello najstarsze partycji danych.</span><span class="sxs-lookup"><span data-stu-id="30a6d-127">A more optimal approach is toosimply drop hello oldest partition of data.</span></span>  <span data-ttu-id="30a6d-128">Gdzie usuwanie wierszy poszczególnych hello może zająć godziny, usunięcie całego partycji może potrwać sekund.</span><span class="sxs-lookup"><span data-stu-id="30a6d-128">Where deleting hello individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-tooqueries"></a><span data-ttu-id="30a6d-129">Tooqueries korzyści</span><span class="sxs-lookup"><span data-stu-id="30a6d-129">Benefits tooqueries</span></span>
<span data-ttu-id="30a6d-130">Partycjonowanie może być również używane tooimprove wydajność zapytań.</span><span class="sxs-lookup"><span data-stu-id="30a6d-130">Partitioning can also be used tooimprove query performance.</span></span>  <span data-ttu-id="30a6d-131">Jeśli zapytanie zastosowanie filtru kolumny podzielone na partycje, może to ograniczyć hello tooonly skanowania hello kwalifikowanie partycje, które mogą być znacznie mniejszy podzbiór danych hello, unikając tabeli pełnego skanowania.</span><span class="sxs-lookup"><span data-stu-id="30a6d-131">If a query applies a filter on a partitioned column, this can limit hello scan tooonly hello qualifying partitions which may be a much smaller subset of hello data, avoiding a full table scan.</span></span>  <span data-ttu-id="30a6d-132">Z wprowadzeniem hello klastrowane indeksy magazynu kolumn zwiększenia wydajności predykatu eliminacji hello są mniej korzystne, ale w niektórych przypadkach może być tooqueries korzyści.</span><span class="sxs-lookup"><span data-stu-id="30a6d-132">With hello introduction of clustered columnstore indexes, hello predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit tooqueries.</span></span>  <span data-ttu-id="30a6d-133">Na przykład jeśli tabela faktów sprzedaży hello jest podzielona na partycje do 36 miesięcy za pomocą pola Data sprzedaży hello, następnie zapytań, które odfiltrować Data sprzedaży hello można pominąć wyszukiwanie w partycji, które nie pasuje do filtru hello.</span><span class="sxs-lookup"><span data-stu-id="30a6d-133">For example, if hello sales fact table is partitioned into 36 months using hello sales date field, then queries that filter on hello sale date can skip searching in partitions that don’t match hello filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="30a6d-134">Wskazówki dotyczące rozmiaru partycji</span><span class="sxs-lookup"><span data-stu-id="30a6d-134">Partition sizing guidance</span></span>
<span data-ttu-id="30a6d-135">Podczas partycjonowania mogą być używane tooimprove wydajności niektórych scenariuszy tworzenia tabeli z **zbyt wiele** partycji może pogarszać wydajność w pewnych okolicznościach.</span><span class="sxs-lookup"><span data-stu-id="30a6d-135">While partitioning can be used tooimprove performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="30a6d-136">Te problemy są szczególnie istotne w przypadku tabel klastrowanego magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="30a6d-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="30a6d-137">Partycjonowanie toobe pomocne, jest ważne toounderstand podczas toouse partycjonowania i hello liczba toocreate partycji.</span><span class="sxs-lookup"><span data-stu-id="30a6d-137">For partitioning toobe helpful, it is important toounderstand when toouse partitioning and hello number of partitions toocreate.</span></span>  <span data-ttu-id="30a6d-138">Jest nie twardych reguły szybkiego jako toohow większej liczby partycji są zbyt wiele, zależy od danych i jak wiele partycji ładowania toosimultaneously.</span><span class="sxs-lookup"><span data-stu-id="30a6d-138">There is no hard fast rule as toohow many partitions are too many, it depends on your data and how many partitions you are loading toosimultaneously.</span></span>  <span data-ttu-id="30a6d-139">Ale jako ogólne zasadą, traktować Dodawanie 10s too100s partycji, nie 1000s.</span><span class="sxs-lookup"><span data-stu-id="30a6d-139">But as a general rule of thumb, think of adding 10s too100s of partitions, not 1000s.</span></span>

<span data-ttu-id="30a6d-140">Podczas tworzenia partycji na **klastrowanego magazynu kolumn** tabel, jest ważne tooconsider, ile wierszy nastąpi przejście do każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="30a6d-140">When creating partitioning on **clustered columnstore** tables, it is important tooconsider how many rows will land in each partition.</span></span>  <span data-ttu-id="30a6d-141">Optymalne kompresji i wydajności tabel klastrowanego magazynu kolumn co najmniej 1 milion wierszy na dystrybucji i partycja na potrzeby.</span><span class="sxs-lookup"><span data-stu-id="30a6d-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="30a6d-142">Przed utworzeniem partycji usługi SQL Data Warehouse już dzieli każdej tabeli 60 rozproszonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="30a6d-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="30a6d-143">Partycjonowania tabeli tooa dodany jest ponadto dystrybucje toohello utworzone w tle hello.</span><span class="sxs-lookup"><span data-stu-id="30a6d-143">Any partitioning added tooa table is in addition toohello distributions created behind hello scenes.</span></span>  <span data-ttu-id="30a6d-144">Jeśli tabela faktów sprzedaży hello zawarte 36 miesięczne partycji i biorąc pod uwagę, że magazyn danych SQL ma 60 dystrybucje hello sprzedaży fakt, że tabela musi zawierać 60 mln wierszy na miesiąc lub 2.1 miliardy wierszy, gdy wszystkie miesiące są wypełniane przy użyciu tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="30a6d-144">Using this example, if hello sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then hello sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="30a6d-145">Jeśli tabela zawiera znacznie mniej wierszy niż hello Zalecana minimalna liczba wierszy przypadających na partycję, rozważ użycie mniejszej liczby partycji w kolejności toomake wzrost hello liczba wierszy przypadających na partycję.</span><span class="sxs-lookup"><span data-stu-id="30a6d-145">If a table contains significantly less rows than hello recommended minimum number of rows per partition, consider using fewer partitions in order toomake increase hello number of rows per partition.</span></span>  <span data-ttu-id="30a6d-146">Zobacz też hello [indeksowanie] [ Index] artykułu, który obejmuje zapytania uruchamiane na SQL Data Warehouse tooassess hello jakości klastra indeksy magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="30a6d-146">Also see hello [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse tooassess hello quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="30a6d-147">Różnica składni z programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="30a6d-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="30a6d-148">Usługa SQL Data Warehouse wprowadza uproszczony definicję partycji, która różni się nieznacznie z programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="30a6d-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="30a6d-149">Partycjonowania funkcje i schematy nie są używane w usłudze SQL Data Warehouse, ponieważ są one w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="30a6d-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="30a6d-150">Zamiast tego toodo wystarczy zidentyfikować partycjonowanej kolumny i hello granic punkty.</span><span class="sxs-lookup"><span data-stu-id="30a6d-150">Instead, all you need toodo is identify partitioned column and hello boundary points.</span></span>  <span data-ttu-id="30a6d-151">Składnia hello partycjonowania może być nieco inne niż SQL Server, podstawowe koncepcje hello są hello tego samego.</span><span class="sxs-lookup"><span data-stu-id="30a6d-151">While hello syntax of partitioning may be slightly different from SQL Server, hello basic concepts are hello same.</span></span>  <span data-ttu-id="30a6d-152">SQL Server i SQL Data Warehouse obsługuje jedna kolumna partycji w tabeli, które mogą być ranged partycji.</span><span class="sxs-lookup"><span data-stu-id="30a6d-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="30a6d-153">toolearn więcej informacji na temat partycjonowania, zobacz [partycjonowane tabele i indeksy][Partitioned Tables and Indexes].</span><span class="sxs-lookup"><span data-stu-id="30a6d-153">toolearn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="30a6d-154">Witaj w poniższym przykładzie usługi SQL Data Warehouse na partycje [CREATE TABLE] [ CREATE TABLE] instrukcji, partycje tabela FactInternetSales hello w kolumnie OrderDateKey hello:</span><span class="sxs-lookup"><span data-stu-id="30a6d-154">hello below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions hello FactInternetSales table on hello OrderDateKey column:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="30a6d-155">Migrowanie partycjonowania z programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="30a6d-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="30a6d-156">toomigrate programu SQL Server po prostu partycji tooSQL definicje magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="30a6d-156">toomigrate SQL Server partition definitions tooSQL Data Warehouse simply:</span></span>

* <span data-ttu-id="30a6d-157">Eliminowanie hello programu SQL Server [schemat partycji][partition scheme].</span><span class="sxs-lookup"><span data-stu-id="30a6d-157">Eliminate hello SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="30a6d-158">Dodaj hello [funkcja partycji] [ partition function] tooyour definicji tworzenia tabeli.</span><span class="sxs-lookup"><span data-stu-id="30a6d-158">Add hello [partition function][partition function] definition tooyour CREATE TABLE.</span></span>

<span data-ttu-id="30a6d-159">W przypadku migracji tabeli partycjonowanej z hello wystąpienia programu SQL Server, poniżej SQL może pomóc toointerrogate hello liczbę wierszy, które znajdują się w każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="30a6d-159">If you are migrating a partitioned table from a SQL Server instance hello below SQL can help you toointerrogate hello number of rows that are in each partition.</span></span>  <span data-ttu-id="30a6d-160">Należy pamiętać, że jeśli hello samej szczegółowości partycjonowania jest używany na SQL Data Warehouse, hello liczba wierszy przypadających na partycję zmniejszy się o 60.</span><span class="sxs-lookup"><span data-stu-id="30a6d-160">Keep in mind that if hello same partitioning granularity is used on SQL Data Warehouse, hello number of rows per partition will decrease by a factor of 60.</span></span>  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a><span data-ttu-id="30a6d-161">Zarządzanie obciążeniami</span><span class="sxs-lookup"><span data-stu-id="30a6d-161">Workload management</span></span>
<span data-ttu-id="30a6d-162">Jest jeden toofactor uwagę ostatni element w decyzji partycji tabeli toohello [zarządzania obciążenia][workload management].</span><span class="sxs-lookup"><span data-stu-id="30a6d-162">One final piece consideration toofactor in toohello table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="30a6d-163">Zarządzanie obciążenia w usłudze SQL Data Warehouse jest głównie hello zarządzania pamięci i współbieżność.</span><span class="sxs-lookup"><span data-stu-id="30a6d-163">Workload management in SQL Data Warehouse is primarily hello management of memory and concurrency.</span></span>  <span data-ttu-id="30a6d-164">W hello SQL Data Warehouse maksymalna ilość pamięci przydzielona tooeach dystrybucji podczas wykonywania zapytania jest klasy zasobów o której działalność.</span><span class="sxs-lookup"><span data-stu-id="30a6d-164">In SQL Data Warehouse hello maximum memory allocated tooeach distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="30a6d-165">W idealnym przypadku będzie o rozmiarze partycji, biorąc pod uwagę innych czynników, takich jak wymagania dotyczące pamięci hello tworzenia klastrowane indeksy magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="30a6d-165">Ideally your partitions will be sized in consideration of other factors like hello memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="30a6d-166">Klastrowane korzyści indeksy magazynu kolumn znacznie, gdy są przydzielone więcej pamięci.</span><span class="sxs-lookup"><span data-stu-id="30a6d-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="30a6d-167">W związku z tym można się, że tooensure, który odbudować indeksu partycji nie jest zagłodzone pamięci.</span><span class="sxs-lookup"><span data-stu-id="30a6d-167">Therefore, you will want tooensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="30a6d-168">Zwiększenie hello ilość pamięci dostępna tooyour zapytania można osiągnąć przełączyć hello domyślnej roli, smallrc, tooone z hello innych ról, takich jak largerc.</span><span class="sxs-lookup"><span data-stu-id="30a6d-168">Increasing hello amount of memory available tooyour query can be achieved by switching from hello default role, smallrc, tooone of hello other roles such as largerc.</span></span>

<span data-ttu-id="30a6d-169">Informacje dotyczące hello alokacji pamięci dla dystrybucji są dostępne, badając hello zasobów zarządcy dynamicznych widoków zarządzania.</span><span class="sxs-lookup"><span data-stu-id="30a6d-169">Information on hello allocation of memory per distribution is available by querying hello resource governor dynamic management views.</span></span> <span data-ttu-id="30a6d-170">W rzeczywistości Twojej przydział pamięci jest mniejsza niż poniższe rysunki hello.</span><span class="sxs-lookup"><span data-stu-id="30a6d-170">In reality your memory grant will be less than hello figures below.</span></span> <span data-ttu-id="30a6d-171">Zapewnia to jednak poziom wskazówki, które można używać podczas określania rozmiaru partycji dla danych operacji zarządzania.</span><span class="sxs-lookup"><span data-stu-id="30a6d-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="30a6d-172">Spróbuj tooavoid zmiany rozmiaru partycji przekracza przydział pamięci hello podał hello klasy zasobów bardzo duża.</span><span class="sxs-lookup"><span data-stu-id="30a6d-172">Try tooavoid sizing your partitions beyond hello memory grant provided by hello extra large resource class.</span></span> <span data-ttu-id="30a6d-173">Jeśli partycji rosnąć poza tym rysunku uruchomieniem hello ryzyko wykorzystania pamięci, co z kolei prowadzi tooless optymalnej kompresji.</span><span class="sxs-lookup"><span data-stu-id="30a6d-173">If your partitions grow beyond this figure you run hello risk of memory pressure which in turn leads tooless optimal compression.</span></span>

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a><span data-ttu-id="30a6d-174">Przełączanie partycji</span><span class="sxs-lookup"><span data-stu-id="30a6d-174">Partition switching</span></span>
<span data-ttu-id="30a6d-175">Magazyn danych SQL obsługuje partycji dzielenia, łączenia i przełączania.</span><span class="sxs-lookup"><span data-stu-id="30a6d-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="30a6d-176">Każda z tych funkcji jest excuted przy użyciu hello [instrukcji ALTER TABLE] [ ALTER TABLE] instrukcji.</span><span class="sxs-lookup"><span data-stu-id="30a6d-176">Each of these functions is excuted using hello [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="30a6d-177">partycje tooswitch między dwiema tabelami Pamiętaj, że partycje hello są wyrównane na ich odpowiednich granice a hello definicje tabel są takie same.</span><span class="sxs-lookup"><span data-stu-id="30a6d-177">tooswitch partitions between two tables you must ensure that hello partitions align on their respective boundaries and that hello table definitions match.</span></span> <span data-ttu-id="30a6d-178">Jako ograniczenia sprawdzania nie są dostępne wartości w tabeli źródłowej tabeli hello tooenforce hello zakresu musi zawierać hello sam partycji granice jako hello tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="30a6d-178">As check constraints are not available tooenforce hello range of values in a table hello source table must contain hello same partition boundaries as hello target table.</span></span> <span data-ttu-id="30a6d-179">Jeśli nie jest to hello, przełącznik partycji hello wystąpi błąd, ponieważ metadane partycji hello nie będą synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="30a6d-179">If this is not hello case, then hello partition switch will fail as hello partition metadata will not be synchronized.</span></span>

### <a name="how-toosplit-a-partition-that-contains-data"></a><span data-ttu-id="30a6d-180">Jak toosplit partycji, która zawiera dane</span><span class="sxs-lookup"><span data-stu-id="30a6d-180">How toosplit a partition that contains data</span></span>
<span data-ttu-id="30a6d-181">Witaj najbardziej efektywny metody toosplit partycji, która zawiera już dane jest toouse `CTAS` instrukcji.</span><span class="sxs-lookup"><span data-stu-id="30a6d-181">hello most efficient method toosplit a partition that already contains data is toouse a `CTAS` statement.</span></span> <span data-ttu-id="30a6d-182">Tabeli partycjonowanej hello jest klastrowanego magazynu kolumn następnie hello partycji tabeli może być puste przed mogą być dzielone.</span><span class="sxs-lookup"><span data-stu-id="30a6d-182">If hello partitioned table is a clustered columnstore then hello table partition must be empty before it can be split.</span></span>

<span data-ttu-id="30a6d-183">Poniżej znajdują się magazynu kolumn partycjonowane przykładową tabelę zawierającą po jednym wierszu w każdej partycji:</span><span class="sxs-lookup"><span data-stu-id="30a6d-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
    ,   [OrderDateKey]          int          NOT NULL
    ,   [CustomerKey]           int          NOT NULL
    ,   [PromotionKey]          int          NOT NULL
    ,   [SalesOrderNumber]      nvarchar(20) NOT NULL
    ,   [OrderQuantity]         smallint     NOT NULL
    ,   [UnitPrice]             money        NOT NULL
    ,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> <span data-ttu-id="30a6d-184">Tworzenie obiektu Statystyka hello możemy upewnij się, że tych metadanych tabeli jest bardziej dokładne.</span><span class="sxs-lookup"><span data-stu-id="30a6d-184">By Creating hello statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="30a6d-185">Jeśli firma Microsoft pominąć tworzenie statystyk, SQL Data Warehouse użyje wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="30a6d-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="30a6d-186">Dla Przejrzyj szczegóły dotyczące statystyk [statystyki][statistics].</span><span class="sxs-lookup"><span data-stu-id="30a6d-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="30a6d-187">Firma Microsoft może następnie wyszukiwać hello liczba wierszy za pomocą hello `sys.partitions` widoku katalogu:</span><span class="sxs-lookup"><span data-stu-id="30a6d-187">We can then query for hello row count using hello `sys.partitions` catalog view:</span></span>

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

<span data-ttu-id="30a6d-188">Jeśli ta tabela spróbujemy toosplit uzyskujemy błąd:</span><span class="sxs-lookup"><span data-stu-id="30a6d-188">If we try toosplit this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="30a6d-189">Msg 35346, 15 poziom, stan 1, wiersz 44 PODZIELONY klauzula instrukcji ALTER PARTITION nie powiodło się, ponieważ partycja hello nie jest pusty.</span><span class="sxs-lookup"><span data-stu-id="30a6d-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because hello partition is not empty.</span></span>  <span data-ttu-id="30a6d-190">Gdy istnieje indeks magazynu kolumn w tabeli hello można podzielić tylko puste partycje w.</span><span class="sxs-lookup"><span data-stu-id="30a6d-190">Only empty partitions can be split in when a columnstore index exists on hello table.</span></span> <span data-ttu-id="30a6d-191">Rozważ wyłączenie indeksu magazynu kolumn hello przed wykonaniem instrukcji ALTER PARTITION hello, a następnie odbudowanie indeksu magazynu kolumn powitania po ukończeniu operacji ALTER PARTITION.</span><span class="sxs-lookup"><span data-stu-id="30a6d-191">Consider disabling hello columnstore index before issuing hello ALTER PARTITION statement, then rebuilding hello columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="30a6d-192">Jednak używamy `CTAS` toocreate nowe toohold tabeli danych.</span><span class="sxs-lookup"><span data-stu-id="30a6d-192">However, we can use `CTAS` toocreate a new table toohold our data.</span></span>

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

<span data-ttu-id="30a6d-193">Jak hello granice partycji są wyrównane przełącznik jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="30a6d-193">As hello partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="30a6d-194">Spowoduje to pozostawienie tabeli źródłowej hello z pustą partycję, który następnie możemy podzielić.</span><span class="sxs-lookup"><span data-stu-id="30a6d-194">This will leave hello source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="30a6d-195">Pozostało toodo jest tooalign toohello naszych danych partycji nowych granic przy użyciu `CTAS` i przejdź wstecz w tabeli głównej toohello naszych danych</span><span class="sxs-lookup"><span data-stu-id="30a6d-195">All that is left toodo is tooalign our data toohello new partition boundaries using `CTAS` and switch our data back in toohello main table</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

<span data-ttu-id="30a6d-196">Po zakończeniu hello przepływu danych hello jest dobrym rozwiązaniem toorefresh hello statystyk na powitania docelowej tabeli tooensure hello dystrybucji nowych danych hello w ich odpowiednich partycji dokładnie odzwierciedlał:</span><span class="sxs-lookup"><span data-stu-id="30a6d-196">Once you have completed hello movement of hello data it is a good idea toorefresh hello statistics on hello target table tooensure they accurately reflect hello new distribution of hello data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="30a6d-197">Tabela partycjonowania kontroli źródła</span><span class="sxs-lookup"><span data-stu-id="30a6d-197">Table partitioning source control</span></span>
<span data-ttu-id="30a6d-198">tooavoid Twojego definicji tabeli z **uszkodzona** w systemie kontroli źródła może być hello tooconsider następujące podejście:</span><span class="sxs-lookup"><span data-stu-id="30a6d-198">tooavoid your table definition from **rusting** in your source control system you may want tooconsider hello following approach:</span></span>

1. <span data-ttu-id="30a6d-199">Utwórz hello tabeli partycjonowanej tabeli, ale bez wartości partycji</span><span class="sxs-lookup"><span data-stu-id="30a6d-199">Create hello table as a partitioned table but with no partition values</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. <span data-ttu-id="30a6d-200">`SPLIT`Tabela Hello jako część procesu wdrażania hello:</span><span class="sxs-lookup"><span data-stu-id="30a6d-200">`SPLIT` hello table as part of hello deployment process:</span></span>

```sql
-- Create a table containing hello partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over hello partition boundaries and split hello table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

<span data-ttu-id="30a6d-201">Z tego podejścia hello pozostaje statyczna kodu w kontroli źródła i partycjonowania wartości granicznych hello mogą toobe dynamiczne; zmieniających się z magazynem hello wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="30a6d-201">With this approach hello code in source control remains static and hello partitioning boundary values are allowed toobe dynamic; evolving with hello warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30a6d-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30a6d-202">Next steps</span></span>
<span data-ttu-id="30a6d-203">toolearn więcej, zobacz artykuły hello na [omówienie tabeli][Overview], [typy danych tabeli][Data Types], [Dystrybucja tabeli] [ Distribute], [Indeksowania tabeli][Index], [utrzymania statystyk tabeli] [ Statistics] i [ Tabele tymczasowe][Temporary].</span><span class="sxs-lookup"><span data-stu-id="30a6d-203">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="30a6d-204">Aby uzyskać więcej informacji na temat najlepszych rozwiązań, zobacz [najlepsze rozwiązania magazynu danych SQL][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="30a6d-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
