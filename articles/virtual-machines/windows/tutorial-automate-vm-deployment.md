---
title: aaaCustomize maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello niestandardowe rozszerzenie skryptu i toocustomize Key Vault maszyn wirtualnych systemu Windows na platformie Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="f3dd8-103">Jak toocustomize maszynę wirtualną systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f3dd8-103">How toocustomize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="f3dd8-104">wymagane jest zwykle tooconfigure maszynach wirtualnych (VM) w sposób szybki i spójne jakiegoś automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-104">tooconfigure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="f3dd8-105">Typowe toocustomize podejście Maszynę wirtualną systemu Windows jest toouse [niestandardowe rozszerzenie skryptu systemu Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="f3dd8-105">A common approach toocustomize a Windows VM is toouse [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="f3dd8-106">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="f3dd8-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f3dd8-107">Użyj hello niestandardowe rozszerzenie skryptu tooinstall usług IIS</span><span class="sxs-lookup"><span data-stu-id="f3dd8-107">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="f3dd8-108">Utwórz maszynę Wirtualną, która używa hello niestandardowe rozszerzenie skryptu</span><span class="sxs-lookup"><span data-stu-id="f3dd8-108">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="f3dd8-109">Wyświetl uruchomionej witryny usług IIS, po zastosowaniu hello rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="f3dd8-109">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="f3dd8-110">Ten samouczek wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-110">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="f3dd8-111">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-111">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="f3dd8-112">Jeśli potrzebujesz tooupgrade, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f3dd8-112">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="f3dd8-113">Omówienie rozszerzenia niestandardowego skryptu</span><span class="sxs-lookup"><span data-stu-id="f3dd8-113">Custom script extension overview</span></span>
<span data-ttu-id="f3dd8-114">Witaj niestandardowe rozszerzenie skryptu pobiera i uruchamia skrypty na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-114">hello Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="f3dd8-115">To rozszerzenie jest przydatne w przypadku konfiguracji wdrożenia post, instalacja oprogramowania lub dowolnej innej konfiguracji / zadanie zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="f3dd8-116">Skryptów można pobrać z magazynu Azure lub usługi GitHub lub podane toohello portalu Azure w rozszerzeniu czas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-116">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span>

<span data-ttu-id="f3dd8-117">Hello rozszerzenia niestandardowego skryptu integruje się z szablonów usługi Azure Resource Manager i można również uruchomić przy użyciu hello wiersza polecenia platformy Azure, programu PowerShell, portalu Azure lub hello interfejsu API REST maszyny wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-117">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="f3dd8-118">W systemach Windows i maszyn wirtualnych systemu Linux, można użyć hello niestandardowe rozszerzenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-118">You can use hello Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="f3dd8-119">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f3dd8-119">Create virtual machine</span></span>
<span data-ttu-id="f3dd8-120">Przed utworzeniem maszyny Wirtualnej, Utwórz nową grupę zasobów o [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="f3dd8-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="f3dd8-121">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupAutomate* w hello *EastUS* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="f3dd8-121">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="f3dd8-122">Ustaw nazwę użytkownika i hasło administratora dla maszyn wirtualnych hello z [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="f3dd8-122">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="f3dd8-123">Teraz możesz utworzyć maszynę Wirtualną za pomocą hello [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f3dd8-123">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="f3dd8-124">Witaj poniższy przykład tworzy hello wymagane składniki sieci wirtualnej, konfiguracja hello systemu operacyjnego, a następnie tworzy Maszynę wirtualną o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="f3dd8-124">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

<span data-ttu-id="f3dd8-125">Trwa kilka minut, aż hello zasobów i utworzyć toobe maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-125">It takes a few minutes for hello resources and VM toobe created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="f3dd8-126">Automatyzowanie instalacji usług IIS</span><span class="sxs-lookup"><span data-stu-id="f3dd8-126">Automate IIS install</span></span>
<span data-ttu-id="f3dd8-127">Użyj [AzureRmVMExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello niestandardowe rozszerzenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="f3dd8-128">Witaj uruchamia rozszerzenia `powershell Add-WindowsFeature Web-Server` tooinstall hello serwer sieci Web usług IIS, a następnie aktualizacje hello *Default.htm* strony tooshow hello nazwy hosta hello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="f3dd8-128">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a><span data-ttu-id="f3dd8-129">Test witryny sieci web</span><span class="sxs-lookup"><span data-stu-id="f3dd8-129">Test web site</span></span>
<span data-ttu-id="f3dd8-130">Uzyskaj hello publicznego adresu IP z usługi równoważenia obciążenia z [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="f3dd8-130">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="f3dd8-131">Witaj poniższy przykład uzyskuje hello adres IP dla *myPublicIP* utworzony wcześniej:</span><span class="sxs-lookup"><span data-stu-id="f3dd8-131">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="f3dd8-132">W przeglądarce sieci web tooa można następnie wprowadzić hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-132">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="f3dd8-133">Hello witryny sieci Web jest wyświetlany, łącznie z nazwą hosta hello hello maszyny Wirtualnej tego modułu równoważenia obciążenia hello rozproszonych tooas ruchu w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f3dd8-133">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Witryna sieci Web IIS uruchomiona](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="f3dd8-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f3dd8-135">Next steps</span></span>

<span data-ttu-id="f3dd8-136">W tym samouczku automatycznego jest hello instalacji usług IIS na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-136">In this tutorial, you automated hello IIS install on a VM.</span></span> <span data-ttu-id="f3dd8-137">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="f3dd8-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f3dd8-138">Użyj hello niestandardowe rozszerzenie skryptu tooinstall usług IIS</span><span class="sxs-lookup"><span data-stu-id="f3dd8-138">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="f3dd8-139">Utwórz maszynę Wirtualną, która używa hello niestandardowe rozszerzenie skryptu</span><span class="sxs-lookup"><span data-stu-id="f3dd8-139">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="f3dd8-140">Wyświetl uruchomionej witryny usług IIS, po zastosowaniu hello rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="f3dd8-140">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="f3dd8-141">Jak przejść dalej toolearn samouczka toohello toocreate niestandardowych obrazów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f3dd8-141">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f3dd8-142">Tworzenie niestandardowych obrazów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="f3dd8-142">Create custom VM images</span></span>](./tutorial-custom-images.md)
