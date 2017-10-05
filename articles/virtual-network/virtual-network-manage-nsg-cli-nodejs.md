---
title: "Zarządzanie grupami zabezpieczeń sieci - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać przy użyciu interfejsu wiersza polecenia platformy Azure (CLI) 1.0 grup zabezpieczeń sieci."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e53c3ff2ffbef95d6b72ca6afb3b4de377f0389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-cli-10"></a><span data-ttu-id="444ca-103">Zarządzanie grupami zabezpieczeń sieci przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="444ca-103">Manage network security groups using the Azure CLI 1.0</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="444ca-104">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="444ca-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="444ca-105">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="444ca-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="444ca-106">[Interfejs wiersza polecenia platformy Azure w wersji 1.0](#View-existing-NSGs) — nasz interfejs wiersza polecenia dla klasycznego modelu wdrażania i modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="444ca-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="444ca-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) -naszej nowej generacji interfejsu wiersza polecenia do zarządzania model wdrażania zasobów (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="444ca-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="444ca-108">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="444ca-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="444ca-109">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów, które firma Microsoft zaleca w przypadku większości nowych wdrożeń zamiast klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="444ca-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="444ca-110">Pobieranie informacji</span><span class="sxs-lookup"><span data-stu-id="444ca-110">Retrieve Information</span></span>
<span data-ttu-id="444ca-111">Można wyświetlić istniejących grup NSG, pobrać reguł dla istniejącej grupy NSG i dowiedzieć się, jakie zasoby grupy NSG jest skojarzona z.</span><span class="sxs-lookup"><span data-stu-id="444ca-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="444ca-112">Wyświetlanie istniejących grup NSG</span><span class="sxs-lookup"><span data-stu-id="444ca-112">View existing NSGs</span></span>
<span data-ttu-id="444ca-113">Aby wyświetlić listę grup NSG w określonej grupy zasobów, uruchom `azure network nsg list` polecenia, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="444ca-113">To view the list of NSGs in a specific resource group, run the `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="444ca-114">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="444ca-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting the network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="444ca-115">Wyświetl listę wszystkich reguł dla grupy NSG</span><span class="sxs-lookup"><span data-stu-id="444ca-115">List all rules for an NSG</span></span>
<span data-ttu-id="444ca-116">Aby wyświetlić reguły NSG o nazwie **frontonu NSG**Uruchom `azure network nsg show` polecenia, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="444ca-116">To view the rules of an NSG named **NSG-FrontEnd**, run the `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="444ca-117">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="444ca-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Name                            : NSG-FrontEnd
    data:    Type                            : Microsoft.Network/networkSecurityGroups
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    Tags                            : displayName=NSG - Front End
    data:    Security group rules:
    data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
    data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
    data:    rdp-rule                       Internet           *            *               3389              Tcp       Inbound    Allow   100
    data:    web-rule                       Internet           *            *               80                Tcp       Inbound    Allow   101
    data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000
    data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001
    data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500
    data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000
    data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001
    data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500
    info:    network nsg show command OK

> [!NOTE]
> <span data-ttu-id="444ca-118">Można również użyć `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` Aby wyświetlić listę reguł z **frontonu NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="444ca-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` to list the rules from the **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="444ca-119">Wyświetlanie NSG powiązań</span><span class="sxs-lookup"><span data-stu-id="444ca-119">View NSG associations</span></span>

<span data-ttu-id="444ca-120">Aby wyświetlić zasobów **NSG frontonu** grupa NSG jest skojarzony z uruchomiony `azure network nsg show` polecenia w sposób przedstawiony poniżej.</span><span class="sxs-lookup"><span data-stu-id="444ca-120">To view what resources the **NSG-FrontEnd** NSG is associate with, run the `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="444ca-121">Zwróć uwagę, że jedyną różnicą jest użycie **--json** parametru.</span><span class="sxs-lookup"><span data-stu-id="444ca-121">Notice that the only difference is the use of the **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="444ca-122">Wyszukaj **Networkinterface** i **podsieci** właściwości, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="444ca-122">Look for the **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="444ca-123">W powyższym przykładzie grupy NSG nie jest skojarzony z żadnych interfejsów sieciowych (NIC) i jest on skojarzony z podsiecią o nazwie **frontonu**.</span><span class="sxs-lookup"><span data-stu-id="444ca-123">In the example above, the NSG is not associated to any network interfaces (NICs), and it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="444ca-124">Zarządzaj regułami</span><span class="sxs-lookup"><span data-stu-id="444ca-124">Manage rules</span></span>
<span data-ttu-id="444ca-125">Można dodać reguły do istniejącej grupy NSG, edytować istniejące zasady i Usuń reguły.</span><span class="sxs-lookup"><span data-stu-id="444ca-125">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="444ca-126">Dodawanie reguły</span><span class="sxs-lookup"><span data-stu-id="444ca-126">Add a rule</span></span>
<span data-ttu-id="444ca-127">Można dodać, dzięki czemu reguły **przychodzących** ruch do portu **443** z dowolnej maszyny do **frontonu NSG** NSG, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="444ca-127">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, enter the following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access to port 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="444ca-128">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="444ca-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up the network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access to port 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="444ca-129">Zmień reguły</span><span class="sxs-lookup"><span data-stu-id="444ca-129">Change a rule</span></span>
<span data-ttu-id="444ca-130">Aby zmienić reguły utworzone powyżej, aby zezwalać na ruch przychodzący z **Internet** , uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="444ca-130">To change the rule created above to allow inbound traffic from the **Internet** only, run the following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="444ca-131">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="444ca-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up the network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access to port 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="444ca-132">Usuwanie reguły</span><span class="sxs-lookup"><span data-stu-id="444ca-132">Delete a rule</span></span>
<span data-ttu-id="444ca-133">Aby usunąć regułę utworzone powyżej, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="444ca-133">To delete the rule created above, run the following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="444ca-134">`--quiet` Parametru zapewnia nie trzeba potwierdzić usunięcie.</span><span class="sxs-lookup"><span data-stu-id="444ca-134">The `--quiet` parameter ensures you don't need to confirm the deletion.</span></span>
>

<span data-ttu-id="444ca-135">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="444ca-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up the network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="444ca-136">Zarządzanie skojarzenia</span><span class="sxs-lookup"><span data-stu-id="444ca-136">Manage associations</span></span>
<span data-ttu-id="444ca-137">Możesz skojarzyć grupy NSG do podsieci i karty sieciowe.</span><span class="sxs-lookup"><span data-stu-id="444ca-137">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="444ca-138">Można również usunąć skojarzenie grupy NSG z dowolnego zasobu, który jest ona skojarzona.</span><span class="sxs-lookup"><span data-stu-id="444ca-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="444ca-139">Kojarzenie grupy NSG z kartą sieciową</span><span class="sxs-lookup"><span data-stu-id="444ca-139">Associate an NSG to a NIC</span></span>
<span data-ttu-id="444ca-140">Aby skojarzyć **frontonu NSG** grupy NSG **TestNICWeb1** karty Sieciowej, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="444ca-140">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, run the following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="444ca-141">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="444ca-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up the network interface "TestNICWeb1"
    + Looking up the network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up the network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Network security group          : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Virtual machine                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="444ca-142">Usuń skojarzenie grupy NSG z karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="444ca-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="444ca-143">Aby usunąć skojarzenie **frontonu NSG** grupy NSG z **TestNICWeb1** karty Sieciowej, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="444ca-143">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, run the following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="444ca-144">Uwaga "" (pusta) wartość `network-security-group-id` parametru.</span><span class="sxs-lookup"><span data-stu-id="444ca-144">Notice the "" (empty) value for the `network-security-group-id` parameter.</span></span> <span data-ttu-id="444ca-145">To, jak usunąć skojarzenie grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="444ca-145">That is how you remove an association to an NSG.</span></span> <span data-ttu-id="444ca-146">Nie można taki sam jak `network-security-group-name` parametru.</span><span class="sxs-lookup"><span data-stu-id="444ca-146">You can't do the same with the `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="444ca-147">Oczekiwany wynik:</span><span class="sxs-lookup"><span data-stu-id="444ca-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up the network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up the network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="444ca-148">Usuń skojarzenie grupy NSG z podsiecią</span><span class="sxs-lookup"><span data-stu-id="444ca-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="444ca-149">Aby usunąć skojarzenie **frontonu NSG** grupy NSG z **frontonu** podsieci, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="444ca-149">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, run the following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="444ca-150">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="444ca-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up the subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up the subnet "FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:    Type                            : Microsoft.Network/virtualNetworks/subnets
    data:    ProvisioningState               : Succeeded
    data:    Name                            : FrontEnd
    data:    Address prefix                  : 192.168.1.0/24
    data:    IP configurations:
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
    data:
    info:    network vnet subnet set command OK

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="444ca-151">Kojarzenie grupy NSG z podsiecią</span><span class="sxs-lookup"><span data-stu-id="444ca-151">Associate an NSG to a subnet</span></span>
<span data-ttu-id="444ca-152">Aby skojarzyć **frontonu NSG** grupy NSG **FronEnd** podsieci ponownie, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="444ca-152">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, run the following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="444ca-153">Polecenie powyżej działa tylko wtedy, ponieważ **frontonu NSG** grupa NSG jest w tej samej grupie zasobów co sieć wirtualna **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="444ca-153">The command above only works because the **NSG-FrontEnd** NSG is in the same resource group as the virtual network **TestVNet**.</span></span> <span data-ttu-id="444ca-154">Jeśli grupa NSG jest w innej grupie zasobów, należy użyć `--network-security-group-id` parametru i podaj pełny identyfikator grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="444ca-154">If the NSG is in a different resource group, you need to use the `--network-security-group-id` parameter instead, and provide the full id for the NSG.</span></span> <span data-ttu-id="444ca-155">Identyfikator można pobrać przez uruchomienie `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` i wyszukując **identyfikator** właściwości.</span><span class="sxs-lookup"><span data-stu-id="444ca-155">You can retrieve the id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for the **id** property.</span></span> 
> 

<span data-ttu-id="444ca-156">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="444ca-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up the subnet "FrontEnd"
        + Looking up the network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
        data:
        info:    network vnet subnet set command OK

## <a name="delete-an-nsg"></a><span data-ttu-id="444ca-157">Usuwanie grupy NSG</span><span class="sxs-lookup"><span data-stu-id="444ca-157">Delete an NSG</span></span>
<span data-ttu-id="444ca-158">Grupy NSG można usuwać tylko, jeśli nie został skojarzony z żadnym zasobem.</span><span class="sxs-lookup"><span data-stu-id="444ca-158">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="444ca-159">Aby usunąć grupy NSG, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="444ca-159">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="444ca-160">Aby sprawdzić zasoby skojarzone grupy NSG, uruchom `azure network nsg show` pokazane [skojarzenia grup NSG widoku](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="444ca-160">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="444ca-161">Jeśli grupa NSG jest skojarzona z dowolnej karty interfejsu sieciowego, uruchom `azure network nic set` pokazane [skojarzenie grupy NSG z karty Sieciowej](#Dissociate-an-NSG-from-a-NIC) dla poszczególnych kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="444ca-161">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="444ca-162">Jeśli grupa NSG jest skojarzona z dowolnej podsieci, uruchom `azure network vnet subnet set` pokazane [skojarzenie grupy NSG z podsiecią](#Dissociate-an-NSG-from-a-subnet) dla każdej podsieci.</span><span class="sxs-lookup"><span data-stu-id="444ca-162">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="444ca-163">Aby usunąć grupy NSG, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="444ca-163">To delete the NSG, run the following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="444ca-164">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="444ca-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up the network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="444ca-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="444ca-165">Next steps</span></span>
* <span data-ttu-id="444ca-166">[Włącz rejestrowanie](virtual-network-nsg-manage-log.md) dla grup NSG.</span><span class="sxs-lookup"><span data-stu-id="444ca-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

