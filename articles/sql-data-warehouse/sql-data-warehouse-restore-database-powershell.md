---
title: aaaRestore magazyn danych SQL Azure (PowerShell) | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="c5c01-103">Przywróć magazyn danych Azure SQL (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="c5c01-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="c5c01-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="c5c01-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="c5c01-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="c5c01-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="c5c01-106">[Środowiska PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="c5c01-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="c5c01-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="c5c01-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="c5c01-108">W tym artykule dowiesz się, jak toorestore Azure SQL Data Warehouse przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5c01-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c5c01-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c5c01-109">Before you begin</span></span>
<span data-ttu-id="c5c01-110">**Sprawdź, czy pojemność jednostek dtu w warstwie.**</span><span class="sxs-lookup"><span data-stu-id="c5c01-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="c5c01-111">Każdy magazyn danych SQL jest obsługiwana przez serwer SQL (np. myserver.database.windows.net), który ma domyślnego przydziału jednostek dtu w warstwie.</span><span class="sxs-lookup"><span data-stu-id="c5c01-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="c5c01-112">Zanim będzie można przywrócić SQL Data Warehouse, sprawdź tego hello programu SQL server ma wystarczająco pozostałych limit przydziału jednostek DTU dla przywracanej hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c5c01-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="c5c01-113">toolearn jak potrzebne toocalculate DTU lub toorequest więcej jednostek dtu w warstwie, zobacz [żądanie zmiany limitu przydziału jednostek dtu w warstwie][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="c5c01-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="c5c01-114">Instalowanie programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5c01-114">Install PowerShell</span></span>
<span data-ttu-id="c5c01-115">W kolejności toouse programu Azure PowerShell z usługą Magazyn danych SQL konieczne będzie tooinstall Azure PowerShell w wersji 1.0 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="c5c01-115">In order toouse Azure PowerShell with SQL Data Warehouse, you will need tooinstall Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="c5c01-116">Wersję można sprawdzić, uruchamiając **Get-Module - ListAvailable-Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="c5c01-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="c5c01-117">Witaj najnowszą wersję można zainstalować z [Instalatora platformy sieci Web firmy Microsoft][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="c5c01-117">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="c5c01-118">Aby uzyskać więcej informacji na temat instalowania najnowszej wersji hello, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="c5c01-118">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="c5c01-119">Przywróć bazę danych aktywnej lub wstrzymana</span><span class="sxs-lookup"><span data-stu-id="c5c01-119">Restore an active or paused database</span></span>
<span data-ttu-id="c5c01-120">toorestore bazy danych z migawki, użyj hello [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5c01-120">toorestore a database from a snapshot use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="c5c01-121">Otwórz program Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5c01-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="c5c01-122">Połącz tooyour konto platformy Azure i wyświetlić wszystkie subskrypcje hello skojarzonych z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="c5c01-122">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="c5c01-123">Wybierz subskrypcję hello, która zawiera toobe bazy danych hello przywrócona.</span><span class="sxs-lookup"><span data-stu-id="c5c01-123">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="c5c01-124">Lista hello przywrócić punkty hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c5c01-124">List hello restore points for hello database.</span></span>
5. <span data-ttu-id="c5c01-125">Wybierz hello żądanego punktu przywracania przy użyciu hello RestorePointCreationDate.</span><span class="sxs-lookup"><span data-stu-id="c5c01-125">Pick hello desired restore point using hello RestorePointCreationDate.</span></span>
6. <span data-ttu-id="c5c01-126">Witaj bazy danych toohello potrzeby przywracania punktu przywracania.</span><span class="sxs-lookup"><span data-stu-id="c5c01-126">Restore hello database toohello desired restore point.</span></span>
7. <span data-ttu-id="c5c01-127">Sprawdź, czy hello przywrócić bazy danych jest w trybie online.</span><span class="sxs-lookup"><span data-stu-id="c5c01-127">Verify that hello restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="c5c01-128">Po ukończeniu przywracania hello można skonfigurować odzyskanej bazy danych, wykonując [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="c5c01-128">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="c5c01-129">Przywracanie usuniętej bazy danych</span><span class="sxs-lookup"><span data-stu-id="c5c01-129">Restore a deleted database</span></span>
<span data-ttu-id="c5c01-130">toorestore usuniętej bazy danych, użyj hello [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c5c01-130">toorestore a deleted database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="c5c01-131">Otwórz program Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5c01-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="c5c01-132">Połącz tooyour konto platformy Azure i wyświetlić wszystkie subskrypcje hello skojarzonych z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="c5c01-132">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="c5c01-133">Wybierz subskrypcję hello, która zawiera hello usunięte bazy danych toobe przywrócona.</span><span class="sxs-lookup"><span data-stu-id="c5c01-133">Select hello subscription that contains hello deleted database toobe restored.</span></span>
4. <span data-ttu-id="c5c01-134">Pobierz hello określonych usunięte bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c5c01-134">Get hello specific deleted database.</span></span>
5. <span data-ttu-id="c5c01-135">Przywróć bazę danych hello usunięte.</span><span class="sxs-lookup"><span data-stu-id="c5c01-135">Restore hello deleted database.</span></span>
6. <span data-ttu-id="c5c01-136">Sprawdź, czy hello przywrócić bazy danych jest w trybie online.</span><span class="sxs-lookup"><span data-stu-id="c5c01-136">Verify that hello restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="c5c01-137">Po ukończeniu przywracania hello można skonfigurować odzyskanej bazy danych, wykonując [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="c5c01-137">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="c5c01-138">Przywróć z regionu geograficznego platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c5c01-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="c5c01-139">toorecover bazy danych, użyj hello [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c5c01-139">toorecover a database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="c5c01-140">Otwórz program Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5c01-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="c5c01-141">Połącz tooyour konto platformy Azure i wyświetlić wszystkie subskrypcje hello skojarzonych z Twoim kontem.</span><span class="sxs-lookup"><span data-stu-id="c5c01-141">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="c5c01-142">Wybierz subskrypcję hello, która zawiera toobe bazy danych hello przywrócona.</span><span class="sxs-lookup"><span data-stu-id="c5c01-142">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="c5c01-143">Pobierz hello bazy danych, które mają toorecover.</span><span class="sxs-lookup"><span data-stu-id="c5c01-143">Get hello database you want toorecover.</span></span>
5. <span data-ttu-id="c5c01-144">Utwórz żądanie odzyskiwania hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c5c01-144">Create hello recovery request for hello database.</span></span>
6. <span data-ttu-id="c5c01-145">Sprawdź stan hello hello przywrócić geograficznie w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c5c01-145">Verify hello status of hello geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="c5c01-146">Zobacz bazy danych po zakończeniu przywracania hello tooconfigure [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="c5c01-146">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="c5c01-147">Witaj odzyskanej bazy danych będzie włączono funkcji TDE hello źródłowej bazy danych jest włączone funkcji TDE.</span><span class="sxs-lookup"><span data-stu-id="c5c01-147">hello recovered database will be TDE-enabled if hello source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5c01-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c5c01-148">Next steps</span></span>
<span data-ttu-id="c5c01-149">toolearn o funkcjach ciągłości biznesowej hello wersji bazy danych SQL Azure, przeczytaj hello [omówienie ciągłości działalności biznesowej usługi Azure SQL Database][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="c5c01-149">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
