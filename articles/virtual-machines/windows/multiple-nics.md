---
title: "Tworzenie i zarządzanie maszynami wirtualnymi systemu Windows na platformie Azure używanego przez wiele kart sieciowych | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia i zarządzania nimi maszyny Wirtualnej systemu Windows, który ma wiele kart sieciowych do niego dołączony przy użyciu szablonów programu Azure PowerShell lub Menedżera zasobów."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 3bd99a67dae41de3533d7f6e244eb7ee3ecc4049
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="f3aab-103">Tworzenie i zarządzanie nimi maszyny wirtualnej systemu Windows, który ma wiele kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="f3aab-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="f3aab-104">Maszynach wirtualnych (VM) na platformie Azure mogą mieć wiele wirtualnych kart interfejsu sieciowego (NIC) dołączona do nich.</span><span class="sxs-lookup"><span data-stu-id="f3aab-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached to them.</span></span> <span data-ttu-id="f3aab-105">Typowy scenariusz ma różne podsieci dla łączności frontonu i zaplecza lub sieć przeznaczona do monitorowania lub kopii zapasowej rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="f3aab-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="f3aab-106">Ten artykuł zawiera szczegóły dotyczące sposobu tworzenia maszyny Wirtualnej, który ma wiele kart sieciowych do niego dołączony.</span><span class="sxs-lookup"><span data-stu-id="f3aab-106">This article details how to create a VM that has multiple NICs attached to it.</span></span> <span data-ttu-id="f3aab-107">Możesz również sposób dodawania lub usuwania kart sieciowych z istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f3aab-107">You also learn how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="f3aab-108">Różne [rozmiarów maszyn wirtualnych](sizes.md) obsługuje różną liczbę kart sieciowych, więc odpowiednio rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f3aab-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="f3aab-109">Aby uzyskać szczegółowe informacje, łącznie ze sposobem tworzenia wielu kart sieciowych w ramach własnych skryptów środowiska PowerShell, zobacz [wdrażanie maszyn wirtualnych kart Sieciowych na wielu](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f3aab-109">For detailed information, including how to create multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3aab-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f3aab-110">Prerequisites</span></span>
<span data-ttu-id="f3aab-111">Upewnij się, że masz [najnowszą wersję programu Azure PowerShell zainstalowany i skonfigurowany](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f3aab-111">Make sure that you have the [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="f3aab-112">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="f3aab-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f3aab-113">Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="f3aab-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="f3aab-114">Tworzenie maszyny wirtualnej z wieloma kartami sieciowymi</span><span class="sxs-lookup"><span data-stu-id="f3aab-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="f3aab-115">Najpierw utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="f3aab-115">First, create a resource group.</span></span> <span data-ttu-id="f3aab-116">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w *EastUs* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="f3aab-116">The following example creates a resource group named *myResourceGroup* in the *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="f3aab-117">Tworzenie sieci wirtualnej i podsieci</span><span class="sxs-lookup"><span data-stu-id="f3aab-117">Create virtual network and subnets</span></span>
<span data-ttu-id="f3aab-118">Typowy scenariusz dotyczy sieci wirtualnej do dwóch lub więcej podsieci.</span><span class="sxs-lookup"><span data-stu-id="f3aab-118">A common scenario is for a virtual network to have two or more subnets.</span></span> <span data-ttu-id="f3aab-119">W jednej podsieci mogą być frontonu ruchu, a drugą dla ruchu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f3aab-119">One subnet may be for front-end traffic, the other for back-end traffic.</span></span> <span data-ttu-id="f3aab-120">Aby połączyć się obie podsieci, będzie używać wielu kart sieciowych na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f3aab-120">To connect to both subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="f3aab-121">Zdefiniuj dwie podsieci sieci wirtualnej z [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="f3aab-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="f3aab-122">W poniższym przykładzie zdefiniowano podsieci dla *mySubnetFrontEnd* i *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="f3aab-122">The following example defines the subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="f3aab-123">Tworzenie sieci wirtualnej i podsieci z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="f3aab-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="f3aab-124">Poniższy przykład tworzy sieć wirtualną o nazwie *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="f3aab-124">The following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="f3aab-125">Tworzenie wielu kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="f3aab-125">Create multiple NICs</span></span>
<span data-ttu-id="f3aab-126">Utwórz dwie karty sieciowe z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="f3aab-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="f3aab-127">Dołącz jedną kartę Sieciową do podsieci frontonu i jednej karcie Sieciowej z podsiecią zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f3aab-127">Attach one NIC to the front-end subnet and one NIC to the back-end subnet.</span></span> <span data-ttu-id="f3aab-128">Poniższy przykład tworzy karty sieciowe o nazwie *myNic1* i *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="f3aab-128">The following example creates NICs named *myNic1* and *myNic2*:</span></span>

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

<span data-ttu-id="f3aab-129">Zwykle również utworzyć [sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md) lub [modułu równoważenia obciążenia](../../load-balancer/load-balancer-overview.md) ułatwia zarządzanie i rozpowszechniają ruch maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f3aab-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="f3aab-130">[Bardziej szczegółowe wielu kart Sieciowych maszyny Wirtualnej](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) artykule opisano tworzenie grupy zabezpieczeń sieci i przypisywanie kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="f3aab-130">The [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-the-virtual-machine"></a><span data-ttu-id="f3aab-131">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f3aab-131">Create the virtual machine</span></span>
<span data-ttu-id="f3aab-132">Teraz rozpocząć tworzenie konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f3aab-132">Now start to build your VM configuration.</span></span> <span data-ttu-id="f3aab-133">Rozmiar każdej maszyny Wirtualnej ma limit całkowitej liczby kart sieciowych, które można dodać do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f3aab-133">Each VM size has a limit for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="f3aab-134">Aby uzyskać więcej informacji, zobacz [rozmiarów maszyn wirtualnych systemu Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="f3aab-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="f3aab-135">Ustaw poświadczenia maszyny Wirtualnej `$cred` zmiennej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f3aab-135">Set your VM credentials to the `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="f3aab-136">Zdefiniuj maszyny Wirtualnej z [nowe AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="f3aab-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="f3aab-137">W poniższym przykładzie zdefiniowano maszyny Wirtualnej o nazwie *myVM* i używa rozmiar maszyny Wirtualnej, która obsługuje więcej niż dwie karty sieciowe (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="f3aab-137">The following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="f3aab-138">Utwórz reszty konfiguracji maszyny Wirtualnej z [AzureRmVMOperatingSystem zestaw](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) i [AzureRmVMSourceImage zestawu](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="f3aab-138">Create the rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="f3aab-139">Poniższy przykład tworzy Maszynę wirtualną systemu Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="f3aab-139">The following example creates a Windows Server 2016 VM:</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. <span data-ttu-id="f3aab-140">Dołącz dwie karty sieciowe utworzone wcześniej przy użyciu [AzureRmVMNetworkInterface Dodaj](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="f3aab-140">Attach the two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="f3aab-141">Na koniec należy utworzyć maszyny Wirtualnej z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f3aab-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-to-an-existing-vm"></a><span data-ttu-id="f3aab-142">Dodać kartę Sieciową do istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f3aab-142">Add a NIC to an existing VM</span></span>
<span data-ttu-id="f3aab-143">Aby dodać wirtualną kartę Sieciową do istniejącej maszyny Wirtualnej, deallocate maszyny Wirtualnej, dodać wirtualnej karty Sieciowej, a następnie uruchom maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="f3aab-143">To add a virtual NIC to an existing VM, you deallocate the VM, add the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="f3aab-144">Cofnięcie przydziału maszyny Wirtualnej z [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f3aab-144">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="f3aab-145">Poniższy przykład cofa alokację maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f3aab-145">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="f3aab-146">Pobierz istniejącej konfiguracji maszyny Wirtualnej z [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f3aab-146">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="f3aab-147">Poniższy przykład pobiera informacje o Maszynie wirtualnej o nazwie *myVM* w *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f3aab-147">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="f3aab-148">Poniższy przykład tworzy wirtualnej karty Sieciowej z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface) o nazwie *myNic3* dołączona do *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="f3aab-148">The following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached to *mySubnetBackEnd*.</span></span> <span data-ttu-id="f3aab-149">Wirtualnej karty Sieciowej jest następnie dołączony do maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup* z [AzureRmVMNetworkInterface Dodaj](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="f3aab-149">The virtual NIC is then attached to the VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for the back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get the ID of the new virtual NIC and add to VM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="f3aab-150">Podstawowy wirtualnych kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="f3aab-150">Primary virtual NICs</span></span>
    <span data-ttu-id="f3aab-151">Jedną z kart sieciowych w maszynie Wirtualnej z wieloma kartami Sieciowymi, musi być podstawowym.</span><span class="sxs-lookup"><span data-stu-id="f3aab-151">One of the NICs on a multi-NIC VM needs to be primary.</span></span> <span data-ttu-id="f3aab-152">Jeśli jeden z istniejących wirtualnych kart sieciowych w maszynie Wirtualnej jest już ustawiony jako podstawowy, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="f3aab-152">If one of the existing virtual NICs on the VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="f3aab-153">W poniższym przykładzie założono, że dwie wirtualne karty sieciowe teraz znajdują się na maszynie Wirtualnej i chcesz dodać pierwszej karty Sieciowej (`[0]`) jako serwera podstawowego:</span><span class="sxs-lookup"><span data-stu-id="f3aab-153">The following example assumes that two virtual NICs are now present on a VM and you wish to add the first NIC (`[0]`) as the primary:</span></span>
        
    ```powershell
    # List existing NICs on the VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 to be primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update the VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="f3aab-154">Uruchom maszynę Wirtualną z [Start AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f3aab-154">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="f3aab-155">Usuń z istniejącej maszyny Wirtualnej karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="f3aab-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="f3aab-156">Usunięcie wirtualnej karty Sieciowej z istniejącej maszyny Wirtualnej, należy cofnąć maszyny Wirtualnej, Usuń wirtualną kartę Sieciową, a następnie uruchom maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="f3aab-156">To remove a virtual NIC from an existing VM, you deallocate the VM, remove the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="f3aab-157">Cofnięcie przydziału maszyny Wirtualnej z [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f3aab-157">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="f3aab-158">Poniższy przykład cofa alokację maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f3aab-158">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="f3aab-159">Pobierz istniejącej konfiguracji maszyny Wirtualnej z [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f3aab-159">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="f3aab-160">Poniższy przykład pobiera informacje o Maszynie wirtualnej o nazwie *myVM* w *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f3aab-160">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="f3aab-161">Pobierz informacje o Usuń kartę Sieciową z [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="f3aab-161">Get information about the NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="f3aab-162">Poniższy przykład pobiera informacje *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="f3aab-162">The following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on the VM if you need to determine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="f3aab-163">Usuń z kartą Sieciową o [AzureRmVMNetworkInterface Usuń](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) , a następnie zaktualizować maszyny Wirtualnej z [AzureRmVm aktualizacji](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f3aab-163">Remove the NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update the VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="f3aab-164">Poniższy przykład umożliwia usunięcie *myNic3* uzyskanych przez `$nicId` w poprzednim kroku:</span><span class="sxs-lookup"><span data-stu-id="f3aab-164">The following example removes *myNic3* as obtained by `$nicId` in the preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="f3aab-165">Uruchom maszynę Wirtualną z [Start AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f3aab-165">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="f3aab-166">Tworzenie wielu kart sieciowych z szablonami</span><span class="sxs-lookup"><span data-stu-id="f3aab-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="f3aab-167">Szablony usługi Azure Resource Manager zapewnia możliwości tworzenia wielu wystąpień zasobu podczas wdrażania, takich jak tworzenie wielu kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="f3aab-167">Azure Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="f3aab-168">Szablony Menedżera zasobów umożliwia definiowanie środowiska deklaratywne pliki w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="f3aab-168">Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="f3aab-169">Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f3aab-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="f3aab-170">Można użyć *kopiowania* umożliwia określenie liczby wystąpień, aby utworzyć:</span><span class="sxs-lookup"><span data-stu-id="f3aab-170">You can use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="f3aab-171">Aby uzyskać więcej informacji, zobacz [tworzenie wielu wystąpień przy użyciu *kopiowania*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f3aab-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="f3aab-172">Można również użyć `copyIndex()` dołączyć numer do nazwy zasobu.</span><span class="sxs-lookup"><span data-stu-id="f3aab-172">You can also use `copyIndex()` to append a number to a resource name.</span></span> <span data-ttu-id="f3aab-173">Następnie możesz utworzyć *myNic1*, *MyNic2* i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="f3aab-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="f3aab-174">Poniższy kod przedstawia przykład dołączanie wartość indeksu:</span><span class="sxs-lookup"><span data-stu-id="f3aab-174">The following code shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="f3aab-175">Pełny przykład można znaleźć [tworzenia wielu kart sieciowych przy użyciu szablonów usługi Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="f3aab-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3aab-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f3aab-176">Next steps</span></span>
<span data-ttu-id="f3aab-177">Przegląd [rozmiarów maszyn wirtualnych systemu Windows](sizes.md) Jeśli próbujesz utworzyć maszynę Wirtualną, która ma wiele kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="f3aab-177">Review [Windows VM sizes](sizes.md) when you're trying to create a VM that has multiple NICs.</span></span> <span data-ttu-id="f3aab-178">Należy zwrócić uwagę na maksymalną liczbę kart sieciowych obsługiwanych przez każdy rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f3aab-178">Pay attention to the maximum number of NICs that each VM size supports.</span></span> 


