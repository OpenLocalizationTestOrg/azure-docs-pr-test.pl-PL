---
title: "aaaUse PowerShell tooback zapasowych i przywracania usługi aplikacji — aplikacje"
description: "Dowiedz się, jak toouse PowerShell tooback zapasowych i przywracania aplikacji w usłudze Azure App Service"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: 7ea8661e-aefb-4823-9626-6bff980cdebf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: 4042166f6c650841926f010056d6c80ab2de57e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a>Użyj programu PowerShell tooback i przywracania usługi aplikacji — aplikacje
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [Interfejs API REST](../app-service-web/websites-csm-backup.md)
> 
> 

Dowiedz się, jak tooback programu Azure PowerShell toouse zapasowych i przywracania [aplikacji usługi App Service](https://azure.microsoft.com/services/app-service/web/). Aby uzyskać więcej informacji na temat kopie zapasowe aplikacji sieci web, w tym wymagań i ograniczeń, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](../app-service-web/web-sites-backup.md).

## <a name="prerequisites"></a>Wymagania wstępne
toouse PowerShell toomanage kopii zapasowych aplikacji, należy po hello:

* **Adres URL SAS** , która umożliwia odczytu i zapisu tooan usługi Azure Storage kontenera. Zobacz [modelu sygnatur dostępu Współdzielonego hello opis](../storage/common/storage-dotnet-shared-access-signature-part-1.md) wyjaśnienie adresy URL SAS. Zobacz [przy użyciu programu Azure PowerShell z usługą Azure Storage](../storage/common/storage-powershell-guide-full.md) przykłady Zarządzanie magazynem Azure za pomocą programu PowerShell.
* **Parametry połączenia bazy danych** Jeśli chcesz tooback zapasowych bazy danych wraz z aplikacji sieci web.

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a>Jak toogenerate toouse adres URL SAS z aplikacji sieci web hello kopii zapasowej polecenia cmdlet
Adres URL SAS można wygenerować za pomocą programu PowerShell. Poniżej przedstawiono przykład sposobu toogenerate, który może być używany z poleceń cmdlet hello omówione w tym artykule.

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>Instalowanie programu Azure PowerShell 1.3.2 lub nowszej
Zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](/powershell/azure/overview) instrukcje dotyczące instalowania i używania programu Azure PowerShell.

## <a name="create-a-backup"></a>Tworzenie kopii zapasowej
Użyj hello AzureRmWebAppBackup nowe polecenia cmdlet toocreate kopii zapasowej aplikacji sieci web.

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

Spowoduje to utworzenie kopii zapasowej z użyciem nazwy wygenerowanej automatycznie. Jeśli chcesz tooprovide nazwę kopii zapasowej, użyj hello Nazwa_kopii_zapasowej opcjonalny parametr.

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

tooinclude bazy danych w usłudze Kopia zapasowa hello najpierw utworzyć przy użyciu polecenia cmdlet New-AzureRmWebAppDatabaseBackupSetting hello ustawienie kopii zapasowej bazy danych, a następnie podaj to ustawienie w hello baz danych parametru polecenia cmdlet New-AzureRmWebAppBackup hello. Parametr baz danych Hello akceptuje tablicę ustawień bazy danych, dzięki czemu tooback więcej niż jednej bazy danych.

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>Pobierz kopii zapasowych
polecenie cmdlet Get-AzureRmWebAppBackupList Hello zwraca tablicę wszystkich kopii zapasowych dla aplikacji sieci web. Należy podać nazwę aplikacji sieci web hello hello i jego grupa zasobów.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

tooget kopii zapasowej, użyj polecenia cmdlet Get-AzureRmWebAppBackup hello.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

Obiekt aplikacji sieci web można również przekazać do dowolnego polecenia cmdlet zarządzania kopiami zapasowymi hello jako udogodnienie.

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>Harmonogram automatycznego tworzenia kopii zapasowych
Toohappen kopii zapasowych można zaplanować automatycznie w określonych odstępach czasu. tooconfigure harmonogram tworzenia kopii zapasowych, użyj polecenia cmdlet hello AzureRmWebAppBackupConfiguration edycji. To polecenie cmdlet przyjmuje kilka parametrów:

* **Nazwa** — Witaj nazwa hello aplikacji sieci web.
* **ResourceGroupName** — Witaj nazwa hello zasobów grupy zawierające hello aplikacji sieci web.
* **Gniazdo** — jest to opcjonalne. Nazwa Hello miejsca aplikacji sieci web hello.
* **StorageAccountUrl** — Witaj adres URL SAS dla kontenera magazynu Azure hello toostore hello tworzenia kopii zapasowych.
* **FrequencyInterval** — wartość liczbową dla częstotliwość hello kopii zapasowych powinno się. Musi być dodatnią liczbą całkowitą.
* **FrequencyUnit** -jednostki czasu dla częstotliwość hello kopii zapasowych powinno się. Opcje są godziny i dnia.
* **RetentionPeriodInDays** — ile dni hello automatycznego tworzenia kopii zapasowych ma zostać zapisany zanim zostaną automatycznie usunięte.
* **Wartość StartTime** — jest to opcjonalne. Witaj czasu rozpoczęcia hello automatycznego tworzenia kopii zapasowych. Kopie zapasowe rozpoczyna się natychmiast, jeśli jest to wartość null. Musi być typu DateTime.
* **Bazy danych** — jest to opcjonalne. Tablica DatabaseBackupSettings dla hello toobackup baz danych.
* **KeepAtLeastOneBackup** — opcjonalnie przełączono parametru. Podaj, to jeśli jedna kopia zapasowa powinna zawsze być przechowywana w hello konta magazynu, niezależnie od tego, jak stare jest.

Poniżej przedstawiono przykładowy sposób toouse tego polecenia cmdlet.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

tooget hello bieżącego harmonogram tworzenia kopii zapasowych, polecenia cmdlet Get-AzureRmWebAppBackupConfiguration hello użycia. Może to być przydatne w przypadku modyfikowania harmonogram, który został już skonfigurowany.

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>Przywracanie z kopii zapasowej aplikacji sieci web
toorestore aplikacji sieci web z kopii zapasowej, polecenia cmdlet służącego do hello AzureRmWebAppBackup przywracania. Witaj Najprostszym sposobem toouse to polecenie cmdlet jest toopipe w obiekcie kopii zapasowej pobierane z polecenia cmdlet Get-AzureRmWebAppBackup hello lub polecenia cmdlet Get-AzureRmWebAppBackupList.

Po utworzeniu obiektu kopii zapasowej, można przekazać go do polecenia cmdlet AzureRmWebAppBackup przywracania hello. Określ hello Zastąp przełącznik parametru tooindicate czy zamierzasz toooverwrite hello zawartość aplikacji sieci web z zawartością hello hello kopii zapasowej. Jeśli kopia zapasowa hello zawiera baz danych, również zostaną przywrócone tych baz danych.

        $backup | Restore-AzureRmWebAppBackup -Overwrite

Poniżej znajduje się przykład sposobu toouse hello Restore AzureRmWebAppBackup, określając wszystkie parametry hello.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>Usuwanie kopii zapasowej
toodelete kopii zapasowej, użyj polecenia cmdlet Remove-AzureRmWebAppBackup hello. Spowoduje to usunięcie hello kopii zapasowej z konta magazynu. Podaj nazwę swojej aplikacji, a jego grupa zasobów i hello identyfikator hello kopii zapasowej chcesz toodelete.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

Możesz również przekazać obiektu kopii zapasowej do toodelete polecenia cmdlet Remove-AzureRmWebAppBackup hello go.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
