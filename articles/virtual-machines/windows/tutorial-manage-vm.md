---
title: "aaaCreate i zarządzania maszynami wirtualnymi systemu Windows z hello modułu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Samouczek — tworzenie i zarządzanie maszynami wirtualnymi systemu Windows z hello modułu Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a><span data-ttu-id="1fe8b-103">Tworzenie i zarządzanie maszynami wirtualnymi systemu Windows z hello modułu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fe8b-103">Create and Manage Windows VMs with hello Azure PowerShell module</span></span>

<span data-ttu-id="1fe8b-104">Maszyny wirtualne platformy Azure zawierają w pełni konfigurowalne i elastyczne środowiska komputerowego.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="1fe8b-105">Ten samouczek obejmuje elementów wdrożenia podstawowej maszyny wirtualnej platformy Azure, takich jak rozmiar maszyny Wirtualnej, wybierając obrazu maszyny Wirtualnej i wdrażanie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="1fe8b-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="1fe8b-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1fe8b-107">Tworzenie i łączenie tooa maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1fe8b-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="1fe8b-108">Wybierz i używać obrazów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="1fe8b-108">Select and use VM images</span></span>
> * <span data-ttu-id="1fe8b-109">Wyświetlanie i używanie określonych rozmiarów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="1fe8b-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="1fe8b-110">Zmienianie rozmiaru maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1fe8b-110">Resize a VM</span></span>
> * <span data-ttu-id="1fe8b-111">Wyświetlanie i zrozumienie stanu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1fe8b-111">View and understand VM state</span></span>

<span data-ttu-id="1fe8b-112">Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-112">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="1fe8b-113">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-113">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="1fe8b-114">Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1fe8b-114">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="1fe8b-115">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="1fe8b-115">Create resource group</span></span>

<span data-ttu-id="1fe8b-116">Utwórz grupę zasobów o hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) polecenia.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-116">Create a resource group with hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="1fe8b-117">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="1fe8b-118">Grupy zasobów musi zostać utworzone przed maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="1fe8b-119">W tym przykładzie grupy zasobów o nazwie *myResourceGroupVM* jest tworzony w hello *EastUS* regionu.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-119">In this example, a resource group named *myResourceGroupVM* is created in hello *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="1fe8b-120">Grupa zasobów Hello jest określony, podczas tworzenia lub modyfikowania maszyn wirtualnych, które są widoczne w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="1fe8b-121">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1fe8b-121">Create virtual machine</span></span>

<span data-ttu-id="1fe8b-122">Maszyna wirtualna musi być tooa połączonych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-122">A virtual machine must be connected tooa virtual network.</span></span> <span data-ttu-id="1fe8b-123">Do komunikacji z maszyny wirtualnej hello za pomocą publicznego adresu IP za pośrednictwem karty interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-123">You communicate with hello virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="1fe8b-124">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1fe8b-124">Create virtual network</span></span>

<span data-ttu-id="1fe8b-125">Utwórz podsieć o [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="1fe8b-126">Tworzenie sieci wirtualnej z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="1fe8b-127">Utwórz publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="1fe8b-127">Create public IP address</span></span>

<span data-ttu-id="1fe8b-128">Utwórz publiczny adres IP z [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="1fe8b-129">Utwórz karty interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="1fe8b-129">Create network interface card</span></span>

<span data-ttu-id="1fe8b-130">Utwórz kartę sieciową z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="1fe8b-131">Utwórz grupę zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="1fe8b-131">Create network security group</span></span>

<span data-ttu-id="1fe8b-132">Azure [sieciowej grupy zabezpieczeń](../../virtual-network/virtual-networks-nsg.md) (NSG) steruje ruchu przychodzącego i wychodzącego dla jednego lub wielu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="1fe8b-133">Reguły grupy zabezpieczeń sieci akceptować lub odrzucać ruchu sieciowego na określonym porcie lub zakres portów.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="1fe8b-134">Te zasady mogą również obejmować prefiks adresu źródłowego, dzięki czemu tylko ruch w źródle wstępnie zdefiniowanych może komunikować się z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="1fe8b-135">tooaccess hello IIS serwer sieci Web, który jest instalowany, należy dodać regułę ruchu przychodzącego grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-135">tooaccess hello IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="1fe8b-136">Użyj toocreate regułę ruchu przychodzącego grupy NSG [AzureRmNetworkSecurityRuleConfig Dodaj](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="1fe8b-136">toocreate an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="1fe8b-137">Witaj poniższy przykład tworzy reguły NSG o nazwie *myNSGRule* który otwiera port *3389* hello maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="1fe8b-137">hello following example creates an NSG rule named *myNSGRule* that opens port *3389* for hello virtual machine:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

<span data-ttu-id="1fe8b-138">Tworzenie przy użyciu NSG hello *myNSGRule* z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-138">Create hello NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="1fe8b-139">Dodaj hello NSG toohello podsieci w sieci wirtualnej hello o [AzureRmVirtualNetworkSubnetConfig zestaw](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-139">Add hello NSG toohello subnet in hello virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="1fe8b-140">Aktualizacja sieci wirtualnej hello o [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-140">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="1fe8b-141">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1fe8b-141">Create virtual machine</span></span>

<span data-ttu-id="1fe8b-142">Podczas tworzenia maszyny wirtualnej, takich jak obraz systemu operacyjnego, dysku zmiany rozmiaru i administracyjnych poświadczeń jest kilka opcji.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="1fe8b-143">W tym przykładzie utworzono maszynę wirtualną o nazwie *myVM* uruchomionych hello najnowszej wersji systemu Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-143">In this example, a virtual machine is created with a name of *myVM* running hello latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="1fe8b-144">Ustaw hello nazwę użytkownika i hasło potrzebne do konta administratora hello na maszynie wirtualnej hello [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-144">Set hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="1fe8b-145">Utwórz hello konfiguracji początkowej dla maszyny wirtualnej hello o [AzureRmVMConfig nowy](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-145">Create hello initial configuration for hello virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="1fe8b-146">Dodaj hello systemu operacyjnego informacji toohello konfiguracji maszyny wirtualnej z [AzureRmVMOperatingSystem zestaw](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-146">Add hello operating system information toohello virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="1fe8b-147">Dodaj hello obrazu informacji toohello konfiguracji maszyny wirtualnej z [AzureRmVMSourceImage zestaw](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-147">Add hello image information toohello virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="1fe8b-148">Dodaj hello systemu operacyjnego dysku ustawienia toohello konfiguracji maszyny wirtualnej z [AzureRmVMOSDisk zestaw](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-148">Add hello operating system disk settings toohello virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="1fe8b-149">Dodaj hello kartom sieciowym wcześniej utworzony toohello konfiguracji maszyny wirtualnej z [AzureRmVMNetworkInterface Dodaj](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-149">Add hello network interface card that you previously created toohello virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="1fe8b-150">Utwórz maszynę wirtualną hello z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="1fe8b-150">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a><span data-ttu-id="1fe8b-151">Połącz tooVM</span><span class="sxs-lookup"><span data-stu-id="1fe8b-151">Connect tooVM</span></span>

<span data-ttu-id="1fe8b-152">Po zakończeniu wdrożenia hello, tworzenia połączenia pulpitu zdalnego z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-152">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="1fe8b-153">Uruchom następujące polecenia tooreturn hello publicznego adresu IP maszyny wirtualnej hello hello.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-153">Run hello following commands tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="1fe8b-154">Zwróć uwagę ten adres IP, więc tooit mogą łączyć się z tootest przeglądarki sieci web łączność w przyszłości kroku.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-154">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="1fe8b-155">Użyj hello następujące polecenie toocreate sesję pulpitu zdalnego z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-155">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="1fe8b-156">Zamień adres IP hello hello *publicznego adresu IP* maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-156">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="1fe8b-157">Po wyświetleniu monitu wprowadź poświadczenia hello używane podczas tworzenia maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-157">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="1fe8b-158">Zrozumienie obrazów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="1fe8b-158">Understand VM images</span></span>

<span data-ttu-id="1fe8b-159">Hello Azure marketplace zawiera wiele obrazów maszyny wirtualnej, które mogą być używane toocreate nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-159">hello Azure marketplace includes many virtual machine images that can be used toocreate a new virtual machine.</span></span> <span data-ttu-id="1fe8b-160">W poprzednich krokach hello maszyny wirtualnej został utworzony przy użyciu obrazu systemu Windows Server 2016-Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-160">In hello previous steps, a virtual machine was created using hello Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="1fe8b-161">W tym kroku hello modułu programu PowerShell jest używane toosearch hello marketplace dla innych obrazów systemu Windows, które może również jako podstawa dla nowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-161">In this step, hello PowerShell module is used toosearch hello marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="1fe8b-162">Proces ten składa się z znajdowanie hello wydawcy, oferty i nazwa obrazu hello (Sku).</span><span class="sxs-lookup"><span data-stu-id="1fe8b-162">This process consists of finding hello publisher, offer, and hello image name (Sku).</span></span> 

<span data-ttu-id="1fe8b-163">Użyj hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) tooreturn polecenia listę wydawców obrazu.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-163">Use hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command tooreturn a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="1fe8b-164">Użyj hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn listę ofert obrazu.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-164">Use hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn a list of image offers.</span></span> <span data-ttu-id="1fe8b-165">To polecenie hello zwracany lista jest przefiltrowana na powitania określonego wydawcę.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-165">With this command, hello returned list is filtered on hello specified publisher.</span></span> 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

<span data-ttu-id="1fe8b-166">Witaj [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) polecenia zostanie następnie odfiltrować tooreturn nazwę wydawcy i oferty hello listę nazw obrazu.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-166">hello [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on hello publisher and offer name tooreturn a list of image names.</span></span>

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

<span data-ttu-id="1fe8b-167">Te informacje mogą być używane toodeploy maszynę Wirtualną za pomocą określonego obrazu.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-167">This information can be used toodeploy a VM with a specific image.</span></span> <span data-ttu-id="1fe8b-168">W tym przykładzie nazwa obrazu hello na powitania obiektu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-168">This example sets hello image name on hello VM object.</span></span> <span data-ttu-id="1fe8b-169">W tym samouczku instrukcje ukończenia wdrożenia można znaleźć toohello poprzednich przykładach.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-169">Refer toohello previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="1fe8b-170">Zrozumienie rozmiarów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="1fe8b-170">Understand VM sizes</span></span>

<span data-ttu-id="1fe8b-171">Rozmiar maszyny wirtualnej określa hello zasobów obliczeniowych, takich jak Procesora GPU i pamięci wprowadzone toohello dostępne maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-171">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="1fe8b-172">Maszyny wirtualne muszą toobe utworzony z rozmiarem odpowiedniego dla hello oczekiwane obciążenia pracą.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-172">Virtual machines need toobe created with a size appropriate for hello expect work load.</span></span> <span data-ttu-id="1fe8b-173">Jeśli zwiększa obciążenie, można zmienić rozmiar istniejącej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="1fe8b-174">Rozmiary maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="1fe8b-174">VM Sizes</span></span>

<span data-ttu-id="1fe8b-175">w poniższej tabeli Hello kategoryzuje rozmiary do przypadków użycia.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-175">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="1fe8b-176">Typ</span><span class="sxs-lookup"><span data-stu-id="1fe8b-176">Type</span></span>                     | <span data-ttu-id="1fe8b-177">Rozmiary</span><span class="sxs-lookup"><span data-stu-id="1fe8b-177">Sizes</span></span>           |    <span data-ttu-id="1fe8b-178">Opis</span><span class="sxs-lookup"><span data-stu-id="1fe8b-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1fe8b-179">Zastosowania ogólne</span><span class="sxs-lookup"><span data-stu-id="1fe8b-179">General purpose</span></span>         |<span data-ttu-id="1fe8b-180">DSv2, Dv2, DS, D, Av2, A0 7</span><span class="sxs-lookup"><span data-stu-id="1fe8b-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="1fe8b-181">Zrównoważonym Procesora do pamięci.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="1fe8b-182">Nadaje się doskonale dla deweloperów / testu i małych toomedium rozwiązania aplikacji i danych.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-182">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| <span data-ttu-id="1fe8b-183">Optymalizacja pod kątem obliczeń</span><span class="sxs-lookup"><span data-stu-id="1fe8b-183">Compute optimized</span></span>      | <span data-ttu-id="1fe8b-184">FS, F</span><span class="sxs-lookup"><span data-stu-id="1fe8b-184">Fs, F</span></span>             | <span data-ttu-id="1fe8b-185">Wysoka Procesora do pamięci.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-185">High CPU-to-memory.</span></span> <span data-ttu-id="1fe8b-186">Nadaje się do aplikacji średnia ruchu, urządzeń sieciowych i procesów wsadowych.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="1fe8b-187">Optymalizacja pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="1fe8b-187">Memory optimized</span></span>       | <span data-ttu-id="1fe8b-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="1fe8b-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="1fe8b-189">Wysoka pamięci do core.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-189">High memory-to-core.</span></span> <span data-ttu-id="1fe8b-190">Doskonałe rozwiązanie dla relacyjnych baz danych, pamięci podręcznych średnia toolarge i analiza w pamięci.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-190">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="1fe8b-191">Optymalizacja pod kątem magazynu</span><span class="sxs-lookup"><span data-stu-id="1fe8b-191">Storage optimized</span></span>       | <span data-ttu-id="1fe8b-192">Ls</span><span class="sxs-lookup"><span data-stu-id="1fe8b-192">Ls</span></span>                | <span data-ttu-id="1fe8b-193">Wysoka przepływność dysku i operacje we/wy.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-193">High disk throughput and IO.</span></span> <span data-ttu-id="1fe8b-194">Idealne rozwiązanie w przypadku danych big data oraz baz danych SQL i NoSQL.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="1fe8b-195">Procesory GPU</span><span class="sxs-lookup"><span data-stu-id="1fe8b-195">GPU</span></span>           | <span data-ttu-id="1fe8b-196">WIRTUALIZACJĄ SIECI, NC</span><span class="sxs-lookup"><span data-stu-id="1fe8b-196">NV, NC</span></span>            | <span data-ttu-id="1fe8b-197">Celem duże Renderowanie grafiki i wideo edycji specjalne maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="1fe8b-198">Wysoka wydajność</span><span class="sxs-lookup"><span data-stu-id="1fe8b-198">High performance</span></span> | <span data-ttu-id="1fe8b-199">H-A8 11</span><span class="sxs-lookup"><span data-stu-id="1fe8b-199">H, A8-11</span></span>          | <span data-ttu-id="1fe8b-200">Nasze najbardziej zaawansowanych Procesora maszyny wirtualne z interfejsami opcjonalne wysokiej przepustowości sieci (RDMA).</span><span class="sxs-lookup"><span data-stu-id="1fe8b-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="1fe8b-201">Znajdowanie dostępnych rozmiarów maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1fe8b-201">Find available VM sizes</span></span>

<span data-ttu-id="1fe8b-202">toosee listę maszyn wirtualnych rozmiarów dostępnych w określonym regionie, użyj hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) polecenia.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-202">toosee a list of VM sizes available in a particular region, use hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="1fe8b-203">Zmienianie rozmiaru maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1fe8b-203">Resize a VM</span></span>

<span data-ttu-id="1fe8b-204">Po wdrożeniu maszyny Wirtualnej można tooincrease po zmianie rozmiaru lub zmniejszenia alokacji zasobów.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-204">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="1fe8b-205">Przed zmianą rozmiaru maszyny Wirtualnej, sprawdź, czy hello wymagany rozmiar w klastrze jest dostępny hello bieżącej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-205">Before resizing a VM, check if hello desired size is available on hello current VM cluster.</span></span> <span data-ttu-id="1fe8b-206">Witaj [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) polecenie zwraca listę rozmiarów.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-206">hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="1fe8b-207">W razie potrzeby hello się, że rozmiar jest dostępny hello maszyny Wirtualnej można zmienić rozmiar ze stanu zasilania na, jednak podczas hello operacji ponownego rozruchu.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-207">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="1fe8b-208">Jeśli hello żądany rozmiar nie jest na powitania bieżący klaster hello wirtualna potrzeb, może wystąpić toobe alokację przed hello operacja zmiany rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-208">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="1fe8b-209">Uwaga: w przypadku hello maszyny Wirtualnej jest włączona ponownie, zostaną usunięte wszystkie dane na dysku tymczasowym hello i zmienić hello publicznego adresu IP, chyba że używana jest statyczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-209">Note, when hello VM is powered back on, any data on hello temp disk are removed, and hello public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="1fe8b-210">Stany zasilania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1fe8b-210">VM power states</span></span>

<span data-ttu-id="1fe8b-211">Maszyny Wirtualnej platformy Azure może mieć jedną z wielu stany zasilania.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="1fe8b-212">Ten stan reprezentuje hello bieżący stan hello maszyny Wirtualnej z punktu widzenia hello hello funkcji hypervisor.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-212">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="1fe8b-213">Stany zasilania</span><span class="sxs-lookup"><span data-stu-id="1fe8b-213">Power states</span></span>

| <span data-ttu-id="1fe8b-214">Stan zasilania</span><span class="sxs-lookup"><span data-stu-id="1fe8b-214">Power State</span></span> | <span data-ttu-id="1fe8b-215">Opis</span><span class="sxs-lookup"><span data-stu-id="1fe8b-215">Description</span></span>
|----|----|
| <span data-ttu-id="1fe8b-216">Uruchamianie</span><span class="sxs-lookup"><span data-stu-id="1fe8b-216">Starting</span></span> | <span data-ttu-id="1fe8b-217">Wskazuje, że jest uruchamiana hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-217">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="1fe8b-218">Działanie</span><span class="sxs-lookup"><span data-stu-id="1fe8b-218">Running</span></span> | <span data-ttu-id="1fe8b-219">Wskazuje, że działa hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-219">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="1fe8b-220">Zatrzymywanie</span><span class="sxs-lookup"><span data-stu-id="1fe8b-220">Stopping</span></span> | <span data-ttu-id="1fe8b-221">Wskazuje, że tej maszyny wirtualnej hello jest zatrzymywana.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-221">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="1fe8b-222">Zatrzymane</span><span class="sxs-lookup"><span data-stu-id="1fe8b-222">Stopped</span></span> | <span data-ttu-id="1fe8b-223">Wskazuje, że tej maszyny wirtualnej hello jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-223">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="1fe8b-224">Należy pamiętać, że maszyny wirtualne w stanie hello zatrzymana nadal naliczenie opłat za obliczenia.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-224">Note that virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="1fe8b-225">Cofanie przydziału</span><span class="sxs-lookup"><span data-stu-id="1fe8b-225">Deallocating</span></span> | <span data-ttu-id="1fe8b-226">Wskazuje, że cofana jest hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-226">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="1fe8b-227">Cofnięcie przydziału</span><span class="sxs-lookup"><span data-stu-id="1fe8b-227">Deallocated</span></span> | <span data-ttu-id="1fe8b-228">Wskazuje, że hello maszyny wirtualnej jest całkowicie usunięte z hello funkcji hypervisor, ale nadal dostępne w płaszczyźnie kontroli hello.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-228">Indicates that hello virtual machine is completely removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="1fe8b-229">Maszyny wirtualne w stanie Deallocated hello nie naliczenie opłat za obliczenia.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-229">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="1fe8b-230">Wskazuje, że stan zasilania hello hello maszyny wirtualnej jest nieznany.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-230">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="1fe8b-231">Znajdź stan zasilania</span><span class="sxs-lookup"><span data-stu-id="1fe8b-231">Find power state</span></span>

<span data-ttu-id="1fe8b-232">Stan hello tooretrieve określonej maszyny wirtualnej, użyj hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) polecenia.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-232">tooretrieve hello state of a particular VM, use hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="1fe8b-233">Należy się toospecify poprawną nazwę maszyny wirtualnej i grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-233">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="1fe8b-234">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="1fe8b-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="1fe8b-235">Zadania zarządzania</span><span class="sxs-lookup"><span data-stu-id="1fe8b-235">Management tasks</span></span>

<span data-ttu-id="1fe8b-236">Podczas cyklu życia hello maszyny wirtualnej może być toorun zadań zarządzania, takich jak uruchamianie, zatrzymywanie lub usuwanie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-236">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="1fe8b-237">Ponadto można toocreate skrypty tooautomate powtarzających się lub złożonych zadań.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-237">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="1fe8b-238">Przy użyciu programu Azure PowerShell, wiele typowych zadań zarządzania można uruchomić z wiersza polecenia hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-238">Using Azure PowerShell, many common management tasks can be run from hello command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="1fe8b-239">Zatrzymaj maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="1fe8b-239">Stop virtual machine</span></span>

<span data-ttu-id="1fe8b-240">Zatrzymaj i cofnięcia przydzielenia maszynie wirtualnej z [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="1fe8b-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="1fe8b-241">Jeśli chcesz maszyny wirtualnej hello tookeep w nim udostępnione, użyj parametru - StayProvisioned hello.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-241">If you want tookeep hello virtual machine in a provisioned state, use hello -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="1fe8b-242">Uruchom maszynę wirtualną</span><span class="sxs-lookup"><span data-stu-id="1fe8b-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="1fe8b-243">Usuń grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="1fe8b-243">Delete resource group</span></span>

<span data-ttu-id="1fe8b-244">Usunięcie grupy zasobów powoduje usunięcie wszystkie zasoby zawarte w ciągu.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="1fe8b-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1fe8b-245">Next steps</span></span>

<span data-ttu-id="1fe8b-246">W tym samouczku poznanie podstawowych tworzenia maszyny Wirtualnej i zarządzania, np.:</span><span class="sxs-lookup"><span data-stu-id="1fe8b-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1fe8b-247">Tworzenie i łączenie tooa maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1fe8b-247">Create and connect tooa VM</span></span>
> * <span data-ttu-id="1fe8b-248">Wybierz i używać obrazów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="1fe8b-248">Select and use VM images</span></span>
> * <span data-ttu-id="1fe8b-249">Wyświetlanie i używanie określonych rozmiarów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="1fe8b-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="1fe8b-250">Zmienianie rozmiaru maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1fe8b-250">Resize a VM</span></span>
> * <span data-ttu-id="1fe8b-251">Wyświetlanie i zrozumienie stanu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1fe8b-251">View and understand VM state</span></span>

<span data-ttu-id="1fe8b-252">Przejdź dalej toolearn samouczka toohello dysków maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1fe8b-252">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="1fe8b-253">Utwórz i Zarządzaj maszyny Wirtualnej dyski</span><span class="sxs-lookup"><span data-stu-id="1fe8b-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
