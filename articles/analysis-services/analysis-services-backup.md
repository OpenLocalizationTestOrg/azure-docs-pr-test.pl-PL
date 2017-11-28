---
title: "Azure kopii zapasowej bazy danych usług Analysis Services i przywracania | Dokumentacja firmy Microsoft"
description: "Opisuje sposób wykonywania kopii zapasowej i przywracanie bazy danych usług Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: bffa481a498b130ef1f2388a5ba856da5d164ee0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="82319-103">Tworzenie kopii zapasowej i przywracanie</span><span class="sxs-lookup"><span data-stu-id="82319-103">Backup and restore</span></span>

<span data-ttu-id="82319-104">Tworzenie kopii zapasowej bazy danych modelu tabelarycznego w usług Azure Analysis Services jest znacznie takie same, jak w przypadku lokalnego Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="82319-104">Backing up tabular model databases in Azure Analysis Services is much the same as for on-premises Analysis Services.</span></span> <span data-ttu-id="82319-105">Podstawowa różnica polega na którym są przechowywane pliki kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="82319-105">The primary difference is where you store your backup files.</span></span> <span data-ttu-id="82319-106">Pliki kopii zapasowej należy zapisać do kontenera w [konto magazynu Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="82319-106">Backup files must be saved to a container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="82319-107">Można było utworzyć, konfigurując ustawienia magazynu dla serwera lub służy konto magazynu i kontener, który już istnieje.</span><span class="sxs-lookup"><span data-stu-id="82319-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="82319-108">Tworzenie konta magazynu może skutkować nową usługą płatną.</span><span class="sxs-lookup"><span data-stu-id="82319-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="82319-109">Aby dowiedzieć się więcej, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="82319-109">To learn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="82319-110">Kopie zapasowe są zapisywane z rozszerzeniem abf.</span><span class="sxs-lookup"><span data-stu-id="82319-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="82319-111">Dla modeli tabelarycznych w pamięci zarówno w modelu danych, jak i metadane są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="82319-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="82319-112">Dla modeli tabelarycznych zapytania bezpośredniego są przechowywane tylko metadane modelu.</span><span class="sxs-lookup"><span data-stu-id="82319-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="82319-113">Kopie zapasowe można skompresować i szyfrowane, w zależności od wybranych opcji.</span><span class="sxs-lookup"><span data-stu-id="82319-113">Backups can be compressed and encrypted, depending on the options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="82319-114">Konfigurowanie ustawień magazynu</span><span class="sxs-lookup"><span data-stu-id="82319-114">Configure storage settings</span></span>
<span data-ttu-id="82319-115">Przed utworzeniem kopii zapasowej, należy skonfigurować ustawienia magazynu dla serwera.</span><span class="sxs-lookup"><span data-stu-id="82319-115">Before backing up, you need to configure storage settings for your server.</span></span>


### <a name="to-configure-storage-settings"></a><span data-ttu-id="82319-116">Aby skonfigurować ustawienia magazynu</span><span class="sxs-lookup"><span data-stu-id="82319-116">To configure storage settings</span></span>
1.  <span data-ttu-id="82319-117">W portalu Azure > **ustawienia**, kliknij przycisk **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="82319-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Tworzenie kopii zapasowych w ustawieniach](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="82319-119">Kliknij przycisk **włączone**, następnie kliknij przycisk **ustawienia magazynu**.</span><span class="sxs-lookup"><span data-stu-id="82319-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Włączanie](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="82319-121">Wybierz konto magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="82319-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="82319-122">Wybierz kontener lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="82319-122">Select a container or create a new one.</span></span>

    ![Wybierz kontener](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="82319-124">Zapisz ustawienia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="82319-124">Save your backup settings.</span></span>

    ![Zapisanie ustawień kopii zapasowej](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="82319-126">Tworzenie kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="82319-126">Backup</span></span>

### <a name="to-backup-by-using-ssms"></a><span data-ttu-id="82319-127">Do wykonania kopii zapasowej przy użyciu narzędzia SSMS</span><span class="sxs-lookup"><span data-stu-id="82319-127">To backup by using SSMS</span></span>

1. <span data-ttu-id="82319-128">W programie SSMS, kliknij prawym przyciskiem myszy bazę danych > **kopię zapasową**.</span><span class="sxs-lookup"><span data-stu-id="82319-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="82319-129">W **instrukcji Backup Database** > **plik kopii zapasowej**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="82319-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="82319-130">W **Zapisz plik jako** okna dialogowego, sprawdź, czy ścieżka folderu, a następnie wpisz nazwę pliku kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="82319-130">In the **Save file as** dialog, verify the folder path, and then type a name for the backup file.</span></span> 

4. <span data-ttu-id="82319-131">W **instrukcji Backup Database** okno dialogowe, wybierz pozycję Opcje.</span><span class="sxs-lookup"><span data-stu-id="82319-131">In the **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="82319-132">**Zezwalaj na plik zastąpić** — wybierz tę opcję, aby zastąpić tworzenia kopii zapasowej plików o takiej samej nazwie.</span><span class="sxs-lookup"><span data-stu-id="82319-132">**Allow file overwrite** - Select this option to overwrite backup files of the same name.</span></span> <span data-ttu-id="82319-133">Jeśli ta opcja nie jest zaznaczona, zapisywanego pliku nie może mieć takiej samej nazwie jako plik już istnieje w tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="82319-133">If this option is not selected, the file you are saving cannot have the same name as a file that already exists in the same location.</span></span>

    <span data-ttu-id="82319-134">**Zastosowanie kompresji** — wybierz tę opcję, aby kompresować pliku kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="82319-134">**Apply compression** - Select this option to compress the backup file.</span></span> <span data-ttu-id="82319-135">Skompresowane pliki kopii zapasowej zaoszczędzić miejsce na dysku, ale wymaga nieco większe użycie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="82319-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="82319-136">**Szyfrowanie pliku kopii zapasowej** — wybierz tę opcję, aby zaszyfrować plik kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="82319-136">**Encrypt backup file** - Select this option to encrypt the backup file.</span></span> <span data-ttu-id="82319-137">Ta opcja wymaga hasło dostarczone przez użytkownika, aby zabezpieczyć plik kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="82319-137">This option requires a user-supplied password to secure the backup file.</span></span> <span data-ttu-id="82319-138">Hasło zapobiega odczytywanie danych kopii zapasowej inny sposób niż operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="82319-138">The password prevents reading of the backup data any other means than a restore operation.</span></span> <span data-ttu-id="82319-139">Jeśli wybierzesz do szyfrowania kopii zapasowych, przechowywania hasła w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="82319-139">If you choose to encrypt backups, store the password in a safe location.</span></span>

5. <span data-ttu-id="82319-140">Kliknij przycisk **OK** Aby utworzyć i zapisać plik kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="82319-140">Click **OK** to create and save the backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="82319-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82319-141">PowerShell</span></span>
<span data-ttu-id="82319-142">Użyj [ASDatabase kopii zapasowej](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="82319-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="82319-143">Przywracanie</span><span class="sxs-lookup"><span data-stu-id="82319-143">Restore</span></span>
<span data-ttu-id="82319-144">Podczas przywracania, pliku kopii zapasowej musi być na koncie magazynu, skonfigurowanego dla serwera.</span><span class="sxs-lookup"><span data-stu-id="82319-144">When restoring, your backup file must be in the storage account you've configured for your server.</span></span> <span data-ttu-id="82319-145">Jeśli musisz przenieść plik kopii zapasowej z lokalizacji lokalnej do konta magazynu, należy użyć [Eksploratora usługi Microsoft Azure Storage](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) lub [AzCopy](../storage/common/storage-use-azcopy.md) narzędzia wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="82319-145">If you need to move a backup file from an on-premises location to your storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or the [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="82319-146">Jeśli jest przywracana z lokalnego serwera, należy usunąć wszystkich użytkowników domeny z modelu ról i dodaj je do ról jako użytkowników usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="82319-146">If you're restoring from an on-premises server, you must remove all the domain users from the model's roles and add them back to the roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="to-restore-by-using-ssms"></a><span data-ttu-id="82319-147">Aby przywrócić za pomocą narzędzia SSMS</span><span class="sxs-lookup"><span data-stu-id="82319-147">To restore by using SSMS</span></span>

1. <span data-ttu-id="82319-148">W programie SSMS, kliknij prawym przyciskiem myszy bazę danych > **przywrócić**.</span><span class="sxs-lookup"><span data-stu-id="82319-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="82319-149">W **instrukcji Backup Database** okna dialogowego, w **plik kopii zapasowej**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="82319-149">In the **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="82319-150">W **zlokalizować pliki bazy danych** okno dialogowe, wybierz plik, który chcesz przywrócić.</span><span class="sxs-lookup"><span data-stu-id="82319-150">In the **Locate Database Files** dialog, select the file you want to restore.</span></span>

4. <span data-ttu-id="82319-151">W **Przywróć bazę danych**, wybierz bazę danych.</span><span class="sxs-lookup"><span data-stu-id="82319-151">In **Restore database**, select the database.</span></span>

5. <span data-ttu-id="82319-152">Określ opcje.</span><span class="sxs-lookup"><span data-stu-id="82319-152">Specify options.</span></span> <span data-ttu-id="82319-153">Opcje zabezpieczeń muszą być zgodne opcje tworzenia kopii zapasowej, używane podczas wykonywania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="82319-153">Security options must match the backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="82319-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82319-154">PowerShell</span></span>

<span data-ttu-id="82319-155">Użyj [ASDatabase przywracania](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="82319-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="82319-156">Informacje pokrewne</span><span class="sxs-lookup"><span data-stu-id="82319-156">Related information</span></span>

[<span data-ttu-id="82319-157">Konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="82319-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="82319-158">[Wysoka dostępność](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="82319-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="82319-159">Zarządzanie usług Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="82319-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
