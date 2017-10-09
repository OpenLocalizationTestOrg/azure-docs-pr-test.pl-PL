---
title: "aaaAttach niezarządzanych danych dysku tooa maszyny Wirtualnej systemu Windows - Azure | Dokumentacja firmy Microsoft"
description: "Jak tooattach niezarządzanych danych nowego lub istniejącego dysku tooa maszyny Wirtualnej systemu Windows w hello przy użyciu portalu Azure hello modelu wdrażania usługi Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="10916-103">Jak tooattach niezarządzanych danych na dysku tooa maszyny Wirtualnej systemu Windows w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="10916-103">How tooattach an unmanaged data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="10916-104">W tym artykule opisano sposób niezarządzanych tooattach istniejących i nowych dysków tooWindows maszyn wirtualnych za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="10916-104">This article shows you how tooattach both new and existing unmanaged disks tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="10916-105">Możesz również [dołączenie dysku danych przy użyciu programu PowerShell](./attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="10916-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="10916-106">Zanim to zrobisz, przejrzyj następujące wskazówki:</span><span class="sxs-lookup"><span data-stu-id="10916-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="10916-107">Hello rozmiar maszyny wirtualnej hello Określa, ile można dołączać dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="10916-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="10916-108">Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="10916-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="10916-109">Magazyn w warstwie Premium toouse, należy serii DS lub GS-series maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="10916-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="10916-110">Z tych maszyn wirtualnych służy dysków z konta magazynu zarówno Premium i standardowa.</span><span class="sxs-lookup"><span data-stu-id="10916-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="10916-111">Magazyn w warstwie Premium jest dostępna w pewnych regionach.</span><span class="sxs-lookup"><span data-stu-id="10916-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="10916-112">Aby uzyskać więcej informacji, zobacz [magazyn w warstwie Premium: magazyn o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10916-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="10916-113">Dla nowego dysku nie ma potrzeby toocreate jej pierwszym ponieważ Azure tworzy go po dołączeniu go.</span><span class="sxs-lookup"><span data-stu-id="10916-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="10916-114">Możesz również [dołączenie dysku danych przy użyciu programu Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="10916-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="10916-115">Znajdź hello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="10916-115">Find hello virtual machine</span></span>
1. <span data-ttu-id="10916-116">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="10916-116">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="10916-117">W menu powitania po lewej stronie powitania kliknij **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="10916-117">In hello menu on hello left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="10916-118">Wybierz maszynę wirtualną hello z listy hello.</span><span class="sxs-lookup"><span data-stu-id="10916-118">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="10916-119">W bloku maszyny wirtualnej powitania kliknij **dysków**.</span><span class="sxs-lookup"><span data-stu-id="10916-119">In hello Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="10916-120">Kontynuuj przez następujące instrukcje dotyczące dołączania albo [nowy dysk](#option-1-attach-a-new-disk) lub [istniejącego dysku](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="10916-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="10916-121">Opcja 1: Dołączać i zainicjuj nowego dysku</span><span class="sxs-lookup"><span data-stu-id="10916-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="10916-122">Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="10916-122">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="10916-123">W hello **dysków zarządzanych w Attach** bloku, wpisz nazwę dysku hello w **nazwa** , a następnie wybierz **New (pusty dysk)** w **typ źródła**.</span><span class="sxs-lookup"><span data-stu-id="10916-123">In hello **Attach managed disk** blade, type a name for hello disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="10916-124">W obszarze **kontenera magazynu**, kliknij przycisk hello **Przeglądaj** przycisk i Przeglądaj toohello konta magazynu i kontener, w którym chcesz hello nowego wirtualnego dysku twardego toobe przechowywane i następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="10916-124">Under **Storage container**, click hello **Browse** button and browse toohello storage account and container where you would like hello new VHD toobe stored and then click **Select**.</span></span> 
  
   ![Przejrzyj ustawienia dysku](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="10916-126">Po wykonaniu hello ustawienia hello dysku danych, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="10916-126">When you are done with hello settings for hello data disk, click **OK**.</span></span>
4. <span data-ttu-id="10916-127">Po powrocie do hello **dysków** bloku, kliknij przycisk **zapisać** konfiguracji maszyny Wirtualnej toohello tooadd hello dysku.</span><span class="sxs-lookup"><span data-stu-id="10916-127">Back in hello **Disks** blade, click **Save** tooadd hello disk toohello VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="10916-128">Zainicjuj nowy dysk danych</span><span class="sxs-lookup"><span data-stu-id="10916-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="10916-129">Połącz toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="10916-129">Connect toohello virtual machine.</span></span> <span data-ttu-id="10916-130">Aby uzyskać instrukcje, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10916-130">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="10916-131">Kliknij przycisk hello **Start** menu wewnątrz hello maszyny Wirtualnej i typ **diskmgmt.msc** i trafień **Enter**.</span><span class="sxs-lookup"><span data-stu-id="10916-131">Click hello **Start** menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="10916-132">Spowoduje to uruchomienie przystawki Zarządzanie dyskami hello.</span><span class="sxs-lookup"><span data-stu-id="10916-132">This starts hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="10916-133">Zarządzanie dyskami uznaje, że znajduje się dysk nowy, niezainicjowanej hello Inicjowanie dysku oknie wyskakującym zostanie.</span><span class="sxs-lookup"><span data-stu-id="10916-133">Disk Management recognizes that you have a new, uninitialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="10916-134">Upewnij się, że wybrano hello nowy dysk i kliknij przycisk **OK** tooinitialize go.</span><span class="sxs-lookup"><span data-stu-id="10916-134">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="10916-135">Witaj nowy dysk jest teraz wyświetlany jako **nieprzydzielonego**.</span><span class="sxs-lookup"><span data-stu-id="10916-135">hello new disk now appears as **unallocated**.</span></span> <span data-ttu-id="10916-136">Kliknij prawym przyciskiem myszy na powitania dysku i wybierz **nowy wolumin prosty**.</span><span class="sxs-lookup"><span data-stu-id="10916-136">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="10916-137">Witaj **Kreatorze nowych woluminów prostych** uruchamia.</span><span class="sxs-lookup"><span data-stu-id="10916-137">hello **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="10916-138">Przejdź przez kreatora hello zapewniają, że wszystkie ustawienia domyślne hello, po zakończeniu wybierz **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="10916-138">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="10916-139">Zamknij program Zarządzanie dyskami.</span><span class="sxs-lookup"><span data-stu-id="10916-139">Close Disk Management.</span></span>
7. <span data-ttu-id="10916-140">Pobierz okno podręczne, które należy tooformat hello nowy dysk przed jego użyciem.</span><span class="sxs-lookup"><span data-stu-id="10916-140">You get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="10916-141">Kliknij przycisk **Format dysku**.</span><span class="sxs-lookup"><span data-stu-id="10916-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="10916-142">W hello **Format nowy dysk** okna dialogowego, sprawdź hello ustawienia, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="10916-142">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="10916-143">Kliknij pozycję wyświetlone ostrzeżenie, że formatowanie hello dysków na partycje powoduje usunięcie wszystkich danych hello **OK**.</span><span class="sxs-lookup"><span data-stu-id="10916-143">You get a warning that formatting hello disks erases all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="10916-144">Po zakończeniu format powitania kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="10916-144">When hello format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="10916-145">Opcja 2: Dołączanie istniejącego dysku</span><span class="sxs-lookup"><span data-stu-id="10916-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="10916-146">Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="10916-146">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="10916-147">Na powitania **dysku niezarządzane Attach** bloku, w **typ źródła** wybierz **blob istniejące**.</span><span class="sxs-lookup"><span data-stu-id="10916-147">On hello **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![Przejrzyj ustawienia dysku](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="10916-149">Kliknij przycisk **Przeglądaj** toonavigate toohello konto magazynu i kontener, w którym hello istniejącego dysku VHD znajduje się.</span><span class="sxs-lookup"><span data-stu-id="10916-149">Click **Browse** toonavigate toohello storage account and container where hello existing VHD is located.</span></span> <span data-ttu-id="10916-150">Kliknij i hello wirtualnego dysku twardego, a następnie kliknij **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="10916-150">Click and hello VHD and then click **Select**.</span></span>
4. <span data-ttu-id="10916-151">Kliknij przycisk **OK** w hello **dysku niezarządzane Attach** bloku.</span><span class="sxs-lookup"><span data-stu-id="10916-151">Click **OK** in hello **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="10916-152">W hello **dysków** bloku, kliknij przycisk **zapisać** tooadd hello dysku toohello Konfiguracja hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="10916-152">In hello **Disks** blade, click **Save** tooadd hello disk toohello configuration for hello VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="10916-153">PRZYCINANIE za pomocą magazynu w warstwie standardowa</span><span class="sxs-lookup"><span data-stu-id="10916-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="10916-154">Jeśli używasz standardowego magazynu (HDD), należy włączyć PRZYCINANIE.</span><span class="sxs-lookup"><span data-stu-id="10916-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="10916-155">PRZYCINANIE odrzuca nieużywanych bloków na dysku hello tak rozliczenie jest przeprowadzane tylko dla magazynu, który faktycznie używasz.</span><span class="sxs-lookup"><span data-stu-id="10916-155">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="10916-156">Można to zapisanie kosztów, jeśli Tworzenie dużych plików, a następnie usuń je.</span><span class="sxs-lookup"><span data-stu-id="10916-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="10916-157">Możesz uruchomić to polecenie toocheck hello PRZYCINANIA ustawienie.</span><span class="sxs-lookup"><span data-stu-id="10916-157">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="10916-158">Otwórz wiersz polecenia na Twojej maszyny Wirtualnej systemu Windows i wpisz:</span><span class="sxs-lookup"><span data-stu-id="10916-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="10916-159">Jeśli polecenie hello zwraca wartość 0, PRZYCINANIE włączono poprawnie.</span><span class="sxs-lookup"><span data-stu-id="10916-159">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="10916-160">Jeśli zmienna zwraca 1, uruchom następujące polecenie tooenable PRZYCINANIE hello:</span><span class="sxs-lookup"><span data-stu-id="10916-160">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="10916-161">Po usunięciu danych z dysku, upewnij się, że hello PRZYCINANIA operacji opróżniania poprawnie, uruchamiając defragmentowania z operacją PRZYCINANIA:</span><span class="sxs-lookup"><span data-stu-id="10916-161">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="10916-162">Ponadto upewnij się, że cały wolumin hello jest ograniczona przez formatowania woluminu hello.</span><span class="sxs-lookup"><span data-stu-id="10916-162">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="10916-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10916-163">Next steps</span></span>
<span data-ttu-id="10916-164">Jeśli użytkownik aplikacji musi toouse hello D: dysku toostore danych, możesz [zmienić hello litera dysku tymczasowego Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="10916-164">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

