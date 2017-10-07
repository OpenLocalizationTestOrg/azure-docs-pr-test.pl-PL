---
title: "T-SQL: Zarządzanie puli elastycznej bazy danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Użyj T-SQL toomanage puli elastycznej bazy danych SQL Azure."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a>Monitorowanie i zarządzanie nimi pula elastyczna o języku Transact-SQL
W tym temacie opisano sposób toomanage skalowalne [pule elastyczne](sql-database-elastic-pool.md) z Transact-SQL.  Można również utworzyć i zarządzać nimi hello Azure puli elastycznej [portalu Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello interfejsu API REST, lub [C#](sql-database-elastic-pool-manage-csharp.md). Można również tworzyć i przenoszenie baz danych do i z pul elastycznych, używając [języka Transact-SQL](sql-database-elastic-pool-manage-tsql.md).


Użyj hello [Create Database (baza danych SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) i [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) polecenia toocreate i przenoszenia baz danych do i z elastyczne pule. Witaj puli elastycznej musi istnieć przed użyciem tych poleceń. Te polecenia mają wpływ tylko bazy danych. Tworzenie nowych pul i hello ustawienie właściwości puli (na przykład Edtu min i max) nie można zmienić za pomocą polecenia T-SQL.

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Tworzenie puli bazy danych w puli elastycznej
Za pomocą polecenia CREATE DATABASE hello hello SERVICE_OBJECTIVE opcji.   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

Wszystkie bazy danych w puli elastycznej dziedziczą hello warstwy usług puli elastycznej hello (Basic, Standard i Premium). 

## <a name="move-a-database-between-elastic-pools"></a>Przenoszenie bazy danych między pul elastycznych
Użyj polecenia ALTER DATABASE hello z hello MODYFIKUJ i ustaw usługę\_celu opcję ELASTYCZNA\_PULI. Ustaw nazwę toohello nazwa hello hello docelową pulę.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a>Przenoszenie bazy danych w puli elastycznej
Użyj polecenia ALTER DATABASE hello z hello MODYFIKUJ i skonfiguruj\_celu opcję ELASTIC_POOL. Ustaw nazwę toohello nazwa hello hello docelową pulę.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a>Przenoszenie bazy danych z puli elastycznej
Użyj polecenia ALTER DATABASE hello i ustaw tooone SERVICE_OBJECTIVE hello hello poziomów wydajności (na przykład S0 lub S1).

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a>Lista baz danych, w puli elastycznej
Użyj hello [sys.database\_usługi \_widoku cele](https://msdn.microsoft.com/library/mt712619) toolist hello wszystkich baz danych w puli elastycznej. Zaloguj się za główny toohello widok hello tooquery bazy danych.

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Pobierz dane o użyciu zasobów dla puli elastycznej
Użyj hello [sys.elastic\_puli \_zasobów \_widoku Statystyka](https://msdn.microsoft.com/library/mt280062.aspx) statystyk użycia zasobów hello tooexamine elastycznej puli na serwerze logicznym. Zaloguj się za główny toohello widok hello tooquery bazy danych.

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a>Pobierz użycie zasobów dla puli bazy danych
Użyj hello [sys.dm\_ bazy danych\_ zasobów\_widoku Statystyka](https://msdn.microsoft.com/library/dn800981.aspx) lub [sys.resource \_widoku Statystyka](https://msdn.microsoft.com/library/dn269979.aspx) statystyk użycia zasobów hello tooexamine z Baza danych w puli elastycznej. Ten proces jest podobny tooquerying użycie zasobów dla pojedynczej bazy danych.

## <a name="next-steps"></a>Następne kroki
Po utworzeniu puli elastycznej, można zarządzać elastycznych baz danych w puli hello za tworzenie zadań elastycznych. Zadania elastyczne ułatwienia uruchamianie skryptów T-SQL na dowolnej liczbie baz danych w puli hello. Aby uzyskać więcej informacji, zobacz [omówienie zadania elastycznej bazy danych](sql-database-elastic-jobs-overview.md). 

Zobacz [skalowanie w poziomie z bazy danych SQL Azure](sql-database-elastic-scale-introduction.md): Użyj tooscale narzędzi elastycznej bazy danych wychodzących, przenoszenia danych, zapytania, lub utworzyć transakcji.

