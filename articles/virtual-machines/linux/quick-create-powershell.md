---
title: "Azure: Szybki start — Tworzenie maszyn wirtualnych za pomocą programu PowerShell | Microsoft Docs"
description: "Szybka nauka tworzenia maszyn wirtualnych z systemem Linux przy użyciu programu PowerShell"
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
ms.openlocfilehash: adcf492d4c2d935c880167675a1ed97566156ec7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="99c00-103">Tworzenie maszyny wirtualnej z systemem Linux za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="99c00-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="99c00-104">Moduł Azure PowerShell umożliwia tworzenie zasobów platformy Azure i zarządzanie nimi za pomocą wiersza polecenia programu PowerShell lub skryptów.</span><span class="sxs-lookup"><span data-stu-id="99c00-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="99c00-105">W tym przewodniku zawarto szczegółowe instrukcje korzystania z modułu Azure PowerShell w celu wdrożenia maszyny wirtualnej z systemem Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="99c00-105">This guide details using the Azure PowerShell module to deploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="99c00-106">Po wdrożeniu serwera zostanie utworzone połączenie SSH i zostanie zainstalowany serwer sieci Web NGINX.</span><span class="sxs-lookup"><span data-stu-id="99c00-106">Once the server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="99c00-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="99c00-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="99c00-108">Dla tego przewodnika Szybki start jest wymagany moduł Azure PowerShell w wersji 3.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="99c00-108">This quick start requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="99c00-109">Uruchom polecenie ` Get-Module -ListAvailable AzureRM`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="99c00-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="99c00-110">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie modułu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="99c00-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="99c00-111">Na koniec zapisz publiczny klucz SSH o nazwie *id_rsa.pub* w katalogu *.ssh* profilu użytkownika systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="99c00-111">Finally, a public SSH key with the name *id_rsa.pub* needs to be stored in the *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="99c00-112">Aby uzyskać szczegółowe informacje na temat tworzenia kluczy SSH dla platformy Azure, zobacz [Tworzenie kluczy SSH dla platformy Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="99c00-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="99c00-113">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="99c00-113">Log in to Azure</span></span>

<span data-ttu-id="99c00-114">Zaloguj się do subskrypcji platformy Azure za pomocą polecenia `Login-AzureRmAccount` i postępuj zgodnie z instrukcjami wyświetlanymi na ekranie.</span><span class="sxs-lookup"><span data-stu-id="99c00-114">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="99c00-115">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="99c00-115">Create resource group</span></span>

<span data-ttu-id="99c00-116">Utwórz grupę zasobów platformy Azure za pomocą polecenia [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="99c00-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="99c00-117">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="99c00-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="99c00-118">Tworzenie zasobów sieciowych</span><span class="sxs-lookup"><span data-stu-id="99c00-118">Create networking resources</span></span>

<span data-ttu-id="99c00-119">Utwórz sieć wirtualną, podsieć i publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="99c00-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="99c00-120">Te zasoby są używane do zapewniania łączności sieciowej z maszyną wirtualną i nawiązywania połączenia z Internetem.</span><span class="sxs-lookup"><span data-stu-id="99c00-120">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

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

<span data-ttu-id="99c00-121">Utwórz sieciową grupę zabezpieczeń i regułę sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="99c00-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="99c00-122">Sieciowa grupa zabezpieczeń chroni maszynę wirtualną za pomocą reguł ruchu przychodzącego i wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="99c00-122">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="99c00-123">W tym przypadku jest tworzona reguła ruchu przychodzącego dla portu 22, która umożliwia nawiązywanie przychodzących połączeń SSH.</span><span class="sxs-lookup"><span data-stu-id="99c00-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="99c00-124">Chcemy też utworzyć regułę ruchu przychodzącego dla portu 80, która zezwala na ruch przychodzący w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="99c00-124">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

<span data-ttu-id="99c00-125">Utwórz kartę sieciową maszyny wirtualnej za pomocą polecenia [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="99c00-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for the virtual machine.</span></span> <span data-ttu-id="99c00-126">Karta sieciowa łączy maszynę wirtualną z podsiecią, sieciową grupą zabezpieczeń i publicznym adresem IP.</span><span class="sxs-lookup"><span data-stu-id="99c00-126">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="99c00-127">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="99c00-127">Create virtual machine</span></span>

<span data-ttu-id="99c00-128">Utwórz konfigurację maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="99c00-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="99c00-129">Ta konfiguracja zawiera ustawienia, które są używane podczas wdrażania maszyny wirtualnej, takie jak obraz maszyny wirtualnej, rozmiar i konfiguracja uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="99c00-129">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

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

<span data-ttu-id="99c00-130">Utwórz maszynę wirtualną za pomocą polecenia [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="99c00-130">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="99c00-131">Nawiązywanie połączenia z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="99c00-131">Connect to virtual machine</span></span>

<span data-ttu-id="99c00-132">Po zakończeniu wdrożenia utwórz połączenie SSH z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="99c00-132">After the deployment has completed, create an SSH connection with the virtual machine.</span></span>

<span data-ttu-id="99c00-133">Wróć do publicznego adresu IP maszyny wirtualnej za pomocą polecenia [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="99c00-133">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command to return the public IP address of the virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="99c00-134">Z poziomu systemu z zainstalowanym protokołem SSH użyj następującego polecenia, aby nawiązać połączenie z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="99c00-134">From a system with SSH installed, used the following command to connect to the virtual machine.</span></span> <span data-ttu-id="99c00-135">W przypadku korzystania z systemu Windows w celu utworzenia połączenia można użyć programu [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty).</span><span class="sxs-lookup"><span data-stu-id="99c00-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used to create the connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="99c00-136">Po wyświetleniu monitu podaj nazwę logowania użytkownika *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="99c00-136">When prompted, the login user name is *azureuser*.</span></span> <span data-ttu-id="99c00-137">Jeśli podczas tworzenia kluczy SSH wprowadzono hasło, należy je również wprowadzić tutaj.</span><span class="sxs-lookup"><span data-stu-id="99c00-137">If a passphrase was entered when creating SSH keys, you need to enter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="99c00-138">Instalowanie serwera NGINX</span><span class="sxs-lookup"><span data-stu-id="99c00-138">Install NGINX</span></span>

<span data-ttu-id="99c00-139">Użyj poniższego skryptu powłoki systemowej w celu zaktualizowania źródeł pakietów i zainstalowania najnowszego pakietu NGINX.</span><span class="sxs-lookup"><span data-stu-id="99c00-139">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-ngix-welcome-page"></a><span data-ttu-id="99c00-140">Wyświetlanie strony powitalnej serwera NGINX</span><span class="sxs-lookup"><span data-stu-id="99c00-140">View the NGIX welcome page</span></span>

<span data-ttu-id="99c00-141">Po zainstalowaniu serwera NGINX i otwarciu portu 80 na maszynie wirtualnej z Internetu możesz użyć wybranej przeglądarki sieci Web, aby wyświetlić domyślną stronę powitalną przeglądarki serwera NGINX.</span><span class="sxs-lookup"><span data-stu-id="99c00-141">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="99c00-142">Upewnij się, że w celu odwiedzenia strony domyślnej używasz udokumentowanego powyżej publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="99c00-142">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![Domyślna witryna serwera NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="99c00-144">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="99c00-144">Clean up resources</span></span>

<span data-ttu-id="99c00-145">Gdy grupa zasobów, maszyna wirtualna i wszystkie pokrewne zasoby nie będą już potrzebne, można je usunąć za pomocą polecenia [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="99c00-145">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="99c00-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="99c00-146">Next steps</span></span>

<span data-ttu-id="99c00-147">W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="99c00-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="99c00-148">Aby dowiedzieć się więcej o maszynach wirtualnych platformy Azure, przejdź do samouczka dla maszyn wirtualnych z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="99c00-148">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="99c00-149">Samouczki dla maszyny wirtualnej platformy Azure z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="99c00-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
