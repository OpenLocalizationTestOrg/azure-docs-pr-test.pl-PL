---
title: "aaaManage sieciowej grupy zabezpieczeń - programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage sieciowych grup zabezpieczeń za pomocą programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="18660-103">Zarządzanie grupami zabezpieczeń sieci przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="18660-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="18660-104">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="18660-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="18660-105">W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello, które firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="18660-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="18660-106">Pobieranie informacji</span><span class="sxs-lookup"><span data-stu-id="18660-106">Retrieve Information</span></span>
<span data-ttu-id="18660-107">Można wyświetlić istniejących grup NSG, pobrać reguł dla istniejącej grupy NSG i dowiedzieć się, jakie zasoby grupy NSG jest skojarzona z.</span><span class="sxs-lookup"><span data-stu-id="18660-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="18660-108">Wyświetlanie istniejących grup NSG</span><span class="sxs-lookup"><span data-stu-id="18660-108">View existing NSGs</span></span>
<span data-ttu-id="18660-109">tooview wszystkich istniejących grup NSG w ramach subskrypcji, uruchom hello `Get-AzureRmNetworkSecurityGroup` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="18660-109">tooview all existing NSGs in a subscription, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="18660-110">Oczekiwany wynik:</span><span class="sxs-lookup"><span data-stu-id="18660-110">Expected result:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


<span data-ttu-id="18660-111">tooview hello lista grup NSG w określonej grupy zasobów, uruchom hello `Get-AzureRmNetworkSecurityGroup` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="18660-111">tooview hello list of NSGs in a specific resource group, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="18660-112">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="18660-112">Expected output:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="18660-113">Wyświetl listę wszystkich reguł dla grupy NSG</span><span class="sxs-lookup"><span data-stu-id="18660-113">List all rules for an NSG</span></span>
<span data-ttu-id="18660-114">tooview hello reguły NSG o nazwie **frontonu NSG**, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="18660-114">tooview hello rules of an NSG named **NSG-FrontEnd**, enter hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="18660-115">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="18660-115">Expected output:</span></span>

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> <span data-ttu-id="18660-116">Można również użyć `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello domyślnych reguł z hello **frontonu NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="18660-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello default rules from hello **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="18660-117">Wyświetlanie grup NSG powiązań</span><span class="sxs-lookup"><span data-stu-id="18660-117">View NSGs associations</span></span>
<span data-ttu-id="18660-118">tooview hello jakie zasoby **frontonu NSG** grupa NSG jest Skojarz z, uruchom hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="18660-118">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="18660-119">Wyszukaj hello **Networkinterface** i **podsieci** właściwości, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="18660-119">Look for hello **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="18660-120">W poprzednim przykładzie hello hello NSG nie jest skojarzony tooany interfejsów sieciowych (NIC); jest tooa skojarzonych podsieci o nazwie **frontonu**.</span><span class="sxs-lookup"><span data-stu-id="18660-120">In hello previous example, hello NSG is not associated tooany network interfaces (NICs); it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="18660-121">Zarządzaj regułami</span><span class="sxs-lookup"><span data-stu-id="18660-121">Manage rules</span></span>
<span data-ttu-id="18660-122">Można dodawać reguły tooan istniejące grupy NSG, edytować istniejące zasady i Usuń reguły.</span><span class="sxs-lookup"><span data-stu-id="18660-122">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="18660-123">Dodawanie reguły</span><span class="sxs-lookup"><span data-stu-id="18660-123">Add a rule</span></span>
<span data-ttu-id="18660-124">tooadd, dzięki czemu reguły **przychodzących** tooport ruchu **443** z dowolnej maszyny toohello **NSG frontonu** NSG, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="18660-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="18660-125">Uruchom następujące polecenie tooretrieve hello istniejące grupy NSG hello i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="18660-125">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="18660-126">Uruchom następujące polecenie tooadd hello toohello reguły NSG:</span><span class="sxs-lookup"><span data-stu-id="18660-126">Run hello following command tooadd a rule toohello NSG:</span></span>

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="18660-127">toosave hello zmian toohello NSG, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="18660-127">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="18660-128">Oczekiwane dane wyjściowe, pokazujący tylko hello reguły zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="18660-128">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a><span data-ttu-id="18660-129">Zmień reguły</span><span class="sxs-lookup"><span data-stu-id="18660-129">Change a rule</span></span>
<span data-ttu-id="18660-130">Reguła hello toochange utworzone powyżej tooallow ruchu przychodzącego ruchu z hello **Internet** , wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="18660-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, follow hello steps below.</span></span>

1. <span data-ttu-id="18660-131">Uruchom następujące polecenie tooretrieve hello istniejące grupy NSG hello i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="18660-131">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="18660-132">Uruchom następujące polecenie, używając nowego ustawienia reguły hello hello:</span><span class="sxs-lookup"><span data-stu-id="18660-132">Run hello following command with hello new rule settings:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="18660-133">toosave hello zmian toohello NSG, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="18660-133">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="18660-134">Oczekiwane dane wyjściowe, pokazujący tylko hello reguły zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="18660-134">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a><span data-ttu-id="18660-135">Usuwanie reguły</span><span class="sxs-lookup"><span data-stu-id="18660-135">Delete a rule</span></span>
1. <span data-ttu-id="18660-136">Uruchom następujące polecenie tooretrieve hello istniejące grupy NSG hello i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="18660-136">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="18660-137">Hello uruchom następujące polecenie tooremove hello reguły hello NSG:</span><span class="sxs-lookup"><span data-stu-id="18660-137">Run hello following command tooremove hello rule from hello NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="18660-138">Zapisz toohello zmian hello NSG, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="18660-138">Save hello changes made toohello NSG, by running hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="18660-139">Oczekiwane dane wyjściowe, pokazujący tylko hello reguły zabezpieczeń, powiadomienia hello **reguła https** nie jest już wyświetlane:</span><span class="sxs-lookup"><span data-stu-id="18660-139">Expected output showing only hello security rules, notice hello **https-rule** is no longer listed:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a><span data-ttu-id="18660-140">Zarządzanie skojarzenia</span><span class="sxs-lookup"><span data-stu-id="18660-140">Manage associations</span></span>
<span data-ttu-id="18660-141">Możesz skojarzyć toosubnets NSG i kart interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="18660-141">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="18660-142">Można również usunąć skojarzenie grupy NSG z dowolnego zasobu, który jest ona skojarzona.</span><span class="sxs-lookup"><span data-stu-id="18660-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="18660-143">Kojarzenie grupy NSG tooa karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="18660-143">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="18660-144">Witaj tooassociate **frontonu NSG** NSG toohello **TestNICWeb1** karty Sieciowej, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="18660-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="18660-145">Uruchom następujące polecenie tooretrieve hello istniejące grupy NSG hello i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="18660-145">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="18660-146">Hello uruchom następujące polecenie hello tooretrieve istniejących kart interfejsu Sieciowego i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="18660-146">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="18660-147">Zestaw hello **grupy NetworkSecurityGroup** właściwości hello **kart** wartość zmiennej toohello hello **NSG** zmiennej, wprowadzając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="18660-147">Set hello **NetworkSecurityGroup** property of hello **NIC** variable toohello value of hello **NSG** variable, by entering hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="18660-148">toosave hello zmian toohello karty Sieciowej, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="18660-148">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="18660-149">Oczekiwane dane wyjściowe przedstawiający tylko hello **grupy NetworkSecurityGroup** właściwości:</span><span class="sxs-lookup"><span data-stu-id="18660-149">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="18660-150">Usuń skojarzenie grupy NSG z karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="18660-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="18660-151">Witaj toodissociate **frontonu NSG** grupy NSG z hello **TestNICWeb1** karty Sieciowej, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="18660-151">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="18660-152">Hello uruchom następujące polecenie hello tooretrieve istniejących kart interfejsu Sieciowego i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="18660-152">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="18660-153">Zestaw hello **grupy NetworkSecurityGroup** właściwości hello **kart** zmiennej zbyt**$null** , uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="18660-153">Set hello **NetworkSecurityGroup** property of hello **NIC** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="18660-154">toosave hello zmian toohello karty Sieciowej, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="18660-154">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="18660-155">Oczekiwane dane wyjściowe przedstawiający tylko hello **grupy NetworkSecurityGroup** właściwości:</span><span class="sxs-lookup"><span data-stu-id="18660-155">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="18660-156">Usuń skojarzenie grupy NSG z podsiecią</span><span class="sxs-lookup"><span data-stu-id="18660-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="18660-157">Witaj toodissociate **frontonu NSG** grupy NSG z hello **frontonu** podsieci, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="18660-157">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="18660-158">Hello uruchom następujące polecenie hello tooretrieve istniejącej sieci wirtualnej i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="18660-158">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="18660-159">Uruchom hello następujące polecenia tooretrieve hello **frontonu** podsieci i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="18660-159">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="18660-160">Zestaw hello **grupy NetworkSecurityGroup** właściwości hello **podsieci** zmiennej zbyt**$null** wprowadzając hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="18660-160">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by entering hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="18660-161">toosave hello zmian toohello podsieci, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="18660-161">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="18660-162">Oczekiwane dane wyjściowe wyświetlane tylko hello właściwości hello **frontonu** podsieci.</span><span class="sxs-lookup"><span data-stu-id="18660-162">Expected output showing only hello properties of hello **FrontEnd** subnet.</span></span> <span data-ttu-id="18660-163">Powiadomienie nie ma właściwości **grupy NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="18660-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="18660-164">Kojarzenie grupy NSG podsieci tooa</span><span class="sxs-lookup"><span data-stu-id="18660-164">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="18660-165">Witaj tooassociate **frontonu NSG** NSG toohello **FronEnd** ponownie podsieci, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="18660-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="18660-166">Hello uruchom następujące polecenie hello tooretrieve istniejącej sieci wirtualnej i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="18660-166">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="18660-167">Uruchom hello następujące polecenia tooretrieve hello **frontonu** podsieci i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="18660-167">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="18660-168">Uruchom następujące polecenie tooretrieve hello istniejące grupy NSG hello i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="18660-168">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="18660-169">Zestaw hello **grupy NetworkSecurityGroup** właściwości hello **podsieci** zmiennej zbyt**$null** , uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="18660-169">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="18660-170">toosave hello zmian toohello podsieci, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="18660-170">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="18660-171">Oczekiwane dane wyjściowe przedstawiający tylko hello **grupy NetworkSecurityGroup** właściwości hello **frontonu** podsieci:</span><span class="sxs-lookup"><span data-stu-id="18660-171">Expected output showing only hello **NetworkSecurityGroup** property of hello **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="18660-172">Usuwanie grupy NSG</span><span class="sxs-lookup"><span data-stu-id="18660-172">Delete an NSG</span></span>
<span data-ttu-id="18660-173">Grupy NSG można usuwać tylko, jeśli nie został skojarzony tooany zasobów.</span><span class="sxs-lookup"><span data-stu-id="18660-173">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="18660-174">toodelete grupy NSG, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="18660-174">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="18660-175">zasoby hello toocheck skojarzony tooan NSG, uruchom hello `azure network nsg show` pokazane [skojarzenia grup NSG widoku](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="18660-175">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="18660-176">Jeśli hello grupa NSG jest skojarzona tooany kart sieciowych, uruchom hello `azure network nic set` pokazane [skojarzenie grupy NSG z karty Sieciowej](#Dissociate-an-NSG-from-a-NIC) dla poszczególnych kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="18660-176">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="18660-177">Jeśli hello NSG jest skojarzona tooany podsieci, uruchom hello `azure network vnet subnet set` pokazane [skojarzenie grupy NSG z podsiecią](#Dissociate-an-NSG-from-a-subnet) dla każdej podsieci.</span><span class="sxs-lookup"><span data-stu-id="18660-177">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="18660-178">Uruchom następujące polecenie hello hello toodelete NSG:</span><span class="sxs-lookup"><span data-stu-id="18660-178">toodelete hello NSG, run hello following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="18660-179">Witaj `-Force` parametru zapewnia nie ma potrzeby usuwania hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="18660-179">hello `-Force` parameter ensures you don't need tooconfirm hello deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="18660-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="18660-180">Next steps</span></span>
* <span data-ttu-id="18660-181">[Włącz rejestrowanie](virtual-network-nsg-manage-log.md) dla grup NSG.</span><span class="sxs-lookup"><span data-stu-id="18660-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

