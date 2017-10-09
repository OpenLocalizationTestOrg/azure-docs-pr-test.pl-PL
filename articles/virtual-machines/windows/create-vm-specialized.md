---
title: aaaCreate maszyny Wirtualnej systemu Windows z specjalne wirtualnego dysku twardego na platformie Azure | Dokumentacja firmy Microsoft
description: "Utwórz nową maszynę Wirtualną systemu Windows przez dołączenie specjalne dysków zarządzanych jako dysk systemu operacyjnego hello przy użyciu modelu wdrażania Menedżera zasobów hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="5ae6e-103">Tworzenie maszyny Wirtualnej systemu Windows z dysku specjalne</span><span class="sxs-lookup"><span data-stu-id="5ae6e-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="5ae6e-104">Dołączanie specjalne dysków zarządzanych jako dysk systemu operacyjnego hello przy użyciu programu Powershell, aby utworzyć nową maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-104">Create a new VM by attaching a specialized managed disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="5ae6e-105">Specjalne dysku jest kopią wirtualnego dysku twardego (VHD) z istniejącej maszyny Wirtualnej utworzonej hello kont użytkowników, aplikacji i innych danych o stanie z oryginalnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains hello user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="5ae6e-106">Użycie specjalnych toocreate wirtualnego dysku twardego nowej maszyny Wirtualnej, powitalne nowej maszyny Wirtualnej zachowuje nazwy komputera hello hello oryginalna maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-106">When you use a specialized VHD toocreate a new VM, hello new VM retains hello computer name of hello original VM.</span></span> <span data-ttu-id="5ae6e-107">Inne informacje specyficzne dla komputera jest również przechowywać, a w niektórych przypadkach te informacje zduplikowane może spowodować problemy.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="5ae6e-108">Należy pamiętać o jakie rodzaje informacji specyficznych dla komputera aplikacje zależne od podczas kopiowania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="5ae6e-109">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="5ae6e-109">You have two options:</span></span>
* [<span data-ttu-id="5ae6e-110">Przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="5ae6e-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="5ae6e-111">Skopiuj istniejącej maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="5ae6e-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="5ae6e-112">W tym temacie przedstawiono sposób toouse zarządzania dyskami.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-112">This topic shows you how toouse managed disks.</span></span> <span data-ttu-id="5ae6e-113">Jeśli masz wdrożenie starszych wymagający przy użyciu konta magazynu, zobacz [utworzyć Maszynę wirtualną z wirtualnego dysku twardego specjalne konta magazynu](sa-create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="5ae6e-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5ae6e-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="5ae6e-114">Before you begin</span></span>
<span data-ttu-id="5ae6e-115">Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję hello modułu AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="5ae6e-116">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5ae6e-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="5ae6e-117">Opcja 1: Przekazanie specjalne dysku VHD</span><span class="sxs-lookup"><span data-stu-id="5ae6e-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="5ae6e-118">Możesz przekazać powitalne wirtualnego dysku twardego z specjalistyczne maszyny Wirtualnej utworzone za pomocą wirtualizacji narzędzia lokalnych, takich jak funkcja Hyper-V lub maszyny Wirtualnej wyeksportowane z innej chmury.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-118">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="5ae6e-119">Przygotowanie hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5ae6e-119">Prepare hello VM</span></span>
<span data-ttu-id="5ae6e-120">Jeśli planujesz toouse hello wirtualnego dysku twardego — jest toocreate nowej maszyny Wirtualnej, upewnij się, hello następujące kroki zostały zakończone.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-120">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="5ae6e-121">[Przygotowanie tooAzure tooupload wirtualnego dysku twardego Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5ae6e-121">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5ae6e-122">**Nie** generalize hello maszyny Wirtualnej przy użyciu narzędzia Sysprep.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-122">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="5ae6e-123">Usuń wszystkie narzędzia wirtualizacji gościa i agentów, które są zainstalowane na powitania maszyny Wirtualnej (np. narzędzi VMware).</span><span class="sxs-lookup"><span data-stu-id="5ae6e-123">Remove any guest virtualization tools and agents that are installed on hello VM (like VMware tools).</span></span>
  * <span data-ttu-id="5ae6e-124">Upewnij się, hello maszyna wirtualna jest skonfigurowana toopull jego adres IP i ustawienia DNS za pośrednictwem protokołu DHCP.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-124">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="5ae6e-125">To zapewnia, że ten serwer hello uzyskuje adres IP w ramach hello sieci wirtualnej podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-125">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="5ae6e-126">Pobierz hello konta magazynu</span><span class="sxs-lookup"><span data-stu-id="5ae6e-126">Get hello storage account</span></span>
<span data-ttu-id="5ae6e-127">Potrzebny jest magazyn konta w hello Azure toostore przekazać wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-127">You need a storage account in Azure toostore hello uploaded VHD.</span></span> <span data-ttu-id="5ae6e-128">Możesz użyć istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="5ae6e-129">tooshow hello dostępny magazyn kont, wpisz:</span><span class="sxs-lookup"><span data-stu-id="5ae6e-129">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="5ae6e-130">Jeśli chcesz toouse istniejącego konta magazynu, przejdź toohello [hello przekazywanie wirtualnego dysku twardego](#upload-the-vhd-to-your-storage-account) sekcji.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-130">If you want toouse an existing storage account, proceed toohello [Upload hello VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="5ae6e-131">Jeśli potrzebujesz toocreate konta magazynu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5ae6e-131">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="5ae6e-132">Potrzebna jest nazwa hello hello grupy zasobów, których można utworzyć konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-132">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="5ae6e-133">toofind limit wszystkie hello grupy zasobów, które są w ramach subskrypcji, wpisz:</span><span class="sxs-lookup"><span data-stu-id="5ae6e-133">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="5ae6e-134">Grupa zasobów o nazwie toocreate *myResourceGroup* w hello *zachodnie stany USA* regionu, wpisz:</span><span class="sxs-lookup"><span data-stu-id="5ae6e-134">toocreate a resource group named *myResourceGroup* in hello *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="5ae6e-135">Utwórz konto magazynu o nazwie *mojekontomagazynu* w tej grupie zasobów za pomocą hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5ae6e-135">Create a storage account named *mystorageaccount* in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="5ae6e-136">Przekaż konta magazynu tooyour wirtualnego dysku twardego hello</span><span class="sxs-lookup"><span data-stu-id="5ae6e-136">Upload hello VHD tooyour storage account</span></span> 
<span data-ttu-id="5ae6e-137">Użyj hello [AzureRmVhd Dodaj](/powershell/module/azurerm.compute/add-azurermvhd) polecenia cmdlet tooupload hello wirtualnego dysku twardego tooa kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-137">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="5ae6e-138">W tym przykładzie przekazywania hello pliku *myVHD.vhd* z `"C:\Users\Public\Documents\Virtual hard disks\"` tooa konto magazynu o nazwie *mojekontomagazynu* w hello *myResourceGroup* grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-138">This example uploads hello file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="5ae6e-139">Plik Hello jest przechowywany w kontenerze hello o nazwie *mojkontener* i będzie hello nową nazwę pliku *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-139">hello file is stored in hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="5ae6e-140">W przypadku powodzenia można uzyskać odpowiedzi, która wygląda podobnie toothis:</span><span class="sxs-lookup"><span data-stu-id="5ae6e-140">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="5ae6e-141">W zależności od połączenia sieciowego i hello rozmiar pliku VHD, polecenie to może chwilę potrwać toocomplete</span><span class="sxs-lookup"><span data-stu-id="5ae6e-141">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

### <a name="create-a-managed-disk-from-hello-vhd"></a><span data-ttu-id="5ae6e-142">Tworzenie dysku zarządzanego z hello wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="5ae6e-142">Create a managed disk from hello VHD</span></span>

<span data-ttu-id="5ae6e-143">Tworzenie dysku zarządzanego z hello specjalizowany wirtualnego dysku twardego za pomocą konta magazynu [AzureRMDisk nowy](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="5ae6e-143">Create a managed disk from hello specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="5ae6e-144">W tym przykładzie użyto **myOSDisk1** nazwa dysku hello naraża hello dysku w *StandardLRS* magazynu i używa *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* jako hello identyfikatora URI źródła hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-144">This example uses **myOSDisk1** for hello disk name, puts hello disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as hello URI for hello source VHD.</span></span>

<span data-ttu-id="5ae6e-145">Utwórz nową grupę zasobów dla hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-145">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="5ae6e-146">Utwórz nowy dysk systemu operacyjnego hello z hello przekazany wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-146">Create hello new OS disk from hello uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="5ae6e-147">Opcja 2: Kopiowanie istniejącej maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="5ae6e-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="5ae6e-148">Można utworzyć kopii maszyny wirtualnej używa zarządza dysków migawki hello maszyny Wirtualnej, a następnie za pomocą tej migawki toocreate nowy managed dysku i nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-148">You can create a copy of a VM that uses managed disks by taking a snapshot of hello VM, then using that snapshot toocreate a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-hello-os-disk"></a><span data-ttu-id="5ae6e-149">Utwórz migawkę hello dysk systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="5ae6e-149">Take a snapshot of hello OS disk</span></span>

<span data-ttu-id="5ae6e-150">Można wykonać migawki elementu i całej maszyny Wirtualnej (w tym wszystkie dyski) lub tylko jednego dysku.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="5ae6e-151">Witaj poniższej procedurze pokazano, jak hello tootake migawki tylko hello systemu operacyjnego dysk przy użyciu maszyny Wirtualnej [AzureRmSnapshot nowy](/powershell/module/azurerm.compute/new-azurermsnapshot) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-151">hello following steps show you how tootake a snapshot of just hello OS disk of your VM using hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="5ae6e-152">Ustaw niektórych parametrów.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="5ae6e-153">Pobierz obiekt VM hello.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-153">Get hello VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="5ae6e-154">Pobierz nazwę dysku hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-154">Get hello OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="5ae6e-155">Utwórz hello migawki konfigurację.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-155">Create hello snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="5ae6e-156">Witaj migawki.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-156">Take hello snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="5ae6e-157">Jeśli planujesz toouse hello migawki toocreate maszynę Wirtualną, która wymaga wydajnych toobe, użyj parametru hello `-AccountType Premium_LRS` za pomocą polecenia hello AzureRmSnapshot nowy.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-157">If you plan toouse hello snapshot toocreate a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="5ae6e-158">Parametr Hello tworzy migawkę hello, aby są przechowywane jako dysk zarządzane Premium.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-158">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="5ae6e-159">Dysków zarządzanych w warstwie Premium są droższe niż standardowe.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="5ae6e-160">Dlatego upewnij się, że naprawdę potrzebny Premium przed użyciem parametru hello.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-160">So be sure you really need Premium before using hello parameter.</span></span>

### <a name="create-a-new-disk-from-hello-snapshot"></a><span data-ttu-id="5ae6e-161">Utwórz nowy dysk z hello migawki</span><span class="sxs-lookup"><span data-stu-id="5ae6e-161">Create a new disk from hello snapshot</span></span>

<span data-ttu-id="5ae6e-162">Tworzenie dysku zarządzanego z hello migawki za pomocą [AzureRMDisk nowy](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="5ae6e-162">Create a managed disk from hello snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="5ae6e-163">W tym przykładzie użyto *myOSDisk* hello nazwy dysku.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-163">This example uses *myOSDisk* for hello disk name.</span></span>

<span data-ttu-id="5ae6e-164">Utwórz nową grupę zasobów dla hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-164">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="5ae6e-165">Ustaw nazwę dysku hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-165">Set hello OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="5ae6e-166">Utwórz hello dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-166">Create hello managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="5ae6e-167">Utwórz hello nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5ae6e-167">Create hello new VM</span></span> 

<span data-ttu-id="5ae6e-168">Tworzenie sieci i innych toobe zasoby maszyn wirtualnych używanych przez hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-168">Create networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="5ae6e-169">Tworzenie hello podsieci i sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5ae6e-169">Create hello subNet and vNet</span></span>

<span data-ttu-id="5ae6e-170">Tworzenie sieci wirtualnej hello i podsieci hello [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ae6e-170">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="5ae6e-171">Utwórz podsieć hello.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-171">Create hello subNet.</span></span> <span data-ttu-id="5ae6e-172">W tym przykładzie tworzy podsieć o nazwie **mySubNet**, w grupie zasobów hello **myDestinationResourceGroup**, i ustawia prefiks adresu podsieci hello zbyt**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-172">This example creates a subnet named **mySubNet**, in hello resource group **myDestinationResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="5ae6e-173">Utwórz sieć wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-173">Create hello vNet.</span></span> <span data-ttu-id="5ae6e-174">W tym przykładzie zestawy hello toobe nazwa sieci wirtualnej **myVnetName**, zbyt hello lokalizacji**zachodnie stany USA**, i hello prefiks adresu sieci wirtualnej hello zbyt**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-174">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="5ae6e-175">Tworzenie grupy zabezpieczeń sieci hello i reguły protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="5ae6e-175">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="5ae6e-176">toobe stanie toolog w tooyour maszyny Wirtualnej przy użyciu protokołu RDP, należy toohave regułę zabezpieczeń, która udziela dostępu RDP do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-176">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="5ae6e-177">Ponieważ hello wirtualnego dysku twardego dla nowej maszyny Wirtualnej został utworzony na podstawie istniejącej maszyny Wirtualnej specjalne hello, można użyć konta ze źródłowej maszyny wirtualnej hello protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-177">Because hello VHD for hello new VM was created from an existing specialized VM, you can use an account from hello source virtual machine for RDP.</span></span>

<span data-ttu-id="5ae6e-178">W tym przykładzie zestawy hello Nazwa grupy NSG zbyt**myNsg** i hello RDP Nazwa reguły zbyt**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-178">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="5ae6e-179">Aby uzyskać więcej informacji na temat punktów końcowych i reguły NSG, zobacz [otwierania portów tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5ae6e-179">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="5ae6e-180">Tworzenie publicznego adresu IP i karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="5ae6e-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="5ae6e-181">tooenable komunikację z maszyną wirtualną hello w sieci wirtualnej hello, należy [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-181">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="5ae6e-182">Utwórz hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-182">Create hello public IP.</span></span> <span data-ttu-id="5ae6e-183">W tym przykładzie ustawiono zbyt hello nazwa publicznego adresu IP**myIP**.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-183">In this example, hello public IP address name is set too**myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="5ae6e-184">Utwórz hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-184">Create hello NIC.</span></span> <span data-ttu-id="5ae6e-185">W tym przykładzie ustawiono zbyt nazwy kart hello**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-185">In this example, hello NIC name is set too**myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="5ae6e-186">Nazwa maszyny Wirtualnej hello zestawu i rozmiaru</span><span class="sxs-lookup"><span data-stu-id="5ae6e-186">Set hello VM name and size</span></span>

<span data-ttu-id="5ae6e-187">W tym przykładzie zestawy hello nazwę maszyny Wirtualnej za*myVM* i hello wirtualna jego rozmiar za*Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-187">This example sets hello VM name too*myVM* and hello VM size too*Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="5ae6e-188">Dodaj hello karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="5ae6e-188">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a><span data-ttu-id="5ae6e-189">Dodaj dysk hello systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="5ae6e-189">Add hello OS disk</span></span> 

<span data-ttu-id="5ae6e-190">Dodaj hello systemu operacyjnego dysku toohello konfiguracji przy użyciu [AzureRmVMOSDisk zestawu](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="5ae6e-190">Add hello OS disk toohello configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="5ae6e-191">W tym przykładzie hello rozmiar dysku hello zbyt*128 GB* i dołącza hello dysków zarządzanych jako *Windows* dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-191">This example sets hello size of hello disk too*128 GB* and attaches hello managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a><span data-ttu-id="5ae6e-192">Ukończyć powitalnych maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="5ae6e-192">Complete hello VM</span></span> 

<span data-ttu-id="5ae6e-193">Utwórz maszynę Wirtualną przy użyciu hello [AzureRMVM nowy](/powershell/module/azurerm.compute/new-azurermvm)hello konfiguracje, które właśnie utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-193">Create hello VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="5ae6e-194">Jeśli to polecenie zakończyło się pomyślnie, zostanie wyświetlone dane wyjściowe w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5ae6e-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="5ae6e-195">Sprawdź hello, że maszyna wirtualna została utworzona</span><span class="sxs-lookup"><span data-stu-id="5ae6e-195">Verify that hello VM was created</span></span>
<span data-ttu-id="5ae6e-196">Powinny pojawić się hello nowo utworzona maszyna wirtualna w hello [portalu Azure](https://portal.azure.com)w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą hello następującego środowiska PowerShell polecenia:</span><span class="sxs-lookup"><span data-stu-id="5ae6e-196">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="5ae6e-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5ae6e-197">Next steps</span></span>
<span data-ttu-id="5ae6e-198">toosign w tooyour nowej maszyny wirtualnej, przeglądania toohello maszyny Wirtualnej w hello [portal](https://portal.azure.com), kliknij przycisk **Connect**i hello Otwórz plik RDP pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-198">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="5ae6e-199">Użyj poświadczeń konta hello z oryginalnego toosign maszyny wirtualnej w tooyour nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="5ae6e-199">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="5ae6e-200">Aby uzyskać więcej informacji, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="5ae6e-200">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

