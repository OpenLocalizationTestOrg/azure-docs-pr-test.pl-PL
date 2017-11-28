---
title: "Zarządzanie grupami zabezpieczeń sieci - programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać grupami zabezpieczeń sieci przy użyciu programu PowerShell."
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
ms.openlocfilehash: ca7f4926ca4edf9d20612aca74f6ae5f0ed847b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="4d433-103">Zarządzanie grupami zabezpieczeń sieci przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d433-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="4d433-104">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4d433-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4d433-105">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów, które firma Microsoft zaleca w przypadku większości nowych wdrożeń zamiast klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="4d433-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="4d433-106">Pobieranie informacji</span><span class="sxs-lookup"><span data-stu-id="4d433-106">Retrieve Information</span></span>
<span data-ttu-id="4d433-107">Można wyświetlić istniejących grup NSG, pobrać reguł dla istniejącej grupy NSG i dowiedzieć się, jakie zasoby grupy NSG jest skojarzona z.</span><span class="sxs-lookup"><span data-stu-id="4d433-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="4d433-108">Wyświetlanie istniejących grup NSG</span><span class="sxs-lookup"><span data-stu-id="4d433-108">View existing NSGs</span></span>
<span data-ttu-id="4d433-109">Aby wyświetlić wszystkich istniejących grup NSG w ramach subskrypcji, uruchom `Get-AzureRmNetworkSecurityGroup` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4d433-109">To view all existing NSGs in a subscription, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="4d433-110">Oczekiwany wynik:</span><span class="sxs-lookup"><span data-stu-id="4d433-110">Expected result:</span></span>

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


<span data-ttu-id="4d433-111">Aby wyświetlić listę grup NSG w określonej grupy zasobów, uruchom `Get-AzureRmNetworkSecurityGroup` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4d433-111">To view the list of NSGs in a specific resource group, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="4d433-112">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="4d433-112">Expected output:</span></span>

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

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="4d433-113">Wyświetl listę wszystkich reguł dla grupy NSG</span><span class="sxs-lookup"><span data-stu-id="4d433-113">List all rules for an NSG</span></span>
<span data-ttu-id="4d433-114">Aby wyświetlić reguły NSG o nazwie **frontonu NSG**, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-114">To view the rules of an NSG named **NSG-FrontEnd**, enter the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="4d433-115">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="4d433-115">Expected output:</span></span>

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
> <span data-ttu-id="4d433-116">Można również użyć `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` Aby wyświetlić listę domyślnych reguł z **frontonu NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="4d433-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` to list the default rules from the **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="4d433-117">Wyświetlanie grup NSG powiązań</span><span class="sxs-lookup"><span data-stu-id="4d433-117">View NSGs associations</span></span>
<span data-ttu-id="4d433-118">Aby wyświetlić zasobów **frontonu NSG** grupa NSG jest skojarzenia, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-118">To view what resources the **NSG-FrontEnd** NSG is associate with, run the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="4d433-119">Wyszukaj **Networkinterface** i **podsieci** właściwości, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="4d433-119">Look for the **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="4d433-120">W poprzednim przykładzie grupa NSG nie jest skojarzony z żadnych interfejsów sieciowych (NIC); jest on skojarzony z podsiecią o nazwie **frontonu**.</span><span class="sxs-lookup"><span data-stu-id="4d433-120">In the previous example, the NSG is not associated to any network interfaces (NICs); it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="4d433-121">Zarządzaj regułami</span><span class="sxs-lookup"><span data-stu-id="4d433-121">Manage rules</span></span>
<span data-ttu-id="4d433-122">Można dodać reguły do istniejącej grupy NSG, edytować istniejące zasady i Usuń reguły.</span><span class="sxs-lookup"><span data-stu-id="4d433-122">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="4d433-123">Dodawanie reguły</span><span class="sxs-lookup"><span data-stu-id="4d433-123">Add a rule</span></span>
<span data-ttu-id="4d433-124">Można dodać, dzięki czemu reguły **przychodzących** ruch do portu **443** z dowolnej maszyny do **frontonu NSG** NSG, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4d433-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="4d433-125">Uruchom następujące polecenie, aby pobrać istniejącej grupy NSG i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="4d433-125">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="4d433-126">Uruchom następujące polecenie, aby dodać regułę do grupy NSG:</span><span class="sxs-lookup"><span data-stu-id="4d433-126">Run the following command to add a rule to the NSG:</span></span>

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

3. <span data-ttu-id="4d433-127">Aby zapisać zmiany wprowadzone w grupie NSG, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-127">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="4d433-128">Oczekiwane dane wyjściowe, pokazujący tylko reguły zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="4d433-128">Expected output showing only the security rules:</span></span>
   
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

### <a name="change-a-rule"></a><span data-ttu-id="4d433-129">Zmień reguły</span><span class="sxs-lookup"><span data-stu-id="4d433-129">Change a rule</span></span>
<span data-ttu-id="4d433-130">Aby zmienić reguły utworzone powyżej, aby zezwalać na ruch przychodzący z **Internet** , wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="4d433-130">To change the rule created above to allow inbound traffic from the **Internet** only, follow the steps below.</span></span>

1. <span data-ttu-id="4d433-131">Uruchom następujące polecenie, aby pobrać istniejącej grupy NSG i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="4d433-131">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="4d433-132">Uruchom następujące polecenie, przy użyciu nowych ustawień reguły:</span><span class="sxs-lookup"><span data-stu-id="4d433-132">Run the following command with the new rule settings:</span></span>

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

3. <span data-ttu-id="4d433-133">Aby zapisać zmiany wprowadzone w grupie NSG, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-133">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="4d433-134">Oczekiwane dane wyjściowe, pokazujący tylko reguły zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="4d433-134">Expected output showing only the security rules:</span></span>
   
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

### <a name="delete-a-rule"></a><span data-ttu-id="4d433-135">Usuwanie reguły</span><span class="sxs-lookup"><span data-stu-id="4d433-135">Delete a rule</span></span>
1. <span data-ttu-id="4d433-136">Uruchom następujące polecenie, aby pobrać istniejącej grupy NSG i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="4d433-136">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="4d433-137">Uruchom następujące polecenie, aby usunąć regułę z grupy NSG:</span><span class="sxs-lookup"><span data-stu-id="4d433-137">Run the following command to remove the rule from the NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="4d433-138">Zapisz zmiany wprowadzone w grupie NSG, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-138">Save the changes made to the NSG, by running the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="4d433-139">Oczekiwano danych wyjściowych wyświetlane tylko zasady zabezpieczeń, a powiadomienie **reguła https** nie jest już wyświetlane:</span><span class="sxs-lookup"><span data-stu-id="4d433-139">Expected output showing only the security rules, notice the **https-rule** is no longer listed:</span></span>
   
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

## <a name="manage-associations"></a><span data-ttu-id="4d433-140">Zarządzanie skojarzenia</span><span class="sxs-lookup"><span data-stu-id="4d433-140">Manage associations</span></span>
<span data-ttu-id="4d433-141">Możesz skojarzyć grupy NSG do podsieci i karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="4d433-141">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="4d433-142">Można również usunąć skojarzenie grupy NSG z dowolnego zasobu, który jest ona skojarzona.</span><span class="sxs-lookup"><span data-stu-id="4d433-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="4d433-143">Kojarzenie grupy NSG z kartą sieciową</span><span class="sxs-lookup"><span data-stu-id="4d433-143">Associate an NSG to a NIC</span></span>
<span data-ttu-id="4d433-144">Aby skojarzyć **frontonu NSG** grupy NSG **TestNICWeb1** karty Sieciowej, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4d433-144">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="4d433-145">Uruchom następujące polecenie, aby pobrać istniejącej grupy NSG i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="4d433-145">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="4d433-146">Uruchom następujące polecenie, aby pobrać istniejącej karty NIC i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="4d433-146">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="4d433-147">Ustaw **grupy NetworkSecurityGroup** właściwość **kart** zmiennej wartość **NSG** zmiennej, wprowadzając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-147">Set the **NetworkSecurityGroup** property of the **NIC** variable to the value of the **NSG** variable, by entering the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="4d433-148">Aby zapisać zmiany wprowadzone do karty Sieciowej, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-148">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="4d433-149">Oczekiwane dane wyjściowe są wyświetlane tylko **grupy NetworkSecurityGroup** właściwości:</span><span class="sxs-lookup"><span data-stu-id="4d433-149">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="4d433-150">Usuń skojarzenie grupy NSG z karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="4d433-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="4d433-151">Aby usunąć skojarzenie **frontonu NSG** grupy NSG z **TestNICWeb1** karty Sieciowej, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4d433-151">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="4d433-152">Uruchom następujące polecenie, aby pobrać istniejącej karty NIC i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="4d433-152">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="4d433-153">Ustaw **grupy NetworkSecurityGroup** właściwość **kart** zmienną **$null** , uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-153">Set the **NetworkSecurityGroup** property of the **NIC** variable to **$null** by running the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="4d433-154">Aby zapisać zmiany wprowadzone do karty Sieciowej, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-154">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="4d433-155">Oczekiwane dane wyjściowe są wyświetlane tylko **grupy NetworkSecurityGroup** właściwości:</span><span class="sxs-lookup"><span data-stu-id="4d433-155">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="4d433-156">Usuń skojarzenie grupy NSG z podsiecią</span><span class="sxs-lookup"><span data-stu-id="4d433-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="4d433-157">Aby usunąć skojarzenie **frontonu NSG** grupy NSG z **frontonu** podsieci, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4d433-157">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="4d433-158">Uruchom następujące polecenie, aby pobrać istniejącej sieci wirtualnej i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="4d433-158">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="4d433-159">Uruchom następujące polecenie, aby pobrać **frontonu** podsieci i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="4d433-159">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="4d433-160">Ustaw **grupy NetworkSecurityGroup** właściwość **podsieci** zmienną **$null** , wprowadzając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-160">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by entering the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="4d433-161">Aby zapisać zmiany wprowadzone do podsieci, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-161">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="4d433-162">Oczekiwano danych wyjściowych, pokazujący tylko właściwości elementu **frontonu** podsieci.</span><span class="sxs-lookup"><span data-stu-id="4d433-162">Expected output showing only the properties of the **FrontEnd** subnet.</span></span> <span data-ttu-id="4d433-163">Powiadomienie nie ma właściwości **grupy NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="4d433-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
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

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="4d433-164">Kojarzenie grupy NSG z podsiecią</span><span class="sxs-lookup"><span data-stu-id="4d433-164">Associate an NSG to a subnet</span></span>
<span data-ttu-id="4d433-165">Aby skojarzyć **frontonu NSG** grupy NSG **FronEnd** podsieci, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4d433-165">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="4d433-166">Uruchom następujące polecenie, aby pobrać istniejącej sieci wirtualnej i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="4d433-166">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="4d433-167">Uruchom następujące polecenie, aby pobrać **frontonu** podsieci i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="4d433-167">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="4d433-168">Uruchom następujące polecenie, aby pobrać istniejącej grupy NSG i zapisze go w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="4d433-168">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="4d433-169">Ustaw **grupy NetworkSecurityGroup** właściwość **podsieci** zmienną **$null** , uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-169">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by running the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="4d433-170">Aby zapisać zmiany wprowadzone do podsieci, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-170">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="4d433-171">Oczekiwane dane wyjściowe są wyświetlane tylko **grupy NetworkSecurityGroup** właściwość **frontonu** podsieci:</span><span class="sxs-lookup"><span data-stu-id="4d433-171">Expected output showing only the **NetworkSecurityGroup** property of the **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="4d433-172">Usuwanie grupy NSG</span><span class="sxs-lookup"><span data-stu-id="4d433-172">Delete an NSG</span></span>
<span data-ttu-id="4d433-173">Grupy NSG można usuwać tylko, jeśli nie został skojarzony z żadnym zasobem.</span><span class="sxs-lookup"><span data-stu-id="4d433-173">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="4d433-174">Aby usunąć grupy NSG, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="4d433-174">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="4d433-175">Aby sprawdzić zasoby skojarzone grupy NSG, uruchom `azure network nsg show` pokazane [skojarzenia grup NSG widoku](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="4d433-175">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="4d433-176">Jeśli grupa NSG jest skojarzona z dowolnej karty interfejsu sieciowego, uruchom `azure network nic set` pokazane [skojarzenie grupy NSG z karty Sieciowej](#Dissociate-an-NSG-from-a-NIC) dla poszczególnych kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="4d433-176">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="4d433-177">Jeśli grupa NSG jest skojarzona z dowolnej podsieci, uruchom `azure network vnet subnet set` pokazane [skojarzenie grupy NSG z podsiecią](#Dissociate-an-NSG-from-a-subnet) dla każdej podsieci.</span><span class="sxs-lookup"><span data-stu-id="4d433-177">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="4d433-178">Aby usunąć grupy NSG, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4d433-178">To delete the NSG, run the following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="4d433-179">`-Force` Parametru zapewnia nie trzeba potwierdzić usunięcie.</span><span class="sxs-lookup"><span data-stu-id="4d433-179">The `-Force` parameter ensures you don't need to confirm the deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="4d433-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4d433-180">Next steps</span></span>
* <span data-ttu-id="4d433-181">[Włącz rejestrowanie](virtual-network-nsg-manage-log.md) dla grup NSG.</span><span class="sxs-lookup"><span data-stu-id="4d433-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

