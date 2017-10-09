---
title: "Środowiska PowerShell: Tworzenie i zarządzanie puli elastycznej Azure SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse PowerShell toomanage puli elastycznej."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="95a7f-103">Tworzenie i zarządzanie nimi przy użyciu programu PowerShell puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="95a7f-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="95a7f-104">W tym temacie opisano sposób toocreate i zarządzanie nimi skalowalne [pule elastyczne](sql-database-elastic-pool.md) przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="95a7f-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="95a7f-105">Można również utworzyć i zarządzać nimi puli elastycznej platformy Azure przy użyciu hello [portalu Azure](https://portal.azure.com/), interfejsu API REST, lub [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="95a7f-105">You can also create and manage an Azure elastic pool using hello [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="95a7f-106">Można również tworzyć i przenoszenie baz danych do i z pul elastycznych, używając [języka Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="95a7f-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="95a7f-107">Tworzenie puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="95a7f-107">Create an elastic pool</span></span>
<span data-ttu-id="95a7f-108">Witaj [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) polecenie cmdlet tworzy puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="95a7f-108">hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="95a7f-109">Witaj wartości jednostek eDTU na pulę oraz minimalne i maksymalne liczby jednostek Dtu są ograniczone przez wartość warstwy usługi hello (Basic, Standard, Premium lub Premium RS).</span><span class="sxs-lookup"><span data-stu-id="95a7f-109">hello values for eDTU per pool, min, and max DTUs are constrained by hello service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="95a7f-110">Zobacz [limity liczby jednostek eDTU i Magazyn puli baz danych i pul elastycznych](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="95a7f-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="95a7f-111">Tworzenie puli bazy danych w puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="95a7f-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="95a7f-112">Użyj hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) polecenia cmdlet i zestaw hello **ElasticPoolName** parametru toohello docelową pulę.</span><span class="sxs-lookup"><span data-stu-id="95a7f-112">Use hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set hello **ElasticPoolName** parameter toohello target pool.</span></span> <span data-ttu-id="95a7f-113">Zobacz toomove istniejącej bazy danych w puli elastycznej [przenieść bazę danych w puli elastycznej](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="95a7f-113">toomove an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="95a7f-114">Kompletny skrypt</span><span class="sxs-lookup"><span data-stu-id="95a7f-114">Complete script</span></span>
<span data-ttu-id="95a7f-115">Ten skrypt tworzy grupę zasobów platformy Azure i serwer.</span><span class="sxs-lookup"><span data-stu-id="95a7f-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="95a7f-116">Po wyświetleniu monitu podaj nazwę użytkownika administratora i hasło hello nowego serwera (inne niż poświadczenia Azure).</span><span class="sxs-lookup"><span data-stu-id="95a7f-116">When prompted, supply an administrator username and password for hello new server (not your Azure credentials).</span></span>

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="95a7f-117">Tworzenie puli elastycznej i dodawanie wielu baz danych w puli</span><span class="sxs-lookup"><span data-stu-id="95a7f-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="95a7f-118">Tworzenie wielu baz danych w puli elastycznej może trwać, jeśli odbywa się za pomocą portalu hello lub poleceń cmdlet programu PowerShell, który tworzenie tylko jednej bazy danych w czasie.</span><span class="sxs-lookup"><span data-stu-id="95a7f-118">Creation of many databases in an elastic pool can take time when done using hello portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="95a7f-119">Tworzenie tooautomate w puli elastycznej, zobacz [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="95a7f-119">tooautomate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="95a7f-120">Przenoszenie bazy danych w puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="95a7f-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="95a7f-121">Można przenieść bazę danych do lub z puli elastycznej z hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="95a7f-121">You can move a database into or out of an elastic pool with hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="95a7f-122">Zmień ustawienia wydajności puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="95a7f-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="95a7f-123">Gdy wystąpi wydajności, możesz zmienić ustawienia hello hello puli tooaccommodate przyrostu.</span><span class="sxs-lookup"><span data-stu-id="95a7f-123">When performance suffers, you can change hello settings of hello pool tooaccommodate growth.</span></span> <span data-ttu-id="95a7f-124">Użyj hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="95a7f-124">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="95a7f-125">Ustaw hello - Dtu parametru toohello Edtu na pulę.</span><span class="sxs-lookup"><span data-stu-id="95a7f-125">Set hello -Dtu parameter toohello eDTUs per pool.</span></span> <span data-ttu-id="95a7f-126">Zobacz [limity liczby jednostek eDTU i magazyn](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) prawidłowych wartości.</span><span class="sxs-lookup"><span data-stu-id="95a7f-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="95a7f-127">Zmień hello limit magazynu elastycznej puli</span><span class="sxs-lookup"><span data-stu-id="95a7f-127">Change hello storage limit for an elastic pool</span></span>

<span data-ttu-id="95a7f-128">Użyj hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) hello tooset polecenia cmdlet _- StorageMB_ parametru.</span><span class="sxs-lookup"><span data-stu-id="95a7f-128">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ parameter.</span></span> <span data-ttu-id="95a7f-129">Podaj hello limit magazynu w Megabajtach (na przykład 2097152 zestawy hello magazynu limit too2 TB).</span><span class="sxs-lookup"><span data-stu-id="95a7f-129">Provide hello storage limit in MB (for example, 2097152 sets hello storage limit too2 TB).</span></span> <span data-ttu-id="95a7f-130">Zobacz [limity liczby jednostek eDTU i magazyn](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) prawidłowych wartości.</span><span class="sxs-lookup"><span data-stu-id="95a7f-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95a7f-131">Hello domyślny maksymalny pamięci masowej na pulę dla pul Premium z Edtu 1500 lub więcej jest 750 GB.</span><span class="sxs-lookup"><span data-stu-id="95a7f-131">hello default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="95a7f-132">wyższy hello tooobtain _maksymalny rozmiar magazynu danych na pulę_, hello limit magazynu musi być wyraźnie ustawione.</span><span class="sxs-lookup"><span data-stu-id="95a7f-132">tooobtain hello higher _max data storage size per pool_, hello storage limit must be explicitly set.</span></span> <span data-ttu-id="95a7f-133">Pule Premium z więcej niż 750 GB przestrzeni dyskowej jest obecnie w wersji zapoznawczej w następujących regionach hello: wschodnie stany USA 2, zachodnie stany USA Virginia nam wersji dla instytucji rządowych, Europa Zachodnia, Niemcy centralnej, Azja południowo-wschodnia, Japonia Wschodnia, Australia Wschodnia, centralnej Zjednoczone i Kanada Wschodnia.</span><span class="sxs-lookup"><span data-stu-id="95a7f-133">Premium pools with more than 750 GB of storage is currently in public preview in hello following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a><span data-ttu-id="95a7f-134">Pobierz stan hello operacji puli</span><span class="sxs-lookup"><span data-stu-id="95a7f-134">Get hello status of pool operations</span></span>
<span data-ttu-id="95a7f-135">Tworzenie puli elastycznej może potrwać.</span><span class="sxs-lookup"><span data-stu-id="95a7f-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="95a7f-136">Stan hello tootrack operacji puli, w tym tworzenia i aktualizacji, użyj hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="95a7f-136">tootrack hello status of pool operations including creation and updates, use hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="95a7f-137">Pobierz stan hello przenoszenia bazy danych do i z puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="95a7f-137">Get hello status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="95a7f-138">Przenoszenie bazy danych może potrwać.</span><span class="sxs-lookup"><span data-stu-id="95a7f-138">Moving a database can take time.</span></span> <span data-ttu-id="95a7f-139">Śledzenie stanu przenoszenia przy użyciu hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="95a7f-139">Track a move status using hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="95a7f-140">Pobierz dane o użyciu zasobów dla puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="95a7f-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="95a7f-141">Metryki, które mogą być pobierane w procentach limit puli zasobów hello:</span><span class="sxs-lookup"><span data-stu-id="95a7f-141">Metrics that can be retrieved as a percentage of hello resource pool limit:</span></span>

| <span data-ttu-id="95a7f-142">Nazwa metryki</span><span class="sxs-lookup"><span data-stu-id="95a7f-142">Metric name</span></span> | <span data-ttu-id="95a7f-143">Opis</span><span class="sxs-lookup"><span data-stu-id="95a7f-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="95a7f-144">Procesor CPU\_procent</span><span class="sxs-lookup"><span data-stu-id="95a7f-144">cpu\_percent</span></span> |<span data-ttu-id="95a7f-145">Średnia obliczeniowe wykorzystania w procentach limit hello hello puli.</span><span class="sxs-lookup"><span data-stu-id="95a7f-145">Average compute utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="95a7f-146">fizyczny\_danych\_odczytu\_procent</span><span class="sxs-lookup"><span data-stu-id="95a7f-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="95a7f-147">Średnie wykorzystanie we/wy w procent opartych na powitania limit hello puli.</span><span class="sxs-lookup"><span data-stu-id="95a7f-147">Average I/O utilization in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="95a7f-148">Dziennik\_zapisu\_procent</span><span class="sxs-lookup"><span data-stu-id="95a7f-148">log\_write\_percent</span></span> |<span data-ttu-id="95a7f-149">Średnia zapisu wykorzystania zasobów w procentach limit hello hello puli.</span><span class="sxs-lookup"><span data-stu-id="95a7f-149">Average write resource utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="95a7f-150">DTU\_zużycie\_procent</span><span class="sxs-lookup"><span data-stu-id="95a7f-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="95a7f-151">Użycie średnią liczbę jednostek eDTU w procentach limit liczby jednostek eDTU puli hello</span><span class="sxs-lookup"><span data-stu-id="95a7f-151">Average eDTU utilization in percentage of eDTU limit for hello pool</span></span> |
| <span data-ttu-id="95a7f-152">Magazyn\_procent</span><span class="sxs-lookup"><span data-stu-id="95a7f-152">storage\_percent</span></span> |<span data-ttu-id="95a7f-153">Średnie wykorzystanie magazynu w procentach hello limit magazynowania puli hello.</span><span class="sxs-lookup"><span data-stu-id="95a7f-153">Average storage utilization in percentage of hello storage limit of hello pool.</span></span> |
| <span data-ttu-id="95a7f-154">Pracownicy\_procent</span><span class="sxs-lookup"><span data-stu-id="95a7f-154">workers\_percent</span></span> |<span data-ttu-id="95a7f-155">Maksymalna równoczesnych pracowników (liczba żądań) procent opartych na powitania limit hello puli.</span><span class="sxs-lookup"><span data-stu-id="95a7f-155">Maximum concurrent workers (requests) in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="95a7f-156">sesje\_procent</span><span class="sxs-lookup"><span data-stu-id="95a7f-156">sessions\_percent</span></span> |<span data-ttu-id="95a7f-157">Maksymalna liczba sesji jednoczesnych wyrażony jako procent oparte na powitania limit hello puli.</span><span class="sxs-lookup"><span data-stu-id="95a7f-157">Maximum concurrent sessions in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="95a7f-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="95a7f-158">eDTU_limit</span></span> |<span data-ttu-id="95a7f-159">Bieżący maksymalny puli elastycznej jednostek dtu w warstwie ustawienie dla tej puli elastycznej w danym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="95a7f-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="95a7f-160">Magazyn\_limit</span><span class="sxs-lookup"><span data-stu-id="95a7f-160">storage\_limit</span></span> |<span data-ttu-id="95a7f-161">Bieżący limit magazynowania puli elastycznej max ustawienie dla tej elastycznej puli w megabajtach w danym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="95a7f-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="95a7f-162">eDTU\_używane</span><span class="sxs-lookup"><span data-stu-id="95a7f-162">eDTU\_used</span></span> |<span data-ttu-id="95a7f-163">Średnia Edtu użytej przez pulę hello w tym zakresie.</span><span class="sxs-lookup"><span data-stu-id="95a7f-163">Average eDTUs used by hello pool in this interval.</span></span> |
| <span data-ttu-id="95a7f-164">Magazyn\_używane</span><span class="sxs-lookup"><span data-stu-id="95a7f-164">storage\_used</span></span> |<span data-ttu-id="95a7f-165">Średni Magazyn używany przez pulę hello w tym interwał, w bajtach</span><span class="sxs-lookup"><span data-stu-id="95a7f-165">Average storage used by hello pool in this interval in bytes</span></span> |

<span data-ttu-id="95a7f-166">**Okresy przechowywania/szczegółowości metryki:**</span><span class="sxs-lookup"><span data-stu-id="95a7f-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="95a7f-167">Dane są zwracane w szczegółowości 5 minut.</span><span class="sxs-lookup"><span data-stu-id="95a7f-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="95a7f-168">Przechowywanie danych jest 35 dni.</span><span class="sxs-lookup"><span data-stu-id="95a7f-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="95a7f-169">To polecenie cmdlet i interfejsu API ogranicza hello liczbę wierszy, które mogą być pobierane w jednym wywołaniu too1000 wierszy (około 3 dni dane o 5 minut).</span><span class="sxs-lookup"><span data-stu-id="95a7f-169">This cmdlet and API limits hello number of rows that can be retrieved in one call too1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="95a7f-170">To polecenie można wywoływać wielokrotnie tooretrieve przedziały czasu rozpoczęcia/zakończenia różnych większej ilości danych, ale</span><span class="sxs-lookup"><span data-stu-id="95a7f-170">But this command can be called multiple times with different start/end time intervals tooretrieve more data</span></span>

<span data-ttu-id="95a7f-171">metryki hello tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="95a7f-171">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="95a7f-172">Pobierz dane o użyciu zasobów dla bazy danych w puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="95a7f-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="95a7f-173">Te interfejsy API są tak samo jak hello interfejsy API używane do monitorowania wykorzystania zasobów hello jednej bazy danych, z wyjątkiem powitania po semantycznego różnica hello: metryki pobierane są wyrażone jako procent hello na Edtu max bazy danych (lub równoważne zakończenia dla hello bazowy metryki, takie jak procesor CPU lub we/wy) ustawić dla tej puli.</span><span class="sxs-lookup"><span data-stu-id="95a7f-173">These APIs are hello same as hello APIs used for monitoring hello resource utilization of a single database, except for hello following semantic difference: metrics retrieved are expressed as a percentage of hello per database max eDTUs (or equivalent cap for hello underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="95a7f-174">Na przykład 50% wykorzystania któregokolwiek z tych metryk wskazuje, że zużycie zasobów specyficznych hello jest na 50% hello limitu zakończenia bazy danych dla tego zasobu w puli nadrzędnej hello.</span><span class="sxs-lookup"><span data-stu-id="95a7f-174">For example, 50% utilization of any of these metrics indicates that hello specific resource consumption is at 50% of hello per database cap limit for that resource in hello parent pool.</span></span>

<span data-ttu-id="95a7f-175">metryki hello tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="95a7f-175">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="95a7f-176">Dodaj zasób puli elastycznej tooan alertu</span><span class="sxs-lookup"><span data-stu-id="95a7f-176">Add an alert tooan elastic pool resource</span></span>
<span data-ttu-id="95a7f-177">Można dodać reguły alertów toosend puli elastycznej tooan wiadomości e-mail z powiadomieniami lub zbyt alert parametry[adres URL punktów końcowych](https://msdn.microsoft.com/library/mt718036.aspx) po puli elastycznej hello trafienia ustawiony próg użycia.</span><span class="sxs-lookup"><span data-stu-id="95a7f-177">You can add alert rules tooan elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when hello elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="95a7f-178">Użyj polecenia cmdlet hello AzureRmMetricAlertRule Dodaj.</span><span class="sxs-lookup"><span data-stu-id="95a7f-178">Use hello Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95a7f-179">Monitorowanie dla pul elastycznych wykorzystania zasobów ma opóźnienie co najmniej 5 minut.</span><span class="sxs-lookup"><span data-stu-id="95a7f-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="95a7f-180">Ustawianie alertów mniej niż 10 minut pule elastyczne nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="95a7f-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="95a7f-181">Ustaw alerty dla pul elastycznych kropką (parametr o nazwie "-Rozmiar_okna" w interfejsie API środowiska PowerShell) mniej niż 10 minut mogą nie zostać wyzwolone.</span><span class="sxs-lookup"><span data-stu-id="95a7f-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="95a7f-182">Upewnij się, że wszystkie alerty zdefiniowane dla pul elastycznych użyć ciągu (rozmiar okna) 10 minut lub więcej.</span><span class="sxs-lookup"><span data-stu-id="95a7f-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="95a7f-183">W tym przykładzie dodaje alert w przypadku uzyskiwania powiadomienia, gdy użycie jednostek eDTU puli elastycznej wykraczają poza pewnej wartości progowej.</span><span class="sxs-lookup"><span data-stu-id="95a7f-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

<span data-ttu-id="95a7f-184">Aby uzyskać więcej informacji, zobacz [tworzyć alerty bazy danych SQL w portalu Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="95a7f-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a><span data-ttu-id="95a7f-185">Dodawanie baz danych tooall alertów w puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="95a7f-185">Add alerts tooall databases in an elastic pool</span></span>
<span data-ttu-id="95a7f-186">Można dodać reguły alertów tooall toosend puli elastycznej bazy danych wiadomości e-mail z powiadomieniami lub zbyt alert parametry[adres URL punktów końcowych](https://msdn.microsoft.com/library/mt718036.aspx) gdy zasób trafienia wartość progową wykorzystania przez hello alertu.</span><span class="sxs-lookup"><span data-stu-id="95a7f-186">You can add alert rules tooall database in an elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by hello alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95a7f-187">Monitorowanie dla pul elastycznych wykorzystania zasobów ma opóźnienie co najmniej 5 minut.</span><span class="sxs-lookup"><span data-stu-id="95a7f-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="95a7f-188">Ustawianie alertów mniej niż 10 minut pule elastyczne nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="95a7f-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="95a7f-189">Ustaw alerty dla pul elastycznych kropką (parametr o nazwie "-Rozmiar_okna" w interfejsie API środowiska PowerShell) mniej niż 10 minut mogą nie zostać wyzwolone.</span><span class="sxs-lookup"><span data-stu-id="95a7f-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="95a7f-190">Upewnij się, że wszystkie alerty zdefiniowane dla pul elastycznych użyć ciągu (rozmiar okna) 10 minut lub więcej.</span><span class="sxs-lookup"><span data-stu-id="95a7f-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="95a7f-191">W tym przykładzie dodaje alertu tooeach hello baz danych w puli elastycznej dla pobierania powiadomienie, gdy użycie jednostek DTU w tej bazie danych przekracza określony próg.</span><span class="sxs-lookup"><span data-stu-id="95a7f-191">This example adds an alert tooeach of hello databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="95a7f-192">Zbieranie i monitorować dane użycia zasobów przez wiele pul w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="95a7f-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="95a7f-193">Jeśli masz wiele baz danych w ramach subskrypcji jest skomplikowane toomonitor każdego elastyczna pula oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="95a7f-193">When you have many databases in a subscription, it is cumbersome toomonitor each elastic pool separately.</span></span> <span data-ttu-id="95a7f-194">Zamiast tego polecenia cmdlet programu PowerShell bazy danych SQL i zapytania T-SQL mogą być połączone toocollect dane o użyciu zasobów z wielu zestawów i ich baz danych monitorowania i analizy użycia zasobów.</span><span class="sxs-lookup"><span data-stu-id="95a7f-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined toocollect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="95a7f-195">A [przykładowe zastosowanie](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) zestawu powershell skryptów znajdują się w repozytorium przykłady GitHub programu SQL Server hello wraz z dokumentacją na działanie i w jaki sposób toouse go.</span><span class="sxs-lookup"><span data-stu-id="95a7f-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in hello GitHub SQL Server samples repository along with documentation on what it does and how toouse it.</span></span>

<span data-ttu-id="95a7f-196">toouse przykładowe zastosowanie, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="95a7f-196">toouse this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="95a7f-197">Pobierz hello [skrypty i dokumentacja](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="95a7f-197">Download hello [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="95a7f-198">Zmodyfikuj skrypty hello w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="95a7f-198">Modify hello scripts for your environment.</span></span> <span data-ttu-id="95a7f-199">Określ co najmniej jeden serwer, na których znajdują się elastyczne pule.</span><span class="sxs-lookup"><span data-stu-id="95a7f-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="95a7f-200">Określ bazę danych telemetrii, gdzie hello zebranych metryk są toobe przechowywane.</span><span class="sxs-lookup"><span data-stu-id="95a7f-200">Specify a telemetry database where hello collected metrics are toobe stored.</span></span>
4. <span data-ttu-id="95a7f-201">Dostosowywanie hello skryptu toospecify hello czas trwania wykonywanie skryptów hello.</span><span class="sxs-lookup"><span data-stu-id="95a7f-201">Customize hello script toospecify hello duration of hello scripts' execution.</span></span>

<span data-ttu-id="95a7f-202">Na wysokim poziomie skrypty hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="95a7f-202">At a high level, hello scripts do hello following:</span></span>

* <span data-ttu-id="95a7f-203">Wylicza wszystkie serwery w ramach danej subskrypcji Azure (lub określona lista serwerów).</span><span class="sxs-lookup"><span data-stu-id="95a7f-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="95a7f-204">Uruchamia zadanie w tle dla każdego serwera.</span><span class="sxs-lookup"><span data-stu-id="95a7f-204">Runs a background job for each server.</span></span> <span data-ttu-id="95a7f-205">zadanie Hello jest uruchamiany w pętli w regularnych odstępach czasu i zbiera dane telemetryczne dla wszystkich pul hello w powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="95a7f-205">hello job runs in a loop at regular intervals and collects telemetry data for all hello pools in hello server.</span></span> <span data-ttu-id="95a7f-206">Następnie ładuje hello zbierane dane do bazy danych telemetrii określonego hello.</span><span class="sxs-lookup"><span data-stu-id="95a7f-206">It then loads hello collected data into hello specified telemetry database.</span></span>
* <span data-ttu-id="95a7f-207">Wylicza listę baz danych w każdej puli toocollect hello bazy danych dane o użyciu zasobów.</span><span class="sxs-lookup"><span data-stu-id="95a7f-207">Enumerates a list of databases in each pool toocollect hello database resource usage data.</span></span> <span data-ttu-id="95a7f-208">Następnie ładuje hello zbierane dane do bazy danych telemetrycznych hello.</span><span class="sxs-lookup"><span data-stu-id="95a7f-208">It then loads hello collected data into hello telemetry database.</span></span>

<span data-ttu-id="95a7f-209">Hello zebranych metryk w bazie danych telemetrycznych hello mogą być przeanalizowane toomonitor hello kondycji pule elastyczne i baz danych hello w nim.</span><span class="sxs-lookup"><span data-stu-id="95a7f-209">hello collected metrics in hello telemetry database can be analyzed toomonitor hello health of elastic pools and hello databases in it.</span></span> <span data-ttu-id="95a7f-210">skrypt Hello instaluje również wstępnie zdefiniowane wartościami przechowywanymi w tabeli funkcji (TVF) w metryki bazy danych telemetrii hello agregacji hello toohelp okna określony czas.</span><span class="sxs-lookup"><span data-stu-id="95a7f-210">hello script also installs a pre-defined Table-Value function (TVF) in hello telemetry database toohelp aggregate hello metrics for a specified time window.</span></span> <span data-ttu-id="95a7f-211">Na przykład wyniki hello funkcji TVF mogą być używane tooshow "pierwszych N pule elastyczne z hello wykorzystania maksymalną liczbę jednostek eDTU w danym momencie oknie."</span><span class="sxs-lookup"><span data-stu-id="95a7f-211">For example, results of hello TVF can be used tooshow “top N elastic pools with hello maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="95a7f-212">Opcjonalnie użyj narzędzia analityczne, takie jak tooquery programu Excel lub Power BI i analizować dane zbierane hello.</span><span class="sxs-lookup"><span data-stu-id="95a7f-212">Optionally, use analytic tools like Excel or Power BI tooquery and analyze hello collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="95a7f-213">Przykład: pobieranie metryk zużycia zasobów dla puli elastycznej i jej baz danych</span><span class="sxs-lookup"><span data-stu-id="95a7f-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="95a7f-214">W tym przykładzie pobierana hello zużycie metryki dla danej puli elastycznej i jej baz danych.</span><span class="sxs-lookup"><span data-stu-id="95a7f-214">This example retrieves hello consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="95a7f-215">Zebrane dane jest sformatowany i zapisywane sformatowanym plikiem CSV tooa.</span><span class="sxs-lookup"><span data-stu-id="95a7f-215">Collected data is formatted and written tooa .csv formatted file.</span></span> <span data-ttu-id="95a7f-216">Plik Hello można przeglądać przy użyciu programu Excel.</span><span class="sxs-lookup"><span data-stu-id="95a7f-216">hello file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="95a7f-217">Czas oczekiwania operacji puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="95a7f-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="95a7f-218">Zmiana hello minimalna liczba jednostek Edtu na bazę danych lub maksymalna liczba jednostek Edtu na bazę danych zazwyczaj kończy się w ciągu 5 minut lub mniej.</span><span class="sxs-lookup"><span data-stu-id="95a7f-218">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="95a7f-219">Zmiana hello Edtu na pulę, zależy od hello łączną ilość miejsca używanego przez wszystkie bazy danych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="95a7f-219">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="95a7f-220">Wprowadzanie zmian trwa średnio 90 minut na każde 100 GB.</span><span class="sxs-lookup"><span data-stu-id="95a7f-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="95a7f-221">Na przykład jeśli całkowita ilość miejsca hello jest używany przez wszystkie bazy danych w puli hello jest 200 GB, a następnie hello oczekuje się, że czas oczekiwania na zmianę hello puli eDTU na pulę wynosi 3 godziny lub mniej.</span><span class="sxs-lookup"><span data-stu-id="95a7f-221">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="95a7f-222">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95a7f-222">Next steps</span></span>
* <span data-ttu-id="95a7f-223">[Tworzenie zadań elastycznych](sql-database-elastic-jobs-overview.md) zadania elastyczne umożliwiają uruchamianie skryptów T-SQL na dowolnej liczbie baz danych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="95a7f-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in hello pool.</span></span>
* <span data-ttu-id="95a7f-224">Zobacz [skalowanie w poziomie z bazy danych SQL Azure](sql-database-elastic-scale-introduction.md): Użyj narzędzi elastycznej tooscale wychodzących, przenoszenia danych, zapytania, lub utworzyć transakcji.</span><span class="sxs-lookup"><span data-stu-id="95a7f-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools tooscale out, move data, query, or create transactions.</span></span>
