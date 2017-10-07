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
# <a name="monitor-your-workload-using-dmvs"></a>Monitor your workload using DMVs
W tym artykule opisano sposób toomonitor dynamicznych widoków zarządzania (widoków DMV) toouse obciążenie i zbadaj wykonywania zapytania w usłudze Azure SQL Data Warehouse.

## <a name="permissions"></a>Uprawnienia
Witaj tooquery widoków DMV w tym artykule potrzebne jest uprawnienie do stanu bazy danych WIDOKU lub FORMANTU. Zazwyczaj udzielającym stan bazy danych w WIDOKU jest uprawnienie hello preferowane, ponieważ jest bardziej restrykcyjne.

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a>Monitor połączenia
Wszystkie tooSQL logowania do magazynu danych są rejestrowane za[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].  Ta DMV zawiera hello ostatniego logowania do 10 000.  Hello session_id jest hello klucza podstawowego i ma przypisany sekwencyjnie dla każdego nowego logowania.

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a>Wykonywanie zapytania monitora
Wszystkie zapytania wykonywane w magazynie danych SQL są rejestrowane za[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].  Ta DMV zawiera hello ostatni 10 000 zapytania są wykonywane.  Hello request_id unikatowo identyfikuje każde zapytanie i jest hello klucz podstawowy dla tego DMV.  Hello request_id jest przypisany sekwencyjnie dla każdego nowego zapytania i jest poprzedzony QID, który oznacza identyfikator zapytania.  Wykonywanie zapytania DMV ten dla danego session_id zawiera wszystkie zapytania dotyczące danego logowania.

> [!NOTE]
> Procedury składowane używać wielu identyfikatorów żądania.  Identyfikatory żądania są przypisywane w kolejności sekwencyjnej. 
> 
> 

Poniżej przedstawiono planów wykonywania kwerend tooinvestigate toofollow kroki i godziny dla określonego zapytania.

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a>: Krok 1 zapytanie hello się, że chcesz tooinvestigate
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

Z hello poprzedzających wyników zapytania **Uwaga hello identyfikator żądania** hello zapytania, które chcesz tooinvestigate.

Zapytania w hello **zawieszone** stanu jest umieszczany w kolejce powodu tooconcurrency limity. Te zapytania są również wyświetlane hello sys.dm_pdw_waits czeka zapytania z typem UserConcurrencyResourceType. Zobacz [zarządzania współbieżności i obciążenia] [ Concurrency and workload management] uzyskać więcej informacji dotyczących ograniczeń współbieżności. Zapytania można również poczekać z innych powodów, takich jak uzyskać blokady obiektu.  Jeśli zapytanie oczekuje dla zasobu, zobacz [badanie zapytania oczekiwania na zasoby] [ Investigating queries waiting for resources] dalsze w dół w tym artykule.

Wyszukiwanie hello toosimplify zapytania w tabeli sys.dm_pdw_exec_requests hello, użyj [etykiety] [ LABEL] tooassign zapytanie tooyour komentarza, które można przeszukiwać w widoku sys.dm_pdw_exec_requests hello.

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a>Krok 2: Zbadaj hello planu zapytania
Użyj hello identyfikator żądania tooretrieve hello zapytania rozproszone planu SQL (DSQL) z [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

DSQL plan trwa dłużej niż oczekiwano, hello przyczyną może być planu złożonych z wielu kroków DSQL lub tylko jeden krok zajmuje dużo czasu.  Jeśli hello plan jest wiele kroków z kilku operacji przenoszenia, należy wziąć pod uwagę optymalizacji przenoszenia danych z tabeli dystrybucje tooreduce. Witaj [tabeli dystrybucji] [ Table distribution] artykule wyjaśniono, dlaczego dane muszą być przeniesiony toosolve zapytania i opisano niektóre przenoszenia danych toominimize strategii dystrybucji.

tooinvestigate bardziej szczegółowe informacje dotyczące jednego kroku, hello *operation_type* kolumny hello kroku i zanotuj, długotrwałą kwerendę hello **indeks kroku**:

* Kontynuuj krok 3a dla **operacji SQL**: OnOperation, RemoteOperation, ReturnOperation.
* Kontynuuj krok 3b dla **operacji przenoszenia danych**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a>KROK 3a: badanie na powitania rozproszonych bazy danych SQL
Użyj hello identyfikator żądania i szczegóły tooretrieve indeks kroku hello [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], który zawiera informacje o wykonanie kroku zapytania hello na wszystkich hello rozproszonych bazy danych.

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

Po uruchomieniu kroku zapytania hello [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] mogą być używane tooretrieve hello programu SQL Server szacowany plan z hello pamięci podręcznej planu programu SQL Server dla kroku hello systemem określonego dystrybucji.

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a>KROK 3b: badanie przenoszenia danych w bazach danych hello rozproszonych
Użyj hello identyfikator żądania i hello indeks kroku tooretrieve informacji o uruchomionych na poszczególnych dystrybucji z krokiem przepływu danych [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* Sprawdź hello *total_elapsed_time* toosee kolumny, jeśli określonym dystrybucyjne trwa znacznie dłużej niż innych do przenoszenia danych.
* Witaj długotrwałe dystrybucji, sprawdź hello *rows_processed* toosee kolumny hello liczba wierszy jest przenoszony z tą dystrybucją jest znacznie większa niż inne. Jeśli tak, może to oznaczać pochylenia danych podstawowych.

Jeśli zapytanie hello jest uruchomiona, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] mogą być używane tooretrieve hello programu SQL Server szacowany plan z hello pamięci podręcznej planu programu SQL Server dla hello aktualnie uruchomione w ramach danego kroku SQL dystrybucji.

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a>Monitor oczekujących zapytań
Jeśli użytkownik stwierdzi, że zapytanie jest nie czyni postępy, ponieważ oczekuje dla zasobu, w tym miejscu jest kwerendę, która zawiera wszystkie zasoby hello kwerendy oczekuje na.

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

Jeśli zapytanie hello aktywnie oczekuje na zasoby z innego zapytania, a następnie hello stan zostanie **AcquireResources**.  Jeśli zapytanie hello ma wszystkie zasoby hello wymagane, a następnie hello stan zostanie **przyznany**.

## <a name="monitor-tempdb"></a>Monitor tempdb
Tempdb wysokie wykorzystanie można przyczynę hello niską wydajnością i poza problemy z pamięcią. Najpierw sprawdź, czy masz rowgroups pochylenia lub niska jakość danych i podjąć odpowiednie działania hello. Należy rozważyć skalowania magazynu danych, jeśli okaże się osiągnięcia limitów jego podczas wykonywania kwerendy w bazie danych tempdb. Witaj poniżej opisano sposób użycia bazy danych tempdb tooidentify ciągu zapytania w każdym węźle. 

Utwórz hello następującego widoku tooassociate hello węzła odpowiedni identyfikator sys.dm_pdw_sql_requests. Zostanie włączony możesz tooleverage innych przekazujące widoków DMV i Dołącz do tych tabel z sys.dm_pdw_sql_requests.

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
Witaj uruchom następujące zapytanie bazy danych tempdb toomonitor:

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
## <a name="monitor-memory"></a>Monitor pamięci

Pamięć może być przyczynę hello niską wydajnością i poza problemy z pamięcią. Najpierw sprawdź, czy masz rowgroups pochylenia lub niska jakość danych i podjąć odpowiednie działania hello. Należy rozważyć skalowania magazynu danych, jeśli okaże się użycie pamięci programu SQL Server osiągnięcia limitów jego podczas wykonywania zapytania.

Witaj następujące zapytanie zwraca programu SQL Server wykorzystania użycia i pamięci pamięci na węzeł: 
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
## <a name="monitor-transaction-log-size"></a>Rozmiar dziennika transakcji monitora
Witaj następujące zapytanie zwraca rozmiar dziennika transakcji hello w poszczególnych dystrybucji. Sprawdź, czy masz rowgroups pochylenia lub niska jakość danych i podjąć odpowiednie działania hello. Jeśli jeden z plików dziennika hello wkrótce osiągnie 160GB, należy rozważyć skalowaniu wystąpienia lub ograniczenie rozmiar transakcji. 
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
## <a name="monitor-transaction-log-rollback"></a>Monitorowanie wycofywania dziennika transakcji
Jeśli kwerendy kończą się niepowodzeniem lub biorąc tooproceed dużo czasu, można sprawdzić i monitorować, jeśli masz wszystkich wycofywanie transakcji.
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

## <a name="next-steps"></a>Następne kroki
Zobacz [widoków systemowych] [ System views] Aby uzyskać więcej informacji na temat widoków DMV.
Zobacz [najlepsze rozwiązania w zakresie usługi SQL Data Warehouse] [ SQL Data Warehouse best practices] Aby uzyskać więcej informacji na temat najlepszych rozwiązań

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
