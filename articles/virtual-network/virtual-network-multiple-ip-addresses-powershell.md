---
title: "aaaMultiple adresów IP dla maszyn wirtualnych platformy Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooassign wielu adresów IP maszyny wirtualnej tooa przy użyciu programu PowerShell | Menedżer zasobów."
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
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a><span data-ttu-id="990cc-103">Przypisz wielu adresów IP maszyny toovirtual przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="990cc-103">Assign multiple IP addresses toovirtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="990cc-104">W tym artykule opisano, jak toocreate maszynę wirtualną (VM) do wdrożenia usługi Azure Resource Manager hello modelu przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="990cc-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="990cc-105">Wiele adresów IP nie można przypisać tooresources został utworzony za pomocą hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="990cc-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="990cc-106">więcej informacji na temat modeli wdrażania platformy Azure, przeczytaj hello toolearn [zrozumieć modele wdrażania](../resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="990cc-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="990cc-107"><a name = "create"></a>Utwórz maszynę Wirtualną z wielu adresów IP</span><span class="sxs-lookup"><span data-stu-id="990cc-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="990cc-108">Hello przestrzeganie objaśniono sposób toocreate przykład maszynę Wirtualną za pomocą wielu IP adresów, zgodnie z opisem w scenariuszu hello.</span><span class="sxs-lookup"><span data-stu-id="990cc-108">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="990cc-109">Zmienianie wartości zmiennych, co jest wymagane dla implementacji.</span><span class="sxs-lookup"><span data-stu-id="990cc-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="990cc-110">Otwórz wiersz polecenia programu PowerShell i pełny hello pozostałe kroki opisane w tej sekcji w ramach jednej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="990cc-110">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="990cc-111">Jeśli nie masz jeszcze programu PowerShell zainstalowany i skonfigurowany, pełną hello etapami hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="990cc-111">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="990cc-112">Konto logowania tooyour z hello `login-azurermaccount` polecenia.</span><span class="sxs-lookup"><span data-stu-id="990cc-112">Login tooyour account with hello `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="990cc-113">Zastąp *myResourceGroup* i *westus* przy użyciu nazwy i lokalizacji wybrane.</span><span class="sxs-lookup"><span data-stu-id="990cc-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="990cc-114">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="990cc-114">Create a resource group.</span></span> <span data-ttu-id="990cc-115">Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="990cc-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="990cc-116">Utwórz sieć wirtualną (VNet) i podsieci w hello tej samej lokalizacji co hello grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="990cc-116">Create a virtual network (VNet) and subnet in hello same location as hello resource group:</span></span>

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

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="990cc-117">Utwórz grupę zabezpieczeń sieci (NSG) i zasady.</span><span class="sxs-lookup"><span data-stu-id="990cc-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="990cc-118">Witaj NSG zabezpiecza hello maszyny Wirtualnej za pomocą reguł ruchu przychodzącego i wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="990cc-118">hello NSG secures hello VM using inbound and outbound rules.</span></span> <span data-ttu-id="990cc-119">W tym przypadku jest tworzona reguła ruchu przychodzącego dla portu 3389, która umożliwia nawiązywanie przychodzących połączeń pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="990cc-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

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

6. <span data-ttu-id="990cc-120">Zdefiniuj hello podstawową konfigurację protokołu IP dla hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="990cc-120">Define hello primary IP configuration for hello NIC.</span></span> <span data-ttu-id="990cc-121">Zmień 10.0.0.4 tooa prawidłowy adres w podsieci hello zostało utworzone, jeśli nie użyto wartości hello wcześniej zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="990cc-121">Change 10.0.0.4 tooa valid address in hello subnet you created, if you didn't use hello value defined previously.</span></span> <span data-ttu-id="990cc-122">Przed przypisaniem statycznego adresu IP, zalecane jest, że należy najpierw upewnij się, że nie jest już używana.</span><span class="sxs-lookup"><span data-stu-id="990cc-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="990cc-123">Wprowadź polecenie hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="990cc-123">Enter hello command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="990cc-124">Jeśli adres hello jest dostępny, hello output zwraca *True*.</span><span class="sxs-lookup"><span data-stu-id="990cc-124">If hello address is available, hello output returns *True*.</span></span> <span data-ttu-id="990cc-125">Jeśli nie jest dostępna, hello output zwraca *False* oraz listę adresów, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="990cc-125">If it's not available, hello output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="990cc-126">W następujące polecenia, hello **Zamień < Zamień z your unikatowy nazwa-> hello unikatowy toouse nazwy DNS.**</span><span class="sxs-lookup"><span data-stu-id="990cc-126">In hello following commands, **Replace <replace-with-your-unique-name> with hello unique DNS name toouse.**</span></span> <span data-ttu-id="990cc-127">Nazwa Hello musi być unikatowa we wszystkich publicznych adresów IP w obrębie regionu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="990cc-127">hello name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="990cc-128">Jest to parametr opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="990cc-128">This is an optional parameter.</span></span> <span data-ttu-id="990cc-129">Można usunąć, jeśli chcesz tylko toohello tooconnect maszyny Wirtualnej przy użyciu hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="990cc-129">It can be removed if you only want tooconnect toohello VM using hello public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="990cc-130">Po przypisaniu wielu tooa konfiguracji adresu IP karty Sieciowej, jednej konfiguracji musi być przypisany jako hello *— podstawowy*.</span><span class="sxs-lookup"><span data-stu-id="990cc-130">When you assign multiple IP configurations tooa NIC, one configuration must be assigned as hello *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="990cc-131">Publiczne adresy IP ma nominalnego opłatą.</span><span class="sxs-lookup"><span data-stu-id="990cc-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="990cc-132">więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony.</span><span class="sxs-lookup"><span data-stu-id="990cc-132">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="990cc-133">Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="990cc-133">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="990cc-134">więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.</span><span class="sxs-lookup"><span data-stu-id="990cc-134">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="990cc-135">Zdefiniuj hello dodatkowej konfiguracji adresów IP hello karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="990cc-135">Define hello secondary IP configurations for hello NIC.</span></span> <span data-ttu-id="990cc-136">Można dodawać i usuwać konfiguracje w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="990cc-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="990cc-137">Każdej konfiguracji adresu IP musi mieć przypisany prywatny adres IP.</span><span class="sxs-lookup"><span data-stu-id="990cc-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="990cc-138">Każdej konfiguracji opcjonalnie może mieć przypisany jeden publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="990cc-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
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

8. <span data-ttu-id="990cc-139">Utworzyć hello kartę Sieciową i skojarzyć hello trzy tooit konfiguracji adresu IP:</span><span class="sxs-lookup"><span data-stu-id="990cc-139">Create hello NIC and associate hello three IP configurations tooit:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="990cc-140">Chociaż wszystkie konfiguracje są przypisane tooone karty Sieciowej, w tym artykule, można przypisać toohello kartę Sieciową podłączoną tooevery konfiguracji IP wiele maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="990cc-140">Though all configurations are assigned tooone NIC in this article, you can assign multiple IP configurations tooevery NIC attached toohello VM.</span></span> <span data-ttu-id="990cc-141">jak toocreate Maszynę wirtualną z wieloma kartami sieciowymi, przeczytaj toolearn hello [tworzenia maszyn wirtualnych z wieloma kartami sieciowymi](virtual-network-deploy-multinic-arm-ps.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="990cc-141">toolearn how toocreate a VM with multiple NICs, read hello [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="990cc-142">Utwórz hello maszyny Wirtualnej, wprowadzając hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="990cc-142">Create hello VM by entering hello following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
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
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="990cc-143">Dodaj hello prywatnego adresu IP dotyczy systemu operacyjnego maszyny Wirtualnej toohello, wykonując kroki hello systemu operacyjnego w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="990cc-143">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="990cc-144">Nie należy dodawać hello publicznego adresu IP adresów toohello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="990cc-144">Do not add hello public IP addresses toohello operating system.</span></span>

## <span data-ttu-id="990cc-145"><a name="add"></a>Dodaj tooa adresów IP maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="990cc-145"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="990cc-146">Wykonując kroki hello, które należy wykonać, można dodać prywatnych i publicznych tooa adresy IP karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="990cc-146">You can add private and public IP addresses tooa NIC by completing hello steps that follow.</span></span> <span data-ttu-id="990cc-147">Witaj przykłady w hello następujące sekcje założono, że już istnieje Maszynę wirtualną z konfiguracji adresów IP hello trzech opisanych w hello [scenariusza](#Scenario) w tym artykule, ale nie jest to wymagane wykonanie.</span><span class="sxs-lookup"><span data-stu-id="990cc-147">hello examples in hello following sections assume that you already have a VM with hello three IP configurations described in hello [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="990cc-148">Otwórz wiersz polecenia programu PowerShell i pełny hello pozostałe kroki opisane w tej sekcji w ramach jednej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="990cc-148">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="990cc-149">Jeśli nie masz jeszcze programu PowerShell zainstalowany i skonfigurowany, pełną hello etapami hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="990cc-149">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="990cc-150">Zmień hello "wartości" hello nazwę toohello $Variables hello karta sieciowa ma tooadd IP address tooand hello zasobu lokalizacji i grupy powitalne karta sieciowa istnieje w następujących:</span><span class="sxs-lookup"><span data-stu-id="990cc-150">Change hello "values" of hello following $Variables toohello name of hello NIC you want tooadd IP address tooand hello resource group and location hello NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="990cc-151">Jeśli nie znasz nazwę hello hello ma toochange karty Sieciowej, wprowadź hello następujące polecenia, a następnie zmień hello wartości zmiennych poprzedniej hello:</span><span class="sxs-lookup"><span data-stu-id="990cc-151">If you don't know hello name of hello NIC you want toochange, enter hello following commands, then change hello values of hello previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="990cc-152">Utwórz zmienną i ustaw ją toohello istniejących kart interfejsu Sieciowego, wpisując następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="990cc-152">Create a variable and set it toohello existing NIC by typing hello following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="990cc-153">W hello następujące polecenia, zmień *MyVNet* i *MySubnet* toohello nazwy hello sieci wirtualnej i podsieci hello jest połączona karta sieciowa.</span><span class="sxs-lookup"><span data-stu-id="990cc-153">In hello following commands, change *MyVNet* and *MySubnet* toohello names of hello VNet and subnet hello NIC is connected to.</span></span> <span data-ttu-id="990cc-154">Wprowadź hello polecenia tooretrieve hello sieci wirtualnej i podsieci obiektów hello podłączenia karty Sieciowej:</span><span class="sxs-lookup"><span data-stu-id="990cc-154">Enter hello commands tooretrieve hello VNet and subnet objects hello NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="990cc-155">Jeśli nie znasz hello sieci wirtualnej lub podsieci nazwę hello podłączenia karty Sieciowej, wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="990cc-155">If you don't know hello VNet or subnet name hello NIC is connected to, enter hello following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="990cc-156">W danych wyjściowych hello Wyszukaj tekst toohello podobne następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="990cc-156">In hello output, look for text similar toohello following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="990cc-157">W tym danych wyjściowych *MyVnet* jest hello sieci wirtualnej i *MySubnet* jest hello podsieci hello jest połączona karta sieciowa.</span><span class="sxs-lookup"><span data-stu-id="990cc-157">In this output, *MyVnet* is hello VNet and *MySubnet* is hello subnet hello NIC is connected to.</span></span>

5. <span data-ttu-id="990cc-158">Wykonaj kroki hello w jednym z następujących sekcji, w zależności od wymagań hello:</span><span class="sxs-lookup"><span data-stu-id="990cc-158">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="990cc-159">**Dodaj prywatnego adresu IP**</span><span class="sxs-lookup"><span data-stu-id="990cc-159">**Add a private IP address**</span></span>

    <span data-ttu-id="990cc-160">tooadd prywatnej tooa adresu IP karty Sieciowej, należy utworzyć konfigurację protokołu IP.</span><span class="sxs-lookup"><span data-stu-id="990cc-160">tooadd a private IP address tooa NIC, you must create an IP configuration.</span></span> <span data-ttu-id="990cc-161">Witaj następujące polecenie tworzy konfiguracji ze statycznym adresem IP 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="990cc-161">hello following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="990cc-162">Określanie statycznego adresu IP, musi być nieużywany adres podsieci hello.</span><span class="sxs-lookup"><span data-stu-id="990cc-162">When specifying a static IP address, it must be an unused address for hello subnet.</span></span> <span data-ttu-id="990cc-163">Zaleca się przetestowanie tooensure adres hello jest dostępna, wprowadzając hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` polecenia.</span><span class="sxs-lookup"><span data-stu-id="990cc-163">It's recommended that you first test hello address tooensure it's available by entering hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="990cc-164">Jeśli adres IP hello jest dostępny, hello output zwraca *True*.</span><span class="sxs-lookup"><span data-stu-id="990cc-164">If hello IP address is available, hello output returns *True*.</span></span> <span data-ttu-id="990cc-165">Jeśli nie jest dostępna, hello output zwraca *False*oraz listę adresów, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="990cc-165">If it's not available, hello output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="990cc-166">Tworzenie konfiguracji tyle, ile potrzebujesz, przy użyciu nazwy konfiguracji unikatowy i prywatnych adresów IP (w przypadku konfiguracji statycznych adresów IP).</span><span class="sxs-lookup"><span data-stu-id="990cc-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="990cc-167">Dodaj hello prywatnego adresu IP adres toohello maszyny Wirtualnej systemu operacyjnego, wykonując kroki hello systemu operacyjnego w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="990cc-167">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="990cc-168">**Dodaj publiczny adres IP**</span><span class="sxs-lookup"><span data-stu-id="990cc-168">**Add a public IP address**</span></span>

    <span data-ttu-id="990cc-169">Publiczny adres IP jest dodawany przez skojarzenie publicznego tooeither zasobów adresu IP nowej konfiguracji IP lub istniejącej konfiguracji adresu IP.</span><span class="sxs-lookup"><span data-stu-id="990cc-169">A public IP address is added by associating a public IP address resource tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="990cc-170">Wykonaj kroki hello w jednym z hello kolejnych sekcjach, ile potrzebujesz.</span><span class="sxs-lookup"><span data-stu-id="990cc-170">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="990cc-171">Publiczne adresy IP ma nominalnego opłatą.</span><span class="sxs-lookup"><span data-stu-id="990cc-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="990cc-172">więcej informacji o IP adresów o cenach, toolearn odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony.</span><span class="sxs-lookup"><span data-stu-id="990cc-172">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="990cc-173">Brak limitu toohello liczba publicznych adresów IP, których można użyć w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="990cc-173">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="990cc-174">więcej informacji na temat limitów hello, przeczytaj hello toolearn [Azure ogranicza](../azure-subscription-service-limits.md#networking-limits) artykułu.</span><span class="sxs-lookup"><span data-stu-id="990cc-174">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="990cc-175">**Skojarz hello publicznej konfiguracji adresu IP zasobu tooa nowego adresu IP**</span><span class="sxs-lookup"><span data-stu-id="990cc-175">**Associate hello public IP address resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="990cc-176">Po dodaniu publicznego adresu IP w nowej konfiguracji adresu IP, musisz również dodać prywatnego adresu IP, ponieważ wszystkie konfiguracje adresów IP muszą mieć prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="990cc-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="990cc-177">Możesz dodać istniejący zasób publiczny adres IP lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="990cc-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="990cc-178">toocreate nową, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="990cc-178">toocreate a new one, enter hello following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="990cc-179">toocreate nowej konfiguracji IP przy użyciu statycznego prywatnego adresu IP i hello skojarzone *myPublicIp3* publicznego adresu IP adresów zasobów, wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="990cc-179">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIp3* public IP address resource, enter hello following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="990cc-180">**Skojarz hello publicznej konfiguracji adresu IP zasobu tooan istniejącego adresu IP**</span><span class="sxs-lookup"><span data-stu-id="990cc-180">**Associate hello public IP address resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="990cc-181">Zasób publicznego adresu IP może być tylko skojarzone tooan konfiguracji adresów IP, który nie ma jeszcze skojarzone.</span><span class="sxs-lookup"><span data-stu-id="990cc-181">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="990cc-182">Można określić, czy konfiguracja IP ma skojarzone publicznego adresu IP, wprowadzając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="990cc-182">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="990cc-183">Zostaną wyświetlone dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="990cc-183">You see output similar toohello following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="990cc-184">Ponieważ hello **publicznego adresu IP** kolumny dla *IpConfig 3* jest puste, zasobu bez publicznego adresu IP jest obecnie skojarzone tooit.</span><span class="sxs-lookup"><span data-stu-id="990cc-184">Since hello **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="990cc-185">Można dodać istniejącego publicznego adresu IP adres zasobów tooIpConfig-3, lub wprowadź powitania po toocreate polecenia, co:</span><span class="sxs-lookup"><span data-stu-id="990cc-185">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="990cc-186">Wprowadź następujące polecenie publicznego adresu IP tooassociate hello adresów zasobów toohello istniejącej konfiguracji IP o nazwie hello *IpConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="990cc-186">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="990cc-187">Ustaw hello kart przy użyciu nowej konfiguracji IP hello wprowadzając hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="990cc-187">Set hello NIC with hello new IP configuration by entering hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="990cc-188">Wyświetlanie hello prywatnych adresów IP i hello publicznego adresu IP adres zasobów przypisanych toohello hello karty Sieciowej, wprowadzając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="990cc-188">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="990cc-189">Dodaj hello prywatnego adresu IP adres toohello maszyny Wirtualnej systemu operacyjnego, wykonując kroki hello systemu operacyjnego w hello [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](#os-config) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="990cc-189">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="990cc-190">Nie należy dodawać hello publicznego adresu IP address toohello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="990cc-190">Do not add hello public IP address toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
