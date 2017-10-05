---
title: "Dołączanie dysku do klasycznej maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Dołączenie dysku danych do maszyny wirtualnej systemu Windows utworzone z klasycznym modelu wdrażania i zainicjować go."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: 087d5cda354f6e1780bddd3725859444177abd16
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="6926e-103">Dołączanie dysku danych do maszyny wirtualnej systemu Windows przy użyciu klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="6926e-103">Attach a data disk to a Windows virtual machine created with the classic deployment model</span></span>
<!--
Refernce article:
    If you want to use the new portal, see [How to attach a data disk to a Windows VM in the Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="6926e-104">W tym artykule pokazano, jak dołączyć dyski nowych i istniejących utworzone za pomocą klasycznego modelu wdrażania z maszyną wirtualną z systemem Windows przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6926e-104">This article shows you how to attach new and existing disks created with the Classic deployment model to a Windows virtual machine using the Azure portal.</span></span>

<span data-ttu-id="6926e-105">Możesz również [dołączenie dysku danych do maszyny Wirtualnej systemu Linux, w portalu Azure](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6926e-105">You can also [attach a data disk to a Linux VM in the Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="6926e-106">Przed dołączeniem dysku, należy przejrzeć te wskazówki:</span><span class="sxs-lookup"><span data-stu-id="6926e-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="6926e-107">Rozmiar maszyny wirtualnej Określa, ile można dołączać dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="6926e-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="6926e-108">Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6926e-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="6926e-109">Aby użyć magazyn w warstwie Premium, należy serii DS lub GS-series maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6926e-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="6926e-110">Z tych maszyn wirtualnych służy dysków z konta magazynu zarówno Premium i standardowa.</span><span class="sxs-lookup"><span data-stu-id="6926e-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="6926e-111">Magazyn w warstwie Premium jest dostępna w pewnych regionach.</span><span class="sxs-lookup"><span data-stu-id="6926e-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="6926e-112">Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6926e-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="6926e-113">Dla nowego dysku nie trzeba go najpierw utworzyć ponieważ Azure tworzy go po dołączeniu go.</span><span class="sxs-lookup"><span data-stu-id="6926e-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="6926e-114">Możesz również [dołączenie dysku danych przy użyciu programu Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6926e-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6926e-115">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6926e-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-the-virtual-machine"></a><span data-ttu-id="6926e-116">Znaleźć maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6926e-116">Find the virtual machine</span></span>
1. <span data-ttu-id="6926e-117">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6926e-117">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6926e-118">Wybierz maszynę wirtualną z zasobów wymienionych na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="6926e-118">Select the virtual machine from the resource listed on the dashboard.</span></span>
3. <span data-ttu-id="6926e-119">W lewym okienku w obszarze **ustawienia**, kliknij przycisk **dysków**.</span><span class="sxs-lookup"><span data-stu-id="6926e-119">In the left pane under **Settings**, click **Disks**.</span></span>

    ![Otwórz ustawienia dysku](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="6926e-121">Kontynuuj przez następujące instrukcje dotyczące dołączania albo [nowy dysk](#option-1-attach-a-new-disk) lub [istniejącego dysku](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="6926e-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="6926e-122">Opcja 1: Dołączać i zainicjuj nowego dysku</span><span class="sxs-lookup"><span data-stu-id="6926e-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="6926e-123">Na **dysków** bloku, kliknij przycisk **Dołącz nowy**.</span><span class="sxs-lookup"><span data-stu-id="6926e-123">On the **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="6926e-124">Przejrzyj ustawienia domyślne, należy zaktualizować odpowiednio do potrzeb, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="6926e-124">Review the default settings, update as necessary, and then click **OK**.</span></span>

   ![Przejrzyj ustawienia dysku](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="6926e-126">Po Azure utworzy dysk i dołącza go do maszyny wirtualnej, nowy dysk ma na liście ustawień dysku maszyny wirtualnej w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="6926e-126">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="6926e-127">Zainicjuj nowy dysk danych</span><span class="sxs-lookup"><span data-stu-id="6926e-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="6926e-128">Połączenie z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="6926e-128">Connect to the virtual machine.</span></span> <span data-ttu-id="6926e-129">Aby uzyskać instrukcje, zobacz [jak połączenia i zaloguj się do maszyny wirtualnej platformy Azure systemem Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6926e-129">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="6926e-130">Po zalogowaniu się do maszyny wirtualnej, należy otworzyć **Menedżera serwera**.</span><span class="sxs-lookup"><span data-stu-id="6926e-130">After you log on to the virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="6926e-131">W okienku po lewej stronie wybierz **usług plików i magazynowania**.</span><span class="sxs-lookup"><span data-stu-id="6926e-131">In the left pane, select **File and Storage Services**.</span></span>

    ![Otwórz Menedżera serwera](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="6926e-133">Wybierz **dysków**.</span><span class="sxs-lookup"><span data-stu-id="6926e-133">Select **Disks**.</span></span>
4. <span data-ttu-id="6926e-134">**Dysków** sekcji znajduje się lista dysków.</span><span class="sxs-lookup"><span data-stu-id="6926e-134">The **Disks** section lists the disks.</span></span> <span data-ttu-id="6926e-135">W większości przypadków maszyny wirtualnej ma dysk 0 na partycje, dysk 1 i 2 dysku.</span><span class="sxs-lookup"><span data-stu-id="6926e-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="6926e-136">Dysk 0 na partycje jest dysk systemu operacyjnego, dysk 1 jest tymczasowy dysku i dysk 2 jest dyskiem danych nowo dołączony do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6926e-136">Disk 0 is the operating system disk, disk 1 is the temporary disk, and disk 2 is the data disk newly attached to the virtual machine.</span></span> <span data-ttu-id="6926e-137">Dysk z danymi wyświetla partycję jako **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="6926e-137">The data disk lists the Partition as **Unknown**.</span></span>

 <span data-ttu-id="6926e-138">Kliknij prawym przyciskiem myszy dysk, a następnie wybierz **zainicjować**.</span><span class="sxs-lookup"><span data-stu-id="6926e-138">Right-click the disk and select **Initialize**.</span></span>

5. <span data-ttu-id="6926e-139">Wiesz, że wszystkie dane zostaną wymazane, gdy dysk jest zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="6926e-139">You're notified that all data will be erased when the disk is initialized.</span></span> <span data-ttu-id="6926e-140">Kliknij przycisk **tak** potwierdzić ostrzeżenia i Zainicjuj dysk.</span><span class="sxs-lookup"><span data-stu-id="6926e-140">Click **Yes** to acknowledge the warning and initialize the disk.</span></span> <span data-ttu-id="6926e-141">Po wykonaniu tych czynności partycji będzie wyświetlany jako **GPT**.</span><span class="sxs-lookup"><span data-stu-id="6926e-141">Once complete, the partition will be listed as **GPT**.</span></span> <span data-ttu-id="6926e-142">Ponownie kliknij prawym przyciskiem myszy dysk, a następnie wybierz **nowy wolumin**.</span><span class="sxs-lookup"><span data-stu-id="6926e-142">Right-click the disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="6926e-143">Ukończ pracę kreatora, przy użyciu wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="6926e-143">Complete the wizard using the default values.</span></span> <span data-ttu-id="6926e-144">Po zakończeniu pracy kreatora **woluminów** sekcja zawiera informacje o nowy wolumin.</span><span class="sxs-lookup"><span data-stu-id="6926e-144">When the wizard is done, the **Volumes** section lists the new volume.</span></span> <span data-ttu-id="6926e-145">Dysk jest teraz w trybie online i jest gotowy do przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="6926e-145">The disk is now online and ready to store data.</span></span>

    ![Wolumin został zainicjowany pomyślnie](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="6926e-147">Opcja 2: Dołączanie istniejącego dysku</span><span class="sxs-lookup"><span data-stu-id="6926e-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="6926e-148">Na **dysków** bloku, kliknij przycisk **Attach istniejących**.</span><span class="sxs-lookup"><span data-stu-id="6926e-148">On the **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="6926e-149">W obszarze **dołączyć istniejącego dysku**, kliknij przycisk **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="6926e-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Dołączanie istniejącego dysku](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="6926e-151">W obszarze **kont magazynu**, wybierz konto i kontener, który zawiera plik VHD.</span><span class="sxs-lookup"><span data-stu-id="6926e-151">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>

   ![Znajdź lokalizację wirtualnego dysku twardego](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="6926e-153">Wybierz plik VHD.</span><span class="sxs-lookup"><span data-stu-id="6926e-153">Select the .vhd file.</span></span>
5. <span data-ttu-id="6926e-154">W obszarze **dołączyć istniejącego dysku**, po prostu wybrany plik jest wyświetlana w obszarze **pliku VHD**.</span><span class="sxs-lookup"><span data-stu-id="6926e-154">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="6926e-155">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6926e-155">Click **OK**.</span></span>
6. <span data-ttu-id="6926e-156">Po Azure dołącza dysk do maszyny wirtualnej, jest wymienione w ustawieniach dysku maszyny wirtualnej w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="6926e-156">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="6926e-157">PRZYCINANIE za pomocą magazynu w warstwie standardowa</span><span class="sxs-lookup"><span data-stu-id="6926e-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="6926e-158">Jeśli używasz standardowego magazynu (HDD), należy włączyć PRZYCINANIE.</span><span class="sxs-lookup"><span data-stu-id="6926e-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="6926e-159">PRZYCINANIE odrzuca nieużywanych bloków na dysku dzięki rozliczenie jest przeprowadzane tylko dla magazynu, który faktycznie używasz.</span><span class="sxs-lookup"><span data-stu-id="6926e-159">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="6926e-160">Korzystając z operacją PRZYCINANIA zapisać kosztów, w tym nieużywanych bloków wynikających z usunięcie dużych plików.</span><span class="sxs-lookup"><span data-stu-id="6926e-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="6926e-161">Można uruchomić tego polecenia, aby sprawdzić ustawienie PRZYCINANIA.</span><span class="sxs-lookup"><span data-stu-id="6926e-161">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="6926e-162">Otwórz wiersz polecenia na Twojej maszyny Wirtualnej systemu Windows i wpisz:</span><span class="sxs-lookup"><span data-stu-id="6926e-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="6926e-163">Jeśli polecenie zwróci wartość 0, PRZYCINANIE jest prawidłowo włączona.</span><span class="sxs-lookup"><span data-stu-id="6926e-163">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="6926e-164">Jeśli zmienna zwraca 1, uruchom następujące polecenie, aby umożliwić PRZYCINANIE:</span><span class="sxs-lookup"><span data-stu-id="6926e-164">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="6926e-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6926e-165">Next steps</span></span>
<span data-ttu-id="6926e-166">Jeśli aplikacja musi używać D: dysków do przechowywania danych, możesz [zmienić literę dysku tymczasowym systemu Windows](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="6926e-166">If your application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6926e-167">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6926e-167">Additional resources</span></span>
[<span data-ttu-id="6926e-168">O dyskach i wirtualne dyski twarde dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="6926e-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
