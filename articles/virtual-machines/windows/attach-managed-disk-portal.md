---
title: "aaaAttach danych zarządzanych dysku tooa maszyny Wirtualnej systemu Windows - Azure | Dokumentacja firmy Microsoft"
description: "Sposób tooattach nowe zarządzania tooa dysku danych maszyny Wirtualnej systemu Windows w hello przy użyciu portalu Azure hello modelu wdrażania usługi Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="1bc21-103">Jak tooattach danych zarządzanych dysku tooa maszyny Wirtualnej systemu Windows w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1bc21-103">How tooattach a managed data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="1bc21-104">W tym artykule opisano, jak tooattach nowych danych zarządzanych dysku tooWindows maszyn wirtualnych za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc21-104">This article shows you how tooattach a new managed data disk tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="1bc21-105">Zanim to zrobisz, przejrzyj następujące wskazówki:</span><span class="sxs-lookup"><span data-stu-id="1bc21-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="1bc21-106">Hello rozmiar maszyny wirtualnej hello Określa, ile można dołączać dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="1bc21-106">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="1bc21-107">Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="1bc21-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="1bc21-108">Dla nowego dysku nie ma potrzeby toocreate jej pierwszym ponieważ Azure tworzy go po dołączeniu go.</span><span class="sxs-lookup"><span data-stu-id="1bc21-108">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="1bc21-109">Możesz również [dołączenie dysku danych przy użyciu programu Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1bc21-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="1bc21-110">Dodaj dysk danych</span><span class="sxs-lookup"><span data-stu-id="1bc21-110">Add a data disk</span></span>
1. <span data-ttu-id="1bc21-111">W menu powitania po lewej stronie powitania kliknij **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-111">In hello menu on hello left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="1bc21-112">Wybierz maszynę wirtualną hello z listy hello.</span><span class="sxs-lookup"><span data-stu-id="1bc21-112">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="1bc21-113">W bloku maszyny wirtualnej hello, kliknij polecenie **dysków**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-113">On hello virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="1bc21-114">Na powitania **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-114">On hello **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="1bc21-115">Z listy rozwijanej dla nowego dysku hello hello, wybierz **utworzyć pusty**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-115">In hello drop-down for hello new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="1bc21-116">W hello **dysków zarządzanych w Utwórz** bloku, wpisz nazwę dla dysku hello i dostosować hello inne ustawienia w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="1bc21-116">In hello **Create managed disk** blade, type in a name for hello disk and adjust hello other settings as necessary.</span></span> <span data-ttu-id="1bc21-117">Gdy wszystko będzie gotowe, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="1bc21-118">W hello **dysków** bloku, kliknij przycisk Zapisz toosave hello nowej konfiguracji dysku dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1bc21-118">In hello **Disks** blade, click save toosave hello new disk configuration for hello VM.</span></span>
6. <span data-ttu-id="1bc21-119">Po Azure tworzy dysk hello i dołącza go toohello maszyny wirtualnej, hello nowego dysku jest wymieniony w ustawienia dysku maszyny wirtualnej hello w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-119">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="1bc21-120">Zainicjuj nowy dysk danych</span><span class="sxs-lookup"><span data-stu-id="1bc21-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="1bc21-121">Połącz toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1bc21-121">Connect toohello VM.</span></span>
1. <span data-ttu-id="1bc21-122">Kliknij menu start hello wewnątrz hello maszyny Wirtualnej i typ **diskmgmt.msc** i trafień **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-122">Click hello start menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="1bc21-123">Spowoduje to uruchomienie przystawki Zarządzanie dyskami hello.</span><span class="sxs-lookup"><span data-stu-id="1bc21-123">This will start hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="1bc21-124">Zarządzanie dyskami rozpozna, że znajduje się dysk nowy, które nie zostały zainicjowane i hello Inicjowanie dysku oknie wyskakującym zostanie.</span><span class="sxs-lookup"><span data-stu-id="1bc21-124">Disk Management will recognize that you have a new, un-initialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="1bc21-125">Upewnij się, że wybrano hello nowy dysk i kliknij przycisk **OK** tooinitialize go.</span><span class="sxs-lookup"><span data-stu-id="1bc21-125">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="1bc21-126">nowy dysk Hello pojawi się jako **nieprzydzielonego**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-126">hello new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="1bc21-127">Kliknij prawym przyciskiem myszy na powitania dysku i wybierz **nowy wolumin prosty**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-127">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="1bc21-128">Witaj **Kreatorze nowych woluminów prostych** zostanie uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="1bc21-128">hello **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="1bc21-129">Przejdź przez kreatora hello zapewniają, że wszystkie ustawienia domyślne hello, po zakończeniu wybierz **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-129">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="1bc21-130">Zamknij program Zarządzanie dyskami.</span><span class="sxs-lookup"><span data-stu-id="1bc21-130">Close Disk Management.</span></span>
7. <span data-ttu-id="1bc21-131">Zostanie wyświetlony okno podręczne należy tooformat hello nowy dysk przed jego użyciem.</span><span class="sxs-lookup"><span data-stu-id="1bc21-131">You will get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="1bc21-132">Kliknij przycisk **Format dysku**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="1bc21-133">W hello **Format nowy dysk** okna dialogowego, sprawdź hello ustawienia, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-133">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="1bc21-134">Zostanie wyświetlone ostrzeżenie, że formatowanie dysków hello spowoduje usunięcie wszystkich danych powitania kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-134">You will get a warning that formatting hello disks will erase all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="1bc21-135">Po zakończeniu format powitania kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="1bc21-135">When hello format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="1bc21-136">PRZYCINANIE za pomocą magazynu w warstwie standardowa</span><span class="sxs-lookup"><span data-stu-id="1bc21-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="1bc21-137">Jeśli używasz standardowego magazynu (HDD), należy włączyć PRZYCINANIE.</span><span class="sxs-lookup"><span data-stu-id="1bc21-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="1bc21-138">PRZYCINANIE odrzuca nieużywanych bloków na dysku hello tak rozliczenie jest przeprowadzane tylko dla magazynu, który faktycznie używasz.</span><span class="sxs-lookup"><span data-stu-id="1bc21-138">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="1bc21-139">Można to zapisanie kosztów, jeśli Tworzenie dużych plików, a następnie usuń je.</span><span class="sxs-lookup"><span data-stu-id="1bc21-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="1bc21-140">Możesz uruchomić to polecenie toocheck hello PRZYCINANIA ustawienie.</span><span class="sxs-lookup"><span data-stu-id="1bc21-140">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="1bc21-141">Otwórz wiersz polecenia na Twojej maszyny Wirtualnej systemu Windows i wpisz:</span><span class="sxs-lookup"><span data-stu-id="1bc21-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="1bc21-142">Jeśli polecenie hello zwraca wartość 0, PRZYCINANIE włączono poprawnie.</span><span class="sxs-lookup"><span data-stu-id="1bc21-142">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="1bc21-143">Jeśli zmienna zwraca 1, uruchom następujące polecenie tooenable PRZYCINANIE hello:</span><span class="sxs-lookup"><span data-stu-id="1bc21-143">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="1bc21-144">Po usunięciu danych z dysku, upewnij się, że hello PRZYCINANIA operacji opróżniania poprawnie, uruchamiając defragmentowania z operacją PRZYCINANIA:</span><span class="sxs-lookup"><span data-stu-id="1bc21-144">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="1bc21-145">Ponadto upewnij się, że cały wolumin hello jest ograniczona przez formatowania woluminu hello.</span><span class="sxs-lookup"><span data-stu-id="1bc21-145">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bc21-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1bc21-146">Next steps</span></span>
<span data-ttu-id="1bc21-147">Jeśli użytkownik aplikacji musi toouse hello D: dysku toostore danych, możesz [zmienić hello litera dysku tymczasowego Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1bc21-147">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
