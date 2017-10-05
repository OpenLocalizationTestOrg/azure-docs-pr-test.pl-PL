---
title: "Monitorowanie bazy danych Azure SQL przy użyciu dynamicznych widoków zarządzania | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wykrywanie i diagnozowanie typowych problemów z wydajnością przy użyciu dynamicznych widoków zarządzania do monitorowania programu Microsoft Azure SQL Database."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: d08f505f-3c62-47d4-bab7-35c9a834b79b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: d9b007d29e06e672db71b4a8415673f258c3fd89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="f8e82-103">Monitorowanie usługi Azure SQL Database przy użyciu dynamicznych widoków zarządzania</span><span class="sxs-lookup"><span data-stu-id="f8e82-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="f8e82-104">Baza danych SQL Azure Microsoft umożliwia podzbiór dynamicznych widoków zarządzania do diagnozowania problemów z wydajnością, które mogą być spowodowane przez zablokowane lub długotrwałe zapytań, wąskich gardeł w zasobach, plany zapytań niska i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="f8e82-104">Microsoft Azure SQL Database enables a subset of dynamic management views to diagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="f8e82-105">Ten temat zawiera informacje na temat sposobu wykryć typowych problemów z wydajnością przy użyciu dynamicznych widoków zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f8e82-105">This topic provides information on how to detect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="f8e82-106">Baza danych SQL obsługuje częściowo dynamicznych widoków zarządzania trzy kategorie:</span><span class="sxs-lookup"><span data-stu-id="f8e82-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="f8e82-107">Związane z bazy danych dynamicznych widoków zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f8e82-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="f8e82-108">Powiązane z wykonywaniem dynamicznych widoków zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f8e82-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="f8e82-109">Związane z transakcji dynamicznych widoków zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f8e82-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="f8e82-110">Aby uzyskać szczegółowe informacje o dynamicznych widoków zarządzania, zobacz [dynamicznych widoków zarządzania i funkcji (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) w dokumentacji SQL Server — książki Online.</span><span class="sxs-lookup"><span data-stu-id="f8e82-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="f8e82-111">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="f8e82-111">Permissions</span></span>
<span data-ttu-id="f8e82-112">W bazie danych SQL, zapytanie widoku dynamicznego zarządzania wymaga **stan bazy danych WIDOKU** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="f8e82-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="f8e82-113">**Stan bazy danych WIDOKU** uprawnienia zwraca informacje o wszystkich obiektów w bieżącej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f8e82-113">The **VIEW DATABASE STATE** permission returns information about all objects within the current database.</span></span>
<span data-ttu-id="f8e82-114">Aby przyznać **stan WIDOKU bazy danych** uprawnienia do użytkownika określonej bazy danych, uruchom następujące zapytanie:</span><span class="sxs-lookup"><span data-stu-id="f8e82-114">To grant the **VIEW DATABASE STATE** permission to a specific database user, run the following query:</span></span>

```GRANT VIEW DATABASE STATE TO database_user; ```

<span data-ttu-id="f8e82-115">W wystąpieniu programu SQL Server, lokalną dynamicznych widoków zarządzania zwraca informacje o stanie serwera.</span><span class="sxs-lookup"><span data-stu-id="f8e82-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="f8e82-116">W bazie danych SQL zwracają informacje dotyczące bieżącej logicznej bazy danych tylko.</span><span class="sxs-lookup"><span data-stu-id="f8e82-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="f8e82-117">Obliczanie rozmiaru bazy danych</span><span class="sxs-lookup"><span data-stu-id="f8e82-117">Calculating database size</span></span>
<span data-ttu-id="f8e82-118">Następujące zapytanie zwraca rozmiar bazy danych (w MB):</span><span class="sxs-lookup"><span data-stu-id="f8e82-118">The following query returns the size of your database (in megabytes):</span></span>

```
-- Calculates the size of the database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="f8e82-119">Następujące zapytanie zwraca rozmiar poszczególnych obiektów (w MB) w bazie danych:</span><span class="sxs-lookup"><span data-stu-id="f8e82-119">The following query returns the size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates the size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="f8e82-120">Monitorowanie połączeń</span><span class="sxs-lookup"><span data-stu-id="f8e82-120">Monitoring connections</span></span>
<span data-ttu-id="f8e82-121">Można użyć [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) widoku można pobrać informacji dotyczących połączeń ustanowionych na określonym serwerze bazy danych SQL Azure i szczegóły każdego połączenia.</span><span class="sxs-lookup"><span data-stu-id="f8e82-121">You can use the [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view to retrieve information about the connections established to a specific Azure SQL Database server and the details of each connection.</span></span> <span data-ttu-id="f8e82-122">Ponadto [widoku sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) widok jest przydatne podczas pobierania informacji o wszystkich aktywnych sesji użytkowników i zadań wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="f8e82-122">In addition, the [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="f8e82-123">Następujące zapytanie pobiera informacje o bieżącym połączeniem:</span><span class="sxs-lookup"><span data-stu-id="f8e82-123">The following query retrieves information on the current connection:</span></span>

```
SELECT
    c.session_id, c.net_transport, c.encrypt_option,
    c.auth_scheme, s.host_name, s.program_name,
    s.client_interface_name, s.login_name, s.nt_domain,
    s.nt_user_name, s.original_login_name, c.connect_time,
    s.login_time
FROM sys.dm_exec_connections AS c
JOIN sys.dm_exec_sessions AS s
    ON c.session_id = s.session_id
WHERE c.session_id = @@SPID;
```

> [!NOTE]
> <span data-ttu-id="f8e82-124">Podczas wykonywania **sys.dm_exec_requests** i **widoków widoku sys.dm_exec_sessions**, jeśli masz **stan WIDOKU bazy danych** uprawnień w bazie danych, zostanie wyświetlony, wszystkie wykonywania Sesje w bazie danych. w przeciwnym razie zostanie wyświetlony w bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="f8e82-124">When executing the **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on the database, you see all executing sessions on the database; otherwise, you see only the current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="f8e82-125">Monitorowanie wydajności kwerendy</span><span class="sxs-lookup"><span data-stu-id="f8e82-125">Monitoring query performance</span></span>
<span data-ttu-id="f8e82-126">Wolno lub czas uruchamiania zapytań może wykorzystać zasoby systemowe znaczące.</span><span class="sxs-lookup"><span data-stu-id="f8e82-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="f8e82-127">W tej sekcji przedstawiono sposób użycia dynamicznych widoków zarządzania do wykrywania kilka typowych problemów wydajności zapytania.</span><span class="sxs-lookup"><span data-stu-id="f8e82-127">This section demonstrates how to use dynamic management views to detect a few common query performance problems.</span></span> <span data-ttu-id="f8e82-128">Starsze, ale nadal przydatne informacje dotyczące rozwiązywania problemów, jest [Rozwiązywanie problemów z wydajnością programu SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) artykułu w serwisie Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="f8e82-128">An older but still helpful reference for troubleshooting, is the [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="f8e82-129">Znajdowanie zapytania pierwszych N</span><span class="sxs-lookup"><span data-stu-id="f8e82-129">Finding top N queries</span></span>
<span data-ttu-id="f8e82-130">Poniższy przykład zwraca informacje o najważniejszych zapytań pięć uszeregowane według Średni czas procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="f8e82-130">The following example returns information about the top five queries ranked by average CPU time.</span></span> <span data-ttu-id="f8e82-131">W tym przykładzie agreguje zapytania zgodnie z ich skrótu zapytania, aby zapytania logicznie równoważne są pogrupowane według ich wykorzystania zasobów zbiorczą.</span><span class="sxs-lookup"><span data-stu-id="f8e82-131">This example aggregates the queries according to their query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

```
SELECT TOP 5 query_stats.query_hash AS "Query Hash",
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",
    MIN(query_stats.statement_text) AS "Statement Text"
FROM
    (SELECT QS.*,
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
    ((CASE statement_end_offset
        WHEN -1 THEN DATALENGTH(ST.text)
        ELSE QS.statement_end_offset END
            - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
```

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="f8e82-132">Monitorowanie zablokowanych zapytań</span><span class="sxs-lookup"><span data-stu-id="f8e82-132">Monitoring blocked queries</span></span>
<span data-ttu-id="f8e82-133">Wolne lub długotrwałe zapytania może przyczynić się do nadmiernego wykorzystania zasobów i być skutkiem zablokowanych zapytań.</span><span class="sxs-lookup"><span data-stu-id="f8e82-133">Slow or long-running queries can contribute to excessive resource consumption and be the consequence of blocked queries.</span></span> <span data-ttu-id="f8e82-134">Przyczyna blokady może być niewłaściwy projekt aplikacji, plany zapytania, brak przydatne indeksy i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="f8e82-134">The cause of the blocking can be poor application design, bad query plans, the lack of useful indexes, and so on.</span></span> <span data-ttu-id="f8e82-135">Widok sys.dm_tran_locks można użyć, aby uzyskać informacje dotyczące bieżącego działania blokady w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e82-135">You can use the sys.dm_tran_locks view to get information about the current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="f8e82-136">Na przykład kodu, zobacz [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) w dokumentacji SQL Server — książki Online.</span><span class="sxs-lookup"><span data-stu-id="f8e82-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="f8e82-137">Monitorowanie plany zapytań</span><span class="sxs-lookup"><span data-stu-id="f8e82-137">Monitoring query plans</span></span>
<span data-ttu-id="f8e82-138">Plan zapytania nieefektywne także może zwiększyć użycie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="f8e82-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="f8e82-139">W poniższym przykładzie użyto [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) widoku, aby określić, które zapytanie używa najbardziej zbiorczą procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="f8e82-139">The following example uses the [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view to determine which query uses the most cumulative CPU.</span></span>

```
SELECT
    highest_cpu_queries.plan_handle,
    highest_cpu_queries.total_worker_time,
    q.dbid,
    q.objectid,
    q.number,
    q.encrypted,
    q.[text]
FROM
    (SELECT TOP 50
        qs.plan_handle,
        qs.total_worker_time
    FROM
        sys.dm_exec_query_stats qs
    ORDER BY qs.total_worker_time desc) AS highest_cpu_queries
    CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS q
ORDER BY highest_cpu_queries.total_worker_time DESC;
```

## <a name="see-also"></a><span data-ttu-id="f8e82-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f8e82-140">See also</span></span>
[<span data-ttu-id="f8e82-141">Wprowadzenie do bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="f8e82-141">Introduction to SQL Database</span></span>](sql-database-technical-overview.md)

