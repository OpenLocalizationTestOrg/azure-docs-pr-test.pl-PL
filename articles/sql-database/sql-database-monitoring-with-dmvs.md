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
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a>Monitorowanie usługi Azure SQL Database przy użyciu dynamicznych widoków zarządzania
Baza danych SQL Azure Microsoft umożliwia podzbiór dynamicznego zarządzania widokach toodiagnose wydajności problemów, które mogą być spowodowane przez zablokowane lub długotrwałe zapytań, wąskich gardeł w zasobach, plany zapytań niska i tak dalej. Ten temat zawiera informacje na temat toodetect typowych problemów z wydajnością przy użyciu dynamicznych widoków zarządzania.

Baza danych SQL obsługuje częściowo dynamicznych widoków zarządzania trzy kategorie:

* Związane z bazy danych dynamicznych widoków zarządzania.
* Powiązane z wykonywaniem dynamicznych widoków zarządzania.
* Związane z transakcji dynamicznych widoków zarządzania.

Aby uzyskać szczegółowe informacje o dynamicznych widoków zarządzania, zobacz [dynamicznych widoków zarządzania i funkcji (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) w dokumentacji SQL Server — książki Online.

## <a name="permissions"></a>Uprawnienia
W bazie danych SQL, zapytanie widoku dynamicznego zarządzania wymaga **stan bazy danych WIDOKU** uprawnienia. Witaj **stan bazy danych WIDOKU** uprawnienia zwraca informacje o wszystkich obiektów w bieżącej bazie danych hello.
Witaj toogrant **stan bazy danych WIDOKU** uprawnienia tooa określonej bazy danych użytkownika, uruchom następujące zapytanie hello:

```GRANT VIEW DATABASE STATE toodatabase_user; ```

W wystąpieniu programu SQL Server, lokalną dynamicznych widoków zarządzania zwraca informacje o stanie serwera. W bazie danych SQL zwracają informacje dotyczące bieżącej logicznej bazy danych tylko.

## <a name="calculating-database-size"></a>Obliczanie rozmiaru bazy danych
Witaj następujące zapytanie zwraca hello rozmiar bazy danych (w MB):

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

Witaj następujące zapytanie zwraca rozmiar hello pojedyncze obiekty (w MB) w bazie danych:

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a>Monitorowanie połączeń
Można użyć hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) wyświetlić tooretrieve informacji dotyczących hello połączeń ustanowionych tooa określonej bazy danych SQL Azure serwera i hello szczegóły każdego połączenia. Ponadto hello [widoku sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) widok jest przydatne podczas pobierania informacji o wszystkich aktywnych sesji użytkowników i zadań wewnętrznych.
Witaj następujące zapytanie pobiera informacje o bieżącym połączeniu hello:

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
> Podczas wykonywania hello **sys.dm_exec_requests** i **widoków widoku sys.dm_exec_sessions**, jeśli masz **stan WIDOKU bazy danych** uprawnień w bazie danych hello, zostanie wyświetlony, wykonywanie wszystkich sesje na powitania bazy danych. w przeciwnym razie zostanie wyświetlony tylko hello bieżącej sesji.
> 
> 

## <a name="monitoring-query-performance"></a>Monitorowanie wydajności kwerendy
Wolno lub czas uruchamiania zapytań może wykorzystać zasoby systemowe znaczące. W tej sekcji przedstawiono sposób dynamicznego zarządzania toouse widoków toodetect kilka typowych problemów wydajności zapytania. Hello jest odwołanie do starszej, ale nadal przydatne przy rozwiązywaniu problemów, [Rozwiązywanie problemów z wydajnością programu SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) artykułu w serwisie Microsoft TechNet.

### <a name="finding-top-n-queries"></a>Znajdowanie zapytania pierwszych N
Witaj poniższy przykład zwraca informacje na temat hello najważniejszych zapytań pięć uszeregowane według Średni czas procesora CPU. W tym przykładzie agreguje hello zapytania zapytanie skrótu, zgodnie z tootheir tak, aby zapytania logicznie równoważne są pogrupowane według ich wykorzystania zasobów zbiorczą.

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

### <a name="monitoring-blocked-queries"></a>Monitorowanie zablokowanych zapytań
Wolne lub długotrwałe zapytania można współtworzyć tooexcessive zużycia zasobów i być skutkiem hello zablokowanych zapytań. Witaj Przyczyna blokady hello może być niewłaściwy projekt aplikacji, zły plany zapytań hello braku przydatne indeksy i tak dalej. Można użyć hello sys.dm_tran_locks widoku tooget informacji na temat hello bieżące działanie blokady w bazie danych SQL Azure. Na przykład kodu, zobacz [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) w dokumentacji SQL Server — książki Online.

### <a name="monitoring-query-plans"></a>Monitorowanie plany zapytań
Plan zapytania nieefektywne także może zwiększyć użycie procesora CPU. Witaj poniższym przykładzie użyto hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) wyświetlić toodetermine które zapytanie używa hello najbardziej zbiorczą procesora CPU.

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

## <a name="see-also"></a>Zobacz też
[Wprowadzenie tooSQL bazy danych](sql-database-technical-overview.md)

