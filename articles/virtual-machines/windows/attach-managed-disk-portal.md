---
title: "Dołączenie dysku danych zarządzanych do maszyny Wirtualnej systemu Windows - Azure | Dokumentacja firmy Microsoft"
description: "Jak można dołączyć nowego dysku danych zarządzanych do maszyny Wirtualnej systemu Windows w portalu Azure przy użyciu modelu wdrażania Menedżera zasobów."
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
ms.openlocfilehash: f0cf88a06c5470ef173b22e7213419a6c8760723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-managed-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="e1f0b-103">Jak można dołączyć dysku danych zarządzanych do maszyny Wirtualnej systemu Windows, w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e1f0b-103">How to attach a managed data disk to a Windows VM in the Azure portal</span></span>

<span data-ttu-id="e1f0b-104">W tym artykule przedstawiono sposób dołączyć nowego dysku danych zarządzanych do maszyn wirtualnych z systemem Windows za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-104">This article shows you how to attach a new managed data disk to Windows virtual machines through the Azure portal.</span></span> <span data-ttu-id="e1f0b-105">Zanim to zrobisz, przejrzyj następujące wskazówki:</span><span class="sxs-lookup"><span data-stu-id="e1f0b-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="e1f0b-106">Rozmiar maszyny wirtualnej Określa, ile można dołączać dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-106">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="e1f0b-107">Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="e1f0b-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="e1f0b-108">Dla nowego dysku nie trzeba go najpierw utworzyć ponieważ Azure tworzy go po dołączeniu go.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-108">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="e1f0b-109">Możesz również [dołączenie dysku danych przy użyciu programu Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e1f0b-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="e1f0b-110">Dodaj dysk danych</span><span class="sxs-lookup"><span data-stu-id="e1f0b-110">Add a data disk</span></span>
1. <span data-ttu-id="e1f0b-111">W menu po lewej stronie kliknij **maszyn wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-111">In the menu on the left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="e1f0b-112">Wybierz maszynę wirtualną z listy.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-112">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="e1f0b-113">W bloku maszyny wirtualnej, kliknij polecenie **dysków**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-113">On the virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="e1f0b-114">Na **dysków** bloku, kliknij przycisk **+ Dodaj dysk danych**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-114">On the **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="e1f0b-115">Z listy rozwijanej dla nowego dysku, wybierz **utworzyć pusty**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-115">In the drop-down for the new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="e1f0b-116">W **dysków zarządzanych w Utwórz** bloku, wpisz nazwę dla dysku i Dostosuj pozostałe ustawienia odpowiednio do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-116">In the **Create managed disk** blade, type in a name for the disk and adjust the other settings as necessary.</span></span> <span data-ttu-id="e1f0b-117">Gdy wszystko będzie gotowe, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="e1f0b-118">W **dysków** bloku, kliknij przycisk Zapisz, aby zapisać nową konfigurację dysku dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-118">In the **Disks** blade, click save to save the new disk configuration for the VM.</span></span>
6. <span data-ttu-id="e1f0b-119">Po Azure utworzy dysk i dołącza go do maszyny wirtualnej, nowy dysk ma na liście ustawień dysku maszyny wirtualnej w obszarze **dysków z danymi**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-119">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="e1f0b-120">Zainicjuj nowy dysk danych</span><span class="sxs-lookup"><span data-stu-id="e1f0b-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="e1f0b-121">Połączenie z maszyną Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-121">Connect to the VM.</span></span>
1. <span data-ttu-id="e1f0b-122">Kliknij menu start wewnątrz maszyny Wirtualnej i typ **diskmgmt.msc** i trafień **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-122">Click the start menu inside the VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="e1f0b-123">Spowoduje to uruchomienie przystawki Zarządzanie dyskami.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-123">This will start the Disk Management snap-in.</span></span>
2. <span data-ttu-id="e1f0b-124">Zarządzanie dyskami rozpozna, że znajduje się dysk nowy, które nie zostały zainicjowane i będzie wyskakujące okno Inicjowanie dysku.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-124">Disk Management will recognize that you have a new, un-initialized disk and the Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="e1f0b-125">Upewnij się, że wybrano nowy dysk i kliknij przycisk **OK** można go zainicjować.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-125">Make sure the new disk is selected and click **OK** to initialize it.</span></span>
4. <span data-ttu-id="e1f0b-126">Nowy dysk będą teraz wyświetlane jako **nieprzydzielonego**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-126">The new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="e1f0b-127">Kliknij prawym przyciskiem myszy w dowolnym miejscu na dysku i wybierz **nowy wolumin prosty**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-127">Right-click anywhere on the disk and select **New simple volume**.</span></span> <span data-ttu-id="e1f0b-128">**Kreatorze nowych woluminów prostych** zostanie uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-128">The **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="e1f0b-129">Przejdź przez kreatora, przechowywanie ustawień domyślnych, po zakończeniu wybierz **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-129">Go through the wizard, keeping all of the defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="e1f0b-130">Zamknij program Zarządzanie dyskami.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-130">Close Disk Management.</span></span>
7. <span data-ttu-id="e1f0b-131">Zostanie wyświetlone okno podręczne, które należy sformatować nowy dysk przed jego użyciem.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-131">You will get a pop-up that you need to format the new disk before you can use it.</span></span> <span data-ttu-id="e1f0b-132">Kliknij przycisk **Format dysku**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="e1f0b-133">W **Format nowy dysk** okna dialogowego, sprawdź ustawienia, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-133">In the **Format new disk** dialog, check the settings and then click **Start**.</span></span>
9. <span data-ttu-id="e1f0b-134">Zostanie wyświetlone ostrzeżenie, że formatowanie dysków spowoduje wymazanie wszystkich danych, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-134">You will get a warning that formatting the disks will erase all of the data, click **OK**.</span></span>
10. <span data-ttu-id="e1f0b-135">Po zakończeniu format kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-135">When the format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="e1f0b-136">PRZYCINANIE za pomocą magazynu w warstwie standardowa</span><span class="sxs-lookup"><span data-stu-id="e1f0b-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="e1f0b-137">Jeśli używasz standardowego magazynu (HDD), należy włączyć PRZYCINANIE.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="e1f0b-138">PRZYCINANIE odrzuca nieużywanych bloków na dysku dzięki rozliczenie jest przeprowadzane tylko dla magazynu, który faktycznie używasz.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-138">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="e1f0b-139">Można to zapisanie kosztów, jeśli Tworzenie dużych plików, a następnie usuń je.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="e1f0b-140">Można uruchomić tego polecenia, aby sprawdzić ustawienie PRZYCINANIA.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-140">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="e1f0b-141">Otwórz wiersz polecenia na Twojej maszyny Wirtualnej systemu Windows i wpisz:</span><span class="sxs-lookup"><span data-stu-id="e1f0b-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="e1f0b-142">Jeśli polecenie zwróci wartość 0, PRZYCINANIE jest prawidłowo włączona.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-142">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="e1f0b-143">Jeśli zmienna zwraca 1, uruchom następujące polecenie, aby umożliwić PRZYCINANIE:</span><span class="sxs-lookup"><span data-stu-id="e1f0b-143">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="e1f0b-144">Po usunięciu danych z dysku, można zapewnić PRZYCINANIA operacje opróżniania poprawnie, uruchamiając defragmentowania z operacją PRZYCINANIA:</span><span class="sxs-lookup"><span data-stu-id="e1f0b-144">After deleting data from your disk, you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="e1f0b-145">Ponadto upewnij się, że cały wolumin jest ograniczona przez formatowania woluminu.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-145">You can also ensure the entire volume is trimmed by formatting the volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1f0b-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e1f0b-146">Next steps</span></span>
<span data-ttu-id="e1f0b-147">Jeśli użytkownik aplikacji musi używać D: dysków do przechowywania danych, możesz [zmienić literę dysku tymczasowym systemu Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1f0b-147">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
