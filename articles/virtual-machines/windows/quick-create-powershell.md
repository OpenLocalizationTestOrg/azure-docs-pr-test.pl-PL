---
title: "Szybki Start - aaaAzure utworzyć Windows PowerShell maszyny Wirtualnej | Dokumentacja firmy Microsoft"
description: "Dowiesz toocreate maszyn wirtualnych systemu Windows, przy użyciu programu PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="25750-103">Tworzenie maszyny wirtualnej z systemem Windows za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="25750-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="25750-104">modułu Azure PowerShell Hello jest używany toocreate i zarządzania zasobami Azure z wiersza polecenia programu PowerShell hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="25750-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="25750-105">Szczegóły tego przewodnika przy użyciu programu PowerShell toocreate i Azure maszyny wirtualnej z systemem Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="25750-105">This guide details using PowerShell toocreate and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="25750-106">Po zakończeniu wdrażania nawiązanie połączenia toohello serwera i zainstaluj usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="25750-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>  

<span data-ttu-id="25750-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="25750-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="25750-108">To szybki start wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="25750-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="25750-109">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="25750-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="25750-110">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="25750-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="25750-111">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="25750-111">Log in tooAzure</span></span>

<span data-ttu-id="25750-112">Zaloguj się za tooyour subskrypcji platformy Azure z hello `Login-AzureRmAccount` poleceń i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="25750-112">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="25750-113">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="25750-113">Create resource group</span></span>

<span data-ttu-id="25750-114">Utwórz grupę zasobów platformy Azure za pomocą polecenia [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="25750-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="25750-115">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="25750-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="25750-116">Tworzenie zasobów sieciowych</span><span class="sxs-lookup"><span data-stu-id="25750-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="25750-117">Utwórz sieć wirtualną, podsieć i publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="25750-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="25750-118">Te zasoby są maszyny wirtualnej toohello łączności sieciowej tooprovide używane i podłącz go toohello internet.</span><span class="sxs-lookup"><span data-stu-id="25750-118">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="25750-119">Utwórz sieciową grupę zabezpieczeń i regułę sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="25750-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="25750-120">grupy zabezpieczeń sieci Hello zabezpiecza hello maszyny wirtualnej za pomocą reguł ruchu przychodzącego i wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="25750-120">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="25750-121">W tym przypadku jest tworzona reguła ruchu przychodzącego dla portu 3389, która umożliwia nawiązywanie przychodzących połączeń pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="25750-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="25750-122">Chcemy też toocreate regułę ruchu przychodzącego dla portu 80, który zezwala na ruch przychodzący sieci web.</span><span class="sxs-lookup"><span data-stu-id="25750-122">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="25750-123">Utwórz karty sieciowej dla maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="25750-123">Create a network card for hello virtual machine.</span></span> 
<span data-ttu-id="25750-124">Tworzenie karty sieciowej z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="25750-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="25750-125">Karta sieciowa Hello łączy hello maszyny wirtualnej tooa podsieci, grupy zabezpieczeń sieci i publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="25750-125">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="25750-126">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="25750-126">Create virtual machine</span></span>

<span data-ttu-id="25750-127">Utwórz konfigurację maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="25750-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="25750-128">Ta konfiguracja zawiera ustawienia hello, które są używane podczas wdrażania maszyny wirtualnej hello, takich jak obraz, rozmiar i uwierzytelniania konfiguracji maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="25750-128">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="25750-129">Podczas wykonywania tego kroku jest wyświetlany monit o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="25750-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="25750-130">wartości Hello są skonfigurowane jako hello nazwy użytkownika i hasła hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="25750-130">hello values that you enter are configured as hello user name and password for hello virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="25750-131">Utwórz maszynę wirtualną hello z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="25750-131">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="25750-132">Podłącz maszynę toovirtual</span><span class="sxs-lookup"><span data-stu-id="25750-132">Connect toovirtual machine</span></span>

<span data-ttu-id="25750-133">Po zakończeniu wdrożenia hello, tworzenia połączenia pulpitu zdalnego z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="25750-133">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="25750-134">Użyj hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) polecenia tooreturn hello publicznego adresu IP hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="25750-134">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="25750-135">Zwróć uwagę ten adres IP, więc tooit mogą łączyć się z tootest przeglądarki sieci web łączność w przyszłości kroku.</span><span class="sxs-lookup"><span data-stu-id="25750-135">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="25750-136">Użyj hello następujące polecenie toocreate sesję pulpitu zdalnego z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="25750-136">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="25750-137">Zamień adres IP hello hello *publicznego adresu IP* maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="25750-137">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="25750-138">Po wyświetleniu monitu wprowadź poświadczenia hello używane podczas tworzenia maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="25750-138">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="25750-139">Instalowanie usług IIS za pośrednictwem programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="25750-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="25750-140">Teraz, gdy użytkownik zalogował się toohello maszyny Wirtualnej platformy Azure, można użyć pojedynczy wiersz tooinstall PowerShell usług IIS i włączyć ruch internetowy tooallow reguły zapory lokalnej hello.</span><span class="sxs-lookup"><span data-stu-id="25750-140">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="25750-141">Otwórz wiersz programu PowerShell i uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="25750-141">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="25750-142">Widok hello strona powitalna usług IIS</span><span class="sxs-lookup"><span data-stu-id="25750-142">View hello IIS welcome page</span></span>

<span data-ttu-id="25750-143">Zainstalowane usługi IIS i portu 80 obecnie otwarte na maszynie Wirtualnej z hello Internet można użyć przeglądarki sieci web na wybór tooview hello domyślne IIS strony powitalnej.</span><span class="sxs-lookup"><span data-stu-id="25750-143">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="25750-144">Należy się hello toouse *publicznego adresu IP* opisane powyżej toovisit hello domyślnej strony.</span><span class="sxs-lookup"><span data-stu-id="25750-144">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Domyślna witryna usług IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="25750-146">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="25750-146">Clean up resources</span></span>

<span data-ttu-id="25750-147">Gdy nie są już potrzebne, można użyć hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) polecenia grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="25750-147">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="25750-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25750-148">Next steps</span></span>

<span data-ttu-id="25750-149">W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="25750-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="25750-150">toolearn więcej informacji o maszynach wirtualnych platformy Azure, nadal samouczek toohello dla maszyn wirtualnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="25750-150">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="25750-151">Samouczki dla maszyny wirtualnej platformy Azure z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="25750-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
