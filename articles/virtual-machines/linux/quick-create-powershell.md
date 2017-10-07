---
title: "Szybki Start - aaaAzure utworzyć VM środowiska PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiesz toocreate maszyn wirtualnych systemu Linux przy użyciu programu PowerShell"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="56e32-103">Tworzenie maszyny wirtualnej z systemem Linux za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="56e32-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="56e32-104">modułu Azure PowerShell Hello jest używany toocreate i zarządzania zasobami Azure z wiersza polecenia programu PowerShell hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="56e32-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="56e32-105">Szczegóły ten przewodnik przy użyciu toodeploy modułu Azure PowerShell hello maszyny wirtualnej z systemem Ubuntu server.</span><span class="sxs-lookup"><span data-stu-id="56e32-105">This guide details using hello Azure PowerShell module toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="56e32-106">Po wdrożeniu serwera hello połączenia SSH jest tworzony, i NGINX, serwer sieci Web jest zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="56e32-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="56e32-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="56e32-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="56e32-108">To szybki start wymaga hello Azure PowerShell w wersji modułu 3,6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="56e32-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="56e32-109">Uruchom ` Get-Module -ListAvailable AzureRM` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="56e32-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="56e32-110">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="56e32-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="56e32-111">Na koniec publiczny klucz SSH o nazwie hello *id_rsa.pub* musi toobe przechowywane w hello *.ssh* katalogu profilu użytkownika systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="56e32-111">Finally, a public SSH key with hello name *id_rsa.pub* needs toobe stored in hello *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="56e32-112">Aby uzyskać szczegółowe informacje na temat tworzenia kluczy SSH dla platformy Azure, zobacz [Tworzenie kluczy SSH dla platformy Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56e32-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="56e32-113">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="56e32-113">Log in tooAzure</span></span>

<span data-ttu-id="56e32-114">Zaloguj się za tooyour subskrypcji platformy Azure z hello `Login-AzureRmAccount` poleceń i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="56e32-114">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="56e32-115">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="56e32-115">Create resource group</span></span>

<span data-ttu-id="56e32-116">Utwórz grupę zasobów platformy Azure za pomocą polecenia [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="56e32-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="56e32-117">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="56e32-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="56e32-118">Tworzenie zasobów sieciowych</span><span class="sxs-lookup"><span data-stu-id="56e32-118">Create networking resources</span></span>

<span data-ttu-id="56e32-119">Utwórz sieć wirtualną, podsieć i publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="56e32-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="56e32-120">Te zasoby są maszyny wirtualnej toohello łączności sieciowej tooprovide używane i podłącz go toohello internet.</span><span class="sxs-lookup"><span data-stu-id="56e32-120">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

<span data-ttu-id="56e32-121">Utwórz sieciową grupę zabezpieczeń i regułę sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="56e32-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="56e32-122">grupy zabezpieczeń sieci Hello zabezpiecza hello maszyny wirtualnej za pomocą reguł ruchu przychodzącego i wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="56e32-122">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="56e32-123">W tym przypadku jest tworzona reguła ruchu przychodzącego dla portu 22, która umożliwia nawiązywanie przychodzących połączeń SSH.</span><span class="sxs-lookup"><span data-stu-id="56e32-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="56e32-124">Chcemy też toocreate regułę ruchu przychodzącego dla portu 80, który zezwala na ruch przychodzący sieci web.</span><span class="sxs-lookup"><span data-stu-id="56e32-124">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

<span data-ttu-id="56e32-125">Tworzenie karty sieciowej z [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="56e32-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="56e32-126">Karta sieciowa Hello łączy hello maszyny wirtualnej tooa podsieci, grupy zabezpieczeń sieci i publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="56e32-126">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="56e32-127">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="56e32-127">Create virtual machine</span></span>

<span data-ttu-id="56e32-128">Utwórz konfigurację maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="56e32-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="56e32-129">Ta konfiguracja zawiera ustawienia hello, które są używane podczas wdrażania maszyny wirtualnej hello, takich jak obraz, rozmiar i uwierzytelniania konfiguracji maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="56e32-129">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

<span data-ttu-id="56e32-130">Utwórz maszynę wirtualną hello z [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="56e32-130">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="56e32-131">Podłącz maszynę toovirtual</span><span class="sxs-lookup"><span data-stu-id="56e32-131">Connect toovirtual machine</span></span>

<span data-ttu-id="56e32-132">Po zakończeniu wdrożenia hello, należy utworzyć połączenie SSH z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="56e32-132">After hello deployment has completed, create an SSH connection with hello virtual machine.</span></span>

<span data-ttu-id="56e32-133">Użyj hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) polecenia tooreturn hello publicznego adresu IP hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="56e32-133">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="56e32-134">Z systemu przy użyciu protokołu SSH zainstalowany hello używane następujące polecenie maszyny wirtualnej toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="56e32-134">From a system with SSH installed, used hello following command tooconnect toohello virtual machine.</span></span> <span data-ttu-id="56e32-135">Jeśli działa w systemie Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) mogą być używane toocreate hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="56e32-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used toocreate hello connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="56e32-136">Po wyświetleniu monitu, nazwa użytkownika logowania hello jest *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="56e32-136">When prompted, hello login user name is *azureuser*.</span></span> <span data-ttu-id="56e32-137">Wprowadzone hasło podczas tworzenia kluczy SSH, należy najpierw tooenter w tym również.</span><span class="sxs-lookup"><span data-stu-id="56e32-137">If a passphrase was entered when creating SSH keys, you need tooenter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="56e32-138">Instalowanie serwera NGINX</span><span class="sxs-lookup"><span data-stu-id="56e32-138">Install NGINX</span></span>

<span data-ttu-id="56e32-139">Użyj następujących hello bash źródła pakietów tooupdate skryptu i zainstaluj najnowszy pakiet NGINX hello.</span><span class="sxs-lookup"><span data-stu-id="56e32-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a><span data-ttu-id="56e32-140">Wyświetlanie hello NGIX strony powitalnej</span><span class="sxs-lookup"><span data-stu-id="56e32-140">View hello NGIX welcome page</span></span>

<span data-ttu-id="56e32-141">NGINX zainstalowane i numer portu 80 obecnie otwarte na maszynie Wirtualnej z hello Internet — można użyć przeglądarki sieci web na wybór tooview hello domyślne NGINX strony powitalnej.</span><span class="sxs-lookup"><span data-stu-id="56e32-141">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="56e32-142">Należy się toouse hello publicznego adresu IP, który opisane powyżej toovisit hello domyślnej strony.</span><span class="sxs-lookup"><span data-stu-id="56e32-142">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Domyślna witryna serwera NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="56e32-144">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="56e32-144">Clean up resources</span></span>

<span data-ttu-id="56e32-145">Gdy nie są już potrzebne, można użyć hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) polecenia grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="56e32-145">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="56e32-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="56e32-146">Next steps</span></span>

<span data-ttu-id="56e32-147">W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="56e32-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="56e32-148">toolearn więcej informacji o maszynach wirtualnych platformy Azure, nadal samouczek toohello dla maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="56e32-148">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="56e32-149">Samouczki dla maszyny wirtualnej platformy Azure z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="56e32-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
