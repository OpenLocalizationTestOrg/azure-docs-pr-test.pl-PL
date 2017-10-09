---
title: "aaaCreate maszyny Wirtualnej z do zarządzanego obrazu maszyny Wirtualnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Utwórz maszynę wirtualną systemu Windows z uogólniony obraz maszyny Wirtualnej zarządzanego w modelu wdrażania usługi Resource Manager hello przy użyciu programu Azure PowerShell."
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
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="72da2-103">Utwórz maszynę Wirtualną z zarządzanego obrazu</span><span class="sxs-lookup"><span data-stu-id="72da2-103">Create a VM from a managed image</span></span>

<span data-ttu-id="72da2-104">Możesz utworzyć wiele maszyn wirtualnych z do zarządzanego obrazu maszyny Wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="72da2-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="72da2-105">Do zarządzanego obrazu maszyny Wirtualnej zawiera hello informacje niezbędne toocreate maszyny Wirtualnej, włączając hello systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="72da2-105">A managed VM image contains hello information necessary toocreate a VM, including hello OS and data disks.</span></span> <span data-ttu-id="72da2-106">Witaj, które tworzą obrazu hello, w tym zarówno dyski hello systemu operacyjnego i dysków z danymi, są przechowywane jako zarządzane dyski wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="72da2-106">hello VHDs that make up hello image, including both hello OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="72da2-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="72da2-107">Prerequisites</span></span>

<span data-ttu-id="72da2-108">Należy toohave już [utworzony obraz maszyny Wirtualnej zarządzanej](capture-image-resource.md) toouse tworzenia hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72da2-108">You need toohave already [created a managed VM image](capture-image-resource.md) toouse for creating hello new VM.</span></span> 

<span data-ttu-id="72da2-109">Upewnij się, że najnowsze wersje hello hello modułów AzureRM.Compute i AzureRM.Network programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72da2-109">Make sure that you have hello latest versions of hello AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="72da2-110">Otwórz wiersz programu PowerShell jako Administrator i uruchom następujące polecenie tooinstall hello je.</span><span class="sxs-lookup"><span data-stu-id="72da2-110">Open a PowerShell prompt as an Administrator and run hello following command tooinstall them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="72da2-111">Aby uzyskać więcej informacji, zobacz [przechowywanie wersji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="72da2-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-hello-image"></a><span data-ttu-id="72da2-112">Zbieranie informacji o hello obrazu</span><span class="sxs-lookup"><span data-stu-id="72da2-112">Collect information about hello image</span></span>

<span data-ttu-id="72da2-113">Najpierw możemy toogather podstawowe informacje o obrazie hello i Tworzenie zmiennej hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="72da2-113">First we need toogather basic information about hello image and create a variable for hello image.</span></span> <span data-ttu-id="72da2-114">W tym przykładzie użyto do zarządzanego obrazu maszyny Wirtualnej o nazwie **myImage** będący w hello **myResourceGroup** grupy zasobów w hello **zachodnie centralnej nam** lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="72da2-114">This example uses a managed VM image named **myImage** that is in hello **myResourceGroup** resource group in hello **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="72da2-115">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="72da2-115">Create a virtual network</span></span>
<span data-ttu-id="72da2-116">Tworzenie sieci wirtualnej hello i podsieci hello [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72da2-116">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="72da2-117">Utwórz podsieć hello.</span><span class="sxs-lookup"><span data-stu-id="72da2-117">Create hello subnet.</span></span> <span data-ttu-id="72da2-118">W tym przykładzie tworzy podsieć o nazwie **mySubnet** z prefiksu adresu hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="72da2-118">This example creates a subnet named **mySubnet** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="72da2-119">Utwórz sieć wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="72da2-119">Create hello virtual network.</span></span> <span data-ttu-id="72da2-120">W tym przykładzie tworzy sieć wirtualną o nazwie **myVnet** z prefiksu adresu hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="72da2-120">This example creates a virtual network named **myVnet** with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="72da2-121">Tworzenie publicznego adresu IP adres i interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="72da2-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="72da2-122">tooenable komunikację z maszyną wirtualną hello w sieci wirtualnej hello, należy [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) i interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="72da2-122">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="72da2-123">Utwórz publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="72da2-123">Create a public IP address.</span></span> <span data-ttu-id="72da2-124">W tym przykładzie jest tworzony publiczny adres IP o nazwie **myPip**.</span><span class="sxs-lookup"><span data-stu-id="72da2-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="72da2-125">Utwórz hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="72da2-125">Create hello NIC.</span></span> <span data-ttu-id="72da2-126">W tym przykładzie jest tworzony karty Sieciowej o nazwie **myNic**.</span><span class="sxs-lookup"><span data-stu-id="72da2-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="72da2-127">Tworzenie grupy zabezpieczeń sieci hello i reguły protokołu RDP</span><span class="sxs-lookup"><span data-stu-id="72da2-127">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="72da2-128">toobe stanie toolog w tooyour maszyny Wirtualnej przy użyciu protokołu RDP, należy toohave reguły zabezpieczeń sieci (NSG), umożliwiająca dostęp RDP do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="72da2-128">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="72da2-129">W tym przykładzie tworzy grupy NSG o nazwie **myNsg** zawierający regułę o nazwie **myRdpRule** za pośrednictwem portu 3389 która zezwala na ruch RDP.</span><span class="sxs-lookup"><span data-stu-id="72da2-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="72da2-130">Aby uzyskać więcej informacji na temat grup NSG, zobacz [otwierania portów tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72da2-130">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="72da2-131">Utwórz zmienną hello sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="72da2-131">Create a variable for hello virtual network</span></span>

<span data-ttu-id="72da2-132">Utwórz zmienną ukończyć powitalnych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72da2-132">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="72da2-133">Uzyskać poświadczenia hello hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="72da2-133">Get hello credentials for hello VM</span></span>

<span data-ttu-id="72da2-134">Witaj następującego polecenia cmdlet zostanie otwarte okno którym wprowadza użytkownika nowe toouse nazwę i hasło jako hello konta administratora lokalnego na zdalny dostęp do hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72da2-134">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a><span data-ttu-id="72da2-135">Ustaw zmienne hello maszyny Wirtualnej name, nazwa komputera i hello rozmiar hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="72da2-135">Set variables for hello VM name, computer name and hello size of hello VM</span></span>

1. <span data-ttu-id="72da2-136">Utwórz zmienne hello maszyny Wirtualnej i nazwy komputera.</span><span class="sxs-lookup"><span data-stu-id="72da2-136">Create variables for hello VM name and computer name.</span></span> <span data-ttu-id="72da2-137">W tym przykładzie nazwa maszyny Wirtualnej hello jako **myVM** i nazwa komputera hello jako **Mój komputer**.</span><span class="sxs-lookup"><span data-stu-id="72da2-137">This example sets hello VM name as **myVM** and hello computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="72da2-138">Ustaw rozmiar hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72da2-138">Set hello size of hello virtual machine.</span></span> <span data-ttu-id="72da2-139">Ten przykład tworzy **Standard_DS1_v2** rozmiaru maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72da2-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="72da2-140">Zobacz hello [rozmiarów maszyn wirtualnych](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) dokumentacji, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="72da2-140">See hello [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="72da2-141">Dodaj hello nazwę maszyny Wirtualnej i konfiguracji maszyny Wirtualnej toohello rozmiar.</span><span class="sxs-lookup"><span data-stu-id="72da2-141">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="72da2-142">Obraz maszyny Wirtualnej hello zestawu jako obraz źródłowy dla hello nowej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="72da2-142">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="72da2-143">Ustaw obraz źródłowy hello przy użyciu Identyfikatora hello hello zarządzanego obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="72da2-143">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="72da2-144">Ustawienia konfiguracji systemu operacyjnego hello i Dodaj hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="72da2-144">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="72da2-145">Wprowadź typ magazynu hello (PremiumLRS lub StandardLRS) i hello rozmiar dysku systemu operacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="72da2-145">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="72da2-146">W tym przykładzie typ konta hello zbyt**PremiumLRS**, zbyt hello rozmiar dysku**128 GB** i buforowania dysku zbyt**ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="72da2-146">This example sets hello account type too**PremiumLRS**, hello disk size too**128 GB** and disk caching too**ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="72da2-147">Utwórz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="72da2-147">Create hello VM</span></span>

<span data-ttu-id="72da2-148">Tworzenie nowej maszyny wirtualnej za pomocą hello konfiguracji, które firma Microsoft utworzone i przechowywane w hello hello **$vm** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="72da2-148">Create hello new Vm using hello configuration that we have built and stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="72da2-149">Sprawdź hello, że maszyna wirtualna została utworzona</span><span class="sxs-lookup"><span data-stu-id="72da2-149">Verify that hello VM was created</span></span>
<span data-ttu-id="72da2-150">Po zakończeniu powinien zostać wyświetlony hello nowo utworzony maszyny Wirtualnej w hello [portalu Azure](https://portal.azure.com) w obszarze **Przeglądaj** > **maszyn wirtualnych**, lub za pomocą następujących hello Polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="72da2-150">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="72da2-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="72da2-151">Next steps</span></span>
<span data-ttu-id="72da2-152">toomanage nowej maszyny wirtualnej przy użyciu programu Azure PowerShell, zobacz [tworzenia i zarządzania maszynami wirtualnymi systemu Windows za pomocą modułu Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72da2-152">toomanage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

