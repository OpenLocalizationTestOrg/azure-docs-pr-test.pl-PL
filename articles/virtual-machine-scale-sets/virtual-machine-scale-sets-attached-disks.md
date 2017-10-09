---
title: "aaaAzure dołączonych dysków danych maszyny wirtualnej skali zestawy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse dołączonych dysków z danymi z zestawy skalowania maszyny wirtualnej"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="a9fc9-103">Zestawy skalowania maszyn wirtualnych platformy Azure i dołączone dyski danych</span><span class="sxs-lookup"><span data-stu-id="a9fc9-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="a9fc9-104">[Zestawy skalowania maszyn wirtualnych](/azure/virtual-machine-scale-sets/) platformy Azure obsługują teraz maszyny wirtualne z dołączonymi dyskami danych.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="a9fc9-105">Dyski danych mogą być definiowane w profilu magazynu powitania dla zestawów skalowania, które zostały utworzone z dyskami zarządzane Azure.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-105">Data disks can be defined in hello storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="a9fc9-106">Wcześniej hello tylko bezpośrednio dołączonego magazynu i opcje maszyn wirtualnych w zestawach skali zostały dysku hello systemu operacyjnego i dysków tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-106">Previously hello only directly attached storage options available with VMs in scale sets were hello OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="a9fc9-107">Podczas tworzenia skali ustawiony za pomocą dysków dołączonych danych zdefiniowany nadal potrzebujesz toomount i format hello dyski z wewnątrz toouse maszyny Wirtualnej je (jak tylko dla autonomicznych maszyn wirtualnych platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="a9fc9-107">When you create a scale set with attached data disks defined, you still need toomount and format hello disks from within a VM toouse them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="a9fc9-108">Toodo wygodny sposób jest toouse rozszerzenia niestandardowego skryptu, który wywołuje toopartition skrypty standardowe i formatowanie hello dysków danych maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-108">A convenient way toodo this is toouse a custom script extension which calls a standard script toopartition and format all hello data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="a9fc9-109">Tworzenie zestawu skalowania z dołączonymi dyskami danych</span><span class="sxs-lookup"><span data-stu-id="a9fc9-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="a9fc9-110">Toocreate prosty sposób skonfigurować skali z dysków dołączonych jest toouse hello [interfejsu wiersza polecenia Azure](https://github.com/Azure/azure-cli) _vmss utworzyć_ polecenia.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-110">A simple way toocreate a scale set with attached disks is toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="a9fc9-111">Witaj poniższy przykład tworzy odpowiednio grupy zasobów platformy Azure oraz zestaw skali maszyny Wirtualnej 10 Ubuntu maszyn wirtualnych mających dyski 2 dołączonych danych, 50 GB i 100 GB.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-111">hello following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="a9fc9-112">Należy pamiętać, że hello _vmss utworzyć_ polecenia domyślnie niektóre wartości konfiguracji, jeśli nie zostanie określony.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-112">Note that hello _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="a9fc9-113">toosee hello dostępne opcje przesłonić spróbuj:</span><span class="sxs-lookup"><span data-stu-id="a9fc9-113">toosee hello available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="a9fc9-114">Inny toocreate sposób skalowania ustawiony za pomocą dysków dołączonych danych jest toodefine skali ustawiona w szablonie usługi Azure Resource Manager obejmują _dataDisks_ części hello _storageProfile_i wdrażanie hello szablon.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-114">Another way toocreate a scale set with attached data disks is toodefine a scale set in an Azure Resource Manager template, include a _dataDisks_ section in hello _storageProfile_, and deploy hello template.</span></span> <span data-ttu-id="a9fc9-115">Hello 50 GB i 100 GB dysku w powyższym przykładzie byłoby zdefiniowane w szablonie hello następująco:</span><span class="sxs-lookup"><span data-stu-id="a9fc9-115">hello 50 GB and 100 GB disk example above would be defined like this in hello template:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
<span data-ttu-id="a9fc9-116">Widać pełną, gotowe toodeploy przykładem szablonu zestaw skali z dysku dołączonym zdefiniowane w tym miejscu: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span><span class="sxs-lookup"><span data-stu-id="a9fc9-116">You can see a complete, ready toodeploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a><span data-ttu-id="a9fc9-117">Dodawanie danych skali istniejącego dysku tooan ustawić</span><span class="sxs-lookup"><span data-stu-id="a9fc9-117">Adding a data disk tooan existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="a9fc9-118">Można dołączać zestaw skali tooa dysków danych, która została utworzona z [dysków zarządzanych Azure](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="a9fc9-118">You can only attach data disks tooa scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="a9fc9-119">Można dodać dysku danych tooa skalowania maszyny Wirtualnej ustawić za pomocą interfejsu wiersza polecenia Azure _dołączyć dysku vmss az_ polecenia.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-119">You can add a data disk tooa VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="a9fc9-120">Należy pamiętać o określeniu właściwości lun, która nie jest jeszcze używana.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="a9fc9-121">Poniższy przykład CLI Hello dodaje toolun dysk 50 GB 3:</span><span class="sxs-lookup"><span data-stu-id="a9fc9-121">hello following CLI example adds a 50 GB drive toolun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="a9fc9-122">Poniższy przykład PowerShell Hello dodaje toolun dysk 50 GB 3:</span><span class="sxs-lookup"><span data-stu-id="a9fc9-122">hello following PowerShell example adds a 50 GB drive toolun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="a9fc9-123">Różne rozmiary maszyny Wirtualnej mają różne limity na powitania liczby dołączone dyski, które obsługują.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-123">Different VM sizes have different limits on hello numbers of attached drives they support.</span></span> <span data-ttu-id="a9fc9-124">Sprawdź hello [właściwości rozmiar maszyny wirtualnej](../virtual-machines/windows/sizes.md) przed dodaniem nowego dysku.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-124">Check hello [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="a9fc9-125">Możesz także dodać dysk, dodając nowe toohello wpis _dataDisks_ właściwości w hello _storageProfile_ skalę Ustaw definicji i stosowania hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-125">You can also add a disk by adding a new entry toohello _dataDisks_ property in hello _storageProfile_ of a scale set definition and applying hello change.</span></span> <span data-ttu-id="a9fc9-126">tootest, Znajdź istniejącej definicji zestawu skali w hello [Eksploratora zasobów Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a9fc9-126">tootest this, find an existing scale set definition in hello [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="a9fc9-127">Wybierz _Edytuj_ i Dodaj nowy dysk toohello listę dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-127">Select _Edit_ and add a new disk toohello list of data disks.</span></span> <span data-ttu-id="a9fc9-128">Na przykład</span><span class="sxs-lookup"><span data-stu-id="a9fc9-128">E.g.</span></span> <span data-ttu-id="a9fc9-129">za pomocą powyższego przykładu hello:</span><span class="sxs-lookup"><span data-stu-id="a9fc9-129">using hello example above:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

<span data-ttu-id="a9fc9-130">Następnie wybierz _PUT_ tooapply hello zmienia tooyour zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-130">Then select _PUT_ tooapply hello changes tooyour scale set.</span></span> <span data-ttu-id="a9fc9-131">Ten przykład sprawdzi się w przypadku korzystania z takiego rozmiaru maszyny wirtualnej, który zapewnia obsługę więcej niż dwóch dołączonych dysków danych.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="a9fc9-132">Po wprowadzeniu zmiany skali tooa ustawić definicji, takie jak dodawanie lub usuwanie dysk z danymi, stosuje tooall nowo tworzone maszyny wirtualne, ale tylko w przypadku maszyn wirtualnych tooexisting hello _upgradePolicy_ właściwość jest ustawiona zbyt "Automatyczny".</span><span class="sxs-lookup"><span data-stu-id="a9fc9-132">When you make a change tooa scale set definition such as adding or removing a data disk, it applies tooall newly created VMs, but only applies tooexisting VMs if hello _upgradePolicy_ property is set too"Automatic".</span></span> <span data-ttu-id="a9fc9-133">Jeśli jest ustawiona zbyt "Manual", należy toomanually zastosować hello nowego modelu tooexisting maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-133">If it is set too"Manual", you need toomanually apply hello new model tooexisting VMs.</span></span> <span data-ttu-id="a9fc9-134">Można to zrobić w portalu hello przy użyciu hello _AzureRmVmssInstance aktualizacji_ PowerShell polecenia lub przy użyciu hello _vmss az update wystąpienia_ polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-134">You can do this in hello portal, using hello _Update-AzureRmVmssInstance_ PowerShell command, or using hello _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a><span data-ttu-id="a9fc9-135">Dodawanie zestawu skalowania istniejących tooan dysków danych wstępnie wypełnione</span><span class="sxs-lookup"><span data-stu-id="a9fc9-135">Adding pre-populated data disks tooan existent scale set</span></span> 
> <span data-ttu-id="a9fc9-136">Podczas dodawania dysków tooan istniejących zestawu skalowania modelu, zgodnie z projektem, dysku hello tworzony jest zawsze pusta.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-136">When you add disks tooan existent scale set model, by design, hello disk will always be created empty.</span></span> <span data-ttu-id="a9fc9-137">Ten scenariusz obejmuje też nowe wystąpienia utworzone przez zestaw skali hello.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-137">This scenario also includes new instances created by hello scale set.</span></span> <span data-ttu-id="a9fc9-138">To zachowanie jest ponieważ definicji scaleset hello ma dysk danych puste.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-138">This behaviour is because hello scaleset definition has an empty data disk.</span></span> <span data-ttu-id="a9fc9-139">W kolejności toocreate wstępnie wypełnione dysków z danymi dla modelu zestawu skali istniejących można wybrać jedną z poniższych dwóch opcji:</span><span class="sxs-lookup"><span data-stu-id="a9fc9-139">In order toocreate pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="a9fc9-140">Kopiowanie danych z hello wystąpienie 0 wirtualna toohello danych dyski w hello innych maszyn wirtualnych przez uruchomienie skryptu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-140">Copy data from hello instance 0 VM toohello data disk(s) in hello other VMs by running a custom script.</span></span>
* <span data-ttu-id="a9fc9-141">Tworzenie zarządzanego obrazu w przypadku dysku hello systemu operacyjnego oraz danych dysku (z danymi hello wymagane) i Utwórz nowe scaleset z hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-141">Create a managed image with hello OS disk plus data disk (with hello required data) and create a new scaleset with hello image.</span></span> <span data-ttu-id="a9fc9-142">W ten sposób każdy nowej maszyny Wirtualnej utworzone będzie mieć danych na dysku czy znajduje się w definicji hello hello scaleset.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-142">This way every new VM created will have a data disk that that is provided in hello definition of hello scaleset.</span></span> <span data-ttu-id="a9fc9-143">Ponieważ ta definicja będzie odnosić się tooan obrazu dysku danych, który został dostosowany danych, co maszyny wirtualnej na powitania scaleset automatycznie rozpocznie pracę z tych zmian.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-143">Since this definition will refer tooan image with a data disk that has customized data, every virtual machine on hello scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="a9fc9-144">Witaj toocreate sposób niestandardowego obrazu można znaleźć tutaj: [tworzenie zarządzanego obrazu uogólniony maszyny wirtualnej na platformie Azure](/azure/virtual-machines/windows/capture-image-resource/)</span><span class="sxs-lookup"><span data-stu-id="a9fc9-144">hello way toocreate a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="a9fc9-145">Witaj użytkownik potrzebuje toocapture hello 0 maszyny Wirtualnej, która ma hello wymagane dane wystąpienia, a następnie użyj tego wirtualnego dysku twardego dla definicji obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-145">hello user needs toocapture hello instance 0 VM which has hello required data, and then use that vhd for hello image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="a9fc9-146">Usuwanie dysku danych z zestawu skalowania</span><span class="sxs-lookup"><span data-stu-id="a9fc9-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="a9fc9-147">Dysk danych można usunąć z zestawu skalowania maszyn wirtualnych przy użyciu polecenia _az vmss disk detach_ interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="a9fc9-148">Na przykład hello następujące polecenie usuwa hello dysk zdefiniowane w jednostce lun 2:</span><span class="sxs-lookup"><span data-stu-id="a9fc9-148">For example hello following command removes hello disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="a9fc9-149">Podobnie można również usunąć dysk z skali ustawiony przez usunięcie wpisu z hello _dataDisks_ właściwości w hello _storageProfile_ i stosowanie hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-149">Similarly you can also remove a disk from a scale set by removing an entry from hello _dataDisks_ property in hello _storageProfile_ and applying hello change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="a9fc9-150">Uwagi dodatkowe</span><span class="sxs-lookup"><span data-stu-id="a9fc9-150">Additional notes</span></span>
<span data-ttu-id="a9fc9-151">Pomoc dla dysków Azure zarządzane i skalę zestawu dysków dołączonych danych jest dostępna w wersji interfejsu API [ _2016-04-30-preview_ ](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) lub nowszej hello Microsoft.Compute interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of hello Microsoft.Compute API.</span></span>

<span data-ttu-id="a9fc9-152">W implementacji początkowej hello dołączono dysk wsparcia dla zestawów skalowania nie można dołączyć lub odłączyć dysków danych z poszczególnych maszyn wirtualnych w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-152">In hello initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="a9fc9-153">W witrynie Azure Portal obsługa dołączonych dysków danych w zestawach skalowania jest wstępnie ograniczona.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="a9fc9-154">W zależności od wymagań, których można użyć szablonów platformy Azure interfejsu wiersza polecenia programu PowerShell, zestawy SDK i interfejsu API REST toomanage dołączone dyski.</span><span class="sxs-lookup"><span data-stu-id="a9fc9-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API toomanage attached disks.</span></span>


