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
# <a name="use-powershell-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="ff206-103">Kopie zapasowe i przywracanie aplikacji usługi App Service przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff206-103">Use PowerShell to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff206-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff206-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="ff206-105">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="ff206-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="ff206-106">Dowiedz się, jak i przywracanie kopii zapasowej przy użyciu programu Azure PowerShell [aplikacji usługi App Service](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="ff206-106">Learn how to use Azure PowerShell to back up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="ff206-107">Aby uzyskać więcej informacji na temat kopie zapasowe aplikacji sieci web, w tym wymagań i ograniczeń, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="ff206-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff206-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ff206-108">Prerequisites</span></span>
<span data-ttu-id="ff206-109">Za pomocą programu PowerShell do zarządzania kopii zapasowych aplikacji, są potrzebne następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ff206-109">To use PowerShell to manage your app backups, you need the following:</span></span>

* <span data-ttu-id="ff206-110">**Adres URL SAS** , która umożliwia odczytu i zapisu do kontenera magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="ff206-110">**A SAS URL** that allows read and write access to an Azure Storage container.</span></span> <span data-ttu-id="ff206-111">Zobacz [opis modelu sygnatur dostępu Współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) wyjaśnienie adresy URL SAS.</span><span class="sxs-lookup"><span data-stu-id="ff206-111">See [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="ff206-112">Zobacz [przy użyciu programu Azure PowerShell z usługą Azure Storage](../storage/common/storage-powershell-guide-full.md) przykłady Zarządzanie magazynem Azure za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff206-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="ff206-113">**Parametry połączenia bazy danych** Jeśli chcesz utworzyć kopię zapasową bazy danych wraz z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ff206-113">**A database connection string** if you want to back up a database along with your web app.</span></span>

### <a name="how-to-generate-a-sas-url-to-use-with-the-web-app-backup-cmdlets"></a><span data-ttu-id="ff206-114">Sposób generowania sygnatury dostępu Współdzielonego adresu URL za pomocą polecenia cmdlet tworzenia kopii zapasowej aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="ff206-114">How to generate a SAS URL to use with the web app backup cmdlets</span></span>
<span data-ttu-id="ff206-115">Adres URL SAS można wygenerować za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff206-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="ff206-116">Poniżej przedstawiono przykładowy sposób generowania, który może być używany z poleceń cmdlet omówione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="ff206-116">Here is an example of how to generate one that can be used with the cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure to select the appropriate key. Here we select the first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="ff206-117">Instalowanie programu Azure PowerShell 1.3.2 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="ff206-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="ff206-118">Zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](/powershell/azure/overview) instrukcje dotyczące instalowania i używania programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff206-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="ff206-119">Tworzenie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="ff206-119">Create a backup</span></span>
<span data-ttu-id="ff206-120">Utworzenie kopii zapasowej aplikacji sieci web za pomocą polecenia cmdlet New-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="ff206-120">Use the New-AzureRmWebAppBackup cmdlet to create a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="ff206-121">Spowoduje to utworzenie kopii zapasowej z użyciem nazwy wygenerowanej automatycznie.</span><span class="sxs-lookup"><span data-stu-id="ff206-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="ff206-122">Jeśli chcesz podać nazwę dla kopii zapasowej, użyj Nazwa_kopii_zapasowej opcjonalny parametr.</span><span class="sxs-lookup"><span data-stu-id="ff206-122">If you would like to provide a name for your backup, use the BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="ff206-123">Aby dołączyć bazę danych z kopii zapasowej, najpierw utwórz ustawienie kopii zapasowej bazy danych przy użyciu polecenia cmdlet New-AzureRmWebAppDatabaseBackupSetting, a następnie podaj ustawienie w parametrze polecenia cmdlet New-AzureRmWebAppBackup baz danych.</span><span class="sxs-lookup"><span data-stu-id="ff206-123">To include a database in the backup, first create a database backup setting using the New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in the Databases parameter of the New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="ff206-124">Parametr baz danych przyjmuje tablicę ustawień bazy danych, co umożliwia tworzenie kopii zapasowej więcej niż jednej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ff206-124">The Databases parameter accepts an array of database settings, allowing you to back up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="ff206-125">Pobierz kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="ff206-125">Get backups</span></span>
<span data-ttu-id="ff206-126">Polecenie cmdlet Get-AzureRmWebAppBackupList zwraca tablicę wszystkich kopii zapasowych dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ff206-126">The Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="ff206-127">Należy podać nazwę aplikacji sieci web i jego grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="ff206-127">You must supply the name of the web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="ff206-128">Aby uzyskać kopii zapasowej, należy użyć polecenia cmdlet Get-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="ff206-128">To get a specific backup, use the Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="ff206-129">Obiekt aplikacji sieci web można również przekazać do dowolnego polecenia cmdlet zarządzania kopiami zapasowymi dla wygody.</span><span class="sxs-lookup"><span data-stu-id="ff206-129">You can also pipe a web app object into any of the backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="ff206-130">Harmonogram automatycznego tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="ff206-130">Schedule automatic backups</span></span>
<span data-ttu-id="ff206-131">Można zaplanować kopie zapasowe wykonywane automatycznie w określonych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="ff206-131">You can schedule backups to happen automatically at a specified interval.</span></span> <span data-ttu-id="ff206-132">Aby skonfigurować harmonogram tworzenia kopii zapasowych, użyj polecenia cmdlet AzureRmWebAppBackupConfiguration edycji.</span><span class="sxs-lookup"><span data-stu-id="ff206-132">To configure a backup schedule, use the Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="ff206-133">To polecenie cmdlet przyjmuje kilka parametrów:</span><span class="sxs-lookup"><span data-stu-id="ff206-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="ff206-134">**Nazwa** — Nazwa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ff206-134">**Name** - The name of the web app.</span></span>
* <span data-ttu-id="ff206-135">**ResourceGroupName** — Nazwa grupy zasobów zawierającej aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="ff206-135">**ResourceGroupName** - The name of the resource group containing the web app.</span></span>
* <span data-ttu-id="ff206-136">**Gniazdo** — jest to opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="ff206-136">**Slot** - Optional.</span></span> <span data-ttu-id="ff206-137">Nazwa miejsca aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ff206-137">The name of the web app slot.</span></span>
* <span data-ttu-id="ff206-138">**StorageAccountUrl** — adres URL SAS dla kontenera magazynu Azure, używany do przechowywania kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="ff206-138">**StorageAccountUrl** - The SAS URL for the Azure Storage container used to store the backups.</span></span>
* <span data-ttu-id="ff206-139">**FrequencyInterval** — wartość liczbową dla częstotliwość powinno się tworzenie kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="ff206-139">**FrequencyInterval** - Numeric value for how often the backups should be made.</span></span> <span data-ttu-id="ff206-140">Musi być dodatnią liczbą całkowitą.</span><span class="sxs-lookup"><span data-stu-id="ff206-140">Must be a positive integer.</span></span>
* <span data-ttu-id="ff206-141">**FrequencyUnit** -jednostki czasu dla częstotliwość powinno się tworzenie kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="ff206-141">**FrequencyUnit** - Unit of time for how often the backups should be made.</span></span> <span data-ttu-id="ff206-142">Opcje są godziny i dnia.</span><span class="sxs-lookup"><span data-stu-id="ff206-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="ff206-143">**RetentionPeriodInDays** — liczbę dni, automatycznego tworzenia kopii zapasowej należy zapisać zanim zostaną automatycznie usunięte.</span><span class="sxs-lookup"><span data-stu-id="ff206-143">**RetentionPeriodInDays** - How many days the automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="ff206-144">**Wartość StartTime** — jest to opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="ff206-144">**StartTime** - Optional.</span></span> <span data-ttu-id="ff206-145">Czas rozpoczęcia automatycznego tworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="ff206-145">The time when the automatic backups should begin.</span></span> <span data-ttu-id="ff206-146">Kopie zapasowe rozpoczyna się natychmiast, jeśli jest to wartość null.</span><span class="sxs-lookup"><span data-stu-id="ff206-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="ff206-147">Musi być typu DateTime.</span><span class="sxs-lookup"><span data-stu-id="ff206-147">Must be a DateTime.</span></span>
* <span data-ttu-id="ff206-148">**Bazy danych** — jest to opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="ff206-148">**Databases** - Optional.</span></span> <span data-ttu-id="ff206-149">Tablica DatabaseBackupSettings dla baz danych do tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ff206-149">An array of DatabaseBackupSettings for the databases to backup.</span></span>
* <span data-ttu-id="ff206-150">**KeepAtLeastOneBackup** — opcjonalnie przełączono parametru.</span><span class="sxs-lookup"><span data-stu-id="ff206-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="ff206-151">Podanie tego Jeśli jedną kopię zapasową zawsze powinna być przechowywana w konta magazynu, niezależnie od tego, jak stare go.</span><span class="sxs-lookup"><span data-stu-id="ff206-151">Supply this if one backup should always be kept in the storage account, regardless of how old it is.</span></span>

<span data-ttu-id="ff206-152">Poniżej znajduje się przykład sposobu użycia tego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ff206-152">Following is an example of how to use this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="ff206-153">Aby uzyskać bieżący harmonogram tworzenia kopii zapasowej, należy użyć polecenia cmdlet Get-AzureRmWebAppBackupConfiguration.</span><span class="sxs-lookup"><span data-stu-id="ff206-153">To get the current backup schedule, use the Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="ff206-154">Może to być przydatne w przypadku modyfikowania harmonogram, który został już skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="ff206-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify the configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply the new configuration by piping it into the Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="ff206-155">Przywracanie z kopii zapasowej aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="ff206-155">Restore a web app from a backup</span></span>
<span data-ttu-id="ff206-156">Aby przywrócić aplikacji sieci web z kopii zapasowej, należy użyć polecenia cmdlet AzureRmWebAppBackup przywracania.</span><span class="sxs-lookup"><span data-stu-id="ff206-156">To restore a web app from a backup, use the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="ff206-157">Najprostszym sposobem, aby użyć tego polecenia cmdlet jest potoku obiektu kopii zapasowej są pobierane z polecenia cmdlet Get-AzureRmWebAppBackup lub polecenia cmdlet Get-AzureRmWebAppBackupList.</span><span class="sxs-lookup"><span data-stu-id="ff206-157">The easiest way to use this cmdlet is to pipe in a backup object retrieved from the Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="ff206-158">Po utworzeniu obiektu kopii zapasowej, można go przekazać do polecenia cmdlet AzureRmWebAppBackup przywracania.</span><span class="sxs-lookup"><span data-stu-id="ff206-158">Once you have a backup object, you can pipe it into the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="ff206-159">Określ parametr przełącznika Zastąp, aby wskazać zamierzają zastąpienie zawartości aplikacji sieci web z zawartością kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ff206-159">Specify the Overwrite switch parameter to indicate that you intend to overwrite the contents of your web app with the contents of the backup.</span></span> <span data-ttu-id="ff206-160">Jeśli kopia zapasowa zawiera baz danych, jak również zostaną przywrócone tych baz danych.</span><span class="sxs-lookup"><span data-stu-id="ff206-160">If the backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="ff206-161">Poniżej znajduje się przykład sposobu użycia Restore AzureRmWebAppBackup, określając wszystkich parametrów.</span><span class="sxs-lookup"><span data-stu-id="ff206-161">Following is an example of how to use the Restore-AzureRmWebAppBackup by specifying all the parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="ff206-162">Usuwanie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="ff206-162">Delete a backup</span></span>
<span data-ttu-id="ff206-163">Aby usunąć kopię zapasową, użyj polecenia cmdlet Remove-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="ff206-163">To delete a backup, use the Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="ff206-164">Spowoduje to usunięcie kopii zapasowej z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ff206-164">This removes the backup from your storage account.</span></span> <span data-ttu-id="ff206-165">Określ nazwę aplikacji, jego grupa zasobów i Identyfikatorem kopii zapasowej, które chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="ff206-165">Specify your app name, its resource group, and the ID of the backup you want to delete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="ff206-166">Obiektu kopii zapasowej można również przekazać do polecenia cmdlet Remove-AzureRmWebAppBackup go usunąć.</span><span class="sxs-lookup"><span data-stu-id="ff206-166">You can also pipe a backup object into the Remove-AzureRmWebAppBackup cmdlet to delete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
