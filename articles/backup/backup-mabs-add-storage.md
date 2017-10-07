---
title: "aaaUse nowoczesnych magazynu kopii zapasowej z serwera usługi Kopia zapasowa Azure w wersji 2 | Dokumentacja firmy Microsoft"
description: "Informacje o nowych funkcjach hello v2 serwer kopii zapasowej Azure. W tym artykule opisano sposób tooupgrade instalacją serwera kopii zapasowej."
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
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a><span data-ttu-id="c88ea-104">Dodaj tooAzure magazynu kopii zapasowej serwera v2</span><span class="sxs-lookup"><span data-stu-id="c88ea-104">Add storage tooAzure Backup Server v2</span></span>

<span data-ttu-id="c88ea-105">Azure v2 Utwórz kopię zapasową serwera jest dostarczany z System Center 2016 ochrony Menedżera Modern kopii zapasowej pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="c88ea-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="c88ea-106">Nowoczesne magazynu kopii zapasowej oferuje oszczędności pojemności magazynu 50 procent kopii zapasowych, które są trzy razy szybszych i bardziej wydajnych magazynu.</span><span class="sxs-lookup"><span data-stu-id="c88ea-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="c88ea-107">Zapewnia także magazynu obsługującej obciążenie.</span><span class="sxs-lookup"><span data-stu-id="c88ea-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="c88ea-108">toouse nowoczesnych magazynu kopii zapasowej, należy uruchomić v2 Utwórz kopię zapasową serwera w systemie Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="c88ea-108">toouse Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="c88ea-109">Po uruchomieniu v2 Utwórz kopię zapasową serwera we wcześniejszej wersji systemu Windows Server, serwer kopii zapasowej Azure nie może korzystać z nowoczesnych magazynu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c88ea-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="c88ea-110">Zamiast tego chroni ona obciążenia, jak w przypadku v1 Utwórz kopię zapasową serwera.</span><span class="sxs-lookup"><span data-stu-id="c88ea-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="c88ea-111">Aby uzyskać więcej informacji, zobacz wersji kopii zapasowej serwera hello [macierzy ochrony](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="c88ea-111">For more information, see hello Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="c88ea-112">Woluminy w kopii zapasowej serwera v2</span><span class="sxs-lookup"><span data-stu-id="c88ea-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="c88ea-113">Kopia zapasowa v2 Server akceptuje woluminów magazynu.</span><span class="sxs-lookup"><span data-stu-id="c88ea-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="c88ea-114">Podczas dodawania woluminu, Utwórz kopię zapasową serwera formatuje hello tooResilient woluminu systemu plików ReFS, co wymaga nowoczesnej magazynu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c88ea-114">When you add a volume, Backup Server formats hello volume tooResilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="c88ea-115">tooadd woluminu, a tooexpand go później, jeśli zajdzie potrzeba, zaleca się używanie tego przepływu pracy:</span><span class="sxs-lookup"><span data-stu-id="c88ea-115">tooadd a volume, and tooexpand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="c88ea-116">Skonfiguruj serwer zapasowy v2 na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c88ea-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="c88ea-117">Utwórz wolumin na dysku wirtualnego w puli magazynów:</span><span class="sxs-lookup"><span data-stu-id="c88ea-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="c88ea-118">Dodaj pulę magazynu tooa dysk i Utwórz dysk wirtualny z układ prosty.</span><span class="sxs-lookup"><span data-stu-id="c88ea-118">Add a disk tooa storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="c88ea-119">Dodaj dodatkowe dyski i rozszerzyć hello dysku wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="c88ea-119">Add any additional disks, and extend hello virtual disk.</span></span>
    3.  <span data-ttu-id="c88ea-120">Utworzyć woluminy na powitania dysku wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="c88ea-120">Create volumes on hello virtual disk.</span></span>
3.  <span data-ttu-id="c88ea-121">Dodaj tooBackup woluminów powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="c88ea-121">Add hello volumes tooBackup Server.</span></span>
4.  <span data-ttu-id="c88ea-122">Konfigurowanie magazynu obsługującej obciążenie.</span><span class="sxs-lookup"><span data-stu-id="c88ea-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="c88ea-123">Tworzenie woluminu dla nowoczesnych magazynu kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="c88ea-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="c88ea-124">Użycie v2 Utwórz kopię zapasową serwera z woluminami jako magazynu danych na dysku może pomóc zachować kontrolę nad magazynu.</span><span class="sxs-lookup"><span data-stu-id="c88ea-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="c88ea-125">Wolumin może być także jeden dysk.</span><span class="sxs-lookup"><span data-stu-id="c88ea-125">A volume can be a single disk.</span></span> <span data-ttu-id="c88ea-126">Jednak tooextend magazynu w hello przyszłych, utworzyć wolumin poza dysk utworzony przy użyciu funkcji miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="c88ea-126">However, if you want tooextend storage in hello future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="c88ea-127">Może to ułatwić, jeśli chcesz tooexpand hello wolumin magazynu kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c88ea-127">This can help if you want tooexpand hello volume for backup storage.</span></span> <span data-ttu-id="c88ea-128">Ta sekcja zawiera najlepsze rozwiązania dotyczące tworzenia woluminu z tej instalacji.</span><span class="sxs-lookup"><span data-stu-id="c88ea-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="c88ea-129">W Menedżerze serwera wybierz **usług plików i magazynowania** > **woluminów** > **pule magazynu**.</span><span class="sxs-lookup"><span data-stu-id="c88ea-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="c88ea-130">W obszarze **dysków fizycznych**, wybierz pozycję **nowa pula magazynu**.</span><span class="sxs-lookup"><span data-stu-id="c88ea-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Tworzenie nowej puli magazynu](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="c88ea-132">W hello **zadania** listy rozwijanej wybierz pozycję **nowego dysku wirtualnego**.</span><span class="sxs-lookup"><span data-stu-id="c88ea-132">In hello **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Dodaj dysk wirtualny](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="c88ea-134">Wybierz pulę magazynu hello, a następnie wybierz **Dodaj dysk fizyczny**.</span><span class="sxs-lookup"><span data-stu-id="c88ea-134">Select hello storage pool, and then select **Add Physical Disk**.</span></span>

    ![Dodaj dysk fizyczny](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="c88ea-136">Wybierz dysk fizyczny hello, a następnie wybierz **Rozszerz dysk wirtualny**.</span><span class="sxs-lookup"><span data-stu-id="c88ea-136">Select hello physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Rozszerzanie dysku wirtualnego hello](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="c88ea-138">Wybierz hello dysku wirtualnego, a następnie wybierz **nowy wolumin**.</span><span class="sxs-lookup"><span data-stu-id="c88ea-138">Select hello virtual disk, and then select **New Volume**.</span></span>

    ![Utwórz nowy wolumin](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="c88ea-140">W hello **wybierz powitania serwera i dysku** okno dialogowe, wybierz powitania serwera i hello nowego dysku.</span><span class="sxs-lookup"><span data-stu-id="c88ea-140">In hello **Select hello server and disk** dialog, select hello server and hello new disk.</span></span> <span data-ttu-id="c88ea-141">Następnie wybierz opcję **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c88ea-141">Then, select **Next**.</span></span>

    ![Wybierz powitania serwera i dysku](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a><span data-ttu-id="c88ea-143">Dodawanie magazynu dyskowego serwera tooBackup woluminów</span><span class="sxs-lookup"><span data-stu-id="c88ea-143">Add volumes tooBackup Server disk storage</span></span>

<span data-ttu-id="c88ea-144">tooadd tooBackup woluminu serwera, w hello **zarządzania** okienku ponownego skanowania magazynu hello, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c88ea-144">tooadd a volume tooBackup Server, in hello **Management** pane, rescan hello storage, and then select **Add**.</span></span> <span data-ttu-id="c88ea-145">Zostanie wyświetlona lista wszystkich hello woluminów dostępnych toobe dodane do magazynu kopii zapasowej serwera.</span><span class="sxs-lookup"><span data-stu-id="c88ea-145">A list of all hello volumes available toobe added for Backup Server Storage appears.</span></span> <span data-ttu-id="c88ea-146">Po dodaniu toohello Lista wybranych woluminów dostępnych woluminów, można przekazać toohelp przyjaznej nazwy, zarządzać nimi.</span><span class="sxs-lookup"><span data-stu-id="c88ea-146">After available volumes are added toohello list of selected volumes, you can give them a friendly name toohelp you manage them.</span></span> <span data-ttu-id="c88ea-147">tooformat tooReFS tych woluminów, Utwórz kopię zapasową serwera można użyć hello zalet nowoczesnych magazynu kopii zapasowej, wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="c88ea-147">tooformat these volumes tooReFS so Backup Server can use hello benefits of Modern Backup Storage, select **OK**.</span></span>

![Dodaj dostępne woluminy](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="c88ea-149">Konfigurowanie magazynu obsługującej obciążenie</span><span class="sxs-lookup"><span data-stu-id="c88ea-149">Set up workload-aware storage</span></span>

<span data-ttu-id="c88ea-150">Z magazynu obsługujących obciążenie można wybrać hello woluminami preferencyjnie przechowywania określonych rodzajów obciążeń.</span><span class="sxs-lookup"><span data-stu-id="c88ea-150">With workload-aware storage, you can select hello volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="c88ea-151">Na przykład można ustawić kosztowne woluminów, które obsługują dużej liczby operacji wejścia/wyjścia na drugi (IOPS) toostore tylko hello obciążeń, które wymagają częstego, dużej liczby kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="c88ea-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only hello workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="c88ea-152">Przykładem jest program SQL Server z dzienników transakcji.</span><span class="sxs-lookup"><span data-stu-id="c88ea-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="c88ea-153">Inne obciążenia, których kopii zapasowej rzadziej, takich jak maszyny wirtualne, utworzeniem kopii zapasowej woluminów toolow kosztów.</span><span class="sxs-lookup"><span data-stu-id="c88ea-153">Other workloads that are backed up less frequently, like VMs, can be backed up toolow-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="c88ea-154">DPMDiskStorage aktualizacji</span><span class="sxs-lookup"><span data-stu-id="c88ea-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="c88ea-155">Magazyn obsługujący obciążenia można skonfigurować za pomocą polecenia cmdlet programu PowerShell hello Update-DPMDiskStorage, która aktualizuje właściwości hello woluminu w puli magazynu hello na serwerze programu Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="c88ea-155">You can set up workload-aware storage by using hello PowerShell cmdlet Update-DPMDiskStorage, which updates hello properties of a volume in hello storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="c88ea-156">Składnia:</span><span class="sxs-lookup"><span data-stu-id="c88ea-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="c88ea-157">Witaj Poniższy zrzut ekranu przedstawia polecenie cmdlet Update-DPMDiskStorage hello w oknie programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c88ea-157">hello following screenshot shows hello Update-DPMDiskStorage cmdlet in hello PowerShell window.</span></span>

![polecenie Update-DPMDiskStorage w oknie programu PowerShell hello Hello](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="c88ea-159">zmiany Hello przy użyciu programu PowerShell są odzwierciedlane w hello konsoli administratora serwera kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="c88ea-159">hello changes you make by using PowerShell are reflected in hello Backup Server Administrator Console.</span></span>

![Dyski i woluminy w hello konsoli administratora](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="c88ea-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c88ea-161">Next steps</span></span>
<span data-ttu-id="c88ea-162">Po zainstalowaniu serwera kopii zapasowej, Dowiedz się jak tooprepare serwera, lub Włącz ochronę obciążeń.</span><span class="sxs-lookup"><span data-stu-id="c88ea-162">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="c88ea-163">Przygotowanie serwera kopii zapasowej obciążeń</span><span class="sxs-lookup"><span data-stu-id="c88ea-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="c88ea-164">Użyj tooback serwera kopii zapasowej serwera VMware</span><span class="sxs-lookup"><span data-stu-id="c88ea-164">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="c88ea-165">Użyj tooback serwera kopii zapasowej serwera SQL</span><span class="sxs-lookup"><span data-stu-id="c88ea-165">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)

