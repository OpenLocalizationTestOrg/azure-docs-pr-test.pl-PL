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
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="ee639-103">Monitorowanie i zarządzanie nimi pula elastyczna o języku Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="ee639-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="ee639-104">W tym temacie opisano sposób toomanage skalowalne [pule elastyczne](sql-database-elastic-pool.md) z Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee639-104">This topic shows you how toomanage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="ee639-105">Można również utworzyć i zarządzać nimi hello Azure puli elastycznej [portalu Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello interfejsu API REST, lub [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="ee639-105">You can also create and manage an Azure elastic pool hello [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="ee639-106">Można również tworzyć i przenoszenie baz danych do i z pul elastycznych, używając [języka Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="ee639-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="ee639-107">Użyj hello [Create Database (baza danych SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) i [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) polecenia toocreate i przenoszenia baz danych do i z elastyczne pule.</span><span class="sxs-lookup"><span data-stu-id="ee639-107">Use hello [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands toocreate and move databases into and out of elastic pools.</span></span> <span data-ttu-id="ee639-108">Witaj puli elastycznej musi istnieć przed użyciem tych poleceń.</span><span class="sxs-lookup"><span data-stu-id="ee639-108">hello elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="ee639-109">Te polecenia mają wpływ tylko bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ee639-109">These commands affect only databases.</span></span> <span data-ttu-id="ee639-110">Tworzenie nowych pul i hello ustawienie właściwości puli (na przykład Edtu min i max) nie można zmienić za pomocą polecenia T-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee639-110">Creation of new pools and hello setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="ee639-111">Tworzenie puli bazy danych w puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="ee639-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="ee639-112">Za pomocą polecenia CREATE DATABASE hello hello SERVICE_OBJECTIVE opcji.</span><span class="sxs-lookup"><span data-stu-id="ee639-112">Use hello CREATE DATABASE command with hello SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="ee639-113">Wszystkie bazy danych w puli elastycznej dziedziczą hello warstwy usług puli elastycznej hello (Basic, Standard i Premium).</span><span class="sxs-lookup"><span data-stu-id="ee639-113">All databases in an elastic pool inherit hello service tier of hello elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="ee639-114">Przenoszenie bazy danych między pul elastycznych</span><span class="sxs-lookup"><span data-stu-id="ee639-114">Move a database between elastic pools</span></span>
<span data-ttu-id="ee639-115">Użyj polecenia ALTER DATABASE hello z hello MODYFIKUJ i ustaw usługę\_celu opcję ELASTYCZNA\_PULI.</span><span class="sxs-lookup"><span data-stu-id="ee639-115">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="ee639-116">Ustaw nazwę toohello nazwa hello hello docelową pulę.</span><span class="sxs-lookup"><span data-stu-id="ee639-116">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="ee639-117">Przenoszenie bazy danych w puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="ee639-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="ee639-118">Użyj polecenia ALTER DATABASE hello z hello MODYFIKUJ i skonfiguruj\_celu opcję ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="ee639-118">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="ee639-119">Ustaw nazwę toohello nazwa hello hello docelową pulę.</span><span class="sxs-lookup"><span data-stu-id="ee639-119">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="ee639-120">Przenoszenie bazy danych z puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="ee639-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="ee639-121">Użyj polecenia ALTER DATABASE hello i ustaw tooone SERVICE_OBJECTIVE hello hello poziomów wydajności (na przykład S0 lub S1).</span><span class="sxs-lookup"><span data-stu-id="ee639-121">Use hello ALTER DATABASE command and set hello SERVICE_OBJECTIVE tooone of hello performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="ee639-122">Lista baz danych, w puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="ee639-122">List databases in an elastic pool</span></span>
<span data-ttu-id="ee639-123">Użyj hello [sys.database\_usługi \_widoku cele](https://msdn.microsoft.com/library/mt712619) toolist hello wszystkich baz danych w puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="ee639-123">Use hello [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) toolist all hello databases in an elastic pool.</span></span> <span data-ttu-id="ee639-124">Zaloguj się za główny toohello widok hello tooquery bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ee639-124">Log in toohello master database tooquery hello view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="ee639-125">Pobierz dane o użyciu zasobów dla puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="ee639-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="ee639-126">Użyj hello [sys.elastic\_puli \_zasobów \_widoku Statystyka](https://msdn.microsoft.com/library/mt280062.aspx) statystyk użycia zasobów hello tooexamine elastycznej puli na serwerze logicznym.</span><span class="sxs-lookup"><span data-stu-id="ee639-126">Use hello [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="ee639-127">Zaloguj się za główny toohello widok hello tooquery bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ee639-127">Log in toohello master database tooquery hello view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="ee639-128">Pobierz użycie zasobów dla puli bazy danych</span><span class="sxs-lookup"><span data-stu-id="ee639-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="ee639-129">Użyj hello [sys.dm\_ bazy danych\_ zasobów\_widoku Statystyka](https://msdn.microsoft.com/library/dn800981.aspx) lub [sys.resource \_widoku Statystyka](https://msdn.microsoft.com/library/dn269979.aspx) statystyk użycia zasobów hello tooexamine z Baza danych w puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="ee639-129">Use hello [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="ee639-130">Ten proces jest podobny tooquerying użycie zasobów dla pojedynczej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ee639-130">This process is similar tooquerying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee639-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ee639-131">Next steps</span></span>
<span data-ttu-id="ee639-132">Po utworzeniu puli elastycznej, można zarządzać elastycznych baz danych w puli hello za tworzenie zadań elastycznych.</span><span class="sxs-lookup"><span data-stu-id="ee639-132">After creating an elastic pool, you can manage elastic databases in hello pool by creating elastic jobs.</span></span> <span data-ttu-id="ee639-133">Zadania elastyczne ułatwienia uruchamianie skryptów T-SQL na dowolnej liczbie baz danych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="ee639-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in hello pool.</span></span> <span data-ttu-id="ee639-134">Aby uzyskać więcej informacji, zobacz [omówienie zadania elastycznej bazy danych](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ee639-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="ee639-135">Zobacz [skalowanie w poziomie z bazy danych SQL Azure](sql-database-elastic-scale-introduction.md): Użyj tooscale narzędzi elastycznej bazy danych wychodzących, przenoszenia danych, zapytania, lub utworzyć transakcji.</span><span class="sxs-lookup"><span data-stu-id="ee639-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools tooscale out, move data, query, or create transactions.</span></span>

