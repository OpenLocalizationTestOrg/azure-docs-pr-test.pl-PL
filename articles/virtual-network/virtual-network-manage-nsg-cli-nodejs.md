---
title: "aaaManage sieciowej grupy zabezpieczeń — 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage sieciowych grup zabezpieczeń za pomocą hello Azure interfejsu wiersza polecenia (CLI) 1.0."
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
ms.openlocfilehash: 9a429f947abbcb5fa6adb40c84504f68efd5e20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="596f1-103">Zarządzanie grupami zabezpieczeń sieci przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="596f1-103">Manage network security groups using hello Azure CLI 1.0</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="596f1-104">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="596f1-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="596f1-105">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="596f1-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="596f1-106">[Azure CLI 1.0](#View-existing-NSGs) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modelami wdrażania</span><span class="sxs-lookup"><span data-stu-id="596f1-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="596f1-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania hello zasobów (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="596f1-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="596f1-108">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="596f1-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="596f1-109">W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello, które firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="596f1-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="596f1-110">Pobieranie informacji</span><span class="sxs-lookup"><span data-stu-id="596f1-110">Retrieve Information</span></span>
<span data-ttu-id="596f1-111">Można wyświetlić istniejących grup NSG, pobrać reguł dla istniejącej grupy NSG i dowiedzieć się, jakie zasoby grupy NSG jest skojarzona z.</span><span class="sxs-lookup"><span data-stu-id="596f1-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="596f1-112">Wyświetlanie istniejących grup NSG</span><span class="sxs-lookup"><span data-stu-id="596f1-112">View existing NSGs</span></span>
<span data-ttu-id="596f1-113">tooview hello lista grup NSG w określonej grupy zasobów, uruchom hello `azure network nsg list` polecenia, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="596f1-113">tooview hello list of NSGs in a specific resource group, run hello `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="596f1-114">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="596f1-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting hello network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="596f1-115">Wyświetl listę wszystkich reguł dla grupy NSG</span><span class="sxs-lookup"><span data-stu-id="596f1-115">List all rules for an NSG</span></span>
<span data-ttu-id="596f1-116">tooview hello reguły NSG o nazwie **frontonu NSG**Uruchom hello `azure network nsg show` polecenia, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="596f1-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="596f1-117">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="596f1-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up hello network security group "NSG-FrontEnd"
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
> <span data-ttu-id="596f1-118">Można również użyć `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` toolist hello reguły z hello **frontonu NSG** NSG.</span><span class="sxs-lookup"><span data-stu-id="596f1-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` toolist hello rules from hello **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="596f1-119">Wyświetlanie NSG powiązań</span><span class="sxs-lookup"><span data-stu-id="596f1-119">View NSG associations</span></span>

<span data-ttu-id="596f1-120">tooview hello jakie zasoby **frontonu NSG** grupa NSG jest hello Skojarz z, uruchom `azure network nsg show` polecenia, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="596f1-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="596f1-121">Zwróć uwagę że hello tylko różnica polega na powitania stosowania hello **--json** parametru.</span><span class="sxs-lookup"><span data-stu-id="596f1-121">Notice that hello only difference is hello use of hello **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="596f1-122">Wyszukaj hello **Networkinterface** i **podsieci** właściwości, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="596f1-122">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="596f1-123">W powyższym przykładzie hello, hello NSG nie jest skojarzony tooany interfejsów sieciowych (NIC) i jest tooa skojarzonych podsieci o nazwie **frontonu**.</span><span class="sxs-lookup"><span data-stu-id="596f1-123">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="596f1-124">Zarządzaj regułami</span><span class="sxs-lookup"><span data-stu-id="596f1-124">Manage rules</span></span>
<span data-ttu-id="596f1-125">Można dodawać reguły tooan istniejące grupy NSG, edytować istniejące zasady i Usuń reguły.</span><span class="sxs-lookup"><span data-stu-id="596f1-125">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="596f1-126">Dodawanie reguły</span><span class="sxs-lookup"><span data-stu-id="596f1-126">Add a rule</span></span>
<span data-ttu-id="596f1-127">tooadd, dzięki czemu reguły **przychodzących** tooport ruchu **443** z dowolnej maszyny toohello **frontonu NSG** NSG, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="596f1-127">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access tooport 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="596f1-128">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="596f1-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up hello network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="596f1-129">Zmień reguły</span><span class="sxs-lookup"><span data-stu-id="596f1-129">Change a rule</span></span>
<span data-ttu-id="596f1-130">Reguła hello toochange utworzone powyżej tooallow ruchu przychodzącego ruchu z hello **Internet** tylko, uruchom hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="596f1-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="596f1-131">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="596f1-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up hello network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="596f1-132">Usuwanie reguły</span><span class="sxs-lookup"><span data-stu-id="596f1-132">Delete a rule</span></span>
<span data-ttu-id="596f1-133">utworzona reguła hello toodelete powyżej, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="596f1-133">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="596f1-134">Witaj `--quiet` parametru zapewnia nie ma potrzeby usuwania hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="596f1-134">hello `--quiet` parameter ensures you don't need tooconfirm hello deletion.</span></span>
>

<span data-ttu-id="596f1-135">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="596f1-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up hello network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="596f1-136">Zarządzanie skojarzenia</span><span class="sxs-lookup"><span data-stu-id="596f1-136">Manage associations</span></span>
<span data-ttu-id="596f1-137">Możesz skojarzyć toosubnets NSG i kart interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="596f1-137">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="596f1-138">Można również usunąć skojarzenie grupy NSG z dowolnego zasobu, który jest ona skojarzona.</span><span class="sxs-lookup"><span data-stu-id="596f1-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="596f1-139">Kojarzenie grupy NSG tooa karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="596f1-139">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="596f1-140">Witaj tooassociate **frontonu NSG** NSG toohello **TestNICWeb1** karty Sieciowej, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="596f1-140">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="596f1-141">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="596f1-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Looking up hello network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
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

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="596f1-142">Usuń skojarzenie grupy NSG z karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="596f1-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="596f1-143">Witaj toodissociate **frontonu NSG** grupy NSG z hello **TestNICWeb1** karty Sieciowej, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="596f1-143">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="596f1-144">Witaj powiadomienia "" (pusta) wartość hello `network-security-group-id` parametru.</span><span class="sxs-lookup"><span data-stu-id="596f1-144">Notice hello "" (empty) value for hello `network-security-group-id` parameter.</span></span> <span data-ttu-id="596f1-145">To, jak usunąć tooan skojarzenie grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="596f1-145">That is how you remove an association tooan NSG.</span></span> <span data-ttu-id="596f1-146">Nie można wykonać hello same z hello `network-security-group-name` parametru.</span><span class="sxs-lookup"><span data-stu-id="596f1-146">You can't do hello same with hello `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="596f1-147">Oczekiwany wynik:</span><span class="sxs-lookup"><span data-stu-id="596f1-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
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

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="596f1-148">Usuń skojarzenie grupy NSG z podsiecią</span><span class="sxs-lookup"><span data-stu-id="596f1-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="596f1-149">Witaj toodissociate **frontonu NSG** grupy NSG z hello **frontonu** podsieci, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="596f1-149">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="596f1-150">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="596f1-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up hello subnet "FrontEnd"
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

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="596f1-151">Kojarzenie grupy NSG podsieci tooa</span><span class="sxs-lookup"><span data-stu-id="596f1-151">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="596f1-152">Witaj tooassociate **frontonu NSG** NSG toohello **FronEnd** podsieci ponownie, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="596f1-152">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="596f1-153">Witaj polecenie powyżej działa tylko wtedy, ponieważ hello **frontonu NSG** grupa NSG jest hello tej samej grupie zasobów co sieć wirtualna hello **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="596f1-153">hello command above only works because hello **NSG-FrontEnd** NSG is in hello same resource group as hello virtual network **TestVNet**.</span></span> <span data-ttu-id="596f1-154">Jeśli hello NSG znajduje się w innej grupie zasobów, należy toouse hello `--network-security-group-id` parametru zamiast tego i podać hello pełny identyfikator hello NSG.</span><span class="sxs-lookup"><span data-stu-id="596f1-154">If hello NSG is in a different resource group, you need toouse hello `--network-security-group-id` parameter instead, and provide hello full id for hello NSG.</span></span> <span data-ttu-id="596f1-155">Można pobrać identyfikatora hello uruchamiając `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` i wyszukując hello **identyfikator** właściwości.</span><span class="sxs-lookup"><span data-stu-id="596f1-155">You can retrieve hello id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for hello **id** property.</span></span> 
> 

<span data-ttu-id="596f1-156">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="596f1-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up hello subnet "FrontEnd"
        + Looking up hello network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up hello subnet "FrontEnd"
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

## <a name="delete-an-nsg"></a><span data-ttu-id="596f1-157">Usuwanie grupy NSG</span><span class="sxs-lookup"><span data-stu-id="596f1-157">Delete an NSG</span></span>
<span data-ttu-id="596f1-158">Grupy NSG można usuwać tylko, jeśli nie został skojarzony tooany zasobów.</span><span class="sxs-lookup"><span data-stu-id="596f1-158">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="596f1-159">toodelete grupy NSG, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="596f1-159">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="596f1-160">zasoby hello toocheck skojarzony tooan NSG, uruchom hello `azure network nsg show` pokazane [skojarzenia grup NSG widoku](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="596f1-160">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="596f1-161">Jeśli hello grupa NSG jest skojarzona tooany kart sieciowych, uruchom hello `azure network nic set` pokazane [skojarzenie grupy NSG z karty Sieciowej](#Dissociate-an-NSG-from-a-NIC) dla poszczególnych kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="596f1-161">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="596f1-162">Jeśli hello NSG jest skojarzona tooany podsieci, uruchom hello `azure network vnet subnet set` pokazane [skojarzenie grupy NSG z podsiecią](#Dissociate-an-NSG-from-a-subnet) dla każdej podsieci.</span><span class="sxs-lookup"><span data-stu-id="596f1-162">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="596f1-163">Uruchom następujące polecenie hello hello toodelete NSG:</span><span class="sxs-lookup"><span data-stu-id="596f1-163">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="596f1-164">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="596f1-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up hello network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="596f1-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="596f1-165">Next steps</span></span>
* <span data-ttu-id="596f1-166">[Włącz rejestrowanie](virtual-network-nsg-manage-log.md) dla grup NSG.</span><span class="sxs-lookup"><span data-stu-id="596f1-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

