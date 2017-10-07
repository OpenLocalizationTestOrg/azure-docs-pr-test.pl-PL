---
title: aaaAttach tooa dysku maszyny Wirtualnej Azure classic | Dokumentacja firmy Microsoft
description: "Dołącz dane dysku tooa systemu Windows maszyny wirtualnej utworzonej z hello klasycznego modelu wdrażania i zainicjować go."
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
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="d3b07-103">Dołącz dane dysku tooa systemu Windows maszyny wirtualnej utworzonej z hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="d3b07-103">Attach a data disk tooa Windows virtual machine created with hello classic deployment model</span></span>
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="d3b07-104">W tym artykule opisano sposób tworzenia tooattach nowych i istniejących dysków w z hello Classic wdrażania modelu tooa maszyny wirtualnej systemu Windows przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d3b07-104">This article shows you how tooattach new and existing disks created with hello Classic deployment model tooa Windows virtual machine using hello Azure portal.</span></span>

<span data-ttu-id="d3b07-105">Możesz również [dołączyć tooa dysku danych maszyny Wirtualnej systemu Linux w portalu Azure hello](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d3b07-105">You can also [attach a data disk tooa Linux VM in hello Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="d3b07-106">Przed dołączeniem dysku, należy przejrzeć te wskazówki:</span><span class="sxs-lookup"><span data-stu-id="d3b07-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="d3b07-107">Hello rozmiar maszyny wirtualnej hello Określa, ile można dołączać dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="d3b07-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="d3b07-108">Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3b07-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="d3b07-109">Magazyn w warstwie Premium toouse, należy serii DS lub GS-series maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d3b07-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="d3b07-110">Z tych maszyn wirtualnych służy dysków z konta magazynu zarówno Premium i standardowa.</span><span class="sxs-lookup"><span data-stu-id="d3b07-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="d3b07-111">Magazyn w warstwie Premium jest dostępna w pewnych regionach.</span><span class="sxs-lookup"><span data-stu-id="d3b07-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="d3b07-112">Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3b07-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="d3b07-113">Dla nowego dysku nie ma potrzeby toocreate jej pierwszym ponieważ Azure tworzy go po dołączeniu go.</span><span class="sxs-lookup"><span data-stu-id="d3b07-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="d3b07-114">Możesz również [dołączenie dysku danych przy użyciu programu Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d3b07-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3b07-115">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d3b07-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-hello-virtual-machine"></a><span data-ttu-id="d3b07-116">Znajdź hello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d3b07-116">Find hello virtual machine</span></span>
1. <span data-ttu-id="d3b07-117">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d3b07-117">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d3b07-118">Wybierz hello maszyny wirtualnej z wymienionych na pulpicie nawigacyjnym hello zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="d3b07-118">Select hello virtual machine from hello resource listed on hello dashboard.</span></span>
3. <span data-ttu-id="d3b07-119">W okienku po lewej stronie powitania w obszarze **ustawienia**, kliknij przycisk **dysków**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-119">In hello left pane under **Settings**, click **Disks**.</span></span>

    ![Otwórz ustawienia dysku](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="d3b07-121">Kontynuuj przez następujące instrukcje dotyczące dołączania albo [nowy dysk](#option-1-attach-a-new-disk) lub [istniejącego dysku](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="d3b07-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="d3b07-122">Opcja 1: Dołączać i zainicjuj nowego dysku</span><span class="sxs-lookup"><span data-stu-id="d3b07-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="d3b07-123">Na powitania **dysków** bloku, kliknij przycisk **Dołącz nowy**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-123">On hello **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="d3b07-124">Przejrzyj ustawienia domyślne hello, zaktualizuj odpowiednio do potrzeb, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-124">Review hello default settings, update as necessary, and then click **OK**.</span></span>

   ![Przejrzyj ustawienia dysku](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="d3b07-126">Po Azure tworzy dysk hello i dołącza go toohello maszyny wirtualnej, hello nowego dysku jest wymieniony w ustawienia dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-126">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="d3b07-127">Zainicjuj nowy dysk danych</span><span class="sxs-lookup"><span data-stu-id="d3b07-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="d3b07-128">Połącz toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d3b07-128">Connect toohello virtual machine.</span></span> <span data-ttu-id="d3b07-129">Aby uzyskać instrukcje, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3b07-129">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="d3b07-130">Po zalogowaniu się na maszynie wirtualnej toohello Otwórz **Menedżera serwera**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-130">After you log on toohello virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="d3b07-131">Wybierz w okienku po lewej stronie powitania **usług plików i magazynowania**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-131">In hello left pane, select **File and Storage Services**.</span></span>

    ![Otwórz Menedżera serwera](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="d3b07-133">Wybierz **dysków**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-133">Select **Disks**.</span></span>
4. <span data-ttu-id="d3b07-134">Witaj **dysków** sekcja zawiera informacje o dyskach hello.</span><span class="sxs-lookup"><span data-stu-id="d3b07-134">hello **Disks** section lists hello disks.</span></span> <span data-ttu-id="d3b07-135">W większości przypadków maszyny wirtualnej ma dysk 0 na partycje, dysk 1 i 2 dysku.</span><span class="sxs-lookup"><span data-stu-id="d3b07-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="d3b07-136">Dysk 0 na partycje jest hello dysk systemu operacyjnego, dysk 1 jest hello tymczasowego i dysk 2 jest dysk danych hello nowo dołączony toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d3b07-136">Disk 0 is hello operating system disk, disk 1 is hello temporary disk, and disk 2 is hello data disk newly attached toohello virtual machine.</span></span> <span data-ttu-id="d3b07-137">Hello list dysku danych hello partycji jako **nieznany**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-137">hello data disk lists hello Partition as **Unknown**.</span></span>

 <span data-ttu-id="d3b07-138">Kliknij prawym przyciskiem myszy dysk hello i wybierz **zainicjować**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-138">Right-click hello disk and select **Initialize**.</span></span>

5. <span data-ttu-id="d3b07-139">Wiesz, że wszystkie dane zostaną usunięte po zainicjowaniu hello dysku.</span><span class="sxs-lookup"><span data-stu-id="d3b07-139">You're notified that all data will be erased when hello disk is initialized.</span></span> <span data-ttu-id="d3b07-140">Kliknij przycisk **tak** tooacknowledge hello ostrzeżenie i zainicjować hello dysku.</span><span class="sxs-lookup"><span data-stu-id="d3b07-140">Click **Yes** tooacknowledge hello warning and initialize hello disk.</span></span> <span data-ttu-id="d3b07-141">Po wykonaniu tych czynności partycji hello będzie wyświetlany jako **GPT**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-141">Once complete, hello partition will be listed as **GPT**.</span></span> <span data-ttu-id="d3b07-142">Ponownie kliknij prawym przyciskiem myszy dysk hello i wybierz **nowy wolumin**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-142">Right-click hello disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="d3b07-143">Ukończ Kreatora hello przy użyciu wartości domyślnych hello.</span><span class="sxs-lookup"><span data-stu-id="d3b07-143">Complete hello wizard using hello default values.</span></span> <span data-ttu-id="d3b07-144">Po zakończeniu pracy Kreatora hello hello **woluminów** sekcji przedstawiono hello nowego woluminu.</span><span class="sxs-lookup"><span data-stu-id="d3b07-144">When hello wizard is done, hello **Volumes** section lists hello new volume.</span></span> <span data-ttu-id="d3b07-145">dysk Hello jest teraz danych toostore w trybie online i gotowe.</span><span class="sxs-lookup"><span data-stu-id="d3b07-145">hello disk is now online and ready toostore data.</span></span>

    ![Wolumin został zainicjowany pomyślnie](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="d3b07-147">Opcja 2: Dołączanie istniejącego dysku</span><span class="sxs-lookup"><span data-stu-id="d3b07-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="d3b07-148">Na powitania **dysków** bloku, kliknij przycisk **Attach istniejących**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-148">On hello **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="d3b07-149">W obszarze **dołączyć istniejącego dysku**, kliknij przycisk **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Dołączanie istniejącego dysku](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="d3b07-151">W obszarze **kont magazynu**, wybierz konto hello i kontener, który zawiera plik VHD hello.</span><span class="sxs-lookup"><span data-stu-id="d3b07-151">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>

   ![Znajdź lokalizację wirtualnego dysku twardego](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="d3b07-153">Wybierz plik VHD hello.</span><span class="sxs-lookup"><span data-stu-id="d3b07-153">Select hello .vhd file.</span></span>
5. <span data-ttu-id="d3b07-154">W obszarze **dołączyć istniejącego dysku**, po prostu wybrany plik hello jest wyświetlana w obszarze **pliku VHD**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-154">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="d3b07-155">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-155">Click **OK**.</span></span>
6. <span data-ttu-id="d3b07-156">Po Azure dołącza hello maszyny wirtualnej toohello dysku, znajduje się w ustawieniach dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="d3b07-156">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="d3b07-157">PRZYCINANIE za pomocą magazynu w warstwie standardowa</span><span class="sxs-lookup"><span data-stu-id="d3b07-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="d3b07-158">Jeśli używasz standardowego magazynu (HDD), należy włączyć PRZYCINANIE.</span><span class="sxs-lookup"><span data-stu-id="d3b07-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="d3b07-159">PRZYCINANIE odrzuca nieużywanych bloków na dysku hello tak rozliczenie jest przeprowadzane tylko dla magazynu, który faktycznie używasz.</span><span class="sxs-lookup"><span data-stu-id="d3b07-159">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="d3b07-160">Korzystając z operacją PRZYCINANIA zapisać kosztów, w tym nieużywanych bloków wynikających z usunięcie dużych plików.</span><span class="sxs-lookup"><span data-stu-id="d3b07-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="d3b07-161">Możesz uruchomić to polecenie toocheck hello PRZYCINANIA ustawienie.</span><span class="sxs-lookup"><span data-stu-id="d3b07-161">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="d3b07-162">Otwórz wiersz polecenia na Twojej maszyny Wirtualnej systemu Windows i wpisz:</span><span class="sxs-lookup"><span data-stu-id="d3b07-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="d3b07-163">Jeśli polecenie hello zwraca wartość 0, PRZYCINANIE włączono poprawnie.</span><span class="sxs-lookup"><span data-stu-id="d3b07-163">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="d3b07-164">Jeśli zmienna zwraca 1, uruchom następujące polecenie tooenable PRZYCINANIE hello:</span><span class="sxs-lookup"><span data-stu-id="d3b07-164">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="d3b07-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d3b07-165">Next steps</span></span>
<span data-ttu-id="d3b07-166">Jeśli aplikacja wymaga toouse hello D: dysku toostore danych, możesz [zmienić hello litera dysku tymczasowego Windows hello](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="d3b07-166">If your application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d3b07-167">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d3b07-167">Additional resources</span></span>
[<span data-ttu-id="d3b07-168">O dyskach i wirtualne dyski twarde dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="d3b07-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
