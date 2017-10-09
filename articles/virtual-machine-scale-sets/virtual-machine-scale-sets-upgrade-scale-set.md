---
title: zestaw skalowania maszyny wirtualnej platformy Azure aaaUpgrade | Dokumentacja firmy Microsoft
description: Uaktualnij zestaw skali maszyny wirtualnej platformy Azure
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="675b3-103">Uaktualnij zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="675b3-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="675b3-104">W tym artykule opisano, jak wdrożenie aktualizacji systemu operacyjnego tooan skali maszyny wirtualnej platformy Azure bez żadnego przestoju.</span><span class="sxs-lookup"><span data-stu-id="675b3-104">This article describes how you can roll out an OS update tooan Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="675b3-105">W tym kontekście aktualizacji systemu operacyjnego obejmuje zmiana wersji hello lub SKU hello systemu operacyjnego lub zmiana hello identyfikatora URI obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="675b3-105">In this context, an OS update involves changing hello version or SKU of hello OS or changing hello URI of a custom image.</span></span> <span data-ttu-id="675b3-106">Aktualizowanie bez przestojów aktualizowanie maszyn wirtualnych co pojedynczo lub w grupach (na przykład w jednej domenie błędów w czasie) zamiast jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="675b3-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="675b3-107">W ten sposób można zachować uruchomiona żadnych maszyn wirtualnych, które nie jest uaktualniany.</span><span class="sxs-lookup"><span data-stu-id="675b3-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="675b3-108">niejednoznaczności tooavoid pozwala odróżnić cztery typy aktualizacji systemu operacyjnego może być tooperform:</span><span class="sxs-lookup"><span data-stu-id="675b3-108">tooavoid ambiguity, let’s distinguish four types of OS update you might want tooperform:</span></span>

* <span data-ttu-id="675b3-109">Zmiana wersji hello lub jednostka SKU obrazu platformy.</span><span class="sxs-lookup"><span data-stu-id="675b3-109">Changing hello version or SKU of a platform image.</span></span> <span data-ttu-id="675b3-110">Na przykład zmiana Ubuntu wersji 14.04.2-LTS z 14.04.201506100 too14.04.201507060 lub zmiana hello Ubuntu 15.10/najnowszej wersji too16.04.0-LTS/latest.</span><span class="sxs-lookup"><span data-stu-id="675b3-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 too14.04.201507060, or changing hello Ubuntu 15.10/latest SKU too16.04.0-LTS/latest.</span></span> <span data-ttu-id="675b3-111">W tym scenariuszu są omówione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="675b3-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="675b3-112">Zmiana hello identyfikator URI, który wskazuje tooa nowej wersji zostanie utworzony niestandardowy obraz (**właściwości** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **obrazu** > **uri**).</span><span class="sxs-lookup"><span data-stu-id="675b3-112">Changing hello URI that points tooa new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="675b3-113">W tym scenariuszu są omówione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="675b3-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="675b3-114">Zmiana hello odwołanie do obrazu zestawu skalowania, który został utworzony przy użyciu dysków zarządzanych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="675b3-114">Changing hello image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="675b3-115">Stosowanie poprawek hello systemu operacyjnego z poziomu maszyny wirtualnej (to przykłady instalowania poprawki zabezpieczeń i uruchamiania usługi Windows Update).</span><span class="sxs-lookup"><span data-stu-id="675b3-115">Patching hello OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="675b3-116">Ten scenariusz jest obsługiwany, ale nie zostały omówione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="675b3-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="675b3-117">Zestawy skalowania maszyn wirtualnych, które są wdrażane w ramach [sieć szkieletowa usług Azure](https://azure.microsoft.com/services/service-fabric/) klastra nie zostały omówione w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="675b3-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="675b3-118">Zobacz [poprawka systemu operacyjnego Windows w klastrze usługi sieć szkieletowa](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) Aby uzyskać więcej informacji na temat stosowania poprawek sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="675b3-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="675b3-119">Witaj podstawowe sekwencji zmiany hello systemu operacyjnego wersji lub jednostki SKU obrazu platformy lub hello URI niestandardowy obraz wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="675b3-119">hello basic sequence for changing hello OS version/SKU of a platform image or hello URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="675b3-120">Pobierz modelu zestawu skali maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="675b3-120">Get hello virtual machine scale set model.</span></span>
2. <span data-ttu-id="675b3-121">Zmień wersję hello, jednostka SKU, odwołanie do obrazu lub wartość identyfikatora URI w modelu hello.</span><span class="sxs-lookup"><span data-stu-id="675b3-121">Change hello version, SKU, image reference, or URI value in hello model.</span></span>
3. <span data-ttu-id="675b3-122">Model hello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="675b3-122">Update hello model.</span></span>
4. <span data-ttu-id="675b3-123">Czy *manualUpgrade* wywołać na maszynach wirtualnych hello w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="675b3-123">Do a *manualUpgrade* call on hello virtual machines in hello scale set.</span></span> <span data-ttu-id="675b3-124">Ten krok ma zastosowanie tylko jeśli *upgradePolicy* ustawiono zbyt**ręcznego** w zestawie skalowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="675b3-124">This step is only relevant if *upgradePolicy* is set too**Manual** in your scale set.</span></span> <span data-ttu-id="675b3-125">Jeśli ustawiono zbyt**automatyczne**, wszystkie maszyny wirtualne hello są uaktualniane na raz, powodując przestoje.</span><span class="sxs-lookup"><span data-stu-id="675b3-125">If it is set too**Automatic**, all hello virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="675b3-126">Dzięki tym informacjom pamiętać Zobaczmy, jak można zaktualizować wersji hello skali, ustaw w programie PowerShell i przy użyciu hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="675b3-126">With this information in mind, let’s see how you could update hello version of a scale set in PowerShell, and by using hello REST API.</span></span> <span data-ttu-id="675b3-127">Te przykłady obejmują hello przypadku obrazu platformy, ale ten artykuł zawiera odpowiednią ilość informacji w przypadku tooadapt obraz niestandardowy tooa procesu.</span><span class="sxs-lookup"><span data-stu-id="675b3-127">These examples cover hello case of a platform image, but this article provides enough information for you tooadapt this process tooa custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="675b3-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="675b3-128">PowerShell</span></span>
<span data-ttu-id="675b3-129">W tym przykładzie aktualizuje zestaw skali maszyny wirtualnej systemu Windows (Tworzenie toohello nową wersję 4.0.20160229.</span><span class="sxs-lookup"><span data-stu-id="675b3-129">This example updates a Windows virtual machine scale set (creating toohello new version 4.0.20160229.</span></span> <span data-ttu-id="675b3-130">Po zaktualizowaniu modelu hello, robi aktualizacji jedno wystąpienie maszyny wirtualnej w czasie.</span><span class="sxs-lookup"><span data-stu-id="675b3-130">After updating hello model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="675b3-131">Aktualizowania hello identyfikatora URI dla niestandardowego obrazu zamiast zmiana wersji obrazu platformy, zastąp "zestaw hello nową wersję" hello wiersza polecenia, który zaktualizuje hello obrazu źródłowego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="675b3-131">If you are updating hello URI for a custom image instead of changing a platform image version, replace hello “set hello new version” line with a command that will update hello source image URI.</span></span> <span data-ttu-id="675b3-132">Na przykład jeśli zestaw skali hello został utworzony bez użycia dysków zarządzanych Azure, hello aktualizacji będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="675b3-132">For example, if hello scale set was created without using Azure Managed Disks, hello update would look like this:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="675b3-133">Jeśli obraz niestandardowy na podstawie zestawu skalowania został utworzony przy użyciu dysków zarządzanych Azure, a następnie będzie można zaktualizować hello odwołanie do obrazu.</span><span class="sxs-lookup"><span data-stu-id="675b3-133">If a custom image based scale set was created using Azure Managed Disks, then hello image reference would be updated.</span></span> <span data-ttu-id="675b3-134">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="675b3-134">For example:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a><span data-ttu-id="675b3-135">Witaj interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="675b3-135">hello REST API</span></span>
<span data-ttu-id="675b3-136">Oto kilka przykładów Python, które używają tooroll interfejsu API REST Azure hello limit aktualizacji wersji systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="675b3-136">Here are a couple of Python examples that use hello Azure REST API tooroll out an OS version update.</span></span> <span data-ttu-id="675b3-137">Oba rozwiązania używają hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) biblioteki interfejsu API REST Azure otoki funkcje toodo GET skali hello ustawić modelu, następuje PUT z zaktualizowanym modelu.</span><span class="sxs-lookup"><span data-stu-id="675b3-137">Both use hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions toodo a GET on hello scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="675b3-138">One również sprawdzić widoków wystąpień maszyny wirtualnej maszyny wirtualne hello tooidentify według domeny aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="675b3-138">They also look at virtual machine instances views tooidentify hello virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="675b3-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="675b3-139">Vmssupgrade</span></span>
 <span data-ttu-id="675b3-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) jest skrypt języka Python, który został użyty tooroll limit tooa uaktualnienia systemu operacyjnego systemem skalowania maszyny wirtualnej ustawić jednej domeny aktualizacji w czasie.</span><span class="sxs-lookup"><span data-stu-id="675b3-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used tooroll out an OS upgrade tooa running virtual machine scale set one update domain at a time.</span></span>

![Skrypt Vmssupgrade dotyczące wybierania maszyn wirtualnych lub domeny aktualizacji](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="675b3-142">Ten skrypt pozwala wybrać tooupdate określone maszyny wirtualne lub określ domenę aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="675b3-142">This script lets you choose specific virtual machines tooupdate or specify an update domain.</span></span> <span data-ttu-id="675b3-143">Obsługuje ona zmiana wersji obrazu platformy lub zmiana hello identyfikatora URI obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="675b3-143">It supports changing a platform image version or changing hello URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="675b3-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="675b3-144">Vmsseditor</span></span>
<span data-ttu-id="675b3-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) jest Edytor ogólnego przeznaczenia dla zestawy skalowania maszyn wirtualnych, które pokazuje wirtualnej maszynie stan jako heatmap gdzie jeden wiersz odpowiada jednej domeny aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="675b3-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="675b3-146">Między innymi można zaktualizować modelu powitania dla zestawu skalowania o nowej wersji, jednostki SKU lub obraz niestandardowy identyfikator URI, a następnie wybierz tooupgrade domen błędów.</span><span class="sxs-lookup"><span data-stu-id="675b3-146">Among other things, you can update hello model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains tooupgrade.</span></span> <span data-ttu-id="675b3-147">Po wykonaniu tej czynności wszystkich hello maszyn wirtualnych w tej domenie aktualizacji są uaktualnionego toohello nowego modelu.</span><span class="sxs-lookup"><span data-stu-id="675b3-147">When you do so, all hello virtual machines in that update domain are upgraded toohello new model.</span></span> <span data-ttu-id="675b3-148">Alternatywnie można wykonać uaktualnienia stopniowego na podstawie rozmiaru partii hello wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="675b3-148">Alternatively, you can do a rolling upgrade based on hello batch size of your choice.</span></span>  

<span data-ttu-id="675b3-149">Witaj Poniższy zrzut ekranu przedstawia model dla Ubuntu 14.04-2LTS wersji 14.04.201507060 skali.</span><span class="sxs-lookup"><span data-stu-id="675b3-149">hello following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="675b3-150">Wiele więcej opcji dodano narzędzia toothis ponieważ wykonano tego zrzutu ekranu.</span><span class="sxs-lookup"><span data-stu-id="675b3-150">Many more options have been added toothis tool since this screenshot was taken.</span></span>

![Model Vmsseditor skali, ustaw dla Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="675b3-152">Po kliknięciu **uaktualnienia** , a następnie **Pobierz szczegóły**, tooupdate start maszyn wirtualnych w UD 0.</span><span class="sxs-lookup"><span data-stu-id="675b3-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start tooupdate.</span></span>

![Trwa aktualizacja przedstawiający Vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

