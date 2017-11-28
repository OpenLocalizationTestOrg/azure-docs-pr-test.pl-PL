---
title: aaaInstall serwer kopii zapasowej Azure w wersji 2 | Dokumentacja firmy Microsoft
description: "Azure v2 Utwórz kopię zapasową serwera udostępnia udoskonalone funkcje tworzenia kopii zapasowej ochrony maszyn wirtualnych, plików i folderów oraz obciążeń. Dowiedz się, jak tooAzure tooinstall lub uaktualnienia Utwórz kopię zapasową serwera v2."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="353fd-104">Zainstaluj serwer kopii zapasowej systemu Azure w wersji 2</span><span class="sxs-lookup"><span data-stu-id="353fd-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="353fd-105">Serwer kopii zapasowej systemu Azure pomaga w ochronie maszyn wirtualnych (VM), obciążenia, pliki i foldery i więcej.</span><span class="sxs-lookup"><span data-stu-id="353fd-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="353fd-106">Azure v2 Utwórz kopię zapasową serwera oparty na serwer kopii zapasowej Azure w wersji 1 i udostępnia nowe funkcje, które nie są dostępne w wersji 1.</span><span class="sxs-lookup"><span data-stu-id="353fd-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="353fd-107">Porównanie funkcji między v1 i v2, zobacz [macierzy ochrona serwer kopii zapasowej Azure](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="353fd-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="353fd-108">uaktualnienie z wersji 1 Utwórz kopię zapasową serwera nie są Hello dodatkowe funkcje w wersji 2 Utwórz kopię zapasową serwera.</span><span class="sxs-lookup"><span data-stu-id="353fd-108">hello additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="353fd-109">Jednak v1 Utwórz kopię zapasową serwera nie jest wymagane w przypadku instalowania serwera kopii zapasowej w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="353fd-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="353fd-110">Jeśli tooupgrade z kopii zapasowej serwera v1 tooBackup Server v2, należy zainstalować v2 Utwórz kopię zapasową serwera na powitania kopii zapasowej ochrony serwera.</span><span class="sxs-lookup"><span data-stu-id="353fd-110">If you want tooupgrade from Backup Server v1 tooBackup Server v2, install Backup Server v2 on hello Backup Server protection server.</span></span> <span data-ttu-id="353fd-111">Istniejących ustawień serwera kopii zapasowej pozostaną nienaruszone.</span><span class="sxs-lookup"><span data-stu-id="353fd-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="353fd-112">Utwórz kopię zapasową serwera v2 można zainstalować w systemie Windows Server 2012 R2 lub Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="353fd-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="353fd-113">tootake korzystać z nowych funkcji, takich jak System Center 2016 ochrony Menedżera Modern kopii zapasowej pamięci masowej, v2 kopii zapasowej serwera należy zainstalować w systemie Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="353fd-113">tootake advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="353fd-114">Przed uaktualnieniem instalacji tooor v2 Utwórz kopię zapasową serwera, przeczytaj o hello [wymagania wstępne instalacji](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="353fd-114">Before you upgrade tooor install Backup Server v2, read about hello [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="353fd-115">Serwer kopii zapasowej systemu Azure ma hello tego samego kodu podstawowej jako System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="353fd-115">Azure Backup Server has hello same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="353fd-116">V1 serwera kopii zapasowej jest równoważne tooData Protection Manager 2012 R2, a v2 Utwórz kopię zapasową serwera jest równoważne tooData Protection Manager 2016.</span><span class="sxs-lookup"><span data-stu-id="353fd-116">Backup Server v1 is equivalent tooData Protection Manager 2012 R2, and Backup Server v2 is equivalent tooData Protection Manager 2016.</span></span> <span data-ttu-id="353fd-117">W tym artykule odwołuje się od czasu do czasu hello dokumentacji programu Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="353fd-117">This article occasionally references hello Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-toov2"></a><span data-ttu-id="353fd-118">Uaktualnij toov2 kopii zapasowej serwera</span><span class="sxs-lookup"><span data-stu-id="353fd-118">Upgrade Backup Server toov2</span></span>
<span data-ttu-id="353fd-119">tooupgrade z kopii zapasowej serwera v1 tooBackup Server v2, upewnij się, że instalacja ma hello wymagane aktualizacje:</span><span class="sxs-lookup"><span data-stu-id="353fd-119">tooupgrade from Backup Server v1 tooBackup Server v2, make sure your installation has hello required updates:</span></span>

- <span data-ttu-id="353fd-120">[Aktualizowanie agentów ochrony hello](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) na powitania chronionymi serwerami.</span><span class="sxs-lookup"><span data-stu-id="353fd-120">[Update hello protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on hello protected servers.</span></span>
- <span data-ttu-id="353fd-121">Uaktualnienie systemu Windows Server 2012 R2 tooWindows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="353fd-121">Upgrade Windows Server 2012 R2 tooWindows Server 2016.</span></span>
- <span data-ttu-id="353fd-122">Uaktualnij administratora zdalnego serwera kopii zapasowej platformy Azure na wszystkich serwerach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="353fd-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="353fd-123">Upewnij się, że kopie zapasowe są ustawione toocontinue bez ponownego uruchomienia serwera produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="353fd-123">Ensure that backups are set toocontinue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="353fd-124">Kroki uaktualniania dla kopii zapasowej serwera w wersji 2</span><span class="sxs-lookup"><span data-stu-id="353fd-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="353fd-125">W Centrum pobierania hello [Pobierz Instalator uaktualnienia hello](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="353fd-125">In hello Download Center, [download hello upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="353fd-126">Po wyodrębnieniu hello Kreatora instalacji upewnij się, że **wykonania setup.exe** jest wybrany, a następnie wybierz **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="353fd-126">After you extract hello setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Instalator Instalatora — należy uruchomić Instalator](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="353fd-128">W Kreatorze hello serwer kopii zapasowej Microsoft Azure w obszarze **zainstalować**, wybierz pozycję **serwer kopii zapasowej Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="353fd-128">In hello Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Instalator Instalatora — wybierz opcję instalacji](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="353fd-130">Na powitania **powitalnej** Przejrzyj hello ostrzeżenia, a następnie wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="353fd-130">On hello **Welcome** page, review hello warnings, and then select **Next**.</span></span>

  ![Instalator Instalatora - strony powitalnej](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="353fd-132">Kreator instalacji Hello wykonuje sprawdzanie wymagań wstępnych toomake się, że w środowisku można uaktualnić.</span><span class="sxs-lookup"><span data-stu-id="353fd-132">hello setup wizard performs prerequisite checks toomake sure your environment can upgrade.</span></span> <span data-ttu-id="353fd-133">Na powitania **wymagań wstępnych sprawdza** wybierz pozycję **Sprawdź**.</span><span class="sxs-lookup"><span data-stu-id="353fd-133">On hello **Prerequisite Checks** page, select **Check**.</span></span>

  ![Instalator — strona kontroli wymagań wstępnych Instalatora](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="353fd-135">Środowisko musi przejść pomyślnie hello wymagań wstępnych.</span><span class="sxs-lookup"><span data-stu-id="353fd-135">Your environment must pass hello prerequisite checks.</span></span> <span data-ttu-id="353fd-136">Jeśli w środowisku nie przeszły pomyślnie testu hello, zanotuj hello problemy, a następnie naprawione.</span><span class="sxs-lookup"><span data-stu-id="353fd-136">If your environment doesn't pass hello checks, note hello issues and fix them.</span></span> <span data-ttu-id="353fd-137">Następnie wybierz opcję **Sprawdź ponownie**.</span><span class="sxs-lookup"><span data-stu-id="353fd-137">Then, select **Check Again**.</span></span> <span data-ttu-id="353fd-138">Po przekazujesz hello wymagań wstępnych, wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="353fd-138">After you pass hello prerequisite checks, select **Next**.</span></span>

  ![Instalator Instalatora — przycisk Sprawdź ponownie](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="353fd-140">Na powitania **ustawienia SQL** , wybierz odpowiednią opcję hello do instalacji programu SQL, a następnie wybierz **Sprawdź i zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="353fd-140">On hello **SQL Settings** page, select hello relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Instalator Instalatora — strona ustawień SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="353fd-142">Sprawdzanie Hello może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="353fd-142">hello checks might take a few minutes.</span></span> <span data-ttu-id="353fd-143">Kiedy kontroli hello są gotowe, wybierz pozycję **dalej**.</span><span class="sxs-lookup"><span data-stu-id="353fd-143">When hello checks are finished, select **Next**.</span></span>

  ![Instalator Instalatora — Sprawdź ustawienia SQL i przycisk Zainstaluj](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="353fd-145">Na powitania **ustawienia instalacji** pozycję dowolnej lokalizacji toohello zmiany, których zainstalowano Utwórz kopię zapasową serwera lub toohello lokalizacji przechowywania plików tymczasowych.</span><span class="sxs-lookup"><span data-stu-id="353fd-145">On hello **Installation Settings** page, make any changes toohello location where Backup Server is installed, or toohello Scratch Location.</span></span> <span data-ttu-id="353fd-146">Wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="353fd-146">Select **Next**.</span></span>

  ![Instalator Instalatora — strona Ustawienia instalacji](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="353fd-148">toofinish hello Kreatora instalacji, wybierz opcję **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="353fd-148">toofinish hello setup wizard, select **Finish**.</span></span>

  ![Instalator Instalatora — zakończenie](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="353fd-150">Dodawanie magazynu dla nowoczesnych magazynu kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="353fd-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="353fd-151">wydajność magazynu kopii zapasowej tooimprove, v2 Utwórz kopię zapasową serwera dodaje obsługę woluminów.</span><span class="sxs-lookup"><span data-stu-id="353fd-151">tooimprove backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="353fd-152">Jak serwer zapasowy v1 v2 Utwórz kopię zapasową serwera obsługuje dyski.</span><span class="sxs-lookup"><span data-stu-id="353fd-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="353fd-153">Dodaj do woluminów i dysków</span><span class="sxs-lookup"><span data-stu-id="353fd-153">Add volumes and disks</span></span>
<span data-ttu-id="353fd-154">Po uruchomieniu v2 Utwórz kopię zapasową serwera w systemie Windows Server 2016 można użyć woluminów toostore kopii zapasowej danych.</span><span class="sxs-lookup"><span data-stu-id="353fd-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes toostore backup data.</span></span> <span data-ttu-id="353fd-155">Woluminy oferują oszczędności pojemności magazynu i szybsze tworzenie kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="353fd-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="353fd-156">Ponieważ woluminy są tooBackup nowego serwera, należy je dodać.</span><span class="sxs-lookup"><span data-stu-id="353fd-156">Because volumes are new tooBackup Server, you must add them.</span></span> 

<span data-ttu-id="353fd-157">Po dodaniu tooBackup woluminu serwera można nadać woluminu hello przyjazną nazwę.</span><span class="sxs-lookup"><span data-stu-id="353fd-157">When you add a volume tooBackup Server, you can give hello volume a friendly name.</span></span> <span data-ttu-id="353fd-158">Kliknij przycisk hello **przyjazną nazwę** kolumny woluminu hello ma tooname.</span><span class="sxs-lookup"><span data-stu-id="353fd-158">Click hello **Friendly Name** column of hello volume you want tooname.</span></span> <span data-ttu-id="353fd-159">Nazwa hello można zmienić później, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="353fd-159">You can change hello name later, if necessary.</span></span> <span data-ttu-id="353fd-160">Możesz również użyć programu PowerShell tooadd lub zmienić przyjazne nazwy dla woluminów.</span><span class="sxs-lookup"><span data-stu-id="353fd-160">You also can use PowerShell tooadd or change friendly names for volumes.</span></span>

<span data-ttu-id="353fd-161">tooadd woluminu w hello Konsola administratora:</span><span class="sxs-lookup"><span data-stu-id="353fd-161">tooadd a volume in hello Administrator Console:</span></span>

1. <span data-ttu-id="353fd-162">W konsoli administratora serwera kopii zapasowej Azure hello, wybierz **zarządzania** > **Magazyn dyskowy** > **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="353fd-162">In hello Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Otwórz hello kreatora Dodawanie magazynu dyskowego](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="353fd-164">Spowoduje to otwarcie kreatora Dodawanie magazynu dyskowego hello.</span><span class="sxs-lookup"><span data-stu-id="353fd-164">This opens hello Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="353fd-165">Na powitania **dodać magazyn dyskowy** strony w hello **dostępnych woluminów** , wybierz wolumin, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="353fd-165">On hello **Add Disk Storage** page, in hello **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="353fd-166">W hello **wybrane woluminy** Wprowadź przyjazną nazwę dla woluminu hello, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="353fd-166">In hello **Selected volumes** box, enter a friendly name for hello volume, and then select **OK**.</span></span>

      ![Magazyn dyskowy Kreator dodawania — Dodawanie woluminu](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="353fd-168">Jeśli chcesz tooadd dysku, dysku hello muszą należeć tooa grupy ochrony, która ma starszej wersji magazynu.</span><span class="sxs-lookup"><span data-stu-id="353fd-168">If you want tooadd a disk, hello disk must belong tooa protection group that has legacy storage.</span></span> <span data-ttu-id="353fd-169">Te dyski mogą być używane tylko dla tych grup ochrony.</span><span class="sxs-lookup"><span data-stu-id="353fd-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="353fd-170">Jeśli serwer zapasowy nie ma źródeł, które mają ochronę za pomocą starszej wersji, nie ma na liście hello dysku.</span><span class="sxs-lookup"><span data-stu-id="353fd-170">If Backup Server doesn't have sources that have legacy protection, hello disk isn't listed.</span></span>

  <span data-ttu-id="353fd-171">Aby uzyskać więcej informacji na temat dodawania dysków, zobacz [Dodawanie magazynu starszych tooincrease dysków](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span><span class="sxs-lookup"><span data-stu-id="353fd-171">For more information about adding disks, see [Adding disks tooincrease legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="353fd-172">Nie można nadać przyjazną nazwę dysku.</span><span class="sxs-lookup"><span data-stu-id="353fd-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-toovolumes"></a><span data-ttu-id="353fd-173">Przypisz toovolumes obciążeń</span><span class="sxs-lookup"><span data-stu-id="353fd-173">Assign workloads toovolumes</span></span>

<span data-ttu-id="353fd-174">Utwórz kopię zapasową serwera, należy określić w obciążeń, które są przypisane toowhich woluminów.</span><span class="sxs-lookup"><span data-stu-id="353fd-174">In Backup Server, you specify which workloads are assigned toowhich volumes.</span></span> <span data-ttu-id="353fd-175">Na przykład można ustawić kosztowne woluminów, które obsługują dużej liczby operacji wejścia/wyjścia na drugim (IOPS) toostore tylko obciążeń, które wymagają częstego, dużej liczby kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="353fd-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="353fd-176">Przykładem jest program SQL Server z dzienników transakcji.</span><span class="sxs-lookup"><span data-stu-id="353fd-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="353fd-177">DPMDiskStorage aktualizacji</span><span class="sxs-lookup"><span data-stu-id="353fd-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="353fd-178">właściwości hello tooupdate woluminu w puli magazynu hello w kopii zapasowej serwera, użyj polecenia cmdlet programu PowerShell hello DPMDiskStorage aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="353fd-178">tooupdate hello properties of a volume in hello storage pool in Backup Server, use hello PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="353fd-179">Składnia:</span><span class="sxs-lookup"><span data-stu-id="353fd-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="353fd-180">Wszystkie zmiany wprowadzone przy użyciu programu PowerShell są odzwierciedlane w hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="353fd-180">All changes that you make by using PowerShell are reflected in hello UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="353fd-181">Ochrona źródeł danych</span><span class="sxs-lookup"><span data-stu-id="353fd-181">Protect data sources</span></span>
<span data-ttu-id="353fd-182">toobegin ochrona źródeł danych, Utwórz grupę ochrony.</span><span class="sxs-lookup"><span data-stu-id="353fd-182">toobegin protecting data sources, create a protection group.</span></span> <span data-ttu-id="353fd-183">Witaj następujące kroki Wyróżnij zmiany lub dodatki toohello Kreatora nowej grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="353fd-183">hello following steps highlight changes or additions toohello New Protection Group wizard.</span></span>

<span data-ttu-id="353fd-184">toocreate grupy ochrony:</span><span class="sxs-lookup"><span data-stu-id="353fd-184">toocreate a protection group:</span></span>

1. <span data-ttu-id="353fd-185">W konsoli administratora serwera kopii zapasowej hello, wybierz **ochrony**.</span><span class="sxs-lookup"><span data-stu-id="353fd-185">In hello Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="353fd-186">Na wstążce narzędzi hello, wybierz **nowy**.</span><span class="sxs-lookup"><span data-stu-id="353fd-186">On hello tool ribbon, select **New**.</span></span>

    <span data-ttu-id="353fd-187">Spowoduje to otwarcie Kreatora tworzenia nowej grupy ochrony hello.</span><span class="sxs-lookup"><span data-stu-id="353fd-187">This opens hello Create New Protection Group wizard.</span></span>

  ![Kreator tworzenia nowej grupy ochrony](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="353fd-189">Na powitania **powitalnej** wybierz pozycję **dalej**.</span><span class="sxs-lookup"><span data-stu-id="353fd-189">On hello **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="353fd-190">Na powitania **wybierz typ grupy ochrony** wybierz typ grupy ochrony mają toocreate, a następnie wybierz hello **dalej**.</span><span class="sxs-lookup"><span data-stu-id="353fd-190">On hello **Select Protection Group Type** page, select hello type of protection group you want toocreate, and then select **Next**.</span></span>

  ![Strona Typ wybierz grupę ochrony](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="353fd-192">Na powitania **Wybierz członków grupy** strony w hello **dostępni członkowie** okienka, hello członków z ochrony agenci są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="353fd-192">On hello **Select Group Members** page, in hello **Available members** pane, hello members with protection agents are listed.</span></span> <span data-ttu-id="353fd-193">Na przykład wybierz wolumin D:\ i E:\ i dodaj je toohello **wybranych składników** okienka.</span><span class="sxs-lookup"><span data-stu-id="353fd-193">For this example, select volume D:\ and E:\ and add them toohello **Selected members** pane.</span></span> <span data-ttu-id="353fd-194">Wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="353fd-194">Select **Next**.</span></span>

  ![Wybierz grupy elementów członkowskich strony](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="353fd-196">Na powitania **wybierz metodę ochrony danych** wprowadź **Nazwa grupy ochrony**, wybierz metodę ochrony hello, a następnie wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="353fd-196">On hello **Select Data Protection Method** page, enter a **Protection group name**, select hello protection method, and then select **Next**.</span></span> <span data-ttu-id="353fd-197">Jeśli chcesz uzyskać krótkoterminową ochronę, musisz wybrać hello **dysku** kopii zapasowej metody.</span><span class="sxs-lookup"><span data-stu-id="353fd-197">If you want short-term protection, you must select hello **Disk** backup method.</span></span>

  ![Wybierz metodę ochrony danych strony](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="353fd-199">Na powitania **Określ cele krótkoterminowe** strony szczegółów wybierz hello **zakres przechowywania** i **częstotliwość synchronizacji**.</span><span class="sxs-lookup"><span data-stu-id="353fd-199">On hello **Specify Short-Term Goals** page, select hello details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="353fd-200">Następnie wybierz opcję **dalej**.</span><span class="sxs-lookup"><span data-stu-id="353fd-200">Then, select **Next**.</span></span> <span data-ttu-id="353fd-201">Opcjonalnie toochange hello harmonogram gdy punkty odzyskiwania są podejmowane, wybierz pozycję **Modyfikuj**.</span><span class="sxs-lookup"><span data-stu-id="353fd-201">Optionally, toochange hello schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Określ cele krótkoterminowe strony](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="353fd-203">Na powitania **Przejrzyj przydział magazynu dyskowego** Przejrzyj szczegóły dotyczące wybranych źródeł danych hello, rozmiar i wartości dla toobe miejsca hello zainicjowano obsługę administracyjną i hello woluminu magazynu docelowego.</span><span class="sxs-lookup"><span data-stu-id="353fd-203">On hello **Review Disk Storage Allocation** page, review details about hello data sources you selected, their size, and  values for hello space toobe provisioned and hello target storage volume.</span></span>

  ![Przejrzyj przydział magazynu dyskowego strony](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="353fd-205">Woluminy magazynu są oparte na alokacji woluminu obciążenia hello (Ustaw przy użyciu programu PowerShell) i hello dostępny magazyn.</span><span class="sxs-lookup"><span data-stu-id="353fd-205">Storage volumes are based on hello workload volume allocation (set by using PowerShell) and hello available storage.</span></span> <span data-ttu-id="353fd-206">Woluminy magazynu hello można zmienić, wybierając w menu rozwijanym hello inne woluminy.</span><span class="sxs-lookup"><span data-stu-id="353fd-206">You can change hello storage volumes by selecting other volumes in hello drop-down menu.</span></span> <span data-ttu-id="353fd-207">W przypadku zmiany wartości hello **docelowy magazyn**, hello wartość **magazynu dostępnego dysku** dynamicznie zmiany wartości tooreflect **wolnego miejsca** i **Underprovisioned miejsca**.</span><span class="sxs-lookup"><span data-stu-id="353fd-207">If you change hello value for **Target Storage**, hello value for **Available disk storage** dynamically changes tooreflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="353fd-208">Jeśli źródeł danych hello wzrostu zgodnie z planem, hello wartość hello **Underprovisioned miejsca** kolumny w **magazynu dostępnego dysku** odzwierciedla hello ilość dodatkowego magazynu, które ma potrzebne.</span><span class="sxs-lookup"><span data-stu-id="353fd-208">If hello data sources grow as planned, hello value for hello **Underprovisioned Space** column in **Available disk storage** reflects hello amount of additional storage that's needed.</span></span> <span data-ttu-id="353fd-209">Użyj tego planu toohelp wartość magazynu musi smooth kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="353fd-209">Use this value toohelp plan your storage needs for smooth backups.</span></span> <span data-ttu-id="353fd-210">Jeśli hello wartość wynosi zero, nie ma żadnych potencjalnych problemów z magazynem, w najbliższej przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="353fd-210">If hello value is zero, there are no potential problems with storage in hello foreseeable future.</span></span> <span data-ttu-id="353fd-211">Jeśli wartość hello jest liczbą różne od zera, nie ma wystarczającej ilości miejsca przydzielone (oparte na sieci ochrony zasad i hello rozmiar danych z chronionych elementów członkowskich).</span><span class="sxs-lookup"><span data-stu-id="353fd-211">If hello value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and hello data size of your protected members).</span></span>

  ![Magazyn dyskowy niedostatecznej alokacji](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="353fd-213">toofinish Tworzenie kreatora hello pełną, grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="353fd-213">toofinish creating your protection group, complete hello wizard.</span></span>

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a><span data-ttu-id="353fd-214">Migrowanie starszych magazynu tooModern magazynu kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="353fd-214">Migrate legacy storage tooModern Backup Storage</span></span>
<span data-ttu-id="353fd-215">Po przeprowadzeniu uaktualnienia instalacji tooor Utwórz kopię zapasową serwera v2 i hello uaktualnienia systemu operacyjnego tooWindows Server 2016, należy zaktualizować toouse grupy z ochrony nowoczesnych magazynu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="353fd-215">After you upgrade tooor install Backup Server v2 and upgrade hello operating system tooWindows Server 2016, update your protection groups toouse Modern Backup Storage.</span></span> <span data-ttu-id="353fd-216">Domyślnie nie są zmieniane grup ochrony.</span><span class="sxs-lookup"><span data-stu-id="353fd-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="353fd-217">Nadal toofunction jako początkowo zostały ustawione.</span><span class="sxs-lookup"><span data-stu-id="353fd-217">They continue toofunction as they were initially set up.</span></span> 

<span data-ttu-id="353fd-218">Aktualizowanie toouse grup ochrony nowoczesnych magazynu kopii zapasowej jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="353fd-218">Updating protection groups toouse Modern Backup Storage is optional.</span></span> <span data-ttu-id="353fd-219">tooupdate hello grupy ochrony, Zatrzymaj ochronę wszystkich źródeł danych za pomocą hello zachować opcji danych.</span><span class="sxs-lookup"><span data-stu-id="353fd-219">tooupdate hello protection group, stop protection of all data sources by using hello retain data option.</span></span> <span data-ttu-id="353fd-220">Następnie należy dodać hello danych źródeł tooa nowej grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="353fd-220">Then, add hello data sources tooa new protection group.</span></span>

1. <span data-ttu-id="353fd-221">W konsoli administratora hello, wybierz hello **ochrony** funkcji.</span><span class="sxs-lookup"><span data-stu-id="353fd-221">In hello Administrator Console, select hello **Protection** feature.</span></span> <span data-ttu-id="353fd-222">W hello **członka grupy ochrony** listy, kliknij prawym przyciskiem myszy element członkowski hello, a następnie wybierz **Zatrzymaj ochronę członka**.</span><span class="sxs-lookup"><span data-stu-id="353fd-222">In hello **Protection Group Member** list, right-click hello member, and then select **Stop protection of member**.</span></span>

  ![Zatrzymaj ochronę członka](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="353fd-224">W hello **Usuń z grupy** okno dialogowe, przejrzyj hello używane miejsce na dysku i hello dostępne wolne miejsce w puli magazynów hello.</span><span class="sxs-lookup"><span data-stu-id="353fd-224">In hello **Remove from Group** dialog box, review hello used disk space and hello available free space for hello storage pool.</span></span> <span data-ttu-id="353fd-225">domyślne Hello jest punktów odzyskiwania hello tooleave na powitania dysku i zezwolić im tooexpire na skojarzonych zasad przechowywania.</span><span class="sxs-lookup"><span data-stu-id="353fd-225">hello default is tooleave hello recovery points on hello disk and allow them tooexpire per their associated retention policy.</span></span> <span data-ttu-id="353fd-226">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="353fd-226">Click **OK**.</span></span>

  <span data-ttu-id="353fd-227">Puli magazynu wolnego toohello miejsca tooimmediately zwracany hello używane dysku, wybierz opcję hello **Usuń replikę z dysku** pole wyboru toodelete hello kopii zapasowej danych (i punktów odzyskiwania) skojarzone z tym członkiem.</span><span class="sxs-lookup"><span data-stu-id="353fd-227">If you want tooimmediately return hello used disk space toohello free storage pool, select hello **Delete replica on disk** check box toodelete hello backup data (and recovery points) associated with that member.</span></span>

  ![Usuń z grupy, okno dialogowe](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="353fd-229">Utwórz grupę ochrony, która używa nowoczesnej magazynu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="353fd-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="353fd-230">Zawierają hello bez ochrony źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="353fd-230">Include hello unprotected data sources.</span></span>


## <a name="add-disks-tooincrease-legacy-storage"></a><span data-ttu-id="353fd-231">Dodawanie dysków tooincrease starszych magazynu</span><span class="sxs-lookup"><span data-stu-id="353fd-231">Add disks tooincrease legacy storage</span></span>

<span data-ttu-id="353fd-232">Toouse starszej wersji magazynu z kopii zapasowej serwera należy może być konieczne tooadd dysków tooincrease starszej wersji magazynu.</span><span class="sxs-lookup"><span data-stu-id="353fd-232">If you want toouse legacy storage with Backup Server, you might need tooadd disks tooincrease legacy storage.</span></span> 

<span data-ttu-id="353fd-233">Magazyn dyskowy tooadd:</span><span class="sxs-lookup"><span data-stu-id="353fd-233">tooadd disk storage:</span></span>

1. <span data-ttu-id="353fd-234">W konsoli administratora hello, wybierz **zarządzania** > **Magazyn dyskowy** > **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="353fd-234">In hello Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Magazyn dyskowy okno dialogowe Dodawanie](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="353fd-236">W hello **dodać magazyn dyskowy** okno dialogowe, wybierz opcję **Dodaj dyski**.</span><span class="sxs-lookup"><span data-stu-id="353fd-236">In hello **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="353fd-237">Hello listy dostępnych dysków, wybierz hello dyski, które chcesz tooadd, wybierz opcję **Dodaj**, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="353fd-237">In hello list of available disks, select hello disks you want tooadd, select **Add**, and then select **OK**.</span></span>

## <a name="update-hello-data-protection-manager-protection-agent"></a><span data-ttu-id="353fd-238">Zaktualizuj agenta ochrony programu Data Protection Manager hello</span><span class="sxs-lookup"><span data-stu-id="353fd-238">Update hello Data Protection Manager protection agent</span></span>

<span data-ttu-id="353fd-239">Utwórz kopię zapasową serwera używa hello System Center Data Protection Manager protection agent aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="353fd-239">Backup Server uses hello System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="353fd-240">Jeśli przeprowadzasz uaktualnienie agenta ochrony, który nie jest połączony toohello sieci, nie można użyć hello toocomplete Data Protection Manager Administrator Console uaktualnienia podłączonego agenta.</span><span class="sxs-lookup"><span data-stu-id="353fd-240">If you are upgrading a protection agent that is not connected toohello network, you cannot use hello Data Protection Manager Administrator Console toocomplete a connected agent upgrade.</span></span> <span data-ttu-id="353fd-241">Należy uaktualnić agenta ochrony hello w środowisku domeny nieaktywny.</span><span class="sxs-lookup"><span data-stu-id="353fd-241">You must upgrade hello protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="353fd-242">Dopóki hello komputer kliencki jest połączony toohello sieci, powitalne Data Protection Manager Administrator Console pokazuje tej aktualizacji agenta ochrony hello jest w stanie oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="353fd-242">Until hello client computer is connected toohello network, hello Data Protection Manager Administrator Console shows that hello protection agent update is pending.</span></span>

<span data-ttu-id="353fd-243">Witaj poniższych sekcjach opisano sposób tooupdate agentów ochrony dla komputerów klienckich, które są połączone i komputery klienckie, które nie są połączone.</span><span class="sxs-lookup"><span data-stu-id="353fd-243">hello following sections describe how tooupdate protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="353fd-244">Zaktualizuj agenta ochrony na podłączonym komputerze klienckim</span><span class="sxs-lookup"><span data-stu-id="353fd-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="353fd-245">W konsoli administratora serwera kopii zapasowej hello, wybierz **zarządzania** > **agentów**.</span><span class="sxs-lookup"><span data-stu-id="353fd-245">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="353fd-246">W okienku wyświetlania hello wybierz komputery klienckie hello, dla których ma agenta ochrony hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="353fd-246">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="353fd-247">Witaj **aktualizacji agenta** kolumna wskazuje, kiedy aktualizacji agenta ochrony jest dostępne dla każdego komputera chronionego.</span><span class="sxs-lookup"><span data-stu-id="353fd-247">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="353fd-248">W hello **akcje** okienka, hello **aktualizacji** akcja jest dostępna tylko wtedy, gdy komputer chroniony jest zaznaczony i są dostępne aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="353fd-248">In hello **Actions** pane, hello **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="353fd-249">tooinstall aktualizacji agentów ochrony na komputerach hello wybrane w hello **akcje** okienku wybierz **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="353fd-249">tooinstall updated protection agents on hello selected computers, in hello **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="353fd-250">Zaktualizuj agenta ochrony na komputerze klienckim, który nie jest połączony</span><span class="sxs-lookup"><span data-stu-id="353fd-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="353fd-251">W konsoli administratora serwera kopii zapasowej hello, wybierz **zarządzania** > **agentów**.</span><span class="sxs-lookup"><span data-stu-id="353fd-251">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="353fd-252">W okienku wyświetlania hello wybierz komputery klienckie hello, dla których ma agenta ochrony hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="353fd-252">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="353fd-253">Witaj **aktualizacji agenta** kolumna wskazuje, kiedy aktualizacji agenta ochrony jest dostępne dla każdego komputera chronionego.</span><span class="sxs-lookup"><span data-stu-id="353fd-253">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="353fd-254">W hello **akcje** okienka, hello **aktualizacji** akcja jest niedostępna, gdy komputer chroniony jest zaznaczony, chyba że są dostępne aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="353fd-254">In hello **Actions** pane, hello **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="353fd-255">tooinstall aktualizacji agentów ochrony na komputerach hello wybrana, wybierz opcję **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="353fd-255">tooinstall updated protection agents on hello selected computers, select **Update**.</span></span>

4. <span data-ttu-id="353fd-256">Dla komputera klienckiego, który nie jest połączonych sieci toohello, dopóki hello komputer jest połączony toohello sieci, hello **stan agenta** kolumna zawiera stan **oczekująca aktualizacja**.</span><span class="sxs-lookup"><span data-stu-id="353fd-256">For a client computer that is not connected toohello network, until hello computer is connected toohello network, hello **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="353fd-257">Komputer kliencki po sieci połączonych toohello hello **aktualizacji agenta** kolumny dla komputera klienckiego hello wskazuje stan **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="353fd-257">After a client computer is connected toohello network, hello **Agent Updates** column for hello client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a><span data-ttu-id="353fd-258">Przenieść starszych grup ochrony z starszą wersję i synchronizacji hello nowej wersji przy użyciu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="353fd-258">Move legacy Protection groups from old version and sync hello new version with Azure</span></span>

<span data-ttu-id="353fd-259">Gdy aktualizacji są zarówno serwer kopii zapasowej Azure i hello systemu operacyjnego, jest gotowy tooprotect nowych źródeł danych przy użyciu nowoczesnych magazynu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="353fd-259">Once Azure Backup Server and hello OS are both updated, you are ready tooprotect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="353fd-260">Jednak już chronione źródła danych będą nadal toobe chronione w starszej wersji hello sposób, jak były na serwerze kopii zapasowej Azure, ale wszystkie nowe ochrony będzie używać nowoczesnych magazynu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="353fd-260">However already protected data sources will continue toobe protected in hello legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="353fd-261">Następujące czynności są toomigrate źródeł danych z magazynu kopii zapasowych tooModern ochrony starszej wersji trybu.</span><span class="sxs-lookup"><span data-stu-id="353fd-261">Below steps are toomigrate data sources from legacy  mode of protection tooModern backup storage.</span></span>

<span data-ttu-id="353fd-262">• Dodaj hello nowych woluminów toohello puli magazynów programu DPM i przypisz przyjazną tagi źródła danych i nazwy, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="353fd-262">• Add hello new volume(s) toohello DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="353fd-263">• Dla każdego źródła danych, która jest w trybie starszej wersji, Zatrzymaj ochronę źródła danych hello i "Zachowaj chronione dane".</span><span class="sxs-lookup"><span data-stu-id="353fd-263">• For each data source that is in legacy mode, stop protection of hello data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="353fd-264">Pozwoli to odzyskiwania starych punktów odzyskiwania po migracji.</span><span class="sxs-lookup"><span data-stu-id="353fd-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="353fd-265">• Utwórz nowy PG i wybierz hello źródeł danych, które są toobe przechowywane przy użyciu nowego formatu.</span><span class="sxs-lookup"><span data-stu-id="353fd-265">• Create a new PG and select hello data sources that are toobe stored using new format.</span></span>
<span data-ttu-id="353fd-266">• Program DPM wykona kopia repliki z magazynu kopii zapasowych starszych hello do hello lokalnie nowoczesnych magazynu kopii zapasowej woluminu.</span><span class="sxs-lookup"><span data-stu-id="353fd-266">• DPM will do a replica copy from hello legacy backup storage into hello Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="353fd-267">Uwaga: To będą widoczne jako • zadania po odzyskiwaniu operacji wszystkie nowe synchronizacji i punktów odzyskiwania będą następnie przechowywane w nowoczesnych magazynu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="353fd-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="353fd-268">• Stare punkty odzyskiwania będą usuwane limit wygaśnie i ostatecznie wolnego miejsca na dysku hello.</span><span class="sxs-lookup"><span data-stu-id="353fd-268">• Old recovery points will be pruned out as they expire and eventually free up hello disk space.</span></span>
<span data-ttu-id="353fd-269">• Po wszystkich woluminów starszych hello są usuwane z hello starego magazynu, dysk hello można usunąć z platformy Azure i hello kopii zapasowych systemu.</span><span class="sxs-lookup"><span data-stu-id="353fd-269">• Once all hello legacy volumes are deleted from hello old storage, hello disk can be removed from Azure backup and hello system.</span></span>
<span data-ttu-id="353fd-270">• Wykonaj kopię zapasową programu hello Azure DPMDB.</span><span class="sxs-lookup"><span data-stu-id="353fd-270">• Take a backup of hello  Azure DPMDB.</span></span>

<span data-ttu-id="353fd-271">Część 2:-ważne elementy > hello nowego serwera należy toobe o nazwie takie same jak hello oryginalny serwer usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="353fd-271">Part 2: -Important items> hello new server will need toobe named same as hello original Azure Backup server.</span></span> <span data-ttu-id="353fd-272">Nie można zmienić nazwy hello hello nowego serwera kopii zapasowej Azure, jeśli chcesz toouse starego pulę magazynu i punkty odzyskiwania tooretain DPMDB — musi mieć kopię zapasową bazy danych dpmdb należy przywrócić toobe</span><span class="sxs-lookup"><span data-stu-id="353fd-272">You cannot change hello name of hello new Azure backup server if you want toouse old storage pool and DPMDB tooretain recovery points -Must have backup of DPMDB  as it will need toobe restored</span></span>

1) <span data-ttu-id="353fd-273">Zamknięcie hello oryginalny serwer kopii zapasowej platformy Azure lub wyłączanie przewodowy hello.</span><span class="sxs-lookup"><span data-stu-id="353fd-273">Shutdown hello original Azure backup server or take it off hello wire.</span></span>
2) <span data-ttu-id="353fd-274">Resetuj hello konta komputera w usłudze active directory.</span><span class="sxs-lookup"><span data-stu-id="353fd-274">Reset hello machine account in active directory.</span></span>
3) <span data-ttu-id="353fd-275">Zainstaluj Server 2016 na nowej maszyny i nazwy jej hello tej samej nazwy komputera jako hello oryginalny serwer usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="353fd-275">Install Server 2016 on new machine and name it hello same machine name as hello original Azure Backup server.</span></span>
4) <span data-ttu-id="353fd-276">Dołącz hello domeny</span><span class="sxs-lookup"><span data-stu-id="353fd-276">Join hello Domain</span></span>
5) <span data-ttu-id="353fd-277">Zainstaluj serwer usługi Kopia zapasowa Azure w wersji 2 (dyski puli magazynów DPM przenieść ze starego serwera, a następnie zaimportuj)</span><span class="sxs-lookup"><span data-stu-id="353fd-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="353fd-278">Przywróć hello DPMDB pobranych z końcem część 2</span><span class="sxs-lookup"><span data-stu-id="353fd-278">Restore hello DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="353fd-279">Dołącz hello magazynu z hello oryginalny serwer zapasowy toohello nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="353fd-279">Attach hello storage from hello original backup server toohello new server.</span></span>
8) <span data-ttu-id="353fd-280">Z hello SQL przywracania bazy danych DPMDB</span><span class="sxs-lookup"><span data-stu-id="353fd-280">From SQL Restore hello DPMDB</span></span>
9) <span data-ttu-id="353fd-281">Z wiersza polecenia administratora na nowy serwer tooMicrosoft cd kopia zapasowa Azure Zainstaluj lokalizacji i otworzyć folder bin</span><span class="sxs-lookup"><span data-stu-id="353fd-281">From admin command line on new server cd tooMicrosoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="353fd-282">Przykład ścieżki: C:\windows\system32 > cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="353fd-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="353fd-283">Kopia zapasowa tooAzure wykonaj polecenie DPMSYNC-SYNC</span><span class="sxs-lookup"><span data-stu-id="353fd-283">tooAzure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="353fd-284">Uruchom polecenie DPMSYNC-SYNC Uwaga Po dodaniu nowej puli magazynu programu DPM toohello dysków zamiast przenoszenia hello stare, następnie uruchom polecenie DPMSYNC - Reallocatereplica</span><span class="sxs-lookup"><span data-stu-id="353fd-284">Run DPMSYNC -SYNC Note If you have added NEW disks toohello DPM Storage pool instead of moving hello old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="353fd-285">Nowe polecenia cmdlet programu PowerShell w wersji 2</span><span class="sxs-lookup"><span data-stu-id="353fd-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="353fd-286">Po zainstalowaniu serwera usługi Kopia zapasowa Azure w wersji 2, dostępne są dwa nowe polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="353fd-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="353fd-287">DPMRecoveryPoint instalacji</span><span class="sxs-lookup"><span data-stu-id="353fd-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="353fd-288">Odinstalowywanie DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="353fd-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="353fd-289">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="353fd-289">Next steps</span></span>

<span data-ttu-id="353fd-290">Dowiedz się, jak tooprepare serwera lub Włącz ochronę obciążenia:</span><span class="sxs-lookup"><span data-stu-id="353fd-290">Learn how tooprepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="353fd-291">Przygotowanie serwera kopii zapasowej obciążeń</span><span class="sxs-lookup"><span data-stu-id="353fd-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="353fd-292">Użyj tooback serwera kopii zapasowej serwera VMware</span><span class="sxs-lookup"><span data-stu-id="353fd-292">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="353fd-293">Użyj tooback serwera kopii zapasowej serwera SQL</span><span class="sxs-lookup"><span data-stu-id="353fd-293">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="353fd-294">Nowoczesne magazynu kopii zapasowej za pomocą kopii zapasowej serwera</span><span class="sxs-lookup"><span data-stu-id="353fd-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

