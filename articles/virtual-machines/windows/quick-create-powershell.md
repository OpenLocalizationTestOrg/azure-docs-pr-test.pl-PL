---
title: "Azure: Szybki start — Tworzenie maszyn wirtualnych z systemem Windows za pomocą programu PowerShell | Microsoft Docs"
description: "Szybka nauka tworzenia maszyn wirtualnych z systemem Windows przy użyciu programu PowerShell"
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
ms.openlocfilehash: 8516cfa2272694496eb353a83eca77c13a516750
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="b8d98-103">Tworzenie maszyny wirtualnej z systemem Windows za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8d98-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="b8d98-104">Moduł Azure PowerShell umożliwia tworzenie zasobów platformy Azure i zarządzanie nimi za pomocą wiersza polecenia programu PowerShell lub skryptów.</span><span class="sxs-lookup"><span data-stu-id="b8d98-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="b8d98-105">W tym przewodniku zawarto szczegółowe instrukcje korzystania z programu PowerShell w celu utworzenia maszyny wirtualnej na platformie Azure z systemem Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="b8d98-105">This guide details using PowerShell to create and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="b8d98-106">Po ukończeniu wdrożenia nawiążemy połączenie z serwerem i zainstalujemy usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="b8d98-106">Once deployment is complete, we connect to the server and install IIS.</span></span>  

<span data-ttu-id="b8d98-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="b8d98-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="b8d98-108">Dla tego przewodnika Szybki start jest wymagany moduł Azure PowerShell w wersji 3.6 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b8d98-108">This quick start requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="b8d98-109">Uruchom polecenie ` Get-Module -ListAvailable AzureRM`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="b8d98-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="b8d98-110">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie modułu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b8d98-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="b8d98-111">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b8d98-111">Log in to Azure</span></span>

<span data-ttu-id="b8d98-112">Zaloguj się do subskrypcji platformy Azure za pomocą polecenia `Login-AzureRmAccount` i postępuj zgodnie z instrukcjami wyświetlanymi na ekranie.</span><span class="sxs-lookup"><span data-stu-id="b8d98-112">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="b8d98-113">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="b8d98-113">Create resource group</span></span>

<span data-ttu-id="b8d98-114">Utwórz grupę zasobów platformy Azure za pomocą polecenia [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="b8d98-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="b8d98-115">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="b8d98-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="b8d98-116">Tworzenie zasobów sieciowych</span><span class="sxs-lookup"><span data-stu-id="b8d98-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="b8d98-117">Utwórz sieć wirtualną, podsieć i publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="b8d98-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="b8d98-118">Te zasoby są używane do zapewniania łączności sieciowej z maszyną wirtualną i nawiązywania połączenia z Internetem.</span><span class="sxs-lookup"><span data-stu-id="b8d98-118">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

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

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="b8d98-119">Utwórz sieciową grupę zabezpieczeń i regułę sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b8d98-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="b8d98-120">Sieciowa grupa zabezpieczeń chroni maszynę wirtualną za pomocą reguł ruchu przychodzącego i wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="b8d98-120">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="b8d98-121">W tym przypadku jest tworzona reguła ruchu przychodzącego dla portu 3389, która umożliwia nawiązywanie przychodzących połączeń pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="b8d98-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="b8d98-122">Chcemy też utworzyć regułę ruchu przychodzącego dla portu 80, która zezwala na ruch przychodzący w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b8d98-122">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

### <a name="create-a-network-card-for-the-virtual-machine"></a><span data-ttu-id="b8d98-123">Utwórz kartę sieciową dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b8d98-123">Create a network card for the virtual machine.</span></span> 
<span data-ttu-id="b8d98-124">Utwórz kartę sieciową maszyny wirtualnej za pomocą polecenia [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="b8d98-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for the virtual machine.</span></span> <span data-ttu-id="b8d98-125">Karta sieciowa łączy maszynę wirtualną z podsiecią, sieciową grupą zabezpieczeń i publicznym adresem IP.</span><span class="sxs-lookup"><span data-stu-id="b8d98-125">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="b8d98-126">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b8d98-126">Create virtual machine</span></span>

<span data-ttu-id="b8d98-127">Utwórz konfigurację maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b8d98-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="b8d98-128">Ta konfiguracja zawiera ustawienia, które są używane podczas wdrażania maszyny wirtualnej, takie jak obraz maszyny wirtualnej, rozmiar i konfiguracja uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b8d98-128">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="b8d98-129">Podczas wykonywania tego kroku jest wyświetlany monit o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="b8d98-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="b8d98-130">Wprowadzane wartości są konfigurowane jako nazwa użytkownika i hasło dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b8d98-130">The values that you enter are configured as the user name and password for the virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="b8d98-131">Utwórz maszynę wirtualną za pomocą polecenia [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="b8d98-131">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="b8d98-132">Nawiązywanie połączenia z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="b8d98-132">Connect to virtual machine</span></span>

<span data-ttu-id="b8d98-133">Po zakończeniu wdrożenia utwórz połączenie pulpitu zdalnego z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="b8d98-133">After the deployment has completed, create a remote desktop connection with the virtual machine.</span></span>

<span data-ttu-id="b8d98-134">Wróć do publicznego adresu IP maszyny wirtualnej za pomocą polecenia [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="b8d98-134">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command to return the public IP address of the virtual machine.</span></span> <span data-ttu-id="b8d98-135">Zapisz ten adres IP, aby połączyć się z nim w przeglądarce w celu przetestowania połączenia z siecią Web w przyszłym kroku.</span><span class="sxs-lookup"><span data-stu-id="b8d98-135">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="b8d98-136">Użyj następującego polecenia, aby utworzyć sesję usług pulpitu zdalnego z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="b8d98-136">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="b8d98-137">Zamień adres IP na *publiczny adres IP* Twojej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b8d98-137">Replace the IP address with the *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="b8d98-138">Po wyświetleniu monitu wprowadź poświadczenia używane podczas tworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b8d98-138">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="b8d98-139">Instalowanie usług IIS za pośrednictwem programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8d98-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="b8d98-140">Teraz po zalogowaniu do maszyny wirtualnej platformy Azure możesz użyć jednego wiersza w programie PowerShell, aby zainstalować usługi IIS i włączyć lokalną regułę zapory, która zezwala na ruch w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b8d98-140">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="b8d98-141">Otwórz wiersz polecenia programu PowerShell i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b8d98-141">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="b8d98-142">Wyświetlanie strony powitalnej usług IIS</span><span class="sxs-lookup"><span data-stu-id="b8d98-142">View the IIS welcome page</span></span>

<span data-ttu-id="b8d98-143">Po zainstalowaniu usług IIS i otwarciu portu 80 na maszynie wirtualnej z Internetu możesz użyć wybranej przeglądarki sieci Web, aby wyświetlić domyślną stronę powitalną przeglądarki usług IIS.</span><span class="sxs-lookup"><span data-stu-id="b8d98-143">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="b8d98-144">Upewnij się, że w celu odwiedzenia strony domyślnej używasz udokumentowanego powyżej *publicznego adresu IP*.</span><span class="sxs-lookup"><span data-stu-id="b8d98-144">Be sure to use the *publicIpAddress* you documented above to visit the default page.</span></span> 

![Domyślna witryna usług IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="b8d98-146">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="b8d98-146">Clean up resources</span></span>

<span data-ttu-id="b8d98-147">Gdy grupa zasobów, maszyna wirtualna i wszystkie pokrewne zasoby nie będą już potrzebne, można je usunąć za pomocą polecenia [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="b8d98-147">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="b8d98-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b8d98-148">Next steps</span></span>

<span data-ttu-id="b8d98-149">W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b8d98-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="b8d98-150">Aby dowiedzieć się więcej o maszynach wirtualnych platformy Azure, przejdź do samouczka dla maszyn wirtualnych z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="b8d98-150">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b8d98-151">Samouczki dla maszyny wirtualnej platformy Azure z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="b8d98-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
