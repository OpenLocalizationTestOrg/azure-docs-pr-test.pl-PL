---
title: "Skonfigurować dysk D: dysku danych maszyny wirtualnej | Dokumentacja firmy Microsoft"
description: "Zawiera opis sposobu zmiany liter dysków dla maszyny Wirtualnej systemu Windows tak, aby dysków D: jako dysk danych."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 7667175c01be2421bfc3badd83b1d8aaeb29bfde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="6ee7b-103">Użyj dysku D: jako dysk z danymi na maszynie Wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="6ee7b-103">Use the D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="6ee7b-104">Jeśli aplikacja wymaga na potrzeby przechowywania danych na dysku D, wykonaj te instrukcje, aby użyć innej litery dysku na dysku tymczasowym.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-104">If your application needs to use the D drive to store data, follow these instructions to use a different drive letter for the temporary disk.</span></span> <span data-ttu-id="6ee7b-105">Nigdy nie używaj tymczasowych dysku do przechowywania danych, które należy zachować.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-105">Never use the temporary disk to store data that you need to keep.</span></span>

<span data-ttu-id="6ee7b-106">Jeśli po zmianie rozmiaru lub **Stop (Deallocate)** maszyny wirtualnej, może to wywołać umieszczania maszyny wirtualnej do nowej funkcji hypervisor.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of the virtual machine to a new hypervisor.</span></span> <span data-ttu-id="6ee7b-107">Planowanego lub nieplanowanego zdarzenia konserwacji może być również przyczyną tego rozmieszczenia.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="6ee7b-108">W tym scenariuszu dysku tymczasowym zostanie przydzielona do pierwszą literę dysku.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-108">In this scenario, the temporary disk will be reassigned to the first available drive letter.</span></span> <span data-ttu-id="6ee7b-109">Jeśli masz aplikację, która wymaga dysku D:, w szczególności należy wykonaj następujące kroki, aby tymczasowo przenieść pagefile.sys, dołączyć nowego dysku danych i przypisać jej literę D i następnie przenieść pagefile.sys z powrotem do tymczasowej stacji.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-109">If you have an application that specifically requires the D: drive, you need to follow these steps to temporarily move the pagefile.sys, attach a new data disk and assign it the letter D and then move the pagefile.sys back to the temporary drive.</span></span> <span data-ttu-id="6ee7b-110">Po wykonaniu tych czynności Azure nie wycofania D: Jeśli maszyna wirtualna zostanie przeniesiona do innej funkcji hypervisor.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-110">Once complete, Azure will not take back the D: if the VM moves to a different hypervisor.</span></span>

<span data-ttu-id="6ee7b-111">Aby uzyskać więcej informacji o używaniu dysku tymczasowym Azure, zobacz [opis dysku tymczasowym na maszynach wirtualnych Azure firmy Microsoft](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="6ee7b-111">For more information about how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-the-data-disk"></a><span data-ttu-id="6ee7b-112">Dołączenie dysku danych</span><span class="sxs-lookup"><span data-stu-id="6ee7b-112">Attach the data disk</span></span>
<span data-ttu-id="6ee7b-113">Najpierw należy dołączyć dysku danych do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-113">First, you'll need to attach the data disk to the virtual machine.</span></span> <span data-ttu-id="6ee7b-114">Aby to zrobić za pomocą portalu, zobacz [jak dołączyć dysk danych zarządzanych w portalu Azure](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6ee7b-114">To do this using the portal, see [How to attach a managed data disk in the Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-to-c-drive"></a><span data-ttu-id="6ee7b-115">Tymczasowo przenieść pagefile.sys dysku c.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-115">Temporarily move pagefile.sys to C drive</span></span>
1. <span data-ttu-id="6ee7b-116">Połączenie z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-116">Connect to the virtual machine.</span></span> 
2. <span data-ttu-id="6ee7b-117">Kliknij prawym przyciskiem myszy **Start** menu i wybierz **systemu**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-117">Right-click the **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="6ee7b-118">W menu po lewej stronie wybierz **Zaawansowane ustawienia systemu**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-118">In the left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="6ee7b-119">W **wydajności** zaznacz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-119">In the **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="6ee7b-120">Wybierz **zaawansowane** kartę.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-120">Select the **Advanced** tab.</span></span>
6. <span data-ttu-id="6ee7b-121">W **pamięci wirtualnej** zaznacz **zmiany**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-121">In the **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="6ee7b-122">Wybierz **C** dysk, a następnie kliknij przycisk **Rozmiar kontrolowany przez System** , a następnie kliknij przycisk **ustawić**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-122">Select the **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="6ee7b-123">Wybierz **D** dysk, a następnie kliknij przycisk **plik stronicowania nie** , a następnie kliknij przycisk **ustawić**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-123">Select the **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="6ee7b-124">Kliknij przycisk Zastosuj.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-124">Click Apply.</span></span> <span data-ttu-id="6ee7b-125">Zostanie wyświetlone ostrzeżenie, że wymagane zmiany zostały uwzględnione, należy uruchomić ponownie komputera.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-125">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
10. <span data-ttu-id="6ee7b-126">Uruchom ponownie maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-126">Restart the virtual machine.</span></span>

## <a name="change-the-drive-letters"></a><span data-ttu-id="6ee7b-127">Zmień litery dysku</span><span class="sxs-lookup"><span data-stu-id="6ee7b-127">Change the drive letters</span></span>
1. <span data-ttu-id="6ee7b-128">Po ponownym uruchomieniu maszyny Wirtualnej, zaloguj się ponownie do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-128">Once the VM restarts, log back on to the VM.</span></span>
2. <span data-ttu-id="6ee7b-129">Kliknij przycisk **Start** menu i typ **diskmgmt.msc** i naciśnij Enter.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-129">Click the **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="6ee7b-130">Rozpocznie się Zarządzanie dyskami.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-130">Disk Management will start.</span></span>
3. <span data-ttu-id="6ee7b-131">Kliknij prawym przyciskiem myszy **D**, magazyn tymczasowy dysku, a następnie wybierz **Zmień literę dysku i ścieżki**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-131">Right-click on **D**, the Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="6ee7b-132">W obszarze literę dysku, wybierz inny dysk takich jak **T** , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="6ee7b-133">Kliknij prawym przyciskiem myszy na dysk z danymi, a następnie wybierz **Zmień literę dysku i ścieżki**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-133">Right-click on the data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="6ee7b-134">W obszarze literę dysku, należy wybrać dysk **D** , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-to-the-temporary-storage-drive"></a><span data-ttu-id="6ee7b-135">Przenieść pagefile.sys z powrotem do dysku magazyn tymczasowy</span><span class="sxs-lookup"><span data-stu-id="6ee7b-135">Move pagefile.sys back to the temporary storage drive</span></span>
1. <span data-ttu-id="6ee7b-136">Kliknij prawym przyciskiem myszy **Start** menu i wybierz **systemu**</span><span class="sxs-lookup"><span data-stu-id="6ee7b-136">Right-click the **Start** menu and select **System**</span></span>
2. <span data-ttu-id="6ee7b-137">W menu po lewej stronie wybierz **Zaawansowane ustawienia systemu**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-137">In the left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="6ee7b-138">W **wydajności** zaznacz **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-138">In the **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="6ee7b-139">Wybierz **zaawansowane** kartę.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-139">Select the **Advanced** tab.</span></span>
5. <span data-ttu-id="6ee7b-140">W **pamięci wirtualnej** zaznacz **zmiany**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-140">In the **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="6ee7b-141">Wybierz dysk systemu operacyjnego **C** i kliknij przycisk **plik stronicowania nie** , a następnie kliknij przycisk **ustawić**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-141">Select the OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="6ee7b-142">Wybierz dysk magazyn tymczasowy **T** , a następnie kliknij przycisk **Rozmiar kontrolowany przez System** , a następnie kliknij przycisk **ustawić**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-142">Select the temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="6ee7b-143">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-143">Click **Apply**.</span></span> <span data-ttu-id="6ee7b-144">Zostanie wyświetlone ostrzeżenie, że wymagane zmiany zostały uwzględnione, należy uruchomić ponownie komputera.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-144">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
9. <span data-ttu-id="6ee7b-145">Uruchom ponownie maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="6ee7b-145">Restart the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ee7b-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ee7b-146">Next steps</span></span>
* <span data-ttu-id="6ee7b-147">Dostępny magazyn może zwiększyć się z maszyną wirtualną przez [dołączenie dysku danych dodatkowych](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6ee7b-147">You can increase the storage available to your virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

