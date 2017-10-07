---
title: "aaaMonitor obciążenia przy użyciu widoków DMV | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor obciążenia przy użyciu widoków DMV."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 69ecd479-0941-48df-b3d0-cf54c79e6549
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: acccf952d165ccec3de3b4b1c633b18bbbf78077
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="c5705-103">Monitor your workload using DMVs</span><span class="sxs-lookup"><span data-stu-id="c5705-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="c5705-104">W tym artykule opisano sposób toomonitor dynamicznych widoków zarządzania (widoków DMV) toouse obciążenie i zbadaj wykonywania zapytania w usłudze Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c5705-104">This article describes how toouse Dynamic Management Views (DMVs) toomonitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="c5705-105">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="c5705-105">Permissions</span></span>
<span data-ttu-id="c5705-106">Witaj tooquery widoków DMV w tym artykule potrzebne jest uprawnienie do stanu bazy danych WIDOKU lub FORMANTU.</span><span class="sxs-lookup"><span data-stu-id="c5705-106">tooquery hello DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="c5705-107">Zazwyczaj udzielającym stan bazy danych w WIDOKU jest uprawnienie hello preferowane, ponieważ jest bardziej restrykcyjne.</span><span class="sxs-lookup"><span data-stu-id="c5705-107">Usually granting VIEW DATABASE STATE is hello preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="c5705-108">Monitor połączenia</span><span class="sxs-lookup"><span data-stu-id="c5705-108">Monitor connections</span></span>
<span data-ttu-id="c5705-109">Wszystkie tooSQL logowania do magazynu danych są rejestrowane za[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="c5705-109">All logins tooSQL Data Warehouse are logged too[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="c5705-110">Ta DMV zawiera hello ostatniego logowania do 10 000.</span><span class="sxs-lookup"><span data-stu-id="c5705-110">This DMV contains hello last 10,000 logins.</span></span>  <span data-ttu-id="c5705-111">Hello session_id jest hello klucza podstawowego i ma przypisany sekwencyjnie dla każdego nowego logowania.</span><span class="sxs-lookup"><span data-stu-id="c5705-111">hello session_id is hello primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="c5705-112">Wykonywanie zapytania monitora</span><span class="sxs-lookup"><span data-stu-id="c5705-112">Monitor query execution</span></span>
<span data-ttu-id="c5705-113">Wszystkie zapytania wykonywane w magazynie danych SQL są rejestrowane za[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="c5705-113">All queries executed on SQL Data Warehouse are logged too[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="c5705-114">Ta DMV zawiera hello ostatni 10 000 zapytania są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="c5705-114">This DMV contains hello last 10,000 queries executed.</span></span>  <span data-ttu-id="c5705-115">Hello request_id unikatowo identyfikuje każde zapytanie i jest hello klucz podstawowy dla tego DMV.</span><span class="sxs-lookup"><span data-stu-id="c5705-115">hello request_id uniquely identifies each query and is hello primary key for this DMV.</span></span>  <span data-ttu-id="c5705-116">Hello request_id jest przypisany sekwencyjnie dla każdego nowego zapytania i jest poprzedzony QID, który oznacza identyfikator zapytania.</span><span class="sxs-lookup"><span data-stu-id="c5705-116">hello request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="c5705-117">Wykonywanie zapytania DMV ten dla danego session_id zawiera wszystkie zapytania dotyczące danego logowania.</span><span class="sxs-lookup"><span data-stu-id="c5705-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="c5705-118">Procedury składowane używać wielu identyfikatorów żądania.</span><span class="sxs-lookup"><span data-stu-id="c5705-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="c5705-119">Identyfikatory żądania są przypisywane w kolejności sekwencyjnej.</span><span class="sxs-lookup"><span data-stu-id="c5705-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="c5705-120">Poniżej przedstawiono planów wykonywania kwerend tooinvestigate toofollow kroki i godziny dla określonego zapytania.</span><span class="sxs-lookup"><span data-stu-id="c5705-120">Here are steps toofollow tooinvestigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a><span data-ttu-id="c5705-121">: Krok 1 zapytanie hello się, że chcesz tooinvestigate</span><span class="sxs-lookup"><span data-stu-id="c5705-121">STEP 1: Identify hello query you wish tooinvestigate</span></span>
```sql
-- Monitor active queries
SELECT * 
FROM sys.dm_pdw_exec_requests 
WHERE status not in ('Completed','Failed','Cancelled')
  AND session_id <> session_id()
ORDER BY submit_time DESC;

-- Find top 10 queries longest running queries
SELECT TOP 10 * 
FROM sys.dm_pdw_exec_requests 
ORDER BY total_elapsed_time DESC;

-- Find a query with hello Label 'My Query'
-- Use brackets when querying hello label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="c5705-122">Z hello poprzedzających wyników zapytania **Uwaga hello identyfikator żądania** hello zapytania, które chcesz tooinvestigate.</span><span class="sxs-lookup"><span data-stu-id="c5705-122">From hello preceding query results, **note hello Request ID** of hello query that you would like tooinvestigate.</span></span>

<span data-ttu-id="c5705-123">Zapytania w hello **zawieszone** stanu jest umieszczany w kolejce powodu tooconcurrency limity.</span><span class="sxs-lookup"><span data-stu-id="c5705-123">Queries in hello **Suspended** state are being queued due tooconcurrency limits.</span></span> <span data-ttu-id="c5705-124">Te zapytania są również wyświetlane hello sys.dm_pdw_waits czeka zapytania z typem UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="c5705-124">These queries also appear in hello sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="c5705-125">Zobacz [zarządzania współbieżności i obciążenia] [ Concurrency and workload management] uzyskać więcej informacji dotyczących ograniczeń współbieżności.</span><span class="sxs-lookup"><span data-stu-id="c5705-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="c5705-126">Zapytania można również poczekać z innych powodów, takich jak uzyskać blokady obiektu.</span><span class="sxs-lookup"><span data-stu-id="c5705-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="c5705-127">Jeśli zapytanie oczekuje dla zasobu, zobacz [badanie zapytania oczekiwania na zasoby] [ Investigating queries waiting for resources] dalsze w dół w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="c5705-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="c5705-128">Wyszukiwanie hello toosimplify zapytania w tabeli sys.dm_pdw_exec_requests hello, użyj [etykiety] [ LABEL] tooassign zapytanie tooyour komentarza, które można przeszukiwać w widoku sys.dm_pdw_exec_requests hello.</span><span class="sxs-lookup"><span data-stu-id="c5705-128">toosimplify hello lookup of a query in hello sys.dm_pdw_exec_requests table, use [LABEL][LABEL] tooassign a comment tooyour query that can be looked up in hello sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a><span data-ttu-id="c5705-129">Krok 2: Zbadaj hello planu zapytania</span><span class="sxs-lookup"><span data-stu-id="c5705-129">STEP 2: Investigate hello query plan</span></span>
<span data-ttu-id="c5705-130">Użyj hello identyfikator żądania tooretrieve hello zapytania rozproszone planu SQL (DSQL) z [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="c5705-130">Use hello Request ID tooretrieve hello query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="c5705-131">DSQL plan trwa dłużej niż oczekiwano, hello przyczyną może być planu złożonych z wielu kroków DSQL lub tylko jeden krok zajmuje dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="c5705-131">When a DSQL plan is taking longer than expected, hello cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="c5705-132">Jeśli hello plan jest wiele kroków z kilku operacji przenoszenia, należy wziąć pod uwagę optymalizacji przenoszenia danych z tabeli dystrybucje tooreduce.</span><span class="sxs-lookup"><span data-stu-id="c5705-132">If hello plan is many steps with several move operations, consider optimizing your table distributions tooreduce data movement.</span></span> <span data-ttu-id="c5705-133">Witaj [tabeli dystrybucji] [ Table distribution] artykule wyjaśniono, dlaczego dane muszą być przeniesiony toosolve zapytania i opisano niektóre przenoszenia danych toominimize strategii dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="c5705-133">hello [Table distribution][Table distribution] article explains why data must be moved toosolve a query and explains some distribution strategies toominimize data movement.</span></span>

<span data-ttu-id="c5705-134">tooinvestigate bardziej szczegółowe informacje dotyczące jednego kroku, hello *operation_type* kolumny hello kroku i zanotuj, długotrwałą kwerendę hello **indeks kroku**:</span><span class="sxs-lookup"><span data-stu-id="c5705-134">tooinvestigate further details about a single step, hello *operation_type* column of hello long-running query step and note hello **Step Index**:</span></span>

* <span data-ttu-id="c5705-135">Kontynuuj krok 3a dla **operacji SQL**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="c5705-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="c5705-136">Kontynuuj krok 3b dla **operacji przenoszenia danych**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="c5705-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a><span data-ttu-id="c5705-137">KROK 3a: badanie na powitania rozproszonych bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="c5705-137">STEP 3a: Investigate SQL on hello distributed databases</span></span>
<span data-ttu-id="c5705-138">Użyj hello identyfikator żądania i szczegóły tooretrieve indeks kroku hello [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], który zawiera informacje o wykonanie kroku zapytania hello na wszystkich hello rozproszonych bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c5705-138">Use hello Request ID and hello Step Index tooretrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of hello query step on all of hello distributed databases.</span></span>

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="c5705-139">Po uruchomieniu kroku zapytania hello [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] mogą być używane tooretrieve hello programu SQL Server szacowany plan z hello pamięci podręcznej planu programu SQL Server dla kroku hello systemem określonego dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="c5705-139">When hello query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello step running on a particular distribution.</span></span>

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a><span data-ttu-id="c5705-140">KROK 3b: badanie przenoszenia danych w bazach danych hello rozproszonych</span><span class="sxs-lookup"><span data-stu-id="c5705-140">STEP 3b: Investigate data movement on hello distributed databases</span></span>
<span data-ttu-id="c5705-141">Użyj hello identyfikator żądania i hello indeks kroku tooretrieve informacji o uruchomionych na poszczególnych dystrybucji z krokiem przepływu danych [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="c5705-141">Use hello Request ID and hello Step Index tooretrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="c5705-142">Sprawdź hello *total_elapsed_time* toosee kolumny, jeśli określonym dystrybucyjne trwa znacznie dłużej niż innych do przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="c5705-142">Check hello *total_elapsed_time* column toosee if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="c5705-143">Witaj długotrwałe dystrybucji, sprawdź hello *rows_processed* toosee kolumny hello liczba wierszy jest przenoszony z tą dystrybucją jest znacznie większa niż inne.</span><span class="sxs-lookup"><span data-stu-id="c5705-143">For hello long-running distribution, check hello *rows_processed* column toosee if hello number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="c5705-144">Jeśli tak, może to oznaczać pochylenia danych podstawowych.</span><span class="sxs-lookup"><span data-stu-id="c5705-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="c5705-145">Jeśli zapytanie hello jest uruchomiona, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] mogą być używane tooretrieve hello programu SQL Server szacowany plan z hello pamięci podręcznej planu programu SQL Server dla hello aktualnie uruchomione w ramach danego kroku SQL dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="c5705-145">If hello query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="c5705-146">Monitor oczekujących zapytań</span><span class="sxs-lookup"><span data-stu-id="c5705-146">Monitor waiting queries</span></span>
<span data-ttu-id="c5705-147">Jeśli użytkownik stwierdzi, że zapytanie jest nie czyni postępy, ponieważ oczekuje dla zasobu, w tym miejscu jest kwerendę, która zawiera wszystkie zasoby hello kwerendy oczekuje na.</span><span class="sxs-lookup"><span data-stu-id="c5705-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all hello resources a query is waiting for.</span></span>

```sql
-- Find queries 
-- Replace request_id with value from Step 1.

SELECT waits.session_id,
      waits.request_id,  
      requests.command,
      requests.status,
      requests.start_time,  
      waits.type,
      waits.state,
      waits.object_type,
      waits.object_name
FROM   sys.dm_pdw_waits waits
   JOIN  sys.dm_pdw_exec_requests requests
   ON waits.request_id=requests.request_id
WHERE waits.request_id = 'QID####'
ORDER BY waits.object_name, waits.object_type, waits.state;
```

<span data-ttu-id="c5705-148">Jeśli zapytanie hello aktywnie oczekuje na zasoby z innego zapytania, a następnie hello stan zostanie **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="c5705-148">If hello query is actively waiting on resources from another query, then hello state will be **AcquireResources**.</span></span>  <span data-ttu-id="c5705-149">Jeśli zapytanie hello ma wszystkie zasoby hello wymagane, a następnie hello stan zostanie **przyznany**.</span><span class="sxs-lookup"><span data-stu-id="c5705-149">If hello query has all hello required resources, then hello state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="c5705-150">Monitor tempdb</span><span class="sxs-lookup"><span data-stu-id="c5705-150">Monitor tempdb</span></span>
<span data-ttu-id="c5705-151">Tempdb wysokie wykorzystanie można przyczynę hello niską wydajnością i poza problemy z pamięcią.</span><span class="sxs-lookup"><span data-stu-id="c5705-151">High tempdb utilization can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="c5705-152">Najpierw sprawdź, czy masz rowgroups pochylenia lub niska jakość danych i podjąć odpowiednie działania hello.</span><span class="sxs-lookup"><span data-stu-id="c5705-152">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="c5705-153">Należy rozważyć skalowania magazynu danych, jeśli okaże się osiągnięcia limitów jego podczas wykonywania kwerendy w bazie danych tempdb.</span><span class="sxs-lookup"><span data-stu-id="c5705-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="c5705-154">Witaj poniżej opisano sposób użycia bazy danych tempdb tooidentify ciągu zapytania w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="c5705-154">hello following describes how tooidentify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="c5705-155">Utwórz hello następującego widoku tooassociate hello węzła odpowiedni identyfikator sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="c5705-155">Create hello following view tooassociate hello appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="c5705-156">Zostanie włączony możesz tooleverage innych przekazujące widoków DMV i Dołącz do tych tabel z sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="c5705-156">This will enable you tooleverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with hello correct node id
CREATE VIEW sql_requests AS
(SELECT
       sr.request_id,
       sr.step_index,
       (CASE 
              WHEN (sr.distribution_id = -1 ) THEN 
              (SELECT pdw_node_id FROM sys.dm_pdw_nodes WHERE type = 'CONTROL') 
              ELSE d.pdw_node_id END) AS pdw_node_id,
       sr.distribution_id,
       sr.status,
       sr.error_id,
       sr.start_time,
       sr.end_time,
       sr.total_elapsed_time,
       sr.row_count,
       sr.spid,
       sr.command
FROM sys.pdw_distributions AS d
RIGHT JOIN sys.dm_pdw_sql_requests AS sr ON d.distribution_id = sr.distribution_id)
```
<span data-ttu-id="c5705-157">Witaj uruchom następujące zapytanie bazy danych tempdb toomonitor:</span><span class="sxs-lookup"><span data-stu-id="c5705-157">Run hello following query toomonitor tempdb:</span></span>

```sql
-- Monitor tempdb
SELECT
    sr.request_id,
    ssu.session_id,
    ssu.pdw_node_id,
    sr.command,
    sr.total_elapsed_time,
    es.login_name AS 'LoginName',
    DB_NAME(ssu.database_id) AS 'DatabaseName',
    (es.memory_usage * 8) AS 'MemoryUsage (in KB)',
    (ssu.user_objects_alloc_page_count * 8) AS 'Space Allocated For User Objects (in KB)',
    (ssu.user_objects_dealloc_page_count * 8) AS 'Space Deallocated For User Objects (in KB)',
    (ssu.internal_objects_alloc_page_count * 8) AS 'Space Allocated For Internal Objects (in KB)',
    (ssu.internal_objects_dealloc_page_count * 8) AS 'Space Deallocated For Internal Objects (in KB)',
    CASE es.is_user_process
    WHEN 1 THEN 'User Session'
    WHEN 0 THEN 'System Session'
    END AS 'SessionType',
    es.row_count AS 'RowCount'
FROM sys.dm_pdw_nodes_db_session_space_usage AS ssu
    INNER JOIN sys.dm_pdw_nodes_exec_sessions AS es ON ssu.session_id = es.session_id AND ssu.pdw_node_id = es.pdw_node_id
    INNER JOIN sys.dm_pdw_nodes_exec_connections AS er ON ssu.session_id = er.session_id AND ssu.pdw_node_id = er.pdw_node_id
    INNER JOIN sql_requests AS sr ON ssu.session_id = sr.spid AND ssu.pdw_node_id = sr.pdw_node_id
WHERE DB_NAME(ssu.database_id) = 'tempdb'
    AND es.session_id <> @@SPID
    AND es.login_name <> 'sa' 
ORDER BY sr.request_id;
```
## <a name="monitor-memory"></a><span data-ttu-id="c5705-158">Monitor pamięci</span><span class="sxs-lookup"><span data-stu-id="c5705-158">Monitor memory</span></span>

<span data-ttu-id="c5705-159">Pamięć może być przyczynę hello niską wydajnością i poza problemy z pamięcią.</span><span class="sxs-lookup"><span data-stu-id="c5705-159">Memory can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="c5705-160">Najpierw sprawdź, czy masz rowgroups pochylenia lub niska jakość danych i podjąć odpowiednie działania hello.</span><span class="sxs-lookup"><span data-stu-id="c5705-160">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="c5705-161">Należy rozważyć skalowania magazynu danych, jeśli okaże się użycie pamięci programu SQL Server osiągnięcia limitów jego podczas wykonywania zapytania.</span><span class="sxs-lookup"><span data-stu-id="c5705-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="c5705-162">Witaj następujące zapytanie zwraca programu SQL Server wykorzystania użycia i pamięci pamięci na węzeł:</span><span class="sxs-lookup"><span data-stu-id="c5705-162">hello following query returns SQL Server memory usage and memory pressure per node:</span></span> 
```sql
-- Memory consumption
SELECT
  pc1.cntr_value as Curr_Mem_KB, 
  pc1.cntr_value/1024.0 as Curr_Mem_MB,
  (pc1.cntr_value/1048576.0) as Curr_Mem_GB,
  pc2.cntr_value as Max_Mem_KB,
  pc2.cntr_value/1024.0 as Max_Mem_MB,
  (pc2.cntr_value/1048576.0) as Max_Mem_GB,
  pc1.cntr_value * 100.0/pc2.cntr_value AS Memory_Utilization_Percentage,
  pc1.pdw_node_id
FROM
-- pc1: current memory
sys.dm_pdw_nodes_os_performance_counters AS pc1
-- pc2: total memory allowed for this SQL instance
JOIN sys.dm_pdw_nodes_os_performance_counters AS pc2 
ON pc1.object_name = pc2.object_name AND pc1.pdw_node_id = pc2.pdw_node_id
WHERE
pc1.counter_name = 'Total Server Memory (KB)'
AND pc2.counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="c5705-163">Rozmiar dziennika transakcji monitora</span><span class="sxs-lookup"><span data-stu-id="c5705-163">Monitor transaction log size</span></span>
<span data-ttu-id="c5705-164">Witaj następujące zapytanie zwraca rozmiar dziennika transakcji hello w poszczególnych dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="c5705-164">hello following query returns hello transaction log size on each distribution.</span></span> <span data-ttu-id="c5705-165">Sprawdź, czy masz rowgroups pochylenia lub niska jakość danych i podjąć odpowiednie działania hello.</span><span class="sxs-lookup"><span data-stu-id="c5705-165">Please check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="c5705-166">Jeśli jeden z plików dziennika hello wkrótce osiągnie 160GB, należy rozważyć skalowaniu wystąpienia lub ograniczenie rozmiar transakcji.</span><span class="sxs-lookup"><span data-stu-id="c5705-166">If one of hello log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
```sql
-- Transaction log size
SELECT
  instance_name as distribution_db,
  cntr_value*1.0/1048576 as log_file_size_used_GB,
  pdw_node_id 
FROM sys.dm_pdw_nodes_os_performance_counters 
WHERE 
instance_name like 'Distribution_%' 
AND counter_name = 'Log File(s) Used Size (KB)'
AND counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="c5705-167">Monitorowanie wycofywania dziennika transakcji</span><span class="sxs-lookup"><span data-stu-id="c5705-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="c5705-168">Jeśli kwerendy kończą się niepowodzeniem lub biorąc tooproceed dużo czasu, można sprawdzić i monitorować, jeśli masz wszystkich wycofywanie transakcji.</span><span class="sxs-lookup"><span data-stu-id="c5705-168">If your queries are failing or taking a long time tooproceed, you can check and monitor if you have any transactions rolling back.</span></span>
```sql
-- Monitor rollback
SELECT 
    SUM(CASE WHEN t.database_transaction_next_undo_lsn IS NOT NULL THEN 1 ELSE 0 END),
    t.pdw_node_id,
    nod.[type]
FROM sys.dm_pdw_nodes_tran_database_transactions t
JOIN sys.dm_pdw_nodes nod ON t.pdw_node_id = nod.pdw_node_id
GROUP BY t.pdw_node_id, nod.[type]
```

## <a name="next-steps"></a><span data-ttu-id="c5705-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c5705-169">Next steps</span></span>
<span data-ttu-id="c5705-170">Zobacz [widoków systemowych] [ System views] Aby uzyskać więcej informacji na temat widoków DMV.</span><span class="sxs-lookup"><span data-stu-id="c5705-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="c5705-171">Zobacz [najlepsze rozwiązania w zakresie usługi SQL Data Warehouse] [ SQL Data Warehouse best practices] Aby uzyskać więcej informacji na temat najlepszych rozwiązań</span><span class="sxs-lookup"><span data-stu-id="c5705-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

<!--Image references-->

<!--Article references-->
[Manage overview]: ./sql-data-warehouse-overview-manage.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Investigating queries waiting for resources]: ./sql-data-warehouse-manage-monitor.md#waiting

<!--MSDN references-->
[sys.dm_pdw_dms_workers]: http://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_exec_requests]: http://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_exec_sessions]: http://msdn.microsoft.com/library/mt203883.aspx
[sys.dm_pdw_request_steps]: http://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: http://msdn.microsoft.com/library/mt203889.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: http://msdn.microsoft.com/library/mt204017.aspx
[DBCC PDW_SHOWSPACEUSED]: http://msdn.microsoft.com/library/mt204028.aspx
[LABEL]: https://msdn.microsoft.com/library/ms190322.aspx
