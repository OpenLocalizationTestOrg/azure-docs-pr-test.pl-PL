---
title: "Zarządzanie maszyn wirtualnych przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej poleceń, które służą do automatyzacji zadań zarządzania maszyn wirtualnych."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: fd2df7e1029ced11974d0b832258bed2cf3bbb27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="31fc3-103">Zarządzanie maszynami wirtualnymi przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="31fc3-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="31fc3-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="31fc3-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="31fc3-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="31fc3-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="31fc3-106">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="31fc3-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="31fc3-107">Typowe poleceń programu PowerShell przy użyciu modelu Resource Manager, zobacz [tutaj](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31fc3-107">For common PowerShell commands using the Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="31fc3-108">Wiele zadań, czy każdego dnia, aby zarządzać maszyn wirtualnych można zautomatyzować za pomocą poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31fc3-108">Many tasks you do each day to manage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="31fc3-109">Ten artykuł zawiera przykładowe polecenia zadania prostszy i łącza do artykułów, które Pokaż polecenia dla bardziej złożonych zadań.</span><span class="sxs-lookup"><span data-stu-id="31fc3-109">This article gives you example commands for simpler tasks, and links to articles that show the commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="31fc3-110">Jeśli nie zostało to jeszcze zainstalowaniu i skonfigurowaniu programu Azure PowerShell, ale można wyświetlić instrukcje w artykule [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="31fc3-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in the article [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-to-use-the-example-commands"></a><span data-ttu-id="31fc3-111">Jak używać przykładowe polecenia</span><span class="sxs-lookup"><span data-stu-id="31fc3-111">How to use the example commands</span></span>
<span data-ttu-id="31fc3-112">Należy zastąpić fragment tekstu w poleceniach tekst, który jest odpowiedni dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="31fc3-112">You'll need to replace some of the text in the commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="31fc3-113">< a > symbole wskazują należy zastąpić tekst.</span><span class="sxs-lookup"><span data-stu-id="31fc3-113">The < and > symbols indicate text you need to replace.</span></span> <span data-ttu-id="31fc3-114">Zamień tekst, Usuń symbole, ale pozostawić znaki cudzysłowu w miejscu.</span><span class="sxs-lookup"><span data-stu-id="31fc3-114">When you replace the text, remove the symbols but leave the quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="31fc3-115">Uzyskiwanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="31fc3-115">Get a VM</span></span>
<span data-ttu-id="31fc3-116">Jest to podstawowe zadania, które będzie używane.</span><span class="sxs-lookup"><span data-stu-id="31fc3-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="31fc3-117">Należy uzyskać informacje na temat maszyny Wirtualnej, wykonywania zadań na maszynie Wirtualnej lub pobrać dane wyjściowe mają być przechowywane w zmiennej.</span><span class="sxs-lookup"><span data-stu-id="31fc3-117">Use it to get information about a VM, perform tasks on a VM, or get output to store in a variable.</span></span>

<span data-ttu-id="31fc3-118">Aby uzyskać informacje o maszynie Wirtualnej, uruchom to polecenie, zastępując wszystko w cudzysłowie, łącznie z < a > znaków:</span><span class="sxs-lookup"><span data-stu-id="31fc3-118">To get information about the VM, run this command, replacing everything in the quotes, including the < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="31fc3-119">Aby przechowywać dane wyjściowe w zmiennej $vm, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="31fc3-119">To store the output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-to-a-windows-based-vm"></a><span data-ttu-id="31fc3-120">Zaloguj się do maszyny Wirtualnej z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="31fc3-120">Log on to a Windows-based VM</span></span>
<span data-ttu-id="31fc3-121">Uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="31fc3-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="31fc3-122">Nazwa maszyny wirtualnej i w chmurze usługi można uzyskać z widoku **Get-AzureVM** polecenia.</span><span class="sxs-lookup"><span data-stu-id="31fc3-122">You can get the virtual machine and cloud service name from the display of the **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="31fc3-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< dysk i lokalizację folderu do przechowywania pobranych plików RDP, przykład: c:\temp >" $localFile = $localPath + "\" $vmname +"RDP"Get-AzureRemoteDesktopFile - ServiceName $svcName-name $vmName - LocalPath $localFile — uruchamianie</span><span class="sxs-lookup"><span data-stu-id="31fc3-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location to store the downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="31fc3-124">Zatrzymywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="31fc3-124">Stop a VM</span></span>
<span data-ttu-id="31fc3-125">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="31fc3-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="31fc3-126">Użyj tego parametru, aby zachować wirtualnego adresu IP (VIP) z usługi w chmurze, w przypadku, gdy jest ostatnia maszyna wirtualna w tej usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="31fc3-126">Use this parameter to keep the virtual IP (VIP) of the cloud service in case it's the last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="31fc3-127">Jeśli parametr StayProvisioned nadal zostaną naliczone opłaty dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="31fc3-127">If you use the StayProvisioned parameter, you'll still be billed for the VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="31fc3-128">Uruchamianie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="31fc3-128">Start a VM</span></span>
<span data-ttu-id="31fc3-129">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="31fc3-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="31fc3-130">Dołączanie dysku danych</span><span class="sxs-lookup"><span data-stu-id="31fc3-130">Attach a data disk</span></span>
<span data-ttu-id="31fc3-131">To zadanie wymaga kilku kroków.</span><span class="sxs-lookup"><span data-stu-id="31fc3-131">This task requires a few steps.</span></span> <span data-ttu-id="31fc3-132">Najpierw użyj *** Dodaj — polecenie cmdlet AzureDataDisk ***, aby dodać dysk do obiektu $vm.</span><span class="sxs-lookup"><span data-stu-id="31fc3-132">First, you use the ****Add-AzureDataDisk**** cmdlet to add the disk to the $vm object.</span></span> <span data-ttu-id="31fc3-133">Następnie należy użyć **AzureVM aktualizacji** polecenia cmdlet można zaktualizować konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="31fc3-133">Then, you use **Update-AzureVM** cmdlet to update the configuration of the VM.</span></span>

<span data-ttu-id="31fc3-134">Musisz także zdecydować, czy dołączyć nowy dysk, czy taki, który zawiera dane.</span><span class="sxs-lookup"><span data-stu-id="31fc3-134">You'll also need to decide whether to attach a new disk or one that contains data.</span></span> <span data-ttu-id="31fc3-135">Dla nowego dysku polecenie tworzy plik VHD i dołącza go.</span><span class="sxs-lookup"><span data-stu-id="31fc3-135">For a new disk, the command creates the .vhd file and attaches it.</span></span>

<span data-ttu-id="31fc3-136">Aby dołączyć nowy dysk, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="31fc3-136">To attach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="31fc3-137">Aby dołączyć istniejący dysk danych, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="31fc3-137">To attach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="31fc3-138">Aby dołączyć dyski danych z istniejącego pliku VHD w magazynie obiektów blob, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="31fc3-138">To attach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="31fc3-139">Tworzenie maszyny Wirtualnej z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="31fc3-139">Create a Windows-based VM</span></span>
<span data-ttu-id="31fc3-140">Aby utworzyć nową maszynę wirtualną z systemem Windows na platformie Azure, skorzystaj z instrukcji w [użycia programu Azure PowerShell do tworzenia i wstępnie skonfigurować maszyn wirtualnych z systemem Windows](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="31fc3-140">To create a new Windows-based virtual machine in Azure, use the instructions in [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="31fc3-141">Kroki tego tematu, podczas tworzenia zestawu poleceń programu PowerShell systemu Azure tworzy Maszynę wirtualną z systemem Windows można wstępnie:</span><span class="sxs-lookup"><span data-stu-id="31fc3-141">This topic steps you through the creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="31fc3-142">Z członkostwa w domenie usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="31fc3-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="31fc3-143">W przypadku dodatkowych dysków.</span><span class="sxs-lookup"><span data-stu-id="31fc3-143">With additional disks.</span></span>
* <span data-ttu-id="31fc3-144">Jako element członkowski istniejącej równoważeniem obciążenia należy ustawić.</span><span class="sxs-lookup"><span data-stu-id="31fc3-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="31fc3-145">Za pomocą statycznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="31fc3-145">With a static IP address.</span></span>

