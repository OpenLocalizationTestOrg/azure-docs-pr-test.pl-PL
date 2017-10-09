---
title: "aaaMonitoring Azure SQL bazy danych przy użyciu dynamicznych widoków zarządzania | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodetect i zdiagnozować typowe problemy z wydajnością przy użyciu toomonitor widoków dynamicznego zarządzania Microsoft Azure SQL Database."
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
ms.openlocfilehash: 43d5fe2dd9a38d031e9334f6ad49fce5866e3bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="b73ef-103">Monitorowanie usługi Azure SQL Database przy użyciu dynamicznych widoków zarządzania</span><span class="sxs-lookup"><span data-stu-id="b73ef-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="b73ef-104">Baza danych SQL Azure Microsoft umożliwia podzbiór dynamicznego zarządzania widokach toodiagnose wydajności problemów, które mogą być spowodowane przez zablokowane lub długotrwałe zapytań, wąskich gardeł w zasobach, plany zapytań niska i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="b73ef-104">Microsoft Azure SQL Database enables a subset of dynamic management views toodiagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="b73ef-105">Ten temat zawiera informacje na temat toodetect typowych problemów z wydajnością przy użyciu dynamicznych widoków zarządzania.</span><span class="sxs-lookup"><span data-stu-id="b73ef-105">This topic provides information on how toodetect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="b73ef-106">Baza danych SQL obsługuje częściowo dynamicznych widoków zarządzania trzy kategorie:</span><span class="sxs-lookup"><span data-stu-id="b73ef-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="b73ef-107">Związane z bazy danych dynamicznych widoków zarządzania.</span><span class="sxs-lookup"><span data-stu-id="b73ef-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="b73ef-108">Powiązane z wykonywaniem dynamicznych widoków zarządzania.</span><span class="sxs-lookup"><span data-stu-id="b73ef-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="b73ef-109">Związane z transakcji dynamicznych widoków zarządzania.</span><span class="sxs-lookup"><span data-stu-id="b73ef-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="b73ef-110">Aby uzyskać szczegółowe informacje o dynamicznych widoków zarządzania, zobacz [dynamicznych widoków zarządzania i funkcji (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) w dokumentacji SQL Server — książki Online.</span><span class="sxs-lookup"><span data-stu-id="b73ef-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="b73ef-111">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="b73ef-111">Permissions</span></span>
<span data-ttu-id="b73ef-112">W bazie danych SQL, zapytanie widoku dynamicznego zarządzania wymaga **stan bazy danych WIDOKU** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="b73ef-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="b73ef-113">Witaj **stan bazy danych WIDOKU** uprawnienia zwraca informacje o wszystkich obiektów w bieżącej bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="b73ef-113">hello **VIEW DATABASE STATE** permission returns information about all objects within hello current database.</span></span>
<span data-ttu-id="b73ef-114">Witaj toogrant **stan bazy danych WIDOKU** uprawnienia tooa określonej bazy danych użytkownika, uruchom następujące zapytanie hello:</span><span class="sxs-lookup"><span data-stu-id="b73ef-114">toogrant hello **VIEW DATABASE STATE** permission tooa specific database user, run hello following query:</span></span>

```GRANT VIEW DATABASE STATE toodatabase_user; ```

<span data-ttu-id="b73ef-115">W wystąpieniu programu SQL Server, lokalną dynamicznych widoków zarządzania zwraca informacje o stanie serwera.</span><span class="sxs-lookup"><span data-stu-id="b73ef-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="b73ef-116">W bazie danych SQL zwracają informacje dotyczące bieżącej logicznej bazy danych tylko.</span><span class="sxs-lookup"><span data-stu-id="b73ef-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="b73ef-117">Obliczanie rozmiaru bazy danych</span><span class="sxs-lookup"><span data-stu-id="b73ef-117">Calculating database size</span></span>
<span data-ttu-id="b73ef-118">Witaj następujące zapytanie zwraca hello rozmiar bazy danych (w MB):</span><span class="sxs-lookup"><span data-stu-id="b73ef-118">hello following query returns hello size of your database (in megabytes):</span></span>

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="b73ef-119">Witaj następujące zapytanie zwraca rozmiar hello pojedyncze obiekty (w MB) w bazie danych:</span><span class="sxs-lookup"><span data-stu-id="b73ef-119">hello following query returns hello size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="b73ef-120">Monitorowanie połączeń</span><span class="sxs-lookup"><span data-stu-id="b73ef-120">Monitoring connections</span></span>
<span data-ttu-id="b73ef-121">Można użyć hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) wyświetlić tooretrieve informacji dotyczących hello połączeń ustanowionych tooa określonej bazy danych SQL Azure serwera i hello szczegóły każdego połączenia.</span><span class="sxs-lookup"><span data-stu-id="b73ef-121">You can use hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view tooretrieve information about hello connections established tooa specific Azure SQL Database server and hello details of each connection.</span></span> <span data-ttu-id="b73ef-122">Ponadto hello [widoku sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) widok jest przydatne podczas pobierania informacji o wszystkich aktywnych sesji użytkowników i zadań wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="b73ef-122">In addition, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="b73ef-123">Witaj następujące zapytanie pobiera informacje o bieżącym połączeniu hello:</span><span class="sxs-lookup"><span data-stu-id="b73ef-123">hello following query retrieves information on hello current connection:</span></span>

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
> <span data-ttu-id="b73ef-124">Podczas wykonywania hello **sys.dm_exec_requests** i **widoków widoku sys.dm_exec_sessions**, jeśli masz **stan WIDOKU bazy danych** uprawnień w bazie danych hello, zostanie wyświetlony, wykonywanie wszystkich sesje na powitania bazy danych. w przeciwnym razie zostanie wyświetlony tylko hello bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="b73ef-124">When executing hello **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on hello database, you see all executing sessions on hello database; otherwise, you see only hello current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="b73ef-125">Monitorowanie wydajności kwerendy</span><span class="sxs-lookup"><span data-stu-id="b73ef-125">Monitoring query performance</span></span>
<span data-ttu-id="b73ef-126">Wolno lub czas uruchamiania zapytań może wykorzystać zasoby systemowe znaczące.</span><span class="sxs-lookup"><span data-stu-id="b73ef-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="b73ef-127">W tej sekcji przedstawiono sposób dynamicznego zarządzania toouse widoków toodetect kilka typowych problemów wydajności zapytania.</span><span class="sxs-lookup"><span data-stu-id="b73ef-127">This section demonstrates how toouse dynamic management views toodetect a few common query performance problems.</span></span> <span data-ttu-id="b73ef-128">Hello jest odwołanie do starszej, ale nadal przydatne przy rozwiązywaniu problemów, [Rozwiązywanie problemów z wydajnością programu SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) artykułu w serwisie Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="b73ef-128">An older but still helpful reference for troubleshooting, is hello [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="b73ef-129">Znajdowanie zapytania pierwszych N</span><span class="sxs-lookup"><span data-stu-id="b73ef-129">Finding top N queries</span></span>
<span data-ttu-id="b73ef-130">Witaj poniższy przykład zwraca informacje na temat hello najważniejszych zapytań pięć uszeregowane według Średni czas procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="b73ef-130">hello following example returns information about hello top five queries ranked by average CPU time.</span></span> <span data-ttu-id="b73ef-131">W tym przykładzie agreguje hello zapytania zapytanie skrótu, zgodnie z tootheir tak, aby zapytania logicznie równoważne są pogrupowane według ich wykorzystania zasobów zbiorczą.</span><span class="sxs-lookup"><span data-stu-id="b73ef-131">This example aggregates hello queries according tootheir query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

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

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="b73ef-132">Monitorowanie zablokowanych zapytań</span><span class="sxs-lookup"><span data-stu-id="b73ef-132">Monitoring blocked queries</span></span>
<span data-ttu-id="b73ef-133">Wolne lub długotrwałe zapytania można współtworzyć tooexcessive zużycia zasobów i być skutkiem hello zablokowanych zapytań.</span><span class="sxs-lookup"><span data-stu-id="b73ef-133">Slow or long-running queries can contribute tooexcessive resource consumption and be hello consequence of blocked queries.</span></span> <span data-ttu-id="b73ef-134">Witaj Przyczyna blokady hello może być niewłaściwy projekt aplikacji, zły plany zapytań hello braku przydatne indeksy i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="b73ef-134">hello cause of hello blocking can be poor application design, bad query plans, hello lack of useful indexes, and so on.</span></span> <span data-ttu-id="b73ef-135">Można użyć hello sys.dm_tran_locks widoku tooget informacji na temat hello bieżące działanie blokady w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b73ef-135">You can use hello sys.dm_tran_locks view tooget information about hello current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="b73ef-136">Na przykład kodu, zobacz [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) w dokumentacji SQL Server — książki Online.</span><span class="sxs-lookup"><span data-stu-id="b73ef-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="b73ef-137">Monitorowanie plany zapytań</span><span class="sxs-lookup"><span data-stu-id="b73ef-137">Monitoring query plans</span></span>
<span data-ttu-id="b73ef-138">Plan zapytania nieefektywne także może zwiększyć użycie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="b73ef-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="b73ef-139">Witaj poniższym przykładzie użyto hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) wyświetlić toodetermine które zapytanie używa hello najbardziej zbiorczą procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="b73ef-139">hello following example uses hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view toodetermine which query uses hello most cumulative CPU.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="b73ef-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b73ef-140">See also</span></span>
[<span data-ttu-id="b73ef-141">Wprowadzenie tooSQL bazy danych</span><span class="sxs-lookup"><span data-stu-id="b73ef-141">Introduction tooSQL Database</span></span>](sql-database-technical-overview.md)

