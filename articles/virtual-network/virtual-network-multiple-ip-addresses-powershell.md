---
title: "Wiele adresów IP dla maszyn wirtualnych platformy Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak można przypisać wiele adresów IP do maszyny wirtualnej przy użyciu programu PowerShell | Menedżer zasobów."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: 29f64aeefc2a7deb1f84d759c2323347536b9c27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-powershell"></a><span data-ttu-id="502de-103">Przypisz wielu adresów IP do maszyn wirtualnych przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="502de-103">Assign multiple IP addresses to virtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="502de-104">W tym artykule opisano sposób tworzenia maszyny wirtualnej (VM) za pośrednictwem modelu wdrażania usługi Azure Resource Manager przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="502de-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="502de-105">Nie można przypisać wiele adresów IP do zasobów została utworzona za pośrednictwem klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="502de-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="502de-106">Aby dowiedzieć się więcej na temat modeli wdrażania platformy Azure, przeczytaj [zrozumieć modele wdrażania](../resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="502de-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="502de-107"><a name = "create"></a>Utwórz maszynę Wirtualną z wielu adresów IP</span><span class="sxs-lookup"><span data-stu-id="502de-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="502de-108">Czynności, które wykonują wyjaśniono, jak utworzyć przykładowy maszyny Wirtualnej z wielu adresów IP, zgodnie z opisem w scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="502de-108">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="502de-109">Zmienianie wartości zmiennych, co jest wymagane dla implementacji.</span><span class="sxs-lookup"><span data-stu-id="502de-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="502de-110">Otwórz wiersz polecenia programu PowerShell i wykonaj pozostałe kroki w tej sekcji w ramach jednej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="502de-110">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="502de-111">Jeśli nie masz jeszcze programu PowerShell zainstalowany i skonfigurowany, wykonaj kroki [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="502de-111">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="502de-112">Zaloguj się do konta z `login-azurermaccount` polecenia.</span><span class="sxs-lookup"><span data-stu-id="502de-112">Login to your account with the `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="502de-113">Zastąp *myResourceGroup* i *westus* przy użyciu nazwy i lokalizacji wybrane.</span><span class="sxs-lookup"><span data-stu-id="502de-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="502de-114">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="502de-114">Create a resource group.</span></span> <span data-ttu-id="502de-115">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="502de-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="502de-116">Utwórz sieć wirtualną (VNet) i podsieci w tej samej lokalizacji co grupa zasobów:</span><span class="sxs-lookup"><span data-stu-id="502de-116">Create a virtual network (VNet) and subnet in the same location as the resource group:</span></span>

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get the subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="502de-117">Utwórz grupę zabezpieczeń sieci (NSG) i zasady.</span><span class="sxs-lookup"><span data-stu-id="502de-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="502de-118">Grupa NSG zabezpiecza maszyny Wirtualnej za pomocą reguł ruchu przychodzącego i wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="502de-118">The NSG secures the VM using inbound and outbound rules.</span></span> <span data-ttu-id="502de-119">W tym przypadku jest tworzona reguła ruchu przychodzącego dla portu 3389, która umożliwia nawiązywanie przychodzących połączeń pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="502de-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. <span data-ttu-id="502de-120">Zdefiniuj podstawową konfigurację protokołu IP dla karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="502de-120">Define the primary IP configuration for the NIC.</span></span> <span data-ttu-id="502de-121">Zmień 10.0.0.4 na prawidłowy adres w podsieci, w której zostały utworzone, jeśli nie używasz wartość zdefiniowana wcześniej.</span><span class="sxs-lookup"><span data-stu-id="502de-121">Change 10.0.0.4 to a valid address in the subnet you created, if you didn't use the value defined previously.</span></span> <span data-ttu-id="502de-122">Przed przypisaniem statycznego adresu IP, zalecane jest, że należy najpierw upewnij się, że nie jest już używana.</span><span class="sxs-lookup"><span data-stu-id="502de-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="502de-123">Wprowadź polecenie `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="502de-123">Enter the command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="502de-124">Jeśli adres jest dostępny, zwraca dane wyjściowe *True*.</span><span class="sxs-lookup"><span data-stu-id="502de-124">If the address is available, the output returns *True*.</span></span> <span data-ttu-id="502de-125">Jeśli nie jest dostępna, zwraca dane wyjściowe *False* oraz listę adresów, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="502de-125">If it's not available, the output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="502de-126">W poniższych poleceniach **Zamień < Zamień z your unikatowy nazwa-> unikatowa nazwa DNS do użycia.**</span><span class="sxs-lookup"><span data-stu-id="502de-126">In the following commands, **Replace <replace-with-your-unique-name> with the unique DNS name to use.**</span></span> <span data-ttu-id="502de-127">Nazwa musi być unikatowa w publicznych adresów IP w obrębie regionu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="502de-127">The name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="502de-128">Jest to parametr opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="502de-128">This is an optional parameter.</span></span> <span data-ttu-id="502de-129">Można usunąć, jeśli chcesz się połączyć z maszyną wirtualną za pomocą publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="502de-129">It can be removed if you only want to connect to the VM using the public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="502de-130">Po przypisaniu wielu konfiguracji adresów IP do karty Sieciowej, należy przypisać jedną konfigurację jako *— podstawowy*.</span><span class="sxs-lookup"><span data-stu-id="502de-130">When you assign multiple IP configurations to a NIC, one configuration must be assigned as the *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="502de-131">Publiczne adresy IP ma nominalnego opłatą.</span><span class="sxs-lookup"><span data-stu-id="502de-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="502de-132">Aby dowiedzieć się więcej o cenach adresu IP, przeczytaj [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony.</span><span class="sxs-lookup"><span data-stu-id="502de-132">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="502de-133">Istnieje ograniczona liczba publicznych adresów IP, których można użyć w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="502de-133">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="502de-134">Aby uzyskać więcej informacji o limitach, przeczytaj artykuł dotyczący [limitów platformy Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="502de-134">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="502de-135">Zdefiniuj dodatkowej konfiguracji adresów IP dla karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="502de-135">Define the secondary IP configurations for the NIC.</span></span> <span data-ttu-id="502de-136">Można dodawać i usuwać konfiguracje w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="502de-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="502de-137">Każdej konfiguracji adresu IP musi mieć przypisany prywatny adres IP.</span><span class="sxs-lookup"><span data-stu-id="502de-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="502de-138">Każdej konfiguracji opcjonalnie może mieć przypisany jeden publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="502de-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. <span data-ttu-id="502de-139">Utwórz kartę Sieciową i skojarz trzech konfiguracji IP do niej:</span><span class="sxs-lookup"><span data-stu-id="502de-139">Create the NIC and associate the three IP configurations to it:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="502de-140">Chociaż wszystkie konfiguracje są przypisane do jednej karty Sieciowej, w tym artykule, można przypisać wielu konfiguracji adresów IP do każdej karty Sieciowej podłączony do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="502de-140">Though all configurations are assigned to one NIC in this article, you can assign multiple IP configurations to every NIC attached to the VM.</span></span> <span data-ttu-id="502de-141">Aby dowiedzieć się, jak utworzyć Maszynę wirtualną z wieloma kartami sieciowymi, przeczytaj [tworzenia maszyn wirtualnych z wieloma kartami sieciowymi](virtual-network-deploy-multinic-arm-ps.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="502de-141">To learn how to create a VM with multiple NICs, read the [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="502de-142">Tworzenie maszyny Wirtualnej, wprowadzając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="502de-142">Create the VM by entering the following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted to enter a sername and password for the VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create the VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="502de-143">Dodaj prywatnych adresów IP do systemu operacyjnego maszyny Wirtualnej, wykonując kroki odpowiednie dla systemu operacyjnego w [adresów IP Dodaj do systemu operacyjnego maszyny Wirtualnej](#os-config) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="502de-143">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="502de-144">Nie dodawaj publiczne adresy IP do systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="502de-144">Do not add the public IP addresses to the operating system.</span></span>

## <span data-ttu-id="502de-145"><a name="add"></a>Dodaj adresy IP do maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="502de-145"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="502de-146">Prywatne i publiczne adresy IP można dodać do karty Sieciowej, wykonując kroki, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="502de-146">You can add private and public IP addresses to a NIC by completing the steps that follow.</span></span> <span data-ttu-id="502de-147">Przykłady w poniższych sekcjach założono, że już istnieje maszyna wirtualna z tych trzech konfiguracji adresu IP, opisane w [scenariusza](#Scenario) w tym artykule, ale nie jest to wymagane wykonanie.</span><span class="sxs-lookup"><span data-stu-id="502de-147">The examples in the following sections assume that you already have a VM with the three IP configurations described in the [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="502de-148">Otwórz wiersz polecenia programu PowerShell i wykonaj pozostałe kroki w tej sekcji w ramach jednej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="502de-148">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="502de-149">Jeśli nie masz jeszcze programu PowerShell zainstalowany i skonfigurowany, wykonaj kroki [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="502de-149">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="502de-150">Zmień nazwę karty Sieciowej, aby dodać adres IP do grupy zasobów i lokalizacja, którą karta sieciowa istnieje w "wartości" $Variables następujące:</span><span class="sxs-lookup"><span data-stu-id="502de-150">Change the "values" of the following $Variables to the name of the NIC you want to add IP address to and the resource group and location the NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="502de-151">Jeśli nie znasz nazwy karty sieciowej, aby zmienić, wpisz następujące polecenia, następnie zmienić wartości zmiennych poprzedniego:</span><span class="sxs-lookup"><span data-stu-id="502de-151">If you don't know the name of the NIC you want to change, enter the following commands, then change the values of the previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="502de-152">Utwórz zmienną i ustaw ją istniejącej karty NIC, wpisując następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="502de-152">Create a variable and set it to the existing NIC by typing the following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="502de-153">W poniższych poleceniach zmienić *MyVNet* i *MySubnet* do nazwy sieci wirtualnej i karty interfejsu Sieciowego jest podłączony do podsieci.</span><span class="sxs-lookup"><span data-stu-id="502de-153">In the following commands, change *MyVNet* and *MySubnet* to the names of the VNet and subnet the NIC is connected to.</span></span> <span data-ttu-id="502de-154">Wprowadź poleceń, aby pobrać obiekty sieci wirtualnej i podsieci, karta sieciowa jest połączona z:</span><span class="sxs-lookup"><span data-stu-id="502de-154">Enter the commands to retrieve the VNet and subnet objects the NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="502de-155">Jeśli nie znasz nazwy sieci wirtualnej lub podsieci, karta sieciowa jest połączona z, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="502de-155">If you don't know the VNet or subnet name the NIC is connected to, enter the following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="502de-156">W wynikach wyszukiwania tekstu, podobnie jak w poniższym przykładzie danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="502de-156">In the output, look for text similar to the following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="502de-157">W tym danych wyjściowych *MyVnet* jest sieci wirtualnej i *MySubnet* jest karta sieciowa jest podłączony do podsieci.</span><span class="sxs-lookup"><span data-stu-id="502de-157">In this output, *MyVnet* is the VNet and *MySubnet* is the subnet the NIC is connected to.</span></span>

5. <span data-ttu-id="502de-158">Wykonaj kroki jednego z następujących sekcji, w zależności od wymagań:</span><span class="sxs-lookup"><span data-stu-id="502de-158">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="502de-159">**Dodaj prywatnego adresu IP**</span><span class="sxs-lookup"><span data-stu-id="502de-159">**Add a private IP address**</span></span>

    <span data-ttu-id="502de-160">Aby dodać prywatnego adresu IP do karty Sieciowej, należy utworzyć konfigurację protokołu IP.</span><span class="sxs-lookup"><span data-stu-id="502de-160">To add a private IP address to a NIC, you must create an IP configuration.</span></span> <span data-ttu-id="502de-161">Poniższe polecenie tworzy konfiguracji ze statycznym adresem IP 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="502de-161">The following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="502de-162">Określanie statycznego adresu IP, musi być nieużywany adres podsieci.</span><span class="sxs-lookup"><span data-stu-id="502de-162">When specifying a static IP address, it must be an unused address for the subnet.</span></span> <span data-ttu-id="502de-163">Zaleca się przetestowanie adres, aby upewnić się, jest dostępna, wprowadzając `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` polecenia.</span><span class="sxs-lookup"><span data-stu-id="502de-163">It's recommended that you first test the address to ensure it's available by entering the `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="502de-164">Jeśli adres IP jest dostępny, zwraca dane wyjściowe *True*.</span><span class="sxs-lookup"><span data-stu-id="502de-164">If the IP address is available, the output returns *True*.</span></span> <span data-ttu-id="502de-165">Jeśli nie jest dostępna, zwraca dane wyjściowe *False*oraz listę adresów, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="502de-165">If it's not available, the output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="502de-166">Tworzenie konfiguracji tyle, ile potrzebujesz, przy użyciu nazwy konfiguracji unikatowy i prywatnych adresów IP (w przypadku konfiguracji statycznych adresów IP).</span><span class="sxs-lookup"><span data-stu-id="502de-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="502de-167">Dodaj prywatnego adresu IP do systemu operacyjnego maszyny Wirtualnej, wykonując kroki odpowiednie dla systemu operacyjnego w [adresów IP Dodaj do systemu operacyjnego maszyny Wirtualnej](#os-config) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="502de-167">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="502de-168">**Dodaj publiczny adres IP**</span><span class="sxs-lookup"><span data-stu-id="502de-168">**Add a public IP address**</span></span>

    <span data-ttu-id="502de-169">Publiczny adres IP jest dodawany przez skojarzenie publicznego zasobu adresu IP do nowej konfiguracji IP lub istniejącej konfiguracji adresu IP.</span><span class="sxs-lookup"><span data-stu-id="502de-169">A public IP address is added by associating a public IP address resource to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="502de-170">Wykonaj kroki opisane w sekcji, które należy wykonać, ile potrzebujesz.</span><span class="sxs-lookup"><span data-stu-id="502de-170">Complete the steps in one of the sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="502de-171">Publiczne adresy IP ma nominalnego opłatą.</span><span class="sxs-lookup"><span data-stu-id="502de-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="502de-172">Aby dowiedzieć się więcej o cenach adresu IP, przeczytaj [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony.</span><span class="sxs-lookup"><span data-stu-id="502de-172">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="502de-173">Istnieje ograniczona liczba publicznych adresów IP, których można użyć w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="502de-173">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="502de-174">Aby uzyskać więcej informacji o limitach, przeczytaj artykuł dotyczący [limitów platformy Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="502de-174">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="502de-175">**Skojarz zasób publicznego adresu IP nowej konfiguracji adresu IP**</span><span class="sxs-lookup"><span data-stu-id="502de-175">**Associate the public IP address resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="502de-176">Po dodaniu publicznego adresu IP w nowej konfiguracji adresu IP, musisz również dodać prywatnego adresu IP, ponieważ wszystkie konfiguracje adresów IP muszą mieć prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="502de-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="502de-177">Możesz dodać istniejący zasób publiczny adres IP lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="502de-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="502de-178">Aby utworzyć nową, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="502de-178">To create a new one, enter the following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="502de-179">Aby utworzyć nową konfigurację adresu IP za pomocą statycznego prywatnego adresu IP oraz skojarzonych z nimi *myPublicIp3* publicznego adresu IP adresów zasobów, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="502de-179">To create a new IP configuration with a static private IP address and the associated *myPublicIp3* public IP address resource, enter the following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="502de-180">**Skojarz zasób publicznego adresu IP do istniejącej konfiguracji adresu IP**</span><span class="sxs-lookup"><span data-stu-id="502de-180">**Associate the public IP address resource to an existing IP configuration**</span></span>

        <span data-ttu-id="502de-181">Zasób publicznego adresu IP może być skojarzony tylko konfiguracją protokołu IP, który nie ma jeszcze skojarzone.</span><span class="sxs-lookup"><span data-stu-id="502de-181">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="502de-182">Można określić, czy konfiguracja IP ma skojarzone publicznego adresu IP, wprowadzając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="502de-182">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="502de-183">Zostaną wyświetlone dane wyjściowe podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="502de-183">You see output similar to the following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="502de-184">Ponieważ **publicznego adresu IP** kolumny dla *IpConfig 3* jest puste, żaden z zasobów publiczny adres IP jest obecnie z nią skojarzona.</span><span class="sxs-lookup"><span data-stu-id="502de-184">Since the **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="502de-185">Dodaj istniejący zasób publicznego adresu IP do IpConfig 3 lub wprowadź następujące polecenie, aby go utworzyć:</span><span class="sxs-lookup"><span data-stu-id="502de-185">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="502de-186">Wprowadź następujące polecenie, aby skojarzyć zasób publicznego adresu IP do istniejącej konfiguracji IP o nazwie *IpConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="502de-186">Enter the following command to associate the public IP address resource to the existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="502de-187">Ustaw kartę Sieciową przy użyciu nowej konfiguracji adresu IP, wprowadzając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="502de-187">Set the NIC with the new IP configuration by entering the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="502de-188">Wyświetl prywatnych adresów IP i zasoby adresów publicznych adresów IP przypisanych do karty Sieciowej, wprowadzając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="502de-188">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="502de-189">Dodaj prywatnego adresu IP do systemu operacyjnego maszyny Wirtualnej, wykonując kroki odpowiednie dla systemu operacyjnego w [adresów IP Dodaj do systemu operacyjnego maszyny Wirtualnej](#os-config) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="502de-189">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="502de-190">Publiczny adres IP nie należy dodawać do systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="502de-190">Do not add the public IP address to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
