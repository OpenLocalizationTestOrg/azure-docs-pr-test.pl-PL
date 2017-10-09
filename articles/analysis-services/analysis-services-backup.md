---
title: Baza danych Analysis Services aaaAzure i przywracania kopii zapasowych | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak toobackup i przywracania usług Azure Analysis bazy danych."
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
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="c3a6a-103">Tworzenie kopii zapasowej i przywracanie</span><span class="sxs-lookup"><span data-stu-id="c3a6a-103">Backup and restore</span></span>

<span data-ttu-id="c3a6a-104">Tworzenie kopii zapasowej bazy danych modelu tabelarycznego w usług Azure Analysis Services jest znacznie Witaj takie same jak w przypadku lokalnego Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-104">Backing up tabular model databases in Azure Analysis Services is much hello same as for on-premises Analysis Services.</span></span> <span data-ttu-id="c3a6a-105">Główną różnicą Hello służy do przechowywania plików kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-105">hello primary difference is where you store your backup files.</span></span> <span data-ttu-id="c3a6a-106">Pliki kopii zapasowej należy zapisać tooa kontenera w [konto magazynu Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-106">Backup files must be saved tooa container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="c3a6a-107">Można było utworzyć, konfigurując ustawienia magazynu dla serwera lub służy konto magazynu i kontener, który już istnieje.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="c3a6a-108">Tworzenie konta magazynu może skutkować nową usługą płatną.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="c3a6a-109">toolearn więcej, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="c3a6a-109">toolearn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="c3a6a-110">Kopie zapasowe są zapisywane z rozszerzeniem abf.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="c3a6a-111">Dla modeli tabelarycznych w pamięci zarówno w modelu danych, jak i metadane są przechowywane.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="c3a6a-112">Dla modeli tabelarycznych zapytania bezpośredniego są przechowywane tylko metadane modelu.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="c3a6a-113">Kopie zapasowe można skompresować i szyfrowane, w zależności od opcji hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-113">Backups can be compressed and encrypted, depending on hello options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="c3a6a-114">Konfigurowanie ustawień magazynu</span><span class="sxs-lookup"><span data-stu-id="c3a6a-114">Configure storage settings</span></span>
<span data-ttu-id="c3a6a-115">Przed utworzeniem kopii zapasowej, należy tooconfigure miejsca do magazynowania dla serwera.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-115">Before backing up, you need tooconfigure storage settings for your server.</span></span>


### <a name="tooconfigure-storage-settings"></a><span data-ttu-id="c3a6a-116">Ustawienia magazynu tooconfigure</span><span class="sxs-lookup"><span data-stu-id="c3a6a-116">tooconfigure storage settings</span></span>
1.  <span data-ttu-id="c3a6a-117">W portalu Azure > **ustawienia**, kliknij przycisk **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Tworzenie kopii zapasowych w ustawieniach](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="c3a6a-119">Kliknij przycisk **włączone**, następnie kliknij przycisk **ustawienia magazynu**.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Włączanie](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="c3a6a-121">Wybierz konto magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="c3a6a-122">Wybierz kontener lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-122">Select a container or create a new one.</span></span>

    ![Wybierz kontener](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="c3a6a-124">Zapisz ustawienia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-124">Save your backup settings.</span></span>

    ![Zapisanie ustawień kopii zapasowej](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="c3a6a-126">Tworzenie kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="c3a6a-126">Backup</span></span>

### <a name="toobackup-by-using-ssms"></a><span data-ttu-id="c3a6a-127">toobackup przy użyciu narzędzia SSMS</span><span class="sxs-lookup"><span data-stu-id="c3a6a-127">toobackup by using SSMS</span></span>

1. <span data-ttu-id="c3a6a-128">W programie SSMS, kliknij prawym przyciskiem myszy bazę danych > **kopię zapasową**.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="c3a6a-129">W **instrukcji Backup Database** > **plik kopii zapasowej**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="c3a6a-130">W hello **Zapisz plik jako** okna dialogowego, sprawdź, czy ścieżka folderu hello, a następnie wpisz nazwę pliku kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-130">In hello **Save file as** dialog, verify hello folder path, and then type a name for hello backup file.</span></span> 

4. <span data-ttu-id="c3a6a-131">W hello **instrukcji Backup Database** okno dialogowe, wybierz pozycję Opcje.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-131">In hello **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="c3a6a-132">**Plik zastąpić** — wybierz to opcja toooverwrite pliki kopii zapasowej hello tej samej nazwy.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-132">**Allow file overwrite** - Select this option toooverwrite backup files of hello same name.</span></span> <span data-ttu-id="c3a6a-133">Jeśli ta opcja nie jest zaznaczona, zapisujesz plik hello nie może mieć hello takie same nazwy jako plik już istnieje w hello sam lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-133">If this option is not selected, hello file you are saving cannot have hello same name as a file that already exists in hello same location.</span></span>

    <span data-ttu-id="c3a6a-134">**Zastosowanie kompresji** — wybierz tej opcję toocompress hello plik kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-134">**Apply compression** - Select this option toocompress hello backup file.</span></span> <span data-ttu-id="c3a6a-135">Skompresowane pliki kopii zapasowej zaoszczędzić miejsce na dysku, ale wymaga nieco większe użycie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="c3a6a-136">**Szyfrowanie pliku kopii zapasowej** — wybierz tej opcję tooencrypt hello plik kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-136">**Encrypt backup file** - Select this option tooencrypt hello backup file.</span></span> <span data-ttu-id="c3a6a-137">Ta opcja wymaga hasła podanego przez użytkownika toosecure hello plik kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-137">This option requires a user-supplied password toosecure hello backup file.</span></span> <span data-ttu-id="c3a6a-138">Witaj hasło zapobiega odczytywanie danych kopii zapasowej hello inny sposób niż operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-138">hello password prevents reading of hello backup data any other means than a restore operation.</span></span> <span data-ttu-id="c3a6a-139">Jeśli wybierzesz tooencrypt kopii zapasowych, przechowywać hello hasła w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-139">If you choose tooencrypt backups, store hello password in a safe location.</span></span>

5. <span data-ttu-id="c3a6a-140">Kliknij przycisk **OK** toocreate i Zapisz plik kopii zapasowej hello.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-140">Click **OK** toocreate and save hello backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="c3a6a-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3a6a-141">PowerShell</span></span>
<span data-ttu-id="c3a6a-142">Użyj [ASDatabase kopii zapasowej](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="c3a6a-143">Przywracanie</span><span class="sxs-lookup"><span data-stu-id="c3a6a-143">Restore</span></span>
<span data-ttu-id="c3a6a-144">Podczas przywracania, pliku kopii zapasowej musi być na koncie magazynu hello skonfigurowanego dla serwera.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-144">When restoring, your backup file must be in hello storage account you've configured for your server.</span></span> <span data-ttu-id="c3a6a-145">Toomove plik kopii zapasowej z konta magazynu tooyour lokalizacji lokalnej, należy użyć [Eksploratora usługi Microsoft Azure Storage](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) lub hello [AzCopy](../storage/common/storage-use-azcopy.md) narzędzia wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-145">If you need toomove a backup file from an on-premises location tooyour storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or hello [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="c3a6a-146">Jeśli jest przywracana z lokalnego serwera, należy usunąć wszystkich użytkowników domeny hello z modelu hello ról i dodać je kopii toohello ról jako użytkowników usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-146">If you're restoring from an on-premises server, you must remove all hello domain users from hello model's roles and add them back toohello roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="toorestore-by-using-ssms"></a><span data-ttu-id="c3a6a-147">toorestore przy użyciu narzędzia SSMS</span><span class="sxs-lookup"><span data-stu-id="c3a6a-147">toorestore by using SSMS</span></span>

1. <span data-ttu-id="c3a6a-148">W programie SSMS, kliknij prawym przyciskiem myszy bazę danych > **przywrócić**.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="c3a6a-149">W hello **instrukcji Backup Database** okna dialogowego, w **plik kopii zapasowej**, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-149">In hello **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="c3a6a-150">W hello **zlokalizować pliki bazy danych** okno dialogowe, wybierz hello pliku, który chcesz toorestore.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-150">In hello **Locate Database Files** dialog, select hello file you want toorestore.</span></span>

4. <span data-ttu-id="c3a6a-151">W **Przywróć bazę danych**, wybierz pozycję hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-151">In **Restore database**, select hello database.</span></span>

5. <span data-ttu-id="c3a6a-152">Określ opcje.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-152">Specify options.</span></span> <span data-ttu-id="c3a6a-153">Opcje zabezpieczeń muszą być zgodne hello opcje tworzenia kopii zapasowej, używane podczas wykonywania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-153">Security options must match hello backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="c3a6a-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3a6a-154">PowerShell</span></span>

<span data-ttu-id="c3a6a-155">Użyj [ASDatabase przywracania](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c3a6a-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="c3a6a-156">Informacje pokrewne</span><span class="sxs-lookup"><span data-stu-id="c3a6a-156">Related information</span></span>

[<span data-ttu-id="c3a6a-157">Konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c3a6a-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="c3a6a-158">[Wysoka dostępność](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="c3a6a-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="c3a6a-159">Zarządzanie usług Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="c3a6a-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
