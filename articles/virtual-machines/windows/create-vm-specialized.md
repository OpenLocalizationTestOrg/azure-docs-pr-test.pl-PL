---
title: Tworzenie maszyny Wirtualnej systemu Windows z specjalne wirtualnego dysku twardego na platformie Azure | Dokumentacja firmy Microsoft
description: "Utwórz nową maszynę Wirtualną systemu Windows przez dołączenie specjalne dysków zarządzanych jako dysk systemu operacyjnego przy użyciu modelu wdrażania Menedżera zasobów."
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
ms.openlocfilehash: fa952286a9ceca8b3b2c7efe2cc4867a2728c477
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="fc501-103">Tworzenie maszyny Wirtualnej systemu Windows z dysku specjalne</span><span class="sxs-lookup"><span data-stu-id="fc501-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="fc501-104">Tworzenie nowej maszyny Wirtualnej przez dołączenie specjalne dysków zarządzanych jako dysk systemu operacyjnego przy użyciu programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="fc501-104">Create a new VM by attaching a specialized managed disk as the OS disk using Powershell.</span></span> <span data-ttu-id="fc501-105">Specjalne dysku jest kopią wirtualnego dysku twardego (VHD) z istniejącej maszyny Wirtualnej, który przechowuje konta użytkowników, aplikacji i innych danych o stanie z oryginalnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc501-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains the user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="fc501-106">Specjalne wirtualnego dysku twardego jest używany do utworzenia nowej maszyny Wirtualnej, nazwy komputera oryginalna maszyna wirtualna zachowuje nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc501-106">When you use a specialized VHD to create a new VM, the new VM retains the computer name of the original VM.</span></span> <span data-ttu-id="fc501-107">Inne informacje specyficzne dla komputera jest również przechowywać, a w niektórych przypadkach te informacje zduplikowane może spowodować problemy.</span><span class="sxs-lookup"><span data-stu-id="fc501-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="fc501-108">Należy pamiętać o jakie rodzaje informacji specyficznych dla komputera aplikacje zależne od podczas kopiowania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc501-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="fc501-109">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="fc501-109">You have two options:</span></span>
* [<span data-ttu-id="fc501-110">Przekazywanie wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="fc501-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="fc501-111">Skopiuj istniejącej maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="fc501-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="fc501-112">W tym temacie przedstawiono sposób użycia dysków zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="fc501-112">This topic shows you how to use managed disks.</span></span> <span data-ttu-id="fc501-113">Jeśli masz wdrożenie starszych wymagający przy użyciu konta magazynu, zobacz [utworzyć Maszynę wirtualną z wirtualnego dysku twardego specjalne konta magazynu](sa-create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="fc501-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fc501-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="fc501-114">Before you begin</span></span>
<span data-ttu-id="fc501-115">Jeśli używasz programu PowerShell, upewnij się, że masz najnowszą wersję modułu programu AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fc501-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="fc501-116">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fc501-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="fc501-117">Opcja 1: Przekazanie specjalne dysku VHD</span><span class="sxs-lookup"><span data-stu-id="fc501-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="fc501-118">Możesz przekazać wirtualnego dysku twardego z specjalne utworzone za pomocą wirtualizacji narzędzia lokalnych, takich jak funkcja Hyper-V lub maszyny Wirtualnej wyeksportowane z innej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc501-118">You can upload the VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-the-vm"></a><span data-ttu-id="fc501-119">Przygotowywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fc501-119">Prepare the VM</span></span>
<span data-ttu-id="fc501-120">Jeśli zamierzasz używać wirtualnego dysku twardego jako — jest, aby utworzyć nową maszynę Wirtualną, upewnij się, wykonywane są następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="fc501-120">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="fc501-121">[Przygotowywanie dysku VHD systemu Windows, aby przekazać do usługi Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc501-121">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="fc501-122">**Nie** generalize maszyny Wirtualnej za pomocą programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="fc501-122">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="fc501-123">Usuń wszystkie narzędzia wirtualizacji gościa i agentów, które są zainstalowane na maszynie Wirtualnej (np. narzędzi VMware).</span><span class="sxs-lookup"><span data-stu-id="fc501-123">Remove any guest virtualization tools and agents that are installed on the VM (like VMware tools).</span></span>
  * <span data-ttu-id="fc501-124">Upewnij się, że maszyna wirtualna jest skonfigurowana do pobierania jego adres IP i ustawienia DNS za pośrednictwem protokołu DHCP.</span><span class="sxs-lookup"><span data-stu-id="fc501-124">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="fc501-125">Daje to pewność, że serwer uzyskuje adres IP w sieci wirtualnej podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="fc501-125">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 


### <a name="get-the-storage-account"></a><span data-ttu-id="fc501-126">Uzyskaj konto magazynu</span><span class="sxs-lookup"><span data-stu-id="fc501-126">Get the storage account</span></span>
<span data-ttu-id="fc501-127">Potrzebujesz konta magazynu na platformie Azure do przechowywania przekazany wirtualny dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="fc501-127">You need a storage account in Azure to store the uploaded VHD.</span></span> <span data-ttu-id="fc501-128">Możesz użyć istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="fc501-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="fc501-129">Aby wyświetlić konta dostępny magazyn, wpisz:</span><span class="sxs-lookup"><span data-stu-id="fc501-129">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="fc501-130">Jeśli chcesz użyć istniejącego konta magazynu, przejdź do [przekazanie dysku VHD](#upload-the-vhd-to-your-storage-account) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fc501-130">If you want to use an existing storage account, proceed to the [Upload the VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="fc501-131">Jeśli musisz utworzyć konto magazynu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fc501-131">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="fc501-132">Potrzebna jest nazwa grupy zasobów, w którym ma zostać utworzony na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="fc501-132">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="fc501-133">Aby dowiedzieć się, wszystkie grupy zasobów, które są w ramach subskrypcji, wpisz:</span><span class="sxs-lookup"><span data-stu-id="fc501-133">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="fc501-134">Aby utworzyć grupę zasobów o nazwie *myResourceGroup* w *zachodnie stany USA* regionu, wpisz:</span><span class="sxs-lookup"><span data-stu-id="fc501-134">To create a resource group named *myResourceGroup* in the *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="fc501-135">Utwórz konto magazynu o nazwie *mojekontomagazynu* w tej grupie zasobów za pomocą [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="fc501-135">Create a storage account named *mystorageaccount* in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="fc501-136">Przekazanie dysku VHD do konta magazynu</span><span class="sxs-lookup"><span data-stu-id="fc501-136">Upload the VHD to your storage account</span></span> 
<span data-ttu-id="fc501-137">Użyj [AzureRmVhd Dodaj](/powershell/module/azurerm.compute/add-azurermvhd) polecenia cmdlet w celu przekazania dysku VHD do kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="fc501-137">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="fc501-138">W tym przykładzie powoduje przekazanie pliku *myVHD.vhd* z `"C:\Users\Public\Documents\Virtual hard disks\"` na konto magazynu o nazwie *mojekontomagazynu* w *myResourceGroup* grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="fc501-138">This example uploads the file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="fc501-139">Plik jest przechowywany w kontenerze o nazwie *mojkontener* i Nowa nazwa pliku będzie *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="fc501-139">The file is stored in the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="fc501-140">W przypadku powodzenia można uzyskać odpowiedzi, która wygląda podobnie do poniższego:</span><span class="sxs-lookup"><span data-stu-id="fc501-140">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="fc501-141">W zależności od połączenia sieciowego i rozmiar pliku VHD to polecenie może zająć trochę czasu, aby zakończyć</span><span class="sxs-lookup"><span data-stu-id="fc501-141">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

### <a name="create-a-managed-disk-from-the-vhd"></a><span data-ttu-id="fc501-142">Tworzenie dysku zarządzanego z dysku VHD</span><span class="sxs-lookup"><span data-stu-id="fc501-142">Create a managed disk from the VHD</span></span>

<span data-ttu-id="fc501-143">Tworzenie dysku zarządzanego z specjalne dysku VHD za pomocą konta magazynu [AzureRMDisk nowy](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="fc501-143">Create a managed disk from the specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="fc501-144">W tym przykładzie użyto **myOSDisk1** dla nazwy dysku umieszcza dysku *StandardLRS* magazynu i używa *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* jako identyfikator URI dysku VHD źródła.</span><span class="sxs-lookup"><span data-stu-id="fc501-144">This example uses **myOSDisk1** for the disk name, puts the disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as the URI for the source VHD.</span></span>

<span data-ttu-id="fc501-145">Utwórz nową grupę zasobów dla nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc501-145">Create a new resource group for the new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="fc501-146">Utwórz nowy dysk systemu operacyjnego na podstawie przekazanego wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="fc501-146">Create the new OS disk from the uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="fc501-147">Opcja 2: Kopiowanie istniejącej maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="fc501-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="fc501-148">Można utworzyć kopii maszyny wirtualnej używa dyskach zarządzanych przez tworzenie migawki maszyny wirtualnej, a następnie za pomocą tej migawki, aby utworzyć nową zarządzane dysku i nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc501-148">You can create a copy of a VM that uses managed disks by taking a snapshot of the VM, then using that snapshot to create a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-the-os-disk"></a><span data-ttu-id="fc501-149">Utwórz migawkę dysk systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="fc501-149">Take a snapshot of the OS disk</span></span>

<span data-ttu-id="fc501-150">Można wykonać migawki elementu i całej maszyny Wirtualnej (w tym wszystkie dyski) lub tylko jednego dysku.</span><span class="sxs-lookup"><span data-stu-id="fc501-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="fc501-151">Poniższe kroki opisano sposób migawki tylko dysk systemu operacyjnego z sieci maszyny Wirtualnej przy użyciu [AzureRmSnapshot nowy](/powershell/module/azurerm.compute/new-azurermsnapshot) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fc501-151">The following steps show you how to take a snapshot of just the OS disk of your VM using the [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="fc501-152">Ustaw niektórych parametrów.</span><span class="sxs-lookup"><span data-stu-id="fc501-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="fc501-153">Pobierz obiekt VM.</span><span class="sxs-lookup"><span data-stu-id="fc501-153">Get the VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="fc501-154">Pobierz nazwę dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fc501-154">Get the OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="fc501-155">Utworzenie migawki konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fc501-155">Create the snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="fc501-156">Migawki.</span><span class="sxs-lookup"><span data-stu-id="fc501-156">Take the snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="fc501-157">Jeśli planujesz używać migawki, aby utworzyć maszynę Wirtualną, która musi być wydajnych, użyj parametru `-AccountType Premium_LRS` przy użyciu polecenia New-AzureRmSnapshot.</span><span class="sxs-lookup"><span data-stu-id="fc501-157">If you plan to use the snapshot to create a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="fc501-158">Parametr tworzy migawkę tak, aby była przechowywana jako dysk zarządzane Premium.</span><span class="sxs-lookup"><span data-stu-id="fc501-158">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="fc501-159">Dysków zarządzanych w warstwie Premium są droższe niż standardowe.</span><span class="sxs-lookup"><span data-stu-id="fc501-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="fc501-160">Dlatego upewnij się, że naprawdę potrzebny Premium przed rozpoczęciem korzystania z parametru.</span><span class="sxs-lookup"><span data-stu-id="fc501-160">So be sure you really need Premium before using the parameter.</span></span>

### <a name="create-a-new-disk-from-the-snapshot"></a><span data-ttu-id="fc501-161">Utwórz nowy dysk z migawki</span><span class="sxs-lookup"><span data-stu-id="fc501-161">Create a new disk from the snapshot</span></span>

<span data-ttu-id="fc501-162">Tworzenie dysku zarządzanego z migawki przy użyciu [AzureRMDisk nowy](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="fc501-162">Create a managed disk from the snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="fc501-163">W tym przykładzie użyto *myOSDisk* dla nazwy dysku.</span><span class="sxs-lookup"><span data-stu-id="fc501-163">This example uses *myOSDisk* for the disk name.</span></span>

<span data-ttu-id="fc501-164">Utwórz nową grupę zasobów dla nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc501-164">Create a new resource group for the new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="fc501-165">Ustaw nazwę dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fc501-165">Set the OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="fc501-166">Tworzenie dysku zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="fc501-166">Create the managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-the-new-vm"></a><span data-ttu-id="fc501-167">Tworzenie nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fc501-167">Create the new VM</span></span> 

<span data-ttu-id="fc501-168">Tworzenie sieci i innych zasobów maszyny Wirtualnej do użycia przez nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc501-168">Create networking and other VM resources to be used by the new VM.</span></span>

### <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="fc501-169">Utwórz podsieć i sieć wirtualna</span><span class="sxs-lookup"><span data-stu-id="fc501-169">Create the subNet and vNet</span></span>

<span data-ttu-id="fc501-170">Utwórz sieć wirtualną i podsieć [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc501-170">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="fc501-171">Utwórz podsieć.</span><span class="sxs-lookup"><span data-stu-id="fc501-171">Create the subNet.</span></span> <span data-ttu-id="fc501-172">W tym przykładzie tworzy podsieć o nazwie **mySubNet**, w grupie zasobów **myDestinationResourceGroup**i ustawia prefiks adresu podsieci **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="fc501-172">This example creates a subnet named **mySubNet**, in the resource group **myDestinationResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="fc501-173">Tworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc501-173">Create the vNet.</span></span> <span data-ttu-id="fc501-174">W tym przykładzie nazwa sieci wirtualnej, który ma zostać **myVnetName**, lokalizacja **zachodnie stany USA**i prefiksu adresu dla sieci wirtualnej do **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="fc501-174">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="fc501-175">Tworzenie grupy zabezpieczeń sieci i reguły protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="fc501-175">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="fc501-176">Aby móc zalogować się do maszyny Wirtualnej za pomocą protokołu RDP, musisz mieć regułę zabezpieczeń, która udziela dostępu RDP do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="fc501-176">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="fc501-177">Ponieważ wirtualny dysk twardy dla nowej maszyny Wirtualnej został utworzony na podstawie istniejącej maszyny Wirtualnej specjalne, można użyć konta ze źródłowej maszyny wirtualnej dla protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="fc501-177">Because the VHD for the new VM was created from an existing specialized VM, you can use an account from the source virtual machine for RDP.</span></span>

<span data-ttu-id="fc501-178">W tym przykładzie nazwa grupy NSG **myNsg** i nazwa reguły protokołu RDP do **myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="fc501-178">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="fc501-179">Aby uzyskać więcej informacji na temat punktów końcowych i reguły NSG, zobacz [Otwieranie portów dla maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc501-179">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="fc501-180">Tworzenie publicznego adresu IP i karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="fc501-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="fc501-181">Aby umożliwić komunikację z maszyną wirtualną w sieci wirtualnej, potrzebujesz [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="fc501-181">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="fc501-182">Tworzenie publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="fc501-182">Create the public IP.</span></span> <span data-ttu-id="fc501-183">W tym przykładzie ustawiono nazwa publicznego adresu IP **myIP**.</span><span class="sxs-lookup"><span data-stu-id="fc501-183">In this example, the public IP address name is set to **myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="fc501-184">Utwórz kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="fc501-184">Create the NIC.</span></span> <span data-ttu-id="fc501-185">W tym przykładzie nazwa karty Sieciowej jest ustawiona **myNicName**.</span><span class="sxs-lookup"><span data-stu-id="fc501-185">In this example, the NIC name is set to **myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-the-vm-name-and-size"></a><span data-ttu-id="fc501-186">Ustaw nazwę maszyny Wirtualnej i rozmiar</span><span class="sxs-lookup"><span data-stu-id="fc501-186">Set the VM name and size</span></span>

<span data-ttu-id="fc501-187">W tym przykładzie nazwa maszyny Wirtualnej *myVM* i rozmiaru maszyny Wirtualnej *Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="fc501-187">This example sets the VM name to *myVM* and the VM size to *Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-the-nic"></a><span data-ttu-id="fc501-188">Dodaj kartę Sieciową</span><span class="sxs-lookup"><span data-stu-id="fc501-188">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-the-os-disk"></a><span data-ttu-id="fc501-189">Dodawanie dysku systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="fc501-189">Add the OS disk</span></span> 

<span data-ttu-id="fc501-190">Dodawanie dysku systemu operacyjnego do konfiguracji przy użyciu [AzureRmVMOSDisk zestawu](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="fc501-190">Add the OS disk to the configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="fc501-191">W tym przykładzie rozmiar dysku do *128 GB* i dołącza dysków zarządzanych jako *Windows* dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fc501-191">This example sets the size of the disk to *128 GB* and attaches the managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-the-vm"></a><span data-ttu-id="fc501-192">Zakończenie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fc501-192">Complete the VM</span></span> 

<span data-ttu-id="fc501-193">Utwórz maszynę Wirtualną przy użyciu [AzureRMVM nowy](/powershell/module/azurerm.compute/new-azurermvm)konfiguracje, które właśnie utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="fc501-193">Create the VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)the configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="fc501-194">Jeśli to polecenie zakończyło się pomyślnie, zostanie wyświetlone dane wyjściowe w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fc501-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="fc501-195">Sprawdź, czy maszyna wirtualna została utworzona</span><span class="sxs-lookup"><span data-stu-id="fc501-195">Verify that the VM was created</span></span>
<span data-ttu-id="fc501-196">Nowo utworzona maszyna wirtualna powinna być widoczna albo w [portalu Azure](https://portal.azure.com)w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących poleceń programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fc501-196">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="fc501-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fc501-197">Next steps</span></span>
<span data-ttu-id="fc501-198">Aby zalogować się do nowej maszyny wirtualnej, przejdź do maszyny Wirtualnej w [portal](https://portal.azure.com), kliknij przycisk **Connect**i Otwórz plik RDP pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="fc501-198">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="fc501-199">Korzystać z poświadczeń konta oryginalnego maszyny wirtualnej, aby zalogować się do nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fc501-199">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="fc501-200">Aby uzyskać więcej informacji, zobacz [jak połączenia i zaloguj się do maszyny wirtualnej platformy Azure systemem Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="fc501-200">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

