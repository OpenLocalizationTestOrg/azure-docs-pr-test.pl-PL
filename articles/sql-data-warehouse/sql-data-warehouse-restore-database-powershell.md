---
title: "Przywróć magazyn danych Azure SQL (PowerShell) | Dokumentacja firmy Microsoft"
description: "Zadania programu PowerShell dla usługi Azure SQL Data Warehouse przywracania."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 6286c0e682bae2d3bf0435a25b8077a53b117b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="6d822-103">Przywróć magazyn danych Azure SQL (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="6d822-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="6d822-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="6d822-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="6d822-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="6d822-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="6d822-106">[Środowiska PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="6d822-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="6d822-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="6d822-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="6d822-108">W tym artykule dowiesz się, jak przywrócić Azure SQL Data Warehouse przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d822-108">In this article you will learn how to restore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6d822-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="6d822-109">Before you begin</span></span>
<span data-ttu-id="6d822-110">**Sprawdź, czy pojemność jednostek dtu w warstwie.**</span><span class="sxs-lookup"><span data-stu-id="6d822-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="6d822-111">Każdy magazyn danych SQL jest obsługiwana przez serwer SQL (np. myserver.database.windows.net), który ma domyślnego przydziału jednostek dtu w warstwie.</span><span class="sxs-lookup"><span data-stu-id="6d822-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="6d822-112">Zanim będzie można przywrócić magazyn danych SQL, upewnij się, że program SQL server ma wystarczającą ilość pozostałych limit przydziału jednostek DTU dla przywracanej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6d822-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="6d822-113">Aby dowiedzieć się, jak można obliczyć jednostek dtu w warstwie potrzebne również z prośbami więcej jednostek dtu w warstwie, zobacz [żądanie zmiany limitu przydziału jednostek dtu w warstwie][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="6d822-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="6d822-114">Instalowanie programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d822-114">Install PowerShell</span></span>
<span data-ttu-id="6d822-115">Aby można było używać programu Azure PowerShell z usługą Magazyn danych SQL, należy zainstalować program Azure PowerShell w wersji 1.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6d822-115">In order to use Azure PowerShell with SQL Data Warehouse, you will need to install Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="6d822-116">Wersję można sprawdzić, uruchamiając **Get-Module - ListAvailable-Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="6d822-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="6d822-117">Najnowszą wersję można zainstalować z [Instalatora platformy sieci Web firmy Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="6d822-117">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="6d822-118">Aby uzyskać więcej informacji na temat instalowania najnowszej wersji, zobacz [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell] (Jak zainstalować i skonfigurować program Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="6d822-118">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="6d822-119">Przywróć bazę danych aktywnej lub wstrzymana</span><span class="sxs-lookup"><span data-stu-id="6d822-119">Restore an active or paused database</span></span>
<span data-ttu-id="6d822-120">Przywracanie bazy danych przed użyciem migawki [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d822-120">To restore a database from a snapshot use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="6d822-121">Otwórz program Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d822-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="6d822-122">Lista wszystkich subskrypcji skojarzonych z Twoim kontem i połącz się z kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d822-122">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="6d822-123">Wybierz subskrypcję, który zawiera bazę danych do przywrócenia.</span><span class="sxs-lookup"><span data-stu-id="6d822-123">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="6d822-124">Lista punktów przywracania dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6d822-124">List the restore points for the database.</span></span>
5. <span data-ttu-id="6d822-125">Wybierz punkt przywracania żądaną przy użyciu RestorePointCreationDate.</span><span class="sxs-lookup"><span data-stu-id="6d822-125">Pick the desired restore point using the RestorePointCreationDate.</span></span>
6. <span data-ttu-id="6d822-126">Przywróć bazę danych do punktu przywracania żądany.</span><span class="sxs-lookup"><span data-stu-id="6d822-126">Restore the database to the desired restore point.</span></span>
7. <span data-ttu-id="6d822-127">Sprawdź, czy przywrócona baza danych jest w trybie online.</span><span class="sxs-lookup"><span data-stu-id="6d822-127">Verify that the restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List the last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get the specific database to restore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify the status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="6d822-128">Po ukończeniu przywracania można skonfigurować odzyskanej bazy danych, wykonując [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="6d822-128">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="6d822-129">Przywracanie usuniętej bazy danych</span><span class="sxs-lookup"><span data-stu-id="6d822-129">Restore a deleted database</span></span>
<span data-ttu-id="6d822-130">Aby przywrócić usunięte bazy danych, należy użyć [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6d822-130">To restore a deleted database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="6d822-131">Otwórz program Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d822-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="6d822-132">Lista wszystkich subskrypcji skojarzonych z Twoim kontem i połącz się z kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d822-132">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="6d822-133">Wybierz subskrypcję, która zawiera usuniętej bazy danych do przywrócenia.</span><span class="sxs-lookup"><span data-stu-id="6d822-133">Select the subscription that contains the deleted database to be restored.</span></span>
4. <span data-ttu-id="6d822-134">Pobierz określone usuniętej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6d822-134">Get the specific deleted database.</span></span>
5. <span data-ttu-id="6d822-135">Przywracanie usuniętej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6d822-135">Restore the deleted database.</span></span>
6. <span data-ttu-id="6d822-136">Sprawdź, czy przywrócona baza danych jest w trybie online.</span><span class="sxs-lookup"><span data-stu-id="6d822-136">Verify that the restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get the deleted database to restore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify the status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="6d822-137">Po ukończeniu przywracania można skonfigurować odzyskanej bazy danych, wykonując [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="6d822-137">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="6d822-138">Przywróć z regionu geograficznego platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6d822-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="6d822-139">Aby odzyskać bazę danych, należy użyć [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6d822-139">To recover a database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="6d822-140">Otwórz program Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6d822-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="6d822-141">Lista wszystkich subskrypcji skojarzonych z Twoim kontem i połącz się z kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d822-141">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="6d822-142">Wybierz subskrypcję, który zawiera bazę danych do przywrócenia.</span><span class="sxs-lookup"><span data-stu-id="6d822-142">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="6d822-143">Pobierz bazę danych, którą chcesz odzyskać.</span><span class="sxs-lookup"><span data-stu-id="6d822-143">Get the database you want to recover.</span></span>
5. <span data-ttu-id="6d822-144">Utwórz żądanie odzyskiwania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6d822-144">Create the recovery request for the database.</span></span>
6. <span data-ttu-id="6d822-145">Sprawdź stan bazy danych przywrócone z magazynu geograficznie.</span><span class="sxs-lookup"><span data-stu-id="6d822-145">Verify the status of the geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get the database you want to recover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that the geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="6d822-146">Aby skonfigurować bazę danych, po ukończeniu przywracania, zobacz [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="6d822-146">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="6d822-147">Odzyskanej bazy danych będzie mieć włączono funkcji TDE, jeśli baza danych jest włączona w funkcji TDE.</span><span class="sxs-lookup"><span data-stu-id="6d822-147">The recovered database will be TDE-enabled if the source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d822-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d822-148">Next steps</span></span>
<span data-ttu-id="6d822-149">Aby dowiedzieć się więcej o funkcjach ciągłości biznesowej wersji bazy danych SQL Azure, przeczytaj [omówienie ciągłości działalności biznesowej usługi Azure SQL Database][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="6d822-149">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
