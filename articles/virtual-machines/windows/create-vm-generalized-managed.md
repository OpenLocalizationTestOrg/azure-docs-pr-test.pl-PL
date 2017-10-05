---
title: "Tworzenie maszyny Wirtualnej z do zarządzanego obrazu maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Utwórz maszynę wirtualną systemu Windows z uogólniony obraz maszyny Wirtualnej zarządzanej przy użyciu programu Azure PowerShell w modelu wdrażania usługi Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 2bb2d66271178a64ec0f4642e46b23f5618a56d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="55dec-103">Utwórz maszynę Wirtualną z zarządzanego obrazu</span><span class="sxs-lookup"><span data-stu-id="55dec-103">Create a VM from a managed image</span></span>

<span data-ttu-id="55dec-104">Możesz utworzyć wiele maszyn wirtualnych z do zarządzanego obrazu maszyny Wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="55dec-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="55dec-105">Do zarządzanego obrazu maszyny Wirtualnej zawiera informacje niezbędne do tworzenia maszyn wirtualnych, dysków systemu operacyjnego i danych.</span><span class="sxs-lookup"><span data-stu-id="55dec-105">A managed VM image contains the information necessary to create a VM, including the OS and data disks.</span></span> <span data-ttu-id="55dec-106">Wirtualne dyski twarde, które tworzą obrazu, w tym zarówno dysków systemu operacyjnego i dysków z danymi, są przechowywane jako dyski zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="55dec-106">The VHDs that make up the image, including both the OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="55dec-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="55dec-107">Prerequisites</span></span>

<span data-ttu-id="55dec-108">Musisz mieć już [utworzony obraz maszyny Wirtualnej zarządzanej](capture-image-resource.md) do użycia podczas tworzenia nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55dec-108">You need to have already [created a managed VM image](capture-image-resource.md) to use for creating the new VM.</span></span> 

<span data-ttu-id="55dec-109">Upewnij się, że najnowsze wersje modułów AzureRM.Compute i AzureRM.Network programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55dec-109">Make sure that you have the latest versions of the AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="55dec-110">Otwórz wiersz programu PowerShell jako Administrator i uruchom następujące polecenie, aby je zainstalować.</span><span class="sxs-lookup"><span data-stu-id="55dec-110">Open a PowerShell prompt as an Administrator and run the following command to install them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="55dec-111">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="55dec-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-the-image"></a><span data-ttu-id="55dec-112">Zbieranie informacji o obrazie</span><span class="sxs-lookup"><span data-stu-id="55dec-112">Collect information about the image</span></span>

<span data-ttu-id="55dec-113">Najpierw musimy zebrać podstawowe informacje o obrazie i utworzyć zmienną dla obrazu.</span><span class="sxs-lookup"><span data-stu-id="55dec-113">First we need to gather basic information about the image and create a variable for the image.</span></span> <span data-ttu-id="55dec-114">W tym przykładzie użyto do zarządzanego obrazu maszyny Wirtualnej o nazwie **myImage** w **myResourceGroup** grupy zasobów w **zachodnie centralnej nam** lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="55dec-114">This example uses a managed VM image named **myImage** that is in the **myResourceGroup** resource group in the **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="55dec-115">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55dec-115">Create a virtual network</span></span>
<span data-ttu-id="55dec-116">Utwórz sieć wirtualną i podsieć [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55dec-116">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="55dec-117">Utwórz podsieć.</span><span class="sxs-lookup"><span data-stu-id="55dec-117">Create the subnet.</span></span> <span data-ttu-id="55dec-118">W tym przykładzie tworzy podsieć o nazwie **mySubnet** z prefiksem adresu o **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="55dec-118">This example creates a subnet named **mySubnet** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="55dec-119">Utwórz sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="55dec-119">Create the virtual network.</span></span> <span data-ttu-id="55dec-120">W tym przykładzie tworzy sieć wirtualną o nazwie **myVnet** z prefiksem adresu o **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="55dec-120">This example creates a virtual network named **myVnet** with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="55dec-121">Tworzenie publicznego adresu IP adres i interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="55dec-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="55dec-122">Aby umożliwić komunikację z maszyną wirtualną w sieci wirtualnej, potrzebujesz [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="55dec-122">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="55dec-123">Utwórz publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="55dec-123">Create a public IP address.</span></span> <span data-ttu-id="55dec-124">W tym przykładzie jest tworzony publiczny adres IP o nazwie **myPip**.</span><span class="sxs-lookup"><span data-stu-id="55dec-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="55dec-125">Utwórz kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="55dec-125">Create the NIC.</span></span> <span data-ttu-id="55dec-126">W tym przykładzie jest tworzony karty Sieciowej o nazwie **myNic**.</span><span class="sxs-lookup"><span data-stu-id="55dec-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="55dec-127">Tworzenie grupy zabezpieczeń sieci i reguły protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="55dec-127">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="55dec-128">Aby móc zalogować się do maszyny Wirtualnej za pomocą protokołu RDP, musisz mieć reguły zabezpieczeń sieci (NSG), umożliwiająca dostęp RDP do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="55dec-128">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="55dec-129">W tym przykładzie tworzy grupy NSG o nazwie **myNsg** zawierający regułę o nazwie **myRdpRule** za pośrednictwem portu 3389 która zezwala na ruch RDP.</span><span class="sxs-lookup"><span data-stu-id="55dec-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="55dec-130">Aby uzyskać więcej informacji na temat grup NSG, zobacz [Otwieranie portów dla maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="55dec-130">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="55dec-131">Utwórz zmienną dla sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55dec-131">Create a variable for the virtual network</span></span>

<span data-ttu-id="55dec-132">Utwórz zmienną dla ukończonych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55dec-132">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="55dec-133">Uzyskiwanie poświadczeń dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55dec-133">Get the credentials for the VM</span></span>

<span data-ttu-id="55dec-134">Następujące polecenie cmdlet zostanie otwarte okno gdzie będą wprowadź nową nazwę użytkownika i hasło do użycia jako konto administratora lokalnego na zdalny dostęp do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55dec-134">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-the-vm-name-computer-name-and-the-size-of-the-vm"></a><span data-ttu-id="55dec-135">Ustaw zmienne nazwę maszyny Wirtualnej, nazwy komputera i rozmiaru maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55dec-135">Set variables for the VM name, computer name and the size of the VM</span></span>

1. <span data-ttu-id="55dec-136">Utwórz zmienne dla nazwy komputera i nazwę maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55dec-136">Create variables for the VM name and computer name.</span></span> <span data-ttu-id="55dec-137">W tym przykładzie nazwa maszyny Wirtualnej jako **myVM** i nazwę komputera, jako **Mój komputer**.</span><span class="sxs-lookup"><span data-stu-id="55dec-137">This example sets the VM name as **myVM** and the computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="55dec-138">Ustaw rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55dec-138">Set the size of the virtual machine.</span></span> <span data-ttu-id="55dec-139">Ten przykład tworzy **Standard_DS1_v2** rozmiaru maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55dec-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="55dec-140">Zobacz [rozmiarów maszyn wirtualnych](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) dokumentacji, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="55dec-140">See the [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="55dec-141">Dodaj nazwę maszyny Wirtualnej i rozmiar do konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55dec-141">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="55dec-142">Ustaw obraz maszyny Wirtualnej jako źródło obrazu dla nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55dec-142">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="55dec-143">Ustaw obraz źródłowy przy użyciu Identyfikatora zarządzanego obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="55dec-143">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="55dec-144">Ustawienia konfiguracji systemu operacyjnego i Dodaj kartę sieciową.</span><span class="sxs-lookup"><span data-stu-id="55dec-144">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="55dec-145">Wprowadź typ magazynu (PremiumLRS lub StandardLRS) i rozmiar dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="55dec-145">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="55dec-146">W tym przykładzie typ konta w **PremiumLRS**, rozmiar dysku do **128 GB** i buforowanie dysku, aby **ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="55dec-146">This example sets the account type to **PremiumLRS**, the disk size to **128 GB** and disk caching to **ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="55dec-147">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="55dec-147">Create the VM</span></span>

<span data-ttu-id="55dec-148">Tworzenie nowej maszyny wirtualnej za pomocą konfiguracji, które firma Microsoft utworzone i przechowywane w **$vm** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="55dec-148">Create the new Vm using the configuration that we have built and stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="55dec-149">Sprawdź, czy maszyna wirtualna została utworzona</span><span class="sxs-lookup"><span data-stu-id="55dec-149">Verify that the VM was created</span></span>
<span data-ttu-id="55dec-150">Po zakończeniu powinien zostać wyświetlony nowo utworzony maszyny Wirtualnej w ramach [portalu Azure](https://portal.azure.com) w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących poleceń programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="55dec-150">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="55dec-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="55dec-151">Next steps</span></span>
<span data-ttu-id="55dec-152">Aby zarządzać nową maszynę wirtualną w taki sposób, z programu Azure PowerShell, zobacz [tworzenia i zarządzania maszynami wirtualnymi systemu Windows za pomocą modułu Azure PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="55dec-152">To manage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

