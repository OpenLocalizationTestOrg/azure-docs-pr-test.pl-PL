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
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="7f37c-103">Użyj programu PowerShell tooback i przywracania usługi aplikacji — aplikacje</span><span class="sxs-lookup"><span data-stu-id="7f37c-103">Use PowerShell tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f37c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f37c-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="7f37c-105">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="7f37c-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="7f37c-106">Dowiedz się, jak tooback programu Azure PowerShell toouse zapasowych i przywracania [aplikacji usługi App Service](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="7f37c-106">Learn how toouse Azure PowerShell tooback up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="7f37c-107">Aby uzyskać więcej informacji na temat kopie zapasowe aplikacji sieci web, w tym wymagań i ograniczeń, zobacz [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="7f37c-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f37c-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7f37c-108">Prerequisites</span></span>
<span data-ttu-id="7f37c-109">toouse PowerShell toomanage kopii zapasowych aplikacji, należy po hello:</span><span class="sxs-lookup"><span data-stu-id="7f37c-109">toouse PowerShell toomanage your app backups, you need hello following:</span></span>

* <span data-ttu-id="7f37c-110">**Adres URL SAS** , która umożliwia odczytu i zapisu tooan usługi Azure Storage kontenera.</span><span class="sxs-lookup"><span data-stu-id="7f37c-110">**A SAS URL** that allows read and write access tooan Azure Storage container.</span></span> <span data-ttu-id="7f37c-111">Zobacz [modelu sygnatur dostępu Współdzielonego hello opis](../storage/common/storage-dotnet-shared-access-signature-part-1.md) wyjaśnienie adresy URL SAS.</span><span class="sxs-lookup"><span data-stu-id="7f37c-111">See [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="7f37c-112">Zobacz [przy użyciu programu Azure PowerShell z usługą Azure Storage](../storage/common/storage-powershell-guide-full.md) przykłady Zarządzanie magazynem Azure za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f37c-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="7f37c-113">**Parametry połączenia bazy danych** Jeśli chcesz tooback zapasowych bazy danych wraz z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7f37c-113">**A database connection string** if you want tooback up a database along with your web app.</span></span>

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a><span data-ttu-id="7f37c-114">Jak toogenerate toouse adres URL SAS z aplikacji sieci web hello kopii zapasowej polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="7f37c-114">How toogenerate a SAS URL toouse with hello web app backup cmdlets</span></span>
<span data-ttu-id="7f37c-115">Adres URL SAS można wygenerować za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f37c-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="7f37c-116">Poniżej przedstawiono przykład sposobu toogenerate, który może być używany z poleceń cmdlet hello omówione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="7f37c-116">Here is an example of how toogenerate one that can be used with hello cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="7f37c-117">Instalowanie programu Azure PowerShell 1.3.2 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="7f37c-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="7f37c-118">Zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](/powershell/azure/overview) instrukcje dotyczące instalowania i używania programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f37c-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="7f37c-119">Tworzenie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="7f37c-119">Create a backup</span></span>
<span data-ttu-id="7f37c-120">Użyj hello AzureRmWebAppBackup nowe polecenia cmdlet toocreate kopii zapasowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7f37c-120">Use hello New-AzureRmWebAppBackup cmdlet toocreate a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="7f37c-121">Spowoduje to utworzenie kopii zapasowej z użyciem nazwy wygenerowanej automatycznie.</span><span class="sxs-lookup"><span data-stu-id="7f37c-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="7f37c-122">Jeśli chcesz tooprovide nazwę kopii zapasowej, użyj hello Nazwa_kopii_zapasowej opcjonalny parametr.</span><span class="sxs-lookup"><span data-stu-id="7f37c-122">If you would like tooprovide a name for your backup, use hello BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="7f37c-123">tooinclude bazy danych w usłudze Kopia zapasowa hello najpierw utworzyć przy użyciu polecenia cmdlet New-AzureRmWebAppDatabaseBackupSetting hello ustawienie kopii zapasowej bazy danych, a następnie podaj to ustawienie w hello baz danych parametru polecenia cmdlet New-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="7f37c-123">tooinclude a database in hello backup, first create a database backup setting using hello New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in hello Databases parameter of hello New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="7f37c-124">Parametr baz danych Hello akceptuje tablicę ustawień bazy danych, dzięki czemu tooback więcej niż jednej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7f37c-124">hello Databases parameter accepts an array of database settings, allowing you tooback up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="7f37c-125">Pobierz kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="7f37c-125">Get backups</span></span>
<span data-ttu-id="7f37c-126">polecenie cmdlet Get-AzureRmWebAppBackupList Hello zwraca tablicę wszystkich kopii zapasowych dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7f37c-126">hello Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="7f37c-127">Należy podać nazwę aplikacji sieci web hello hello i jego grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f37c-127">You must supply hello name of hello web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="7f37c-128">tooget kopii zapasowej, użyj polecenia cmdlet Get-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="7f37c-128">tooget a specific backup, use hello Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="7f37c-129">Obiekt aplikacji sieci web można również przekazać do dowolnego polecenia cmdlet zarządzania kopiami zapasowymi hello jako udogodnienie.</span><span class="sxs-lookup"><span data-stu-id="7f37c-129">You can also pipe a web app object into any of hello backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="7f37c-130">Harmonogram automatycznego tworzenia kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="7f37c-130">Schedule automatic backups</span></span>
<span data-ttu-id="7f37c-131">Toohappen kopii zapasowych można zaplanować automatycznie w określonych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="7f37c-131">You can schedule backups toohappen automatically at a specified interval.</span></span> <span data-ttu-id="7f37c-132">tooconfigure harmonogram tworzenia kopii zapasowych, użyj polecenia cmdlet hello AzureRmWebAppBackupConfiguration edycji.</span><span class="sxs-lookup"><span data-stu-id="7f37c-132">tooconfigure a backup schedule, use hello Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="7f37c-133">To polecenie cmdlet przyjmuje kilka parametrów:</span><span class="sxs-lookup"><span data-stu-id="7f37c-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="7f37c-134">**Nazwa** — Witaj nazwa hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7f37c-134">**Name** - hello name of hello web app.</span></span>
* <span data-ttu-id="7f37c-135">**ResourceGroupName** — Witaj nazwa hello zasobów grupy zawierające hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7f37c-135">**ResourceGroupName** - hello name of hello resource group containing hello web app.</span></span>
* <span data-ttu-id="7f37c-136">**Gniazdo** — jest to opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="7f37c-136">**Slot** - Optional.</span></span> <span data-ttu-id="7f37c-137">Nazwa Hello miejsca aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="7f37c-137">hello name of hello web app slot.</span></span>
* <span data-ttu-id="7f37c-138">**StorageAccountUrl** — Witaj adres URL SAS dla kontenera magazynu Azure hello toostore hello tworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="7f37c-138">**StorageAccountUrl** - hello SAS URL for hello Azure Storage container used toostore hello backups.</span></span>
* <span data-ttu-id="7f37c-139">**FrequencyInterval** — wartość liczbową dla częstotliwość hello kopii zapasowych powinno się.</span><span class="sxs-lookup"><span data-stu-id="7f37c-139">**FrequencyInterval** - Numeric value for how often hello backups should be made.</span></span> <span data-ttu-id="7f37c-140">Musi być dodatnią liczbą całkowitą.</span><span class="sxs-lookup"><span data-stu-id="7f37c-140">Must be a positive integer.</span></span>
* <span data-ttu-id="7f37c-141">**FrequencyUnit** -jednostki czasu dla częstotliwość hello kopii zapasowych powinno się.</span><span class="sxs-lookup"><span data-stu-id="7f37c-141">**FrequencyUnit** - Unit of time for how often hello backups should be made.</span></span> <span data-ttu-id="7f37c-142">Opcje są godziny i dnia.</span><span class="sxs-lookup"><span data-stu-id="7f37c-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="7f37c-143">**RetentionPeriodInDays** — ile dni hello automatycznego tworzenia kopii zapasowych ma zostać zapisany zanim zostaną automatycznie usunięte.</span><span class="sxs-lookup"><span data-stu-id="7f37c-143">**RetentionPeriodInDays** - How many days hello automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="7f37c-144">**Wartość StartTime** — jest to opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="7f37c-144">**StartTime** - Optional.</span></span> <span data-ttu-id="7f37c-145">Witaj czasu rozpoczęcia hello automatycznego tworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="7f37c-145">hello time when hello automatic backups should begin.</span></span> <span data-ttu-id="7f37c-146">Kopie zapasowe rozpoczyna się natychmiast, jeśli jest to wartość null.</span><span class="sxs-lookup"><span data-stu-id="7f37c-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="7f37c-147">Musi być typu DateTime.</span><span class="sxs-lookup"><span data-stu-id="7f37c-147">Must be a DateTime.</span></span>
* <span data-ttu-id="7f37c-148">**Bazy danych** — jest to opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="7f37c-148">**Databases** - Optional.</span></span> <span data-ttu-id="7f37c-149">Tablica DatabaseBackupSettings dla hello toobackup baz danych.</span><span class="sxs-lookup"><span data-stu-id="7f37c-149">An array of DatabaseBackupSettings for hello databases toobackup.</span></span>
* <span data-ttu-id="7f37c-150">**KeepAtLeastOneBackup** — opcjonalnie przełączono parametru.</span><span class="sxs-lookup"><span data-stu-id="7f37c-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="7f37c-151">Podaj, to jeśli jedna kopia zapasowa powinna zawsze być przechowywana w hello konta magazynu, niezależnie od tego, jak stare jest.</span><span class="sxs-lookup"><span data-stu-id="7f37c-151">Supply this if one backup should always be kept in hello storage account, regardless of how old it is.</span></span>

<span data-ttu-id="7f37c-152">Poniżej przedstawiono przykładowy sposób toouse tego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7f37c-152">Following is an example of how toouse this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="7f37c-153">tooget hello bieżącego harmonogram tworzenia kopii zapasowych, polecenia cmdlet Get-AzureRmWebAppBackupConfiguration hello użycia.</span><span class="sxs-lookup"><span data-stu-id="7f37c-153">tooget hello current backup schedule, use hello Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="7f37c-154">Może to być przydatne w przypadku modyfikowania harmonogram, który został już skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="7f37c-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="7f37c-155">Przywracanie z kopii zapasowej aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="7f37c-155">Restore a web app from a backup</span></span>
<span data-ttu-id="7f37c-156">toorestore aplikacji sieci web z kopii zapasowej, polecenia cmdlet służącego do hello AzureRmWebAppBackup przywracania.</span><span class="sxs-lookup"><span data-stu-id="7f37c-156">toorestore a web app from a backup, use hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="7f37c-157">Witaj Najprostszym sposobem toouse to polecenie cmdlet jest toopipe w obiekcie kopii zapasowej pobierane z polecenia cmdlet Get-AzureRmWebAppBackup hello lub polecenia cmdlet Get-AzureRmWebAppBackupList.</span><span class="sxs-lookup"><span data-stu-id="7f37c-157">hello easiest way toouse this cmdlet is toopipe in a backup object retrieved from hello Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="7f37c-158">Po utworzeniu obiektu kopii zapasowej, można przekazać go do polecenia cmdlet AzureRmWebAppBackup przywracania hello.</span><span class="sxs-lookup"><span data-stu-id="7f37c-158">Once you have a backup object, you can pipe it into hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="7f37c-159">Określ hello Zastąp przełącznik parametru tooindicate czy zamierzasz toooverwrite hello zawartość aplikacji sieci web z zawartością hello hello kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="7f37c-159">Specify hello Overwrite switch parameter tooindicate that you intend toooverwrite hello contents of your web app with hello contents of hello backup.</span></span> <span data-ttu-id="7f37c-160">Jeśli kopia zapasowa hello zawiera baz danych, również zostaną przywrócone tych baz danych.</span><span class="sxs-lookup"><span data-stu-id="7f37c-160">If hello backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="7f37c-161">Poniżej znajduje się przykład sposobu toouse hello Restore AzureRmWebAppBackup, określając wszystkie parametry hello.</span><span class="sxs-lookup"><span data-stu-id="7f37c-161">Following is an example of how toouse hello Restore-AzureRmWebAppBackup by specifying all hello parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="7f37c-162">Usuwanie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="7f37c-162">Delete a backup</span></span>
<span data-ttu-id="7f37c-163">toodelete kopii zapasowej, użyj polecenia cmdlet Remove-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="7f37c-163">toodelete a backup, use hello Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="7f37c-164">Spowoduje to usunięcie hello kopii zapasowej z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7f37c-164">This removes hello backup from your storage account.</span></span> <span data-ttu-id="7f37c-165">Podaj nazwę swojej aplikacji, a jego grupa zasobów i hello identyfikator hello kopii zapasowej chcesz toodelete.</span><span class="sxs-lookup"><span data-stu-id="7f37c-165">Specify your app name, its resource group, and hello ID of hello backup you want toodelete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="7f37c-166">Możesz również przekazać obiektu kopii zapasowej do toodelete polecenia cmdlet Remove-AzureRmWebAppBackup hello go.</span><span class="sxs-lookup"><span data-stu-id="7f37c-166">You can also pipe a backup object into hello Remove-AzureRmWebAppBackup cmdlet toodelete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
