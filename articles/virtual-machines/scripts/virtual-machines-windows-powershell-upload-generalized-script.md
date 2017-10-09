---
title: "aaaUpload uogólniony tooAzure wirtualnego dysku twardego przykładowy skrypt programu PowerShell | Dokumentacja firmy Microsoft"
description: "PowerShell przykładowy skrypt tooupload uogólniony tooAzure wirtualnego dysku twardego i utworzyć nową maszynę Wirtualną przy użyciu modelu wdrażania Menedżera zasobów hello i dysków zarządzanych."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/18/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 72b4ff09eb7a6ba1604b9d5cbac51e60eded7545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a><span data-ttu-id="02546-103">Przykładowy skrypt tooupload tooAzure wirtualnego dysku twardego i utworzyć nową maszynę Wirtualną</span><span class="sxs-lookup"><span data-stu-id="02546-103">Sample script tooupload a VHD tooAzure and create a new VM</span></span>

<span data-ttu-id="02546-104">Ten skrypt ma plik VHD lokalnego z ogólnych maszyny Wirtualnej i przekazanie jej tooAzure, tworzy obraz dysku zarządzane i używa toocreate hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="02546-104">This script takes a local .vhd file from a generalized VM and uploads it tooAzure, creates a Managed Disk image and uses hello toocreate a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="02546-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="02546-105">Sample script</span></span>

```powershell
# Provide values for hello variables
$resourceGroup = 'myResourceGroup'
$location = 'EastUS'
$storageaccount = 'mystorageaccount'
$storageType = 'Standard_LRS'
$containername = 'mycontainer'
$localPath = 'C:\Users\Public\Documents\Hyper-V\VHDs\generalized.vhd'
$vmName = 'myVM'
$imageName = 'myImage'
$vhdName = 'myUploadedVhd.vhd'
$diskSizeGB = '128'
$subnetName = 'mySubnet'
$vnetName = 'myVnet'
$ipName = 'myPip'
$nicName = 'myNic'
$nsgName = 'myNsg'
$ruleName = 'myRdpRule'
$vmName = 'myVM'
$computerName = 'myComputerName'
$vmSize = 'Standard_DS1_v2'

# Get hello username and password toobe used for hello administrators account on hello VM. 
# This is used when connecting toohello VM using RDP.

$cred = Get-Credential

# Upload hello VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading hello VHD may take awhile!

# Create a managed image from hello uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create hello networking resources
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $resourceGroup -Location $location `
    -AllocationMethod Dynamic
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroup -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description 'Allow RDP' -Access Allow `
    -Protocol Tcp -Direction Inbound -Priority 110 -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $resourceGroup -Name $vnetName

# Start building hello VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set hello VM image as source image for hello new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish hello VM configuration and add hello NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create hello VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that hello VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="02546-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="02546-106">Clean up deployment</span></span> 

<span data-ttu-id="02546-107">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="02546-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="02546-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="02546-108">Script explanation</span></span>

<span data-ttu-id="02546-109">Ten skrypt używa hello następujące polecenia toocreate hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="02546-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="02546-110">Każdy element w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="02546-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="02546-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="02546-111">Command</span></span>                                                                                                             | <span data-ttu-id="02546-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="02546-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="02546-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="02546-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="02546-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="02546-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="02546-115">Nowe AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="02546-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="02546-116">Tworzy konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="02546-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="02546-117">Dodaj AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="02546-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="02546-118">Przekazywanie wirtualnego dysku twardego z lokalnej maszyny wirtualnej tooa obiektu blob w konta magazynu w chmurze na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="02546-118">Uploads a virtual hard disk from an on-premises virtual machine tooa blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="02546-119">Nowe AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="02546-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="02546-120">Tworzy obiekt obrazu można konfigurować.</span><span class="sxs-lookup"><span data-stu-id="02546-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="02546-121">Zestaw AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="02546-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="02546-122">Ustawia systemu operacyjnego hello dysku właściwości obiektu obrazu.</span><span class="sxs-lookup"><span data-stu-id="02546-122">Sets hello operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="02546-123">Nowe AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="02546-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="02546-124">Tworzy nowy obraz.</span><span class="sxs-lookup"><span data-stu-id="02546-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="02546-125">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="02546-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="02546-126">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="02546-126">Creates a subnet configuration.</span></span> <span data-ttu-id="02546-127">Ta konfiguracja jest używana z procesu tworzenia hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="02546-127">This configuration is used with hello virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="02546-128">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="02546-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="02546-129">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="02546-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="02546-130">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="02546-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="02546-131">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="02546-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="02546-132">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="02546-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="02546-133">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="02546-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="02546-134">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="02546-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="02546-135">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="02546-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="02546-136">Ta konfiguracja jest używane toocreate reguły NSG, po utworzeniu hello NSG.</span><span class="sxs-lookup"><span data-stu-id="02546-136">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span>                                                       |
| [<span data-ttu-id="02546-137">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="02546-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="02546-138">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="02546-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="02546-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="02546-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="02546-140">Pobiera sieć wirtualną w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="02546-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="02546-141">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="02546-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="02546-142">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="02546-142">Creates a VM configuration.</span></span> <span data-ttu-id="02546-143">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="02546-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="02546-144">Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="02546-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="02546-145">Zestaw AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="02546-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="02546-146">Określa obraz maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="02546-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="02546-147">Zestaw AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="02546-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="02546-148">Ustawia właściwości dysku systemu operacyjnego hello, na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="02546-148">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="02546-149">Zestaw AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="02546-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="02546-150">Ustawia właściwości dysku systemu operacyjnego hello, na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="02546-150">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="02546-151">Dodaj AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="02546-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="02546-152">Dodaje maszynę wirtualną tooa interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="02546-152">Adds a network interface tooa virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="02546-153">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="02546-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="02546-154">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="02546-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="02546-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="02546-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="02546-156">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="02546-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="02546-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02546-157">Next steps</span></span>

<span data-ttu-id="02546-158">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="02546-158">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="02546-159">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="02546-159">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
