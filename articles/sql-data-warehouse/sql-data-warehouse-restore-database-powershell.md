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
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a>Przywróć magazyn danych Azure SQL (PowerShell)
> [!div class="op_single_selector"]
> * [Omówienie][Overview]
> * [Portal][Portal]
> * [Środowiska PowerShell][PowerShell]
> * [REST][REST]
> 
> 

W tym artykule dowiesz się, jak toorestore Azure SQL Data Warehouse przy użyciu programu PowerShell.

## <a name="before-you-begin"></a>Przed rozpoczęciem
**Sprawdź, czy pojemność jednostek dtu w warstwie.** Każdy magazyn danych SQL jest obsługiwana przez serwer SQL (np. myserver.database.windows.net), który ma domyślnego przydziału jednostek dtu w warstwie.  Zanim będzie można przywrócić SQL Data Warehouse, sprawdź tego hello programu SQL server ma wystarczająco pozostałych limit przydziału jednostek DTU dla przywracanej hello w bazie danych. toolearn jak potrzebne toocalculate DTU lub toorequest więcej jednostek dtu w warstwie, zobacz [żądanie zmiany limitu przydziału jednostek dtu w warstwie][Request a DTU quota change].

### <a name="install-powershell"></a>Instalowanie programu PowerShell
W kolejności toouse programu Azure PowerShell z usługą Magazyn danych SQL konieczne będzie tooinstall Azure PowerShell w wersji 1.0 lub nowszego.  Wersję można sprawdzić, uruchamiając **Get-Module - ListAvailable-Name AzureRM**.  Witaj najnowszą wersję można zainstalować z [Instalatora platformy sieci Web firmy Microsoft][Microsoft Web Platform Installer].  Aby uzyskać więcej informacji na temat instalowania najnowszej wersji hello, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell][How tooinstall and configure Azure PowerShell].

## <a name="restore-an-active-or-paused-database"></a>Przywróć bazę danych aktywnej lub wstrzymana
toorestore bazy danych z migawki, użyj hello [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] polecenia cmdlet programu PowerShell.

1. Otwórz program Windows PowerShell.
2. Połącz tooyour konto platformy Azure i wyświetlić wszystkie subskrypcje hello skojarzonych z Twoim kontem.
3. Wybierz subskrypcję hello, która zawiera toobe bazy danych hello przywrócona.
4. Lista hello przywrócić punkty hello bazy danych.
5. Wybierz hello żądanego punktu przywracania przy użyciu hello RestorePointCreationDate.
6. Witaj bazy danych toohello potrzeby przywracania punktu przywracania.
7. Sprawdź, czy hello przywrócić bazy danych jest w trybie online.

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
> Po ukończeniu przywracania hello można skonfigurować odzyskanej bazy danych, wykonując [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Przywracanie usuniętej bazy danych
toorestore usuniętej bazy danych, użyj hello [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] polecenia cmdlet.

1. Otwórz program Windows PowerShell.
2. Połącz tooyour konto platformy Azure i wyświetlić wszystkie subskrypcje hello skojarzonych z Twoim kontem.
3. Wybierz subskrypcję hello, która zawiera hello usunięte bazy danych toobe przywrócona.
4. Pobierz hello określonych usunięte bazy danych.
5. Przywróć bazę danych hello usunięte.
6. Sprawdź, czy hello przywrócić bazy danych jest w trybie online.

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
> Po ukończeniu przywracania hello można skonfigurować odzyskanej bazy danych, wykonując [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a>Przywróć z regionu geograficznego platformy Azure
toorecover bazy danych, użyj hello [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] polecenia cmdlet.

1. Otwórz program Windows PowerShell.
2. Połącz tooyour konto platformy Azure i wyświetlić wszystkie subskrypcje hello skojarzonych z Twoim kontem.
3. Wybierz subskrypcję hello, która zawiera toobe bazy danych hello przywrócona.
4. Pobierz hello bazy danych, które mają toorecover.
5. Utwórz żądanie odzyskiwania hello hello bazy danych.
6. Sprawdź stan hello hello przywrócić geograficznie w bazie danych.

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
> Zobacz bazy danych po zakończeniu przywracania hello tooconfigure [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].
> 
> 

Witaj odzyskanej bazy danych będzie włączono funkcji TDE hello źródłowej bazy danych jest włączone funkcji TDE.

## <a name="next-steps"></a>Następne kroki
toolearn o funkcjach ciągłości biznesowej hello wersji bazy danych SQL Azure, przeczytaj hello [omówienie ciągłości działalności biznesowej usługi Azure SQL Database][Azure SQL Database business continuity overview].

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
