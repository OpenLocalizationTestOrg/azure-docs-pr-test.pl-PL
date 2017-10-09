---
title: "aaaConfigure prywatnych adresów IP dla maszyn wirtualnych - programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak adresy IP prywatnej tooconfigure dla maszyn wirtualnych przy użyciu programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: d5f18929-15e3-40a2-9ee3-8188bc248ed8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4a3eb67de583e08208fcab40de1c2a8a9b65618c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="e0d4f-103">Konfigurowanie prywatnych adresów IP dla maszyny wirtualnej przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0d4f-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="e0d4f-104">Platforma Azure ma dwa modele wdrażania: usługa Azure Resource Manager i wersja klasyczna.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="e0d4f-105">Firma Microsoft zaleca utworzenie zasobów za pośrednictwem modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="e0d4f-106">więcej informacji o toolearn hello różnice między modelami hello dwa odczytu hello [modele wdrażania zrozumieć Azure](../azure-resource-manager/resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="e0d4f-107">W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="e0d4f-108">Możesz również [Zarządzanie statycznego prywatnego adresu IP w hello klasycznego modelu wdrażania](virtual-networks-static-private-ip-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e0d4f-108">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="e0d4f-109">w powyższym scenariuszu hello na podstawie próbek Hello PowerShell poniższe polecenia oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="e0d4f-110">Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, najpierw utworzyć środowisko testowe hello opisane w [utworzyć sieć wirtualną](virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e0d4f-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="e0d4f-111">Tworzenie maszyny wirtualnej ze statycznym prywatnym adresem IP</span><span class="sxs-lookup"><span data-stu-id="e0d4f-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="e0d4f-112">toocreate maszyny Wirtualnej o nazwie *DNS01* w hello *frontonu* podsieci sieci wirtualnej o nazwie *TestVNet* z statycznego prywatnego adresu IP z *192.168.1.101*, Wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e0d4f-112">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="e0d4f-113">Ustaw zmienne dla konta magazynu hello, lokalizacja grupy zasobów i toobe poświadczenia używane.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-113">Set variables for hello storage account, location, resource group, and credentials toobe used.</span></span> <span data-ttu-id="e0d4f-114">Konieczne będzie tooenter nazwę użytkownika i hasło dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-114">You will need tooenter a user name and password for hello VM.</span></span> <span data-ttu-id="e0d4f-115">Grupa kont i zasobów magazynu Hello musi już istnieć.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-115">hello storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type hello name and password of hello local administrator account."
    ```

2. <span data-ttu-id="e0d4f-116">Sieć wirtualna hello pobierania i podsieć ma toocreate hello maszyny Wirtualnej w ramach.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-116">Retrieve hello virtual network and subnet you want toocreate hello VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="e0d4f-117">Jeśli to konieczne, Utwórz publicznego adresu IP adres tooaccess hello maszyny Wirtualnej na podstawie hello Internet.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-117">If necessary, create a public IP address tooaccess hello VM from hello Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="e0d4f-118">Utwórz kartę Sieciową przy użyciu hello statycznego prywatnego adresu IP ma toohello tooassign maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-118">Create a NIC using hello static private IP address you want tooassign toohello VM.</span></span> <span data-ttu-id="e0d4f-119">Upewnij się, że hello IP jest z zakresu podsieci hello dodawanego hello maszyny Wirtualnej, aby.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-119">Make sure hello IP is from hello subnet range you are adding hello VM to.</span></span> <span data-ttu-id="e0d4f-120">Jest głównym krok hello tego artykułu, w którym ustawić hello prywatnego adresu IP toobe statycznych.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-120">This is hello main step for this article, where you set hello private IP toobe static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="e0d4f-121">Utwórz hello utworzenia maszyny Wirtualnej przy użyciu hello karty Sieciowej powyżej.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-121">Create hello VM using hello NIC created above.</span></span>

    ```powershell
    $vm = New-AzureRmVMConfig -VMName DNS01 -VMSize "Standard_A1"
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName DNS01 `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/WindowsVMosDisk.vhd"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name "windowsvmosdisk" -VhdUri $osDiskUri `
    -CreateOption fromImage
    New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm 
    ```

    <span data-ttu-id="e0d4f-122">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e0d4f-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="e0d4f-123">Pobrać statycznych prywatne informacje o adresie IP dla karty sieciowej</span><span class="sxs-lookup"><span data-stu-id="e0d4f-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="e0d4f-124">tooview hello statycznego prywatnego adresu IP adres dla hello maszyny Wirtualnej utworzone za pomocą skryptu hello powyżej, uruchom następujące polecenia programu PowerShell hello i sprawdź wartości hello *elementu PrivateIpAddress* i  *PrivateIpAllocationMethod*:</span><span class="sxs-lookup"><span data-stu-id="e0d4f-124">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="e0d4f-125">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e0d4f-125">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Static",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="e0d4f-126">Usuń statycznego prywatnego adresu IP z karty sieciowej</span><span class="sxs-lookup"><span data-stu-id="e0d4f-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="e0d4f-127">tooremove hello statycznego prywatnego adresu IP dodane toohello maszyny Wirtualnej w skrypcie hello powyżej hello uruchom następujące polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e0d4f-127">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="e0d4f-128">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e0d4f-128">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WindowsVM"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Dynamic",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="add-a-static-private-ip-address-tooa-network-interface"></a><span data-ttu-id="e0d4f-129">Dodawanie statycznego prywatnego adresu IP adres tooa interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="e0d4f-129">Add a static private IP address tooa network interface</span></span>
<span data-ttu-id="e0d4f-130">tooadd statycznego prywatnego adresu IP adres toohello maszyny Wirtualnej utworzonej przy użyciu skryptu hello powyżej, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="e0d4f-130">tooadd a static private IP address toohello VM created using hello script above, run hello following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-hello-allocation-method-for-a-private-ip-address-assigned-tooa-network-interface"></a><span data-ttu-id="e0d4f-131">Zmień hello metoda przydziału prywatnego adresu IP przypisany tooa interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="e0d4f-131">Change hello allocation method for a private IP address assigned tooa network interface</span></span>

<span data-ttu-id="e0d4f-132">Prywatny adres IP jest przypisany tooa karty Sieciowej z metody statyczne lub dynamiczne alokacji hello.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-132">A private IP address is assigned tooa NIC with hello static or dynamic allocation method.</span></span> <span data-ttu-id="e0d4f-133">Dynamiczne adresy IP można zmienić po uruchamiania maszyny Wirtualnej, który wcześniej był w hello zatrzymane (cofnięciu przydziału) stanu.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-133">Dynamic IP addresses can change after starting a VM that was previously in hello stopped (deallocated) state.</span></span> <span data-ttu-id="e0d4f-134">To może powodować problemy jeśli hello maszyny Wirtualnej jest hostem usługi wymagającej hello tego samego adresu IP, nawet po uruchomieniu z zatrzymana (cofnięciu przydziału).</span><span class="sxs-lookup"><span data-stu-id="e0d4f-134">This can potentially cause issues if hello VM is hosting a service that requires hello same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="e0d4f-135">Statyczne adresy IP są zachowywane, aż do usunięcia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-135">Static IP addresses are retained until hello VM is deleted.</span></span> <span data-ttu-id="e0d4f-136">Metoda alokacji hello toochange adresu IP, uruchom hello następującego skryptu, który zmienia hello metodę alokacji z toostatic dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-136">toochange hello allocation method of an IP address, run hello following script, which changes hello allocation method from dynamic toostatic.</span></span> <span data-ttu-id="e0d4f-137">Jeśli hello metodę alokacji dla bieżącego prywatnego adresu IP hello jest statyczny, zmień *statycznych* za*dynamiczne* przed wykonaniem skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-137">If hello allocation method for hello current private IP address is static, change *Static* too*Dynamic* before executing hello script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "hello allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for hello IP address" $IP"." -NoNewline
```

<span data-ttu-id="e0d4f-138">Jeśli nie znasz nazwy hello hello kart interfejsu Sieciowego, można wyświetlić listę kart sieciowych w grupie zasobów, wprowadzając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e0d4f-138">If you don't know hello name of hello NIC, you can view a list of NICs within a resource group by entering hello following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="e0d4f-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0d4f-139">Next steps</span></span>
* <span data-ttu-id="e0d4f-140">Dowiedz się więcej o [zastrzeżone publicznego adresu IP](virtual-networks-reserved-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="e0d4f-141">Dowiedz się więcej o [poziomie wystąpienia publicznego adresu IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresów.</span><span class="sxs-lookup"><span data-stu-id="e0d4f-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="e0d4f-142">Zapoznaj się hello [zastrzeżonego adresu IP interfejsów API REST](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0d4f-142">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

