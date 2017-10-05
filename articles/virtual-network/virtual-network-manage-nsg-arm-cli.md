---
title: "Zarządzanie grupami zabezpieczeń sieci - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać przy użyciu interfejsu wiersza polecenia platformy Azure (CLI) 2.0 grup zabezpieczeń sieci."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed17d314-07e6-4c7f-bcf1-a8a2535d7c14
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 11ec0d3d9e33c06d4c0a164f7fba5dd5cca73872
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-cli-20"></a><span data-ttu-id="04ed5-103">Zarządzanie grupami zabezpieczeń sieci przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="04ed5-103">Manage network security groups using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="04ed5-104">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="04ed5-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="04ed5-105">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="04ed5-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="04ed5-106">[Interfejs wiersza polecenia platformy Azure w wersji 1.0](virtual-network-manage-nsg-cli-nodejs.md) — nasz interfejs wiersza polecenia dla klasycznego modelu wdrażania i modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="04ed5-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="04ed5-107">[Azure CLI 2.0](#View-existing-NSGs) -naszej nowej generacji interfejsu wiersza polecenia do zarządzania model wdrażania zasobów (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="04ed5-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for the resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="04ed5-108">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="04ed5-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="04ed5-109">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów, które firma Microsoft zaleca w przypadku większości nowych wdrożeń zamiast klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="04ed5-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="04ed5-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="04ed5-110">Prerequisite</span></span>
<span data-ttu-id="04ed5-111">Jeśli nie zostało jeszcze, instalowania i konfigurowania najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się do platformy Azure konta przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="04ed5-111">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="04ed5-112">Wyświetlanie istniejących grup NSG</span><span class="sxs-lookup"><span data-stu-id="04ed5-112">View existing NSGs</span></span>
<span data-ttu-id="04ed5-113">Aby wyświetlić listę grup NSG w określonej grupy zasobów, uruchom [lista nsg sieci az](/cli/azure/network/nsg#list) z `-o table` format wyjściowy:</span><span class="sxs-lookup"><span data-stu-id="04ed5-113">To view the list of NSGs in a specific resource group, run the [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="04ed5-114">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="04ed5-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="04ed5-115">Wyświetl listę wszystkich reguł dla grupy NSG</span><span class="sxs-lookup"><span data-stu-id="04ed5-115">List all rules for an NSG</span></span>
<span data-ttu-id="04ed5-116">Aby wyświetlić reguły NSG o nazwie **frontonu NSG**Uruchom [Pokaż nsg sieci az](/cli/azure/network/nsg#show) polecenie, używając [Filtr kwerendy JMESPATH](/cli/azure/query-az-cli2) i `-o table` format wyjściowy:</span><span class="sxs-lookup"><span data-stu-id="04ed5-116">To view the rules of an NSG named **NSG-FrontEnd**, run the [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and the `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="04ed5-117">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="04ed5-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs to all VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs to Internet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="04ed5-118">Można również użyć [listy reguł nsg sieci az](/cli/azure/network/nsg/rule#list) Aby wyświetlić listę reguł niestandardowych z grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="04ed5-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) to list only the custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="04ed5-119">Wyświetlanie NSG powiązań</span><span class="sxs-lookup"><span data-stu-id="04ed5-119">View NSG associations</span></span>

<span data-ttu-id="04ed5-120">Aby wyświetlić zasobów **NSG frontonu** grupa NSG jest skojarzony z uruchomiony `az network nsg show` polecenia w sposób przedstawiony poniżej.</span><span class="sxs-lookup"><span data-stu-id="04ed5-120">To view what resources the **NSG-FrontEnd** NSG is associate with, run the `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="04ed5-121">Wyszukaj **Networkinterface** i **podsieci** właściwości, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="04ed5-121">Look for the **networkInterfaces** and **subnets** properties as shown below:</span></span>

```json
[
  [
    {
      "addressPrefix": null,
      "etag": null,
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
      "ipConfigurations": null,
      "name": null,
      "networkSecurityGroup": null,
      "provisioningState": null,
      "resourceGroup": "RG-NSG",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  null
]
```

<span data-ttu-id="04ed5-122">W powyższym przykładzie grupy NSG nie jest skojarzony z żadnych interfejsów sieciowych (NIC) i jest on skojarzony z podsiecią o nazwie **frontonu**.</span><span class="sxs-lookup"><span data-stu-id="04ed5-122">In the example above, the NSG is not associated to any network interfaces (NICs), and it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="04ed5-123">Dodawanie reguły</span><span class="sxs-lookup"><span data-stu-id="04ed5-123">Add a rule</span></span>
<span data-ttu-id="04ed5-124">Można dodać, dzięki czemu reguły **przychodzących** ruch do portu **443** z dowolnej maszyny do **frontonu NSG** NSG, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="04ed5-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, enter the following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access to port 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="04ed5-125">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="04ed5-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access to port 443 for HTTPS",
  "destinationAddressPrefix": "*",
  "destinationPortRange": "443",
  "direction": "Inbound",
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
  "name": "allow-https",
  "priority": 102,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

## <a name="change-a-rule"></a><span data-ttu-id="04ed5-126">Zmień reguły</span><span class="sxs-lookup"><span data-stu-id="04ed5-126">Change a rule</span></span>
<span data-ttu-id="04ed5-127">Aby zmienić reguły utworzone powyżej, aby zezwalać na ruch przychodzący z **Internet** , uruchom [aktualizacja reguły nsg sieci az](/cli/azure/network/nsg/rule#update) polecenia:</span><span class="sxs-lookup"><span data-stu-id="04ed5-127">To change the rule created above to allow inbound traffic from the **Internet** only, run the [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="04ed5-128">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="04ed5-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access to port 443 for HTTPS",
"destinationAddressPrefix": "*",
"destinationPortRange": "443",
"direction": "Inbound",
"etag": "W/\"<guid>\"",
"id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
"name": "allow-https",
"priority": 102,
"protocol": "Tcp",
"provisioningState": "Succeeded",
"resourceGroup": "RG-NSG",
"sourceAddressPrefix": "Internet",
"sourcePortRange": "*"
}
```

## <a name="delete-a-rule"></a><span data-ttu-id="04ed5-129">Usuwanie reguły</span><span class="sxs-lookup"><span data-stu-id="04ed5-129">Delete a rule</span></span>
<span data-ttu-id="04ed5-130">Aby usunąć regułę utworzone powyżej, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="04ed5-130">To delete the rule created above, run the following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="04ed5-131">Kojarzenie grupy NSG z kartą sieciową</span><span class="sxs-lookup"><span data-stu-id="04ed5-131">Associate an NSG to a NIC</span></span>
<span data-ttu-id="04ed5-132">Aby skojarzyć **frontonu NSG** grupy NSG **TestNICWeb1** karty Sieciowej, użyj [aktualizacji kart sieciowych az](/cli/azure/network/nic#update) polecenia:</span><span class="sxs-lookup"><span data-stu-id="04ed5-132">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, use the [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="04ed5-133">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="04ed5-133">Expected output:</span></span>

```json
{
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": [],
    "internalDnsNameLabel": null,
    "internalDomainNameSuffix": "k0wkaguidnqrh0ud.gx.internal.cloudapp.net",
    "internalFqdn": null
  },
  "enableAcceleratedNetworking": false,
  "enableIpForwarding": false,
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1",
  "ipConfigurations": [
    {
      "applicationGatewayBackendAddressPools": null,
      "etag": "W/\"<guid>\"",
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1",
      "loadBalancerBackendAddressPools": null,
      "loadBalancerInboundNatRules": null,
      "name": "ipconfig1",
      "primary": true,
      "privateIpAddress": "192.168.1.6",
      "privateIpAddressVersion": "IPv4",
      "privateIpAllocationMethod": "Static",
      "provisioningState": "Succeeded",
      "publicIpAddress": null,
      "resourceGroup": "RG-NSG",
      "subnet": {
        "addressPrefix": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
        "ipConfigurations": null,
        "name": null,
        "networkSecurityGroup": null,
        "provisioningState": null,
        "resourceGroup": "RG-NSG",
        "resourceNavigationLinks": null,
        "routeTable": null
      }
    }
  ],
  "location": "centralus",
  "macAddress": "00-0D-3A-91-A9-60",
  "name": "TestNICWeb1",
  "networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  },
  "primary": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "resourceGuid": "<guid>",
  "tags": {},
  "type": "Microsoft.Network/networkInterfaces",
  "virtualMachine": null
}
```

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="04ed5-134">Usuń skojarzenie grupy NSG z karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="04ed5-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="04ed5-135">Można usunąć skojarzenia **frontonu NSG** grupy NSG z **TestNICWeb1** karty Sieciowej, uruchom [aktualizacja reguły nsg sieci az](/cli/azure/network/nsg/rule#update) polecenia ponownie zostać zastąpiony `--network-security-group` argumentu z pusty ciąg (`""`).</span><span class="sxs-lookup"><span data-stu-id="04ed5-135">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, run the [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace the `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="04ed5-136">W danych wyjściowych `networkSecurityGroup` jest ustawiona na wartość null.</span><span class="sxs-lookup"><span data-stu-id="04ed5-136">In the output, the `networkSecurityGroup` key is set to null.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="04ed5-137">Usuń skojarzenie grupy NSG z podsiecią</span><span class="sxs-lookup"><span data-stu-id="04ed5-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="04ed5-138">Można usunąć skojarzenia **frontonu NSG** grupy NSG z **frontonu** podsieci, ponownie uruchom [aktualizacja reguły nsg sieci az](/cli/azure/network/nsg/rule#update) polecenia ponownie zostać zastąpiony `--network-security-group` argumentu za pomocą ciągu pustego (`""`).</span><span class="sxs-lookup"><span data-stu-id="04ed5-138">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, again run the [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace the `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="04ed5-139">W danych wyjściowych `networkSecurityGroup` jest ustawiona na wartość null.</span><span class="sxs-lookup"><span data-stu-id="04ed5-139">In the output, the `networkSecurityGroup` key is set to null.</span></span>

## <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="04ed5-140">Kojarzenie grupy NSG z podsiecią</span><span class="sxs-lookup"><span data-stu-id="04ed5-140">Associate an NSG to a subnet</span></span>
<span data-ttu-id="04ed5-141">Aby skojarzyć **frontonu NSG** grupy NSG **frontonu** podsieci ponownie, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="04ed5-141">To associate the **NSG-FrontEnd** NSG to the **FrontEnd** subnet again, run the following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="04ed5-142">W danych wyjściowych `networkSecurityGroup` klucz ma podobny dla wartości:</span><span class="sxs-lookup"><span data-stu-id="04ed5-142">In the output, the `networkSecurityGroup` key has something similar for the value:</span></span>

```json
"networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  }
  ```

## <a name="delete-an-nsg"></a><span data-ttu-id="04ed5-143">Usuwanie grupy NSG</span><span class="sxs-lookup"><span data-stu-id="04ed5-143">Delete an NSG</span></span>
<span data-ttu-id="04ed5-144">Grupy NSG można usuwać tylko, jeśli nie został skojarzony z żadnym zasobem.</span><span class="sxs-lookup"><span data-stu-id="04ed5-144">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="04ed5-145">Aby usunąć grupy NSG, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="04ed5-145">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="04ed5-146">Aby sprawdzić zasoby skojarzone grupy NSG, uruchom `azure network nsg show` pokazane [skojarzenia grup NSG widoku](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="04ed5-146">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="04ed5-147">Jeśli grupa NSG jest skojarzona z dowolnej karty interfejsu sieciowego, uruchom `azure network nic set` pokazane [skojarzenie grupy NSG z karty Sieciowej](#Dissociate-an-NSG-from-a-NIC) dla poszczególnych kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="04ed5-147">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="04ed5-148">Jeśli grupa NSG jest skojarzona z dowolnej podsieci, uruchom `azure network vnet subnet set` pokazane [skojarzenie grupy NSG z podsiecią](#Dissociate-an-NSG-from-a-subnet) dla każdej podsieci.</span><span class="sxs-lookup"><span data-stu-id="04ed5-148">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="04ed5-149">Aby usunąć grupy NSG, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="04ed5-149">To delete the NSG, run the following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="04ed5-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04ed5-150">Next steps</span></span>
* <span data-ttu-id="04ed5-151">[Włącz rejestrowanie](virtual-network-nsg-manage-log.md) dla grup NSG.</span><span class="sxs-lookup"><span data-stu-id="04ed5-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

