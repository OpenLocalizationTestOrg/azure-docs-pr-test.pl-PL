---
title: "Kopie zapasowe i przywracanie aplikacji usługi App Service przy użyciu programu PowerShell"
description: "Dowiedz się, jak wykonać kopię zapasową i przywrócić aplikacji w usłudze Azure App Service przy użyciu programu PowerShell"
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
ms.openlocfilehash: 34a7e1d025c301ca056753d964bb3c5f4f1a62d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-powershell-to-back-up-and-restore-app-service-apps"></a>Kopie zapasowe i przywracanie aplikacji usługi App Service przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [Interfejs API REST](../app-service-web/websites-csm-backup.md)
> 
> 

Dowiedz się, jak i przywracanie kopii zapasowej przy użyciu programu Azure PowerShell [aplikacji usługi App Service](https://azure.microsoft.com/services/app-service/web/). Aby uzyskać więcej informacji na temat kopie zapasowe aplikacji sieci web, w tym wymagań i ograniczeń, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](../app-service-web/web-sites-backup.md).

## <a name="prerequisites"></a>Wymagania wstępne
Za pomocą programu PowerShell do zarządzania kopii zapasowych aplikacji, są potrzebne następujące elementy:

* **Adres URL SAS** , która umożliwia odczytu i zapisu do kontenera magazynu Azure. Zobacz [opis modelu sygnatur dostępu Współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) wyjaśnienie adresy URL SAS. Zobacz [przy użyciu programu Azure PowerShell z usługą Azure Storage](../storage/common/storage-powershell-guide-full.md) przykłady Zarządzanie magazynem Azure za pomocą programu PowerShell.
* **Parametry połączenia bazy danych** Jeśli chcesz utworzyć kopię zapasową bazy danych wraz z aplikacji sieci web.

### <a name="how-to-generate-a-sas-url-to-use-with-the-web-app-backup-cmdlets"></a>Sposób generowania sygnatury dostępu Współdzielonego adresu URL za pomocą polecenia cmdlet tworzenia kopii zapasowej aplikacji sieci web
Adres URL SAS można wygenerować za pomocą programu PowerShell. Poniżej przedstawiono przykładowy sposób generowania, który może być używany z poleceń cmdlet omówione w tym artykule.

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure to select the appropriate key. Here we select the first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>Instalowanie programu Azure PowerShell 1.3.2 lub nowszej
Zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](/powershell/azure/overview) instrukcje dotyczące instalowania i używania programu Azure PowerShell.

## <a name="create-a-backup"></a>Tworzenie kopii zapasowej
Utworzenie kopii zapasowej aplikacji sieci web za pomocą polecenia cmdlet New-AzureRmWebAppBackup.

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

Spowoduje to utworzenie kopii zapasowej z użyciem nazwy wygenerowanej automatycznie. Jeśli chcesz podać nazwę dla kopii zapasowej, użyj Nazwa_kopii_zapasowej opcjonalny parametr.

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

Aby dołączyć bazę danych z kopii zapasowej, najpierw utwórz ustawienie kopii zapasowej bazy danych przy użyciu polecenia cmdlet New-AzureRmWebAppDatabaseBackupSetting, a następnie podaj ustawienie w parametrze polecenia cmdlet New-AzureRmWebAppBackup baz danych. Parametr baz danych przyjmuje tablicę ustawień bazy danych, co umożliwia tworzenie kopii zapasowej więcej niż jednej bazy danych.

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>Pobierz kopii zapasowych
Polecenie cmdlet Get-AzureRmWebAppBackupList zwraca tablicę wszystkich kopii zapasowych dla aplikacji sieci web. Należy podać nazwę aplikacji sieci web i jego grupa zasobów.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

Aby uzyskać kopii zapasowej, należy użyć polecenia cmdlet Get-AzureRmWebAppBackup.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

Obiekt aplikacji sieci web można również przekazać do dowolnego polecenia cmdlet zarządzania kopiami zapasowymi dla wygody.

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>Harmonogram automatycznego tworzenia kopii zapasowych
Można zaplanować kopie zapasowe wykonywane automatycznie w określonych odstępach czasu. Aby skonfigurować harmonogram tworzenia kopii zapasowych, użyj polecenia cmdlet AzureRmWebAppBackupConfiguration edycji. To polecenie cmdlet przyjmuje kilka parametrów:

* **Nazwa** — Nazwa aplikacji sieci web.
* **ResourceGroupName** — Nazwa grupy zasobów zawierającej aplikację sieci web.
* **Gniazdo** — jest to opcjonalne. Nazwa miejsca aplikacji sieci web.
* **StorageAccountUrl** — adres URL SAS dla kontenera magazynu Azure, używany do przechowywania kopii zapasowych.
* **FrequencyInterval** — wartość liczbową dla częstotliwość powinno się tworzenie kopii zapasowych. Musi być dodatnią liczbą całkowitą.
* **FrequencyUnit** -jednostki czasu dla częstotliwość powinno się tworzenie kopii zapasowych. Opcje są godziny i dnia.
* **RetentionPeriodInDays** — liczbę dni, automatycznego tworzenia kopii zapasowej należy zapisać zanim zostaną automatycznie usunięte.
* **Wartość StartTime** — jest to opcjonalne. Czas rozpoczęcia automatycznego tworzenia kopii zapasowych. Kopie zapasowe rozpoczyna się natychmiast, jeśli jest to wartość null. Musi być typu DateTime.
* **Bazy danych** — jest to opcjonalne. Tablica DatabaseBackupSettings dla baz danych do tworzenia kopii zapasowej.
* **KeepAtLeastOneBackup** — opcjonalnie przełączono parametru. Podanie tego Jeśli jedną kopię zapasową zawsze powinna być przechowywana w konta magazynu, niezależnie od tego, jak stare go.

Poniżej znajduje się przykład sposobu użycia tego polecenia cmdlet.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

Aby uzyskać bieżący harmonogram tworzenia kopii zapasowej, należy użyć polecenia cmdlet Get-AzureRmWebAppBackupConfiguration. Może to być przydatne w przypadku modyfikowania harmonogram, który został już skonfigurowany.

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify the configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply the new configuration by piping it into the Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>Przywracanie z kopii zapasowej aplikacji sieci web
Aby przywrócić aplikacji sieci web z kopii zapasowej, należy użyć polecenia cmdlet AzureRmWebAppBackup przywracania. Najprostszym sposobem, aby użyć tego polecenia cmdlet jest potoku obiektu kopii zapasowej są pobierane z polecenia cmdlet Get-AzureRmWebAppBackup lub polecenia cmdlet Get-AzureRmWebAppBackupList.

Po utworzeniu obiektu kopii zapasowej, można go przekazać do polecenia cmdlet AzureRmWebAppBackup przywracania. Określ parametr przełącznika Zastąp, aby wskazać zamierzają zastąpienie zawartości aplikacji sieci web z zawartością kopii zapasowej. Jeśli kopia zapasowa zawiera baz danych, jak również zostaną przywrócone tych baz danych.

        $backup | Restore-AzureRmWebAppBackup -Overwrite

Poniżej znajduje się przykład sposobu użycia Restore AzureRmWebAppBackup, określając wszystkich parametrów.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>Usuwanie kopii zapasowej
Aby usunąć kopię zapasową, użyj polecenia cmdlet Remove-AzureRmWebAppBackup. Spowoduje to usunięcie kopii zapasowej z konta magazynu. Określ nazwę aplikacji, jego grupa zasobów i Identyfikatorem kopii zapasowej, które chcesz usunąć.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

Obiektu kopii zapasowej można również przekazać do polecenia cmdlet Remove-AzureRmWebAppBackup go usunąć.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
