---
title: aaaAzure sieci wirtualnych i maszyn wirtualnych z systemem Windows | Dokumentacja firmy Microsoft
description: "Samouczek — Zarządzanie sieciami wirtualnymi platformy Azure i maszyn wirtualnych z systemem Windows przy użyciu programu Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="555bb-103">Zarządzanie sieciami wirtualnymi platformy Azure i maszyn wirtualnych z systemem Windows przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="555bb-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="555bb-104">Maszyny wirtualne platformy Azure używania sieci platformy Azure do komunikacji sieciowej wewnętrznych i zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="555bb-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="555bb-105">W tym samouczku należy utworzyć wiele maszyn wirtualnych (VM) w sieci wirtualnej i skonfigurować łączność sieciową między nimi.</span><span class="sxs-lookup"><span data-stu-id="555bb-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="555bb-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="555bb-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="555bb-107">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="555bb-107">Create a virtual network</span></span>
> * <span data-ttu-id="555bb-108">Tworzenie podsieci sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="555bb-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="555bb-109">Kontrola ruchu sieciowego z grup zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="555bb-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="555bb-110">Widok reguły ruchu w akcji</span><span class="sxs-lookup"><span data-stu-id="555bb-110">View traffic rules in action</span></span>

<span data-ttu-id="555bb-111">Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="555bb-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="555bb-112">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="555bb-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="555bb-113">Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="555bb-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="555bb-114">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="555bb-114">Create VNet</span></span>

<span data-ttu-id="555bb-115">Sieci wirtualnej jest reprezentację sieci w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="555bb-115">A VNet is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="555bb-116">Sieci wirtualnej jest logiczną izolacją hello subskrypcji tooyour chmury Azure w wersji dedykowanej.</span><span class="sxs-lookup"><span data-stu-id="555bb-116">A VNet is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="555bb-117">W ramach sieci wirtualnej można znaleźć podsieci, zasad łączności toothose podsieci i połączeń z podsieciami toohello maszyn wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="555bb-117">Within a VNet, you find subnets, rules for connectivity toothose subnets, and connections from hello VMs toohello subnets.</span></span>

<span data-ttu-id="555bb-118">Przed utworzeniem innych zasobów platformy Azure, należy toocreate grupą zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="555bb-118">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="555bb-119">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myRGNetwork* w hello *EastUS* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="555bb-119">hello following example creates a resource group named *myRGNetwork* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="555bb-120">Podsieć jest zasobem podrzędnych sieci wirtualnej i pomaga zdefiniować segmenty przestrzeni adresów w obrębie blok CIDR, przy użyciu prefiksów adresów IP.</span><span class="sxs-lookup"><span data-stu-id="555bb-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="555bb-121">Karty sieciowe mogą być dodawane toosubnets i tooVMs połączone, zapewniają łączność dla różnych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="555bb-121">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="555bb-122">Utwórz podsieć o [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="555bb-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="555bb-123">Tworzenie sieci Wirtualnej o nazwie *myVNet* przy użyciu *myFrontendSubnet* z [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="555bb-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="555bb-124">Tworzenie maszyny Wirtualnej z frontonu</span><span class="sxs-lookup"><span data-stu-id="555bb-124">Create front-end VM</span></span>

<span data-ttu-id="555bb-125">Toocommunicate maszyny Wirtualnej w sieci wirtualnej musi on interfejs sieci wirtualnej (NIC).</span><span class="sxs-lookup"><span data-stu-id="555bb-125">For a VM toocommunicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="555bb-126">Witaj *myFrontendVM* jest dostępny z hello internetowe, dlatego też potrzebuje publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="555bb-126">hello *myFrontendVM* is accessed from hello internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="555bb-127">Utwórz publiczny adres IP z [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="555bb-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="555bb-128">Utwórz kartę Sieciową z [nowe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="555bb-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="555bb-129">Ustaw hello nazwę użytkownika i hasło potrzebne do konta administratora hello na powitania maszyny Wirtualnej z [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="555bb-129">Set hello username and password needed for hello administrator account on hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="555bb-130">Tworzenie maszyn wirtualnych hello z [AzureRmVMConfig nowy](/powershell/module/azurerm.compute/new-azurermvmconfig), [AzureRmVMOperatingSystem zestaw](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [AzureRmVMSourceImage zestaw](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Dodać AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), i [nowe AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="555bb-130">Create hello VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a><span data-ttu-id="555bb-131">Zainstaluj serwer sieci web</span><span class="sxs-lookup"><span data-stu-id="555bb-131">Install web server</span></span>

<span data-ttu-id="555bb-132">Można zainstalować usługi IIS na *myFrontendVM* przy użyciu sesji pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="555bb-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="555bb-133">Należy tooget hello publicznego adresu IP hello wirtualna tooaccess go.</span><span class="sxs-lookup"><span data-stu-id="555bb-133">You need tooget hello public IP address of hello VM tooaccess it.</span></span>

<span data-ttu-id="555bb-134">Można uzyskać hello publicznego adresu IP *myFrontendVM* z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="555bb-134">You can get hello public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="555bb-135">Witaj poniższy przykład uzyskuje hello adres IP dla *myPublicIPAddress* utworzony wcześniej:</span><span class="sxs-lookup"><span data-stu-id="555bb-135">hello following example obtains hello IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="555bb-136">Zwróć uwagę, ten adres IP, dzięki czemu można używać w przyszłości czynności.</span><span class="sxs-lookup"><span data-stu-id="555bb-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="555bb-137">Użyj hello następujące polecenie toocreate sesję pulpitu zdalnego z *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="555bb-137">Use hello following command toocreate a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="555bb-138">Zastąp  *<publicIPAddress>*  z adresem hello uprzednio zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="555bb-138">Replace *<publicIPAddress>* with hello address that you previously recorded.</span></span> <span data-ttu-id="555bb-139">Po wyświetleniu monitu wprowadź poświadczenia hello przy tworzeniu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="555bb-139">When prompted, enter hello credentials used when you created hello VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="555bb-140">Teraz, gdy użytkownik zalogował się za*myFrontendVM*, można użyć pojedynczy wiersz tooinstall PowerShell usług IIS i włączyć ruchu tooallow reguły hello lokalnej zapory w sieci web.</span><span class="sxs-lookup"><span data-stu-id="555bb-140">Now that you have logged in too*myFrontendVM*, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="555bb-141">Otwórz wiersz programu PowerShell i uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="555bb-141">Open a PowerShell prompt and run hello following command:</span></span>

<span data-ttu-id="555bb-142">Użyj [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello niestandardowe rozszerzenie skryptu, który instaluje serwer sieci Web usług IIS hello:</span><span class="sxs-lookup"><span data-stu-id="555bb-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello custom script extension that installs hello IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="555bb-143">Teraz można używać hello publicznego adresu IP adres toobrowse toohello wirtualna toosee hello witryny usług IIS.</span><span class="sxs-lookup"><span data-stu-id="555bb-143">Now you can use hello public IP address toobrowse toohello VM toosee hello IIS site.</span></span>

![Domyślna witryna usług IIS](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="555bb-145">Zarządzanie ruchem wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="555bb-145">Manage internal traffic</span></span>

<span data-ttu-id="555bb-146">Grupa zabezpieczeń sieci (NSG) zawiera listę reguł zabezpieczeń, które lub odmawiają tooa tooresources połączone ruchu sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="555bb-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooa VNet.</span></span> <span data-ttu-id="555bb-147">Grupy NSG mogą być skojarzone toosubnets lub tooVMs dołączony poszczególnymi kartami sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="555bb-147">NSGs can be associated toosubnets or individual NICs attached tooVMs.</span></span> <span data-ttu-id="555bb-148">Otwarcie lub zamknięcie tooVMs dostęp za pośrednictwem portów jest wykonywane przy użyciu reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="555bb-148">Opening or closing access tooVMs through ports is done using NSG rules.</span></span> <span data-ttu-id="555bb-149">Podczas tworzenia *myFrontendVM*, przychodzący port 3389 automatycznie zostało otwarte połączenia RDP.</span><span class="sxs-lookup"><span data-stu-id="555bb-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="555bb-150">Za pomocą grupy NSG można skonfigurować komunikację wewnętrzną maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="555bb-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="555bb-151">W tej sekcji omówiono sposób toocreate dodatkowe podsieci w hello sieciowe i przypisz tooallow tooit NSG połączenia z *myFrontendVM* za*myBackendVM* na porcie 1433.</span><span class="sxs-lookup"><span data-stu-id="555bb-151">In this section, you learn how toocreate an additional subnet in hello network and assign an NSG tooit tooallow a connection from *myFrontendVM* too*myBackendVM* on port 1433.</span></span> <span data-ttu-id="555bb-152">podsieci Hello jest przypisywana toohello maszyny Wirtualnej po jej utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="555bb-152">hello subnet is then assigned toohello VM when it is created.</span></span>

<span data-ttu-id="555bb-153">Można ograniczyć ruch wewnętrzny zbyt*myBackendVM* tylko od *myFrontendVM* przez utworzenie grupy NSG podsieci wewnętrznej hello.</span><span class="sxs-lookup"><span data-stu-id="555bb-153">You can limit internal traffic too*myBackendVM* from only *myFrontendVM* by creating an NSG for hello back-end subnet.</span></span> <span data-ttu-id="555bb-154">Witaj poniższy przykład tworzy reguły NSG o nazwie *myBackendNSGRule* z [AzureRmNetworkSecurityRuleConfig nowy](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="555bb-154">hello following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

<span data-ttu-id="555bb-155">Dodaj sieciową grupę zabezpieczeń o nazwie *myBackendNSG* z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="555bb-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="555bb-156">Dodaj podsieć zaplecza</span><span class="sxs-lookup"><span data-stu-id="555bb-156">Add back-end subnet</span></span>

<span data-ttu-id="555bb-157">Dodaj *myBackEndSubnet* za*myVNet* z [AzureRmVirtualNetworkSubnetConfig Dodaj](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="555bb-157">Add *myBackEndSubnet* too*myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a><span data-ttu-id="555bb-158">Tworzenie maszyny Wirtualnej z zaplecza</span><span class="sxs-lookup"><span data-stu-id="555bb-158">Create back-end VM</span></span>

<span data-ttu-id="555bb-159">Witaj Najprostszym sposobem toocreate Witaj zaplecza maszyny Wirtualnej jest przy użyciu obrazu programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="555bb-159">hello easiest way toocreate hello back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="555bb-160">W tym samouczku tylko tworzy hello maszyny Wirtualnej z serwerem bazy danych hello, ale nie dostarcza informacji na temat uzyskiwania dostępu do bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="555bb-160">This tutorial only creates hello VM with hello database server, but doesn't provide information about accessing hello database.</span></span>

<span data-ttu-id="555bb-161">Utwórz *myBackendNic*:</span><span class="sxs-lookup"><span data-stu-id="555bb-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="555bb-162">Ustaw hello nazwę użytkownika i hasło potrzebne do konta administratora hello na powitania maszyny Wirtualnej z Get-Credential:</span><span class="sxs-lookup"><span data-stu-id="555bb-162">Set hello username and password needed for hello administrator account on hello VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="555bb-163">Utwórz *myBackendVM*:</span><span class="sxs-lookup"><span data-stu-id="555bb-163">Create *myBackendVM*:</span></span>

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

<span data-ttu-id="555bb-164">Obraz powitania, który jest używany zainstalowany program SQL Server, ale nie jest używana w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="555bb-164">hello image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="555bb-165">Jest dołączony tooshow możesz sposobu konfigurowania ruchu w sieci web toohandle maszyny Wirtualnej i zarządzania bazy danych toohandle maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="555bb-165">It is included tooshow you how you can configure a VM toohandle web traffic and a VM toohandle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="555bb-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="555bb-166">Next steps</span></span>

<span data-ttu-id="555bb-167">W tym samouczku zostało utworzone i zabezpieczonej sieci platformy Azure jako powiązane toovirtual maszyny.</span><span class="sxs-lookup"><span data-stu-id="555bb-167">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="555bb-168">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="555bb-168">Create a virtual network</span></span>
> * <span data-ttu-id="555bb-169">Tworzenie podsieci sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="555bb-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="555bb-170">Kontrola ruchu sieciowego z grup zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="555bb-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="555bb-171">Widok reguły ruchu w akcji</span><span class="sxs-lookup"><span data-stu-id="555bb-171">View traffic rules in action</span></span>

<span data-ttu-id="555bb-172">Przejdź dalej toolearn samouczka toohello o monitorowaniu Zabezpieczanie danych w przypadku maszyn wirtualnych przy użyciu kopii zapasowej systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="555bb-172">Advance toohello next tutorial toolearn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="555bb-173">.</span><span class="sxs-lookup"><span data-stu-id="555bb-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="555bb-174">Tworzenie kopii zapasowych maszyn wirtualnych systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="555bb-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
