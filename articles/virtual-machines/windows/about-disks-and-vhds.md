---
title: O dyskach i wirtualne dyski twarde dla maszyn wirtualnych systemu Windows, Microsoft Azure | Dokumentacja firmy Microsoft
description: "Podstawowe informacje na temat dysków i wirtualne dyski twarde dla systemu Windows maszyny wirtualne na platformie Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: c194ca0f31d077ffa998764b9d63b12dd596ac32
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a><span data-ttu-id="e397b-103">O dyskach i wirtualne dyski twarde dla maszyn wirtualnych systemu Windows Azure</span><span class="sxs-lookup"><span data-stu-id="e397b-103">About disks and VHDs for Azure Windows VMs</span></span>
<span data-ttu-id="e397b-104">Podobnie jak dowolnego innego komputera maszynach wirtualnych platformy Azure używać dysków jako miejsce do przechowywania systemu operacyjnego, aplikacji i danych.</span><span class="sxs-lookup"><span data-stu-id="e397b-104">Just like any other computer, virtual machines in Azure use disks as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="e397b-105">Wszystkie maszyny wirtualne platformy Azure są co najmniej dwa dyski — dysk systemu operacyjnego Windows i dysku tymczasowym.</span><span class="sxs-lookup"><span data-stu-id="e397b-105">All Azure virtual machines have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="e397b-106">Dysk systemu operacyjnego jest tworzony z obrazu, a jednocześnie dysku systemu operacyjnego i obrazu są wirtualnych dysków twardych (VHD) przechowywane w koncie magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e397b-106">The operating system disk is created from an image, and both the operating system disk and the image are virtual hard disks (VHDs) stored in an Azure storage account.</span></span> <span data-ttu-id="e397b-107">Maszyny wirtualne mogą także mieć co najmniej jeden dysk danych, które są także przechowywane jako wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="e397b-107">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span> 

<span data-ttu-id="e397b-108">W tym artykule firma Microsoft będzie porozmawiać na temat różnych zastosowań dysków, a następnie omówiono różne typy dysków, można tworzyć i używać.</span><span class="sxs-lookup"><span data-stu-id="e397b-108">In this article, we will talk about the different uses for the disks, and then discuss the different types of disks you can create and use.</span></span> <span data-ttu-id="e397b-109">W tym artykule jest również dostępny do [maszyn wirtualnych systemu Linux](about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="e397b-109">This article is also available for [Linux virtual machines](about-disks-and-vhds.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a><span data-ttu-id="e397b-110">Dysków używanych przez maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="e397b-110">Disks used by VMs</span></span>

<span data-ttu-id="e397b-111">Spójrzmy na jak dyski są używane przez maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="e397b-111">Let's take a look at how the disks are used by the VMs.</span></span>

### <a name="operating-system-disk"></a><span data-ttu-id="e397b-112">Dysk systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="e397b-112">Operating system disk</span></span>
<span data-ttu-id="e397b-113">Co maszyna wirtualna ma jeden dysk systemu operacyjnego podłączonego.</span><span class="sxs-lookup"><span data-stu-id="e397b-113">Every virtual machine has one attached operating system disk.</span></span> <span data-ttu-id="e397b-114">Ma ona zarejestrowana jako dyski SATA i oznaczone jako dysk C: domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e397b-114">It's registered as a SATA drive and labeled as the C: drive by default.</span></span> <span data-ttu-id="e397b-115">Ten dysk ma maksymalną pojemność 2048 gigabajtów (GB).</span><span class="sxs-lookup"><span data-stu-id="e397b-115">This disk has a maximum capacity of 2048 gigabytes (GB).</span></span> 

### <a name="temporary-disk"></a><span data-ttu-id="e397b-116">Tymczasowe dysku</span><span class="sxs-lookup"><span data-stu-id="e397b-116">Temporary disk</span></span>
<span data-ttu-id="e397b-117">Każda maszyna wirtualna zawiera dysku tymczasowym.</span><span class="sxs-lookup"><span data-stu-id="e397b-117">Each VM contains a temporary disk.</span></span> <span data-ttu-id="e397b-118">Dysku tymczasowym zapewnia krótkoterminowy magazyn dla aplikacji i procesów i jest przeznaczona tylko przechowywania danych, takich jak pliki strony lub wymiany.</span><span class="sxs-lookup"><span data-stu-id="e397b-118">The temporary disk provides short-term storage for applications and processes and is intended to only store data such as page or swap files.</span></span> <span data-ttu-id="e397b-119">Dane na dysku tymczasowym mogą zostać utracone podczas [zdarzenia konserwacji](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) lub gdy użytkownik [ponownego wdrażania maszyny Wirtualnej](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e397b-119">Data on the temporary disk may be lost during a [maintenance event](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) or when you [redeploy a VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e397b-120">Podczas standardowego ponownego uruchomienia maszyny wirtualnej ma utrwalić danych na dysku tymczasowym.</span><span class="sxs-lookup"><span data-stu-id="e397b-120">During a standard reboot of the VM, the data on the temporary drive should persist.</span></span>

<span data-ttu-id="e397b-121">Dysku tymczasowym jest oznaczony jako dysk D: domyślnie i używany do przechowywania pagefile.sys.</span><span class="sxs-lookup"><span data-stu-id="e397b-121">The temporary disk is labeled as the D: drive by default and it used for storing pagefile.sys.</span></span> <span data-ttu-id="e397b-122">Aby mapować dysk inną literę dysku, zobacz [zmienić literę dysku tymczasowym systemu Windows](change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="e397b-122">To remap this disk to a different drive letter, see [Change the drive letter of the Windows temporary disk](change-drive-letter.md).</span></span> <span data-ttu-id="e397b-123">Rozmiar dysku tymczasowym różni się zależnie od rozmiaru maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e397b-123">The size of the temporary disk varies, based on the size of the virtual machine.</span></span> <span data-ttu-id="e397b-124">Aby uzyskać więcej informacji, zobacz [maszyn wirtualnych rozmiary dla systemu Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="e397b-124">For more information, see [Sizes for Windows virtual machines](sizes.md).</span></span>

<span data-ttu-id="e397b-125">Aby uzyskać więcej informacji o używaniu dysku tymczasowym Azure, zobacz [opis dysku tymczasowym na maszynach wirtualnych Azure firmy Microsoft](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="e397b-125">For more information on how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>


### <a name="data-disk"></a><span data-ttu-id="e397b-126">Dysk z danymi</span><span class="sxs-lookup"><span data-stu-id="e397b-126">Data disk</span></span>
<span data-ttu-id="e397b-127">Dysk z danymi jest wirtualnego dysku twardego, który jest dołączony do maszyny wirtualnej do przechowywania danych aplikacji lub innych danych, które należy zachować.</span><span class="sxs-lookup"><span data-stu-id="e397b-127">A data disk is a VHD that's attached to a virtual machine to store application data, or other data you need to keep.</span></span> <span data-ttu-id="e397b-128">Dyski danych są rejestrowane jako dyski SCSI i są oznaczone literą, którą można wybrać.</span><span class="sxs-lookup"><span data-stu-id="e397b-128">Data disks are registered as SCSI drives and are labeled with a letter that you choose.</span></span> <span data-ttu-id="e397b-129">Każdy dysk danych ma maksymalną pojemność 4095 GB.</span><span class="sxs-lookup"><span data-stu-id="e397b-129">Each data disk has a maximum capacity of 4095 GB.</span></span> <span data-ttu-id="e397b-130">Rozmiar maszyny wirtualnej Określa, jak wiele dysków z danymi można dołączyć do jego i typ magazynu służy do obsługi dysków.</span><span class="sxs-lookup"><span data-stu-id="e397b-130">The size of the virtual machine determines how many data disks you can attach to it and the type of storage you can use to host the disks.</span></span>

> [!NOTE]
> <span data-ttu-id="e397b-131">Aby uzyskać więcej informacji na temat pojemności maszyn wirtualnych, zobacz [maszyn wirtualnych rozmiary dla systemu Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="e397b-131">For more information about virtual machines capacities, see [Sizes for Windows virtual machines](sizes.md).</span></span>
> 

<span data-ttu-id="e397b-132">Azure tworzy dysk systemu operacyjnego, podczas tworzenia maszyny wirtualnej z obrazu.</span><span class="sxs-lookup"><span data-stu-id="e397b-132">Azure creates an operating system disk when you create a virtual machine from an image.</span></span> <span data-ttu-id="e397b-133">Jeśli używasz obrazu, który zawiera dyski danych Azure tworzy także dysków danych podczas tworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e397b-133">If you use an image that includes data disks, Azure also creates the data disks when it creates the virtual machine.</span></span> <span data-ttu-id="e397b-134">W przeciwnym razie możesz dodać dysk danych, po utworzeniu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e397b-134">Otherwise, you add data disks after you create the virtual machine.</span></span>

<span data-ttu-id="e397b-135">Można dodać dysków z danymi do maszyny wirtualnej w dowolnym momencie przez **dołączanie** dysku do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e397b-135">You can add data disks to a virtual machine at any time, by **attaching** the disk to the virtual machine.</span></span> <span data-ttu-id="e397b-136">Można użyć wirtualnego dysku twardego, który został przekazany lub kopiowane do konta magazynu lub taki, który tworzy Azure.</span><span class="sxs-lookup"><span data-stu-id="e397b-136">You can use a VHD that you've uploaded or copied to your storage account, or one that Azure creates for you.</span></span> <span data-ttu-id="e397b-137">Dołączenie dysku danych skojarzenie pliku wirtualnego dysku twardego z maszyną Wirtualną przez umieszczenie dzierżawy na dysku VHD nie może być usunięty z magazynu nadal będzie dołączony.</span><span class="sxs-lookup"><span data-stu-id="e397b-137">Attaching a data disk associates the VHD file with the VM by placing a 'lease' on the VHD so it can't be deleted from storage while it's still attached.</span></span>


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a><span data-ttu-id="e397b-138">Zalecamy ostatniego: Użyj PRZYCINANIE z niezarządzanego dyski standardowe</span><span class="sxs-lookup"><span data-stu-id="e397b-138">One last recommendation: Use TRIM with unmanaged standard disks</span></span> 

<span data-ttu-id="e397b-139">Jeśli używasz niezarządzane dyski standardowe (HDD), należy włączyć PRZYCINANIE.</span><span class="sxs-lookup"><span data-stu-id="e397b-139">If you use unmanaged standard disks (HDD), you should enable TRIM.</span></span> <span data-ttu-id="e397b-140">PRZYCINANIE odrzuca nieużywanych bloków na dysku dzięki rozliczenie jest przeprowadzane tylko dla magazynu, który faktycznie używasz.</span><span class="sxs-lookup"><span data-stu-id="e397b-140">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="e397b-141">Można to zapisanie kosztów, jeśli Tworzenie dużych plików, a następnie usuń je.</span><span class="sxs-lookup"><span data-stu-id="e397b-141">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="e397b-142">Można uruchomić tego polecenia, aby sprawdzić ustawienie PRZYCINANIA.</span><span class="sxs-lookup"><span data-stu-id="e397b-142">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="e397b-143">Otwórz wiersz polecenia na Twojej maszyny Wirtualnej systemu Windows i wpisz:</span><span class="sxs-lookup"><span data-stu-id="e397b-143">Open a command prompt on your Windows VM and type:</span></span>


```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="e397b-144">Jeśli polecenie zwróci wartość 0, PRZYCINANIE jest prawidłowo włączona.</span><span class="sxs-lookup"><span data-stu-id="e397b-144">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="e397b-145">Jeśli zmienna zwraca 1, uruchom następujące polecenie, aby umożliwić PRZYCINANIE:</span><span class="sxs-lookup"><span data-stu-id="e397b-145">If it returns 1, run the following command to enable TRIM:</span></span>

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> <span data-ttu-id="e397b-146">Uwaga: Obsługa funkcji usuwania rozpoczyna się od systemu Windows Server 2012 / Windows 8 lub nowszym, można znaleźć w temacie [nowy interfejs API umożliwia aplikacjom wysyłania "PRZYCINANIE i Usuń mapowanie" wskazówki na nośnikach magazynowania](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span><span class="sxs-lookup"><span data-stu-id="e397b-146">Note: Trim support starts with Windows Server 2012 / Windows 8 and above, see see [New API allows apps to send "TRIM and Unmap" hints to storage media](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).</span></span>
> 

<!-- Might want to match next-steps from overview of managed disks -->
## <a name="next-steps"></a><span data-ttu-id="e397b-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e397b-147">Next steps</span></span>
* <span data-ttu-id="e397b-148">[Dołączenie dysku](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) dodać dodatkowy magazyn dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e397b-148">[Attach a disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to add additional storage for your VM.</span></span>
* <span data-ttu-id="e397b-149">[Zmienić literę dysku tymczasowym systemu Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) , aplikacja może używać dysków D: danych.</span><span class="sxs-lookup"><span data-stu-id="e397b-149">[Change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) so your application can use the D: drive for data.</span></span>

