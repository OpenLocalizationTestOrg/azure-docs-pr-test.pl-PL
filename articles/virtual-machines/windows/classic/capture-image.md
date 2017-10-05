---
title: "Przechwyć obraz maszyny Wirtualnej systemu Windows Azure | Dokumentacja firmy Microsoft"
description: "Przechwytywanie obrazu maszyny wirtualnej systemu Windows przy użyciu klasycznego modelu wdrażania."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 6032263848c469ce2f416306e5c91c29f4cb30e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="e5bce-103">Przechwytywanie obrazu maszyny wirtualnej systemu Windows przy użyciu klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="e5bce-103">Capture an image of an Azure Windows virtual machine created with the classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e5bce-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e5bce-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e5bce-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e5bce-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="e5bce-106">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5bce-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="e5bce-107">Menedżer zasobów modelu informacji, zobacz [Przechwyć obraz zarządzanych uogólniony maszyny wirtualnej na platformie Azure](../capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="e5bce-107">For Resource Manager model information, see [Capture a managed image of a generalized VM in Azure](../capture-image-resource.md).</span></span>

<span data-ttu-id="e5bce-108">W tym artykule przedstawiono, jak przechwycić maszynę wirtualną platformy Azure systemem Windows, tak jak obraz służy do tworzenia innych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e5bce-108">This article shows you how to capture an Azure virtual machine running Windows so you can use it as an image to create other virtual machines.</span></span> <span data-ttu-id="e5bce-109">Ten obraz zawiera dysku systemu operacyjnego i wszystkich dysków danych, które są dołączone do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5bce-109">This image includes the operating system disk and any data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="e5bce-110">Nie ma wśród nich konfiguracje sieci, więc musisz skonfigurować konfiguracji sieci, podczas tworzenia innych maszyn wirtualnych korzystających z obrazu.</span><span class="sxs-lookup"><span data-stu-id="e5bce-110">It doesn't include networking configurations, so you'll need to set up network configurations when you create the other virtual machines that use the image.</span></span>

<span data-ttu-id="e5bce-111">Azure zapisuje obraz w obszarze **obrazów maszyn wirtualnych (klasyczne)**, **obliczeniowe** usługi na liście, podczas wyświetlania wszystkich usług Azure.</span><span class="sxs-lookup"><span data-stu-id="e5bce-111">Azure stores the image under **VM images (classic)**, a **Compute** service that is listed when you view all the Azure services.</span></span> <span data-ttu-id="e5bce-112">To jest tym samym miejscu, w którym są przechowywane wszystkie obrazy przekazanego.</span><span class="sxs-lookup"><span data-stu-id="e5bce-112">This is the same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="e5bce-113">Aby uzyskać więcej informacji o obrazach, zobacz [o obrazów maszyn wirtualnych](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5bce-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e5bce-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="e5bce-114">Before you begin</span></span>
<span data-ttu-id="e5bce-115">Tych krokach przyjęto założenie, że zostały już utworzeniu maszyny wirtualnej platformy Azure i skonfigurowaniu systemu operacyjnego, w tym dołączanie dowolnego dysku z danymi.</span><span class="sxs-lookup"><span data-stu-id="e5bce-115">These steps assume that you've already created an Azure virtual machine and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="e5bce-116">Jeśli to nie zostało to jeszcze zrobione jeszcze, zobacz następujące artykuły, aby uzyskać informacje na temat tworzenia i przygotowywanie maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e5bce-116">If you haven't done this yet, see the following articles for information on creating and preparing the virtual machine:</span></span>

* [<span data-ttu-id="e5bce-117">Utwórz maszynę wirtualną z obrazu</span><span class="sxs-lookup"><span data-stu-id="e5bce-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="e5bce-118">Jak można dołączyć dysku danych do maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e5bce-118">How to attach a data disk to a virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="e5bce-119">Upewnij się, że role serwera są obsługiwane przy użyciu narzędzia Sysprep.</span><span class="sxs-lookup"><span data-stu-id="e5bce-119">Make sure the server roles are supported with Sysprep.</span></span> <span data-ttu-id="e5bce-120">Aby uzyskać więcej informacji, zobacz [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="e5bce-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="e5bce-121">Ten proces powoduje usunięcie oryginalna maszyna wirtualna po jego przechwyceniu.</span><span class="sxs-lookup"><span data-stu-id="e5bce-121">This process deletes the original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="e5bce-122">Przed przechwyceniem obrazu maszyny wirtualnej platformy Azure, zaleca się docelowej maszyny wirtualnej można wykonać kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="e5bce-122">Prior to capturing an image of an Azure virtual machine, it is recommended the target virtual machine be backed up.</span></span> <span data-ttu-id="e5bce-123">Maszyny wirtualne platformy Azure można kopii zapasowej za pomocą usługi Kopia zapasowa Azure.</span><span class="sxs-lookup"><span data-stu-id="e5bce-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="e5bce-124">Aby uzyskać szczegółowe informacje, zobacz [Tworzenie kopii zapasowych maszyn wirtualnych platformy Azure](../../../backup/backup-azure-vms.md).</span><span class="sxs-lookup"><span data-stu-id="e5bce-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="e5bce-125">Inne rozwiązania są dostępne u certyfikowanych partnerów.</span><span class="sxs-lookup"><span data-stu-id="e5bce-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="e5bce-126">Aby dowiedzieć się, co jest obecnie dostępne, przeszukaj witrynę Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e5bce-126">To find out what’s currently available, search the Azure Marketplace.</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="e5bce-127">Przechwytywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e5bce-127">Capture the virtual machine</span></span>
1. <span data-ttu-id="e5bce-128">W [portalu Azure](http://portal.azure.com), **Connect** do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5bce-128">In the [Azure portal](http://portal.azure.com), **Connect** to the virtual machine.</span></span> <span data-ttu-id="e5bce-129">Aby uzyskać instrukcje, zobacz [jak zalogować się do maszyny wirtualnej z systemem Windows Server][How to sign in to a virtual machine running Windows Server].</span><span class="sxs-lookup"><span data-stu-id="e5bce-129">For instructions, see [How to sign in to a virtual machine running Windows Server][How to sign in to a virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="e5bce-130">Otwórz okno wiersza polecenia z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="e5bce-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="e5bce-131">Zmień katalog na `%windir%\system32\sysprep`, a następnie uruchom sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="e5bce-131">Change the directory to `%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="e5bce-132">**Narzędzie przygotowania systemu** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="e5bce-132">The **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="e5bce-133">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e5bce-133">Do the following:</span></span>

   * <span data-ttu-id="e5bce-134">W **Akcja oczyszczania systemu**, wybierz pozycję **wprowadź systemu Out-of-Box Experience (OOBE)** i upewnij się, że **Generalize** jest zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="e5bce-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="e5bce-135">Aby uzyskać więcej informacji o korzystaniu z programu Sysprep, zobacz [sposobu użycia programu Sysprep: wprowadzenie][How to Use Sysprep: An Introduction].</span><span class="sxs-lookup"><span data-stu-id="e5bce-135">For more information about using Sysprep, see [How to Use Sysprep: An Introduction][How to Use Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="e5bce-136">W **opcje zamykania**, wybierz pozycję **zamknięcia**.</span><span class="sxs-lookup"><span data-stu-id="e5bce-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="e5bce-137">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5bce-137">Click **OK**.</span></span>

   ![Uruchom program Sysprep](./media/capture-image/SysprepGeneral.png)
5. <span data-ttu-id="e5bce-139">Narzędzie Sysprep zamyka maszynę wirtualną, która zmieni stan maszyny wirtualnej w portalu Azure, aby **zatrzymane**.</span><span class="sxs-lookup"><span data-stu-id="e5bce-139">Sysprep shuts down the virtual machine, which changes the status of the virtual machine in the Azure portal to **Stopped**.</span></span>
6. <span data-ttu-id="e5bce-140">W portalu Azure kliknij **maszyn wirtualnych (klasyczne)** i wybierz maszynę wirtualną, które mają być przechwytywane.</span><span class="sxs-lookup"><span data-stu-id="e5bce-140">In the Azure portal, click **Virtual Machines (classic)** and select the virtual machine you want to capture.</span></span> <span data-ttu-id="e5bce-141">**Obrazów maszyn wirtualnych (klasyczne)** grupy znajduje się w obszarze **obliczeniowe** podczas wyświetlania **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="e5bce-141">The **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="e5bce-142">Na pasku poleceń, kliknij przycisk **przechwytywania**.</span><span class="sxs-lookup"><span data-stu-id="e5bce-142">On the command bar, click **Capture**.</span></span>

   ![Przechwytywanie maszyny wirtualnej](./media/capture-image/CaptureVM.png)

   <span data-ttu-id="e5bce-144">**Przechwytywanie maszyny wirtualnej** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="e5bce-144">The **Capture the Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="e5bce-145">W **nazwa obrazu**, wpisz nazwę nowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="e5bce-145">In **Image name**, type a name for the new image.</span></span> <span data-ttu-id="e5bce-146">W **etykiety obrazu**, wpisz etykietę dla nowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="e5bce-146">In **Image label**, type a label for the new image.</span></span>

9. <span data-ttu-id="e5bce-147">Kliknij przycisk **uruchomiono program Sysprep na maszynie wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="e5bce-147">Click **I've run Sysprep on the virtual machine**.</span></span> <span data-ttu-id="e5bce-148">To pole wyboru odwołuje się do akcji przy użyciu narzędzia Sysprep w krokach 3 – 5.</span><span class="sxs-lookup"><span data-stu-id="e5bce-148">This checkbox refers to the actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="e5bce-149">Obraz _musi_ uogólnione przed dodaniem obrazu systemu Windows Server do zestawu niestandardowych obrazów, uruchamiając program Sysprep.</span><span class="sxs-lookup"><span data-stu-id="e5bce-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image to your set of custom images.</span></span>

10. <span data-ttu-id="e5bce-150">Po zakończeniu Przechwytywanie nowego obrazu staje się dostępna **Marketplace**w **obliczeniowe**, **obrazów maszyn wirtualnych (klasyczne)** kontenera.</span><span class="sxs-lookup"><span data-stu-id="e5bce-150">Once the capture completes, the new image becomes available in the **Marketplace**, in the **Compute**, **VM images (classic)** container.</span></span>

    ![Pomyślne przechwytywania obrazu](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="e5bce-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5bce-152">Next steps</span></span>
<span data-ttu-id="e5bce-153">Obraz jest gotowy do utworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5bce-153">The image is ready to be used to create virtual machines.</span></span> <span data-ttu-id="e5bce-154">Aby to zrobić, należy utworzyć maszynę wirtualną, wybierając **więcej usług** element menu u dołu menu usługi, następnie **obrazów maszyn wirtualnych (klasyczne)** w **obliczeniowe** grupy.</span><span class="sxs-lookup"><span data-stu-id="e5bce-154">To do this, you'll create a virtual machine by selecting the **More services** menu item at the bottom of the services menu, then **VM images (classic)** in the **Compute** group.</span></span> <span data-ttu-id="e5bce-155">Aby uzyskać instrukcje, zobacz [Utwórz maszynę wirtualną z obrazu](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="e5bce-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How to sign in to a virtual machine running Windows Server]:connect-logon.md
[How to Use Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[The virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of the virtual machine]: ./media/capture-image/CaptureVM.png
[Enter the image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use the captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
