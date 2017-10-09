---
title: "aaaManage maszyn wirtualnych przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej poleceń służy tooautomate zadań zarządzania maszyn wirtualnych."
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
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="4a2db-103">Zarządzanie maszynami wirtualnymi przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a2db-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="4a2db-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4a2db-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4a2db-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="4a2db-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4a2db-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4a2db-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="4a2db-107">Przy użyciu modelu Resource Manager hello typowych poleceń programu PowerShell, zobacz [tutaj](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4a2db-107">For common PowerShell commands using hello Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="4a2db-108">Wiele zadań, czy maszyny wirtualne toomanage każdego dnia można zautomatyzować za pomocą poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a2db-108">Many tasks you do each day toomanage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="4a2db-109">Ten artykuł zawiera przykładowe polecenia zadania prostszy i tooarticles łącza, zawierające hello polecenia dla bardziej złożonych zadań.</span><span class="sxs-lookup"><span data-stu-id="4a2db-109">This article gives you example commands for simpler tasks, and links tooarticles that show hello commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="4a2db-110">Jeśli nie zostało to jeszcze zainstalowaniu i skonfigurowaniu programu Azure PowerShell, ale można wyświetlić instrukcje w artykule hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4a2db-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-toouse-hello-example-commands"></a><span data-ttu-id="4a2db-111">Jak toouse hello przykładowe polecenia</span><span class="sxs-lookup"><span data-stu-id="4a2db-111">How toouse hello example commands</span></span>
<span data-ttu-id="4a2db-112">Będziesz potrzebować tooreplace część tekstu hello w hello poleceń z tekstem, który jest odpowiedni dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="4a2db-112">You'll need tooreplace some of hello text in hello commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="4a2db-113">Witaj < i > symbole wskazują należy tooreplace tekstu.</span><span class="sxs-lookup"><span data-stu-id="4a2db-113">hello < and > symbols indicate text you need tooreplace.</span></span> <span data-ttu-id="4a2db-114">Zastąp tekst hello, Usuń symbole hello, ale pozostawić hello znaki cudzysłowu w miejscu.</span><span class="sxs-lookup"><span data-stu-id="4a2db-114">When you replace hello text, remove hello symbols but leave hello quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="4a2db-115">Uzyskiwanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4a2db-115">Get a VM</span></span>
<span data-ttu-id="4a2db-116">Jest to podstawowe zadania, które będzie używane.</span><span class="sxs-lookup"><span data-stu-id="4a2db-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="4a2db-117">Używać jej tooget informacji o maszynie Wirtualnej, wykonywania zadań na maszynie Wirtualnej lub pobrać dane wyjściowe toostore w zmiennej.</span><span class="sxs-lookup"><span data-stu-id="4a2db-117">Use it tooget information about a VM, perform tasks on a VM, or get output toostore in a variable.</span></span>

<span data-ttu-id="4a2db-118">tooget informacji na temat hello maszynę Wirtualną, uruchom następujące polecenie, zastępując wszystko w cudzysłowy hello, w tym hello < i > znaków:</span><span class="sxs-lookup"><span data-stu-id="4a2db-118">tooget information about hello VM, run this command, replacing everything in hello quotes, including hello < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="4a2db-119">dane wyjściowe w zmiennej $vm hello toostore Uruchom:</span><span class="sxs-lookup"><span data-stu-id="4a2db-119">toostore hello output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a><span data-ttu-id="4a2db-120">Zaloguj się na tooa maszyny Wirtualnej z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="4a2db-120">Log on tooa Windows-based VM</span></span>
<span data-ttu-id="4a2db-121">Uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="4a2db-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="4a2db-122">Witaj maszyny wirtualnej i nazwa usługi w chmurze można uzyskać z widoku hello hello **Get-AzureVM** polecenia.</span><span class="sxs-lookup"><span data-stu-id="4a2db-122">You can get hello virtual machine and cloud service name from hello display of hello **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="4a2db-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< dysk i folder lokalizacji toostore hello pobrany plik RDP, na przykład: c:\temp >" $localFile = $localPath + "\" $vmname +"RDP"Get-AzureRemoteDesktopFile - ServiceName $svcName-Name $vmName - LocalPath $localFile — uruchamianie</span><span class="sxs-lookup"><span data-stu-id="4a2db-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location toostore hello downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="4a2db-124">Zatrzymywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4a2db-124">Stop a VM</span></span>
<span data-ttu-id="4a2db-125">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4a2db-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="4a2db-126">Użyj tego hello tookeep parametru wirtualnego adresu IP (VIP) hello chmury usługi, w razie hello ostatnia maszyna wirtualna w tej usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="4a2db-126">Use this parameter tookeep hello virtual IP (VIP) of hello cloud service in case it's hello last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="4a2db-127">Jeśli parametr hello StayProvisioned, nadal zostaną naliczone opłaty dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4a2db-127">If you use hello StayProvisioned parameter, you'll still be billed for hello VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="4a2db-128">Uruchamianie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4a2db-128">Start a VM</span></span>
<span data-ttu-id="4a2db-129">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4a2db-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="4a2db-130">Dołączanie dysku danych</span><span class="sxs-lookup"><span data-stu-id="4a2db-130">Attach a data disk</span></span>
<span data-ttu-id="4a2db-131">To zadanie wymaga kilku kroków.</span><span class="sxs-lookup"><span data-stu-id="4a2db-131">This task requires a few steps.</span></span> <span data-ttu-id="4a2db-132">Najpierw użyj hello *** Add-AzureDataDisk *** polecenia cmdlet tooadd hello dysku toohello $vm obiektu.</span><span class="sxs-lookup"><span data-stu-id="4a2db-132">First, you use hello ****Add-AzureDataDisk**** cmdlet tooadd hello disk toohello $vm object.</span></span> <span data-ttu-id="4a2db-133">Następnie należy użyć **AzureVM aktualizacji** polecenia cmdlet tooupdate hello konfiguracji hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4a2db-133">Then, you use **Update-AzureVM** cmdlet tooupdate hello configuration of hello VM.</span></span>

<span data-ttu-id="4a2db-134">Należy również toodecide czy tooattach nowy dysk lub jeden zawierający dane.</span><span class="sxs-lookup"><span data-stu-id="4a2db-134">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="4a2db-135">Dla nowego dysku hello polecenie tworzy plik VHD hello i dołącza go.</span><span class="sxs-lookup"><span data-stu-id="4a2db-135">For a new disk, hello command creates hello .vhd file and attaches it.</span></span>

<span data-ttu-id="4a2db-136">tooattach nowego dysku, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4a2db-136">tooattach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="4a2db-137">tooattach istniejący dysk danych, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4a2db-137">tooattach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="4a2db-138">tooattach dysków danych z istniejącego pliku VHD w magazynie obiektów blob, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4a2db-138">tooattach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="4a2db-139">Tworzenie maszyny Wirtualnej z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="4a2db-139">Create a Windows-based VM</span></span>
<span data-ttu-id="4a2db-140">toocreate nowej systemu Windows maszyny wirtualnej na platformie Azure, użyj instrukcji hello w [toocreate użycia programu Azure PowerShell i wstępnie skonfigurować maszyn wirtualnych z systemem Windows](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4a2db-140">toocreate a new Windows-based virtual machine in Azure, use hello instructions in [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="4a2db-141">Kroki tego tematu użytkownika przez proces tworzenia hello programu Azure PowerShell zestawu poleceń tworzy Maszynę wirtualną z systemem Windows można wstępnie:</span><span class="sxs-lookup"><span data-stu-id="4a2db-141">This topic steps you through hello creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="4a2db-142">Z członkostwa w domenie usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a2db-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="4a2db-143">W przypadku dodatkowych dysków.</span><span class="sxs-lookup"><span data-stu-id="4a2db-143">With additional disks.</span></span>
* <span data-ttu-id="4a2db-144">Jako element członkowski istniejącej równoważeniem obciążenia należy ustawić.</span><span class="sxs-lookup"><span data-stu-id="4a2db-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="4a2db-145">Za pomocą statycznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="4a2db-145">With a static IP address.</span></span>

