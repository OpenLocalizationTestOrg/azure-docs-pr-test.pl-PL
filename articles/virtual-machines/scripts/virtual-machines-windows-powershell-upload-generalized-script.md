---
title: "Przekaż uogólniony wirtualny dysk twardy do przykładowy skrypt programu PowerShell Azure | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell do przekazywania uogólniony wirtualny dysk twardy na platformie Azure i utworzyć nową maszynę Wirtualną przy użyciu modelu wdrażania Menedżera zasobów i dysków zarządzanych."
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
ms.openlocfilehash: cd3d87bb4384971e28d3330cd5c1a3d351129036
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sample-script-to-upload-a-vhd-to-azure-and-create-a-new-vm"></a><span data-ttu-id="09a6b-103">Przykładowy skrypt do przekazania dysku VHD na platformie Azure i utworzyć nową maszynę Wirtualną</span><span class="sxs-lookup"><span data-stu-id="09a6b-103">Sample script to upload a VHD to Azure and create a new VM</span></span>

<span data-ttu-id="09a6b-104">Ten skrypt ma plik VHD lokalnego z ogólnych maszyny Wirtualnej i przekazuje ją do platformy Azure, tworzy obraz dysku zarządzane i używa do tworzenia nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="09a6b-104">This script takes a local .vhd file from a generalized VM and uploads it to Azure, creates a Managed Disk image and uses the to create a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="09a6b-105">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="09a6b-105">Sample script</span></span>

```powershell
# Provide values for the variables
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

# Get the username and password to be used for the administrators account on the VM. 
# This is used when connecting to the VM using RDP.

$cred = Get-Credential

# Upload the VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading the VHD may take awhile!

# Create a managed image from the uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create the networking resources
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

# Start building the VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set the VM image as source image for the new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish the VM configuration and add the NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create the VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that the VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="09a6b-106">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="09a6b-106">Clean up deployment</span></span> 

<span data-ttu-id="09a6b-107">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="09a6b-107">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="09a6b-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="09a6b-108">Script explanation</span></span>

<span data-ttu-id="09a6b-109">Ten skrypt używa następujących poleceń w celu utworzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="09a6b-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="09a6b-110">Każdy element w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="09a6b-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="09a6b-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="09a6b-111">Command</span></span>                                                                                                             | <span data-ttu-id="09a6b-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="09a6b-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="09a6b-113">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="09a6b-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="09a6b-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="09a6b-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="09a6b-115">Nowe AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="09a6b-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="09a6b-116">Tworzy konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="09a6b-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="09a6b-117">Dodaj AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="09a6b-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="09a6b-118">Przekazywanie wirtualnego dysku twardego z lokalnej maszyny wirtualnej do obiektu blob w konta magazynu w chmurze na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="09a6b-118">Uploads a virtual hard disk from an on-premises virtual machine to a blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="09a6b-119">Nowe AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="09a6b-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="09a6b-120">Tworzy obiekt obrazu można konfigurować.</span><span class="sxs-lookup"><span data-stu-id="09a6b-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="09a6b-121">Zestaw AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="09a6b-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="09a6b-122">Ustawia właściwości dysku systemu operacyjnego, w obiekcie image.</span><span class="sxs-lookup"><span data-stu-id="09a6b-122">Sets the operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="09a6b-123">Nowe AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="09a6b-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="09a6b-124">Tworzy nowy obraz.</span><span class="sxs-lookup"><span data-stu-id="09a6b-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="09a6b-125">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="09a6b-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="09a6b-126">Tworzy konfiguracji podsieci.</span><span class="sxs-lookup"><span data-stu-id="09a6b-126">Creates a subnet configuration.</span></span> <span data-ttu-id="09a6b-127">Ta konfiguracja jest używana z procesu tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="09a6b-127">This configuration is used with the virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="09a6b-128">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="09a6b-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="09a6b-129">Tworzy sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="09a6b-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="09a6b-130">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="09a6b-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="09a6b-131">Tworzy publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="09a6b-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="09a6b-132">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="09a6b-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="09a6b-133">Tworzy interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="09a6b-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="09a6b-134">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="09a6b-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="09a6b-135">Tworzy konfiguracji reguły grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="09a6b-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="09a6b-136">Ta konfiguracja jest używana do utworzenia reguły NSG, gdy grupa NSG jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="09a6b-136">This configuration is used to create an NSG rule when the NSG is created.</span></span>                                                       |
| [<span data-ttu-id="09a6b-137">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="09a6b-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="09a6b-138">Tworzy sieciową grupę zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="09a6b-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="09a6b-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="09a6b-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="09a6b-140">Pobiera sieć wirtualną w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="09a6b-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="09a6b-141">Nowe AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="09a6b-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="09a6b-142">Tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="09a6b-142">Creates a VM configuration.</span></span> <span data-ttu-id="09a6b-143">Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="09a6b-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="09a6b-144">Konfiguracja jest używany podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="09a6b-144">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="09a6b-145">Zestaw AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="09a6b-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="09a6b-146">Określa obraz maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="09a6b-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="09a6b-147">Zestaw AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="09a6b-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="09a6b-148">Ustawia właściwości dysku systemu operacyjnego, na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="09a6b-148">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="09a6b-149">Zestaw AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="09a6b-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="09a6b-150">Ustawia właściwości dysku systemu operacyjnego, na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="09a6b-150">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="09a6b-151">Dodaj AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="09a6b-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="09a6b-152">Dodaje interfejs sieciowy do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="09a6b-152">Adds a network interface to a virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="09a6b-153">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="09a6b-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="09a6b-154">Utwórz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="09a6b-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="09a6b-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="09a6b-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="09a6b-156">Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="09a6b-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="09a6b-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="09a6b-157">Next steps</span></span>

<span data-ttu-id="09a6b-158">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="09a6b-158">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="09a6b-159">Przykłady skryptów PowerShell dodatkowe maszyny wirtualnej znajdują się w [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="09a6b-159">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
