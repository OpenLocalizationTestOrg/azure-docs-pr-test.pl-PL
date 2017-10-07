---
title: "aaaCreate i zarządzania maszynami wirtualnymi systemu Windows na platformie Azure używanego przez wiele kart sieciowych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i zarządzanie nimi maszyny Wirtualnej systemu Windows, który ma wiele kart sieciowych tooit dołączone przy użyciu szablonów programu Azure PowerShell lub Menedżera zasobów."
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
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="f0f82-103">Tworzenie i zarządzanie nimi maszyny wirtualnej systemu Windows, który ma wiele kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="f0f82-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="f0f82-104">Maszynach wirtualnych (VM) na platformie Azure mogą mieć wiele toothem kart sieciowych dołączonych interfejsu sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0f82-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached toothem.</span></span> <span data-ttu-id="f0f82-105">Typowy scenariusz obejmuje toohave w różnych podsieciach łączności frontonu i zaplecza, lub sieci dedykowanej tooa monitorowania lub tworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="f0f82-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="f0f82-106">W tym artykule szczegółowo sposób toocreate maszynę Wirtualną, która ma wiele kart sieciowych dołączonych tooit.</span><span class="sxs-lookup"><span data-stu-id="f0f82-106">This article details how toocreate a VM that has multiple NICs attached tooit.</span></span> <span data-ttu-id="f0f82-107">Możesz także dowiedzieć się, jak tooadd lub usuń karty sieciowe z istniejącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0f82-107">You also learn how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="f0f82-108">Różne [rozmiarów maszyn wirtualnych](sizes.md) obsługuje różną liczbę kart sieciowych, więc odpowiednio rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0f82-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="f0f82-109">Aby uzyskać szczegółowe informacje, łącznie ze sposobem toocreate wiele kart sieciowych w ramach własnych skryptów środowiska PowerShell, zobacz [wdrażanie maszyn wirtualnych kart Sieciowych na wielu](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f0f82-109">For detailed information, including how toocreate multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0f82-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f0f82-110">Prerequisites</span></span>
<span data-ttu-id="f0f82-111">Upewnij się, że masz hello [najnowszą wersję programu Azure PowerShell zainstalowany i skonfigurowany](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f0f82-111">Make sure that you have hello [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="f0f82-112">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="f0f82-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f0f82-113">Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="f0f82-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="f0f82-114">Tworzenie maszyny wirtualnej z wieloma kartami sieciowymi</span><span class="sxs-lookup"><span data-stu-id="f0f82-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="f0f82-115">Najpierw utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="f0f82-115">First, create a resource group.</span></span> <span data-ttu-id="f0f82-116">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *EastUs* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="f0f82-116">hello following example creates a resource group named *myResourceGroup* in hello *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="f0f82-117">Tworzenie sieci wirtualnej i podsieci</span><span class="sxs-lookup"><span data-stu-id="f0f82-117">Create virtual network and subnets</span></span>
<span data-ttu-id="f0f82-118">Typowy scenariusz dotyczy toohave sieci wirtualnej co najmniej dwie podsieci.</span><span class="sxs-lookup"><span data-stu-id="f0f82-118">A common scenario is for a virtual network toohave two or more subnets.</span></span> <span data-ttu-id="f0f82-119">W jednej podsieci może być w przypadku ruchu frontonu hello innych transmisji zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f0f82-119">One subnet may be for front-end traffic, hello other for back-end traffic.</span></span> <span data-ttu-id="f0f82-120">tooconnect tooboth podsieci, można następnie używać wielu kart sieciowych na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0f82-120">tooconnect tooboth subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="f0f82-121">Zdefiniuj dwie podsieci sieci wirtualnej z [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="f0f82-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="f0f82-122">Witaj poniższym przykładzie zdefiniowano hello podsieci dla *mySubnetFrontEnd* i *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="f0f82-122">hello following example defines hello subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="f0f82-123">Tworzenie sieci wirtualnej i podsieci z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="f0f82-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="f0f82-124">Witaj poniższy przykład tworzy sieć wirtualną o nazwie *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="f0f82-124">hello following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="f0f82-125">Tworzenie wielu kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="f0f82-125">Create multiple NICs</span></span>
<span data-ttu-id="f0f82-126">Utwórz dwie karty sieciowe z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="f0f82-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="f0f82-127">Dołącz jednej podsieci frontonu toohello karty Sieciowej i jedną podsieć zaplecza toohello karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="f0f82-127">Attach one NIC toohello front-end subnet and one NIC toohello back-end subnet.</span></span> <span data-ttu-id="f0f82-128">Witaj poniższy przykład tworzy karty sieciowe o nazwie *myNic1* i *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="f0f82-128">hello following example creates NICs named *myNic1* and *myNic2*:</span></span>

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

<span data-ttu-id="f0f82-129">Zwykle również utworzyć [sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md) lub [modułu równoważenia obciążenia](../../load-balancer/load-balancer-overview.md) toohelp zarządzania i rozpowszechniają ruch maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f0f82-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="f0f82-130">Witaj [bardziej szczegółowe wielu kart Sieciowych maszyny Wirtualnej](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) artykule opisano tworzenie grupy zabezpieczeń sieci i przypisywanie kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="f0f82-130">hello [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="f0f82-131">Utwórz maszynę wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="f0f82-131">Create hello virtual machine</span></span>
<span data-ttu-id="f0f82-132">Teraz uruchomić toobuild konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0f82-132">Now start toobuild your VM configuration.</span></span> <span data-ttu-id="f0f82-133">Rozmiar każdej maszyny Wirtualnej ma limit hello całkowitą liczbę kart sieciowych, że można dodawać tooa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0f82-133">Each VM size has a limit for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="f0f82-134">Aby uzyskać więcej informacji, zobacz [rozmiarów maszyn wirtualnych systemu Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="f0f82-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="f0f82-135">Ustaw toohello poświadczenia sieci VM `$cred` zmiennej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f0f82-135">Set your VM credentials toohello `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="f0f82-136">Zdefiniuj maszyny Wirtualnej z [nowe AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="f0f82-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="f0f82-137">Witaj poniższym przykładzie zdefiniowano maszyny Wirtualnej o nazwie *myVM* i używa rozmiar maszyny Wirtualnej, która obsługuje więcej niż dwie karty sieciowe (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="f0f82-137">hello following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="f0f82-138">Utwórz hello reszty konfiguracji maszyny Wirtualnej z [AzureRmVMOperatingSystem zestaw](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) i [AzureRmVMSourceImage zestawu](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="f0f82-138">Create hello rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="f0f82-139">Witaj poniższy przykład tworzy Maszynę wirtualną systemu Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="f0f82-139">hello following example creates a Windows Server 2016 VM:</span></span>

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

4. <span data-ttu-id="f0f82-140">Dołącz Witaj dwie karty sieciowe, wcześniej utworzone przy użyciu [AzureRmVMNetworkInterface Dodaj](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="f0f82-140">Attach hello two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="f0f82-141">Na koniec należy utworzyć maszyny Wirtualnej z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f0f82-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a><span data-ttu-id="f0f82-142">Dodaj tooan karty Sieciowej, istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f0f82-142">Add a NIC tooan existing VM</span></span>
<span data-ttu-id="f0f82-143">Dodaj tooadd wirtualnego tooan kart istniejącej maszyny Wirtualnej, deallocate hello maszyny Wirtualnej, hello wirtualnej karty Sieciowej, a następnie uruchomić hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0f82-143">tooadd a virtual NIC tooan existing VM, you deallocate hello VM, add hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="f0f82-144">Cofnięcie przydziału hello maszyny Wirtualnej z [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f0f82-144">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="f0f82-145">Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f0f82-145">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="f0f82-146">Pobierz hello istniejącej konfiguracji hello maszyny Wirtualnej z [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f0f82-146">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="f0f82-147">Witaj poniższy przykład pobiera informacje o hello maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f0f82-147">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="f0f82-148">Witaj poniższy przykład tworzy wirtualnej karty Sieciowej z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface) o nazwie *myNic3* dołączona za*mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="f0f82-148">hello following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached too*mySubnetBackEnd*.</span></span> <span data-ttu-id="f0f82-149">Witaj wirtualnej karty Sieciowej jest dołączony toohello maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup* z [AzureRmVMNetworkInterface Dodaj](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="f0f82-149">hello virtual NIC is then attached toohello VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="f0f82-150">Podstawowy wirtualnych kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="f0f82-150">Primary virtual NICs</span></span>
    <span data-ttu-id="f0f82-151">Jedną z kart sieciowych w maszynie Wirtualnej z wieloma kartami Sieciowymi hello musi toobe podstawowej.</span><span class="sxs-lookup"><span data-stu-id="f0f82-151">One of hello NICs on a multi-NIC VM needs toobe primary.</span></span> <span data-ttu-id="f0f82-152">Jeśli jeden z hello istniejących wirtualnych kart sieciowych na powitania maszyna wirtualna jest już ustawiony jako podstawowy, możesz pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="f0f82-152">If one of hello existing virtual NICs on hello VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="f0f82-153">Witaj poniższym przykładzie założono, że dwie wirtualne karty sieciowe teraz znajdują się na maszynie Wirtualnej i chcesz tooadd hello pierwszej karty Sieciowej (`[0]`) jako podstawowy hello:</span><span class="sxs-lookup"><span data-stu-id="f0f82-153">hello following example assumes that two virtual NICs are now present on a VM and you wish tooadd hello first NIC (`[0]`) as hello primary:</span></span>
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="f0f82-154">Uruchom hello maszyny Wirtualnej z [Start AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f0f82-154">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="f0f82-155">Usuń z istniejącej maszyny Wirtualnej karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="f0f82-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="f0f82-156">tooremove wirtualnej karty Sieciowej z istniejącej maszyny Wirtualnej, deallocate hello maszyna wirtualna, Usuń hello wirtualnej karty Sieciowej, a następnie hello uruchomienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0f82-156">tooremove a virtual NIC from an existing VM, you deallocate hello VM, remove hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="f0f82-157">Cofnięcie przydziału hello maszyny Wirtualnej z [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f0f82-157">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="f0f82-158">Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f0f82-158">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="f0f82-159">Pobierz hello istniejącej konfiguracji hello maszyny Wirtualnej z [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f0f82-159">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="f0f82-160">Witaj poniższy przykład pobiera informacje o hello maszyny Wirtualnej o nazwie *myVM* w *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f0f82-160">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="f0f82-161">Pobierz informacje o hello Usuń kartę Sieciową z [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="f0f82-161">Get information about hello NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="f0f82-162">Witaj poniższy przykład pobiera informacje *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="f0f82-162">hello following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="f0f82-163">Usuń hello kartą Sieciową o [AzureRmVMNetworkInterface Usuń](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) , a następnie aktualizacji hello maszyny Wirtualnej z [AzureRmVm aktualizacji](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f0f82-163">Remove hello NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update hello VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="f0f82-164">Witaj poniższy przykład umożliwia usunięcie *myNic3* uzyskanych przez `$nicId` w hello poprzedzających krok:</span><span class="sxs-lookup"><span data-stu-id="f0f82-164">hello following example removes *myNic3* as obtained by `$nicId` in hello preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="f0f82-165">Uruchom hello maszyny Wirtualnej z [Start AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f0f82-165">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="f0f82-166">Tworzenie wielu kart sieciowych z szablonami</span><span class="sxs-lookup"><span data-stu-id="f0f82-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="f0f82-167">Szablony usługi Azure Resource Manager Podaj toocreate sposób wielu wystąpień zasobu podczas wdrażania, takich jak tworzenie wielu kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="f0f82-167">Azure Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="f0f82-168">Szablony Menedżera zasobów za pomocą deklaratywne toodefine pliki JSON Twojego środowiska.</span><span class="sxs-lookup"><span data-stu-id="f0f82-168">Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="f0f82-169">Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f0f82-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="f0f82-170">Można użyć *kopiowania* toospecify hello liczbę wystąpień toocreate:</span><span class="sxs-lookup"><span data-stu-id="f0f82-170">You can use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="f0f82-171">Aby uzyskać więcej informacji, zobacz [tworzenie wielu wystąpień przy użyciu *kopiowania*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="f0f82-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="f0f82-172">Można również użyć `copyIndex()` tooappend numer tooa Nazwa zasobu.</span><span class="sxs-lookup"><span data-stu-id="f0f82-172">You can also use `copyIndex()` tooappend a number tooa resource name.</span></span> <span data-ttu-id="f0f82-173">Następnie możesz utworzyć *myNic1*, *MyNic2* i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="f0f82-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="f0f82-174">Witaj poniższy kod przedstawia przykład dołączanie wartość indeksu hello:</span><span class="sxs-lookup"><span data-stu-id="f0f82-174">hello following code shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="f0f82-175">Pełny przykład można znaleźć [tworzenia wielu kart sieciowych przy użyciu szablonów usługi Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="f0f82-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0f82-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0f82-176">Next steps</span></span>
<span data-ttu-id="f0f82-177">Przegląd [rozmiarów maszyn wirtualnych systemu Windows](sizes.md) Jeśli próbujesz toocreate maszynę Wirtualną, która ma wiele kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="f0f82-177">Review [Windows VM sizes](sizes.md) when you're trying toocreate a VM that has multiple NICs.</span></span> <span data-ttu-id="f0f82-178">Należy zwrócić uwagę toohello maksymalną liczbę kart sieciowych obsługiwanych przez każdy rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f0f82-178">Pay attention toohello maximum number of NICs that each VM size supports.</span></span> 


