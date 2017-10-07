---
title: "aaaManage sieciowej grupy zabezpieczeń - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage sieciowych grup zabezpieczeń za pomocą hello Azure interfejsu wiersza polecenia (CLI) 2.0."
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
ms.openlocfilehash: a3036b465e1e4049cba00e5e13ce1b479a2301d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="8c467-103">Zarządzanie grupami zabezpieczeń sieci przy użyciu hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8c467-103">Manage network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="8c467-104">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="8c467-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="8c467-105">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="8c467-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="8c467-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modelami wdrażania</span><span class="sxs-lookup"><span data-stu-id="8c467-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="8c467-107">[Azure CLI 2.0](#View-existing-NSGs) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania hello zasobów (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="8c467-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for hello resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="8c467-108">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8c467-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8c467-109">W tym artykule omówiono przy użyciu modelu wdrażania usługi Resource Manager hello, które firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="8c467-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="8c467-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8c467-110">Prerequisite</span></span>
<span data-ttu-id="8c467-111">Jeśli nie zostało jeszcze, instalowania i konfigurowania hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8c467-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="8c467-112">Wyświetlanie istniejących grup NSG</span><span class="sxs-lookup"><span data-stu-id="8c467-112">View existing NSGs</span></span>
<span data-ttu-id="8c467-113">tooview hello lista grup NSG w określonej grupy zasobów, uruchom hello [lista nsg sieci az](/cli/azure/network/nsg#list) z `-o table` format wyjściowy:</span><span class="sxs-lookup"><span data-stu-id="8c467-113">tooview hello list of NSGs in a specific resource group, run hello [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="8c467-114">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="8c467-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="8c467-115">Wyświetl listę wszystkich reguł dla grupy NSG</span><span class="sxs-lookup"><span data-stu-id="8c467-115">List all rules for an NSG</span></span>
<span data-ttu-id="8c467-116">tooview hello reguły NSG o nazwie **frontonu NSG**Uruchom hello [Pokaż nsg sieci az](/cli/azure/network/nsg#show) polecenie, używając [Filtr kwerendy JMESPATH](/cli/azure/query-az-cli2) i hello `-o table` format wyjściowy:</span><span class="sxs-lookup"><span data-stu-id="8c467-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and hello `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="8c467-117">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="8c467-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs tooall VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs tooInternet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="8c467-118">Można również użyć [listy reguł nsg sieci az](/cli/azure/network/nsg/rule#list) toolist tylko hello niestandardowych zasad z grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="8c467-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) toolist only hello custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="8c467-119">Wyświetlanie NSG powiązań</span><span class="sxs-lookup"><span data-stu-id="8c467-119">View NSG associations</span></span>

<span data-ttu-id="8c467-120">tooview hello jakie zasoby **frontonu NSG** grupa NSG jest hello Skojarz z, uruchom `az network nsg show` polecenia, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="8c467-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="8c467-121">Wyszukaj hello **Networkinterface** i **podsieci** właściwości, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="8c467-121">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

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

<span data-ttu-id="8c467-122">W powyższym przykładzie hello, hello NSG nie jest skojarzony tooany interfejsów sieciowych (NIC) i jest tooa skojarzonych podsieci o nazwie **frontonu**.</span><span class="sxs-lookup"><span data-stu-id="8c467-122">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="8c467-123">Dodawanie reguły</span><span class="sxs-lookup"><span data-stu-id="8c467-123">Add a rule</span></span>
<span data-ttu-id="8c467-124">tooadd, dzięki czemu reguły **przychodzących** tooport ruchu **443** z dowolnej maszyny toohello **frontonu NSG** NSG, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="8c467-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access tooport 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="8c467-125">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="8c467-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access tooport 443 for HTTPS",
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

## <a name="change-a-rule"></a><span data-ttu-id="8c467-126">Zmień reguły</span><span class="sxs-lookup"><span data-stu-id="8c467-126">Change a rule</span></span>
<span data-ttu-id="8c467-127">Reguła hello toochange utworzone powyżej tooallow ruchu przychodzącego ruchu z hello **Internet** , uruchom hello [aktualizacja reguły nsg sieci az](/cli/azure/network/nsg/rule#update) polecenia:</span><span class="sxs-lookup"><span data-stu-id="8c467-127">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="8c467-128">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="8c467-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access tooport 443 for HTTPS",
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

## <a name="delete-a-rule"></a><span data-ttu-id="8c467-129">Usuwanie reguły</span><span class="sxs-lookup"><span data-stu-id="8c467-129">Delete a rule</span></span>
<span data-ttu-id="8c467-130">utworzona reguła hello toodelete powyżej, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="8c467-130">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="8c467-131">Kojarzenie grupy NSG tooa karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="8c467-131">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="8c467-132">Witaj tooassociate **frontonu NSG** NSG toohello **TestNICWeb1** karty Sieciowej, użyj hello [aktualizacji kart sieciowych az](/cli/azure/network/nic#update) polecenia:</span><span class="sxs-lookup"><span data-stu-id="8c467-132">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, use hello [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="8c467-133">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="8c467-133">Expected output:</span></span>

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

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="8c467-134">Usuń skojarzenie grupy NSG z karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="8c467-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="8c467-135">toodissociate hello **frontonu NSG** grupy NSG z hello **TestNICWeb1** karty Sieciowej, uruchom hello [aktualizacja reguły nsg sieci az](/cli/azure/network/nsg/rule#update) polecenia ponownie zostać zastąpiony hello `--network-security-group` argument za pomocą ciągu pustego (`""`).</span><span class="sxs-lookup"><span data-stu-id="8c467-135">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="8c467-136">W danych wyjściowych hello hello `networkSecurityGroup` ustawiono toonull klucza.</span><span class="sxs-lookup"><span data-stu-id="8c467-136">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="8c467-137">Usuń skojarzenie grupy NSG z podsiecią</span><span class="sxs-lookup"><span data-stu-id="8c467-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="8c467-138">toodissociate hello **frontonu NSG** grupy NSG z hello **frontonu** podsieci, ponownie uruchom hello [aktualizacja reguły nsg sieci az](/cli/azure/network/nsg/rule#update) polecenia ponownie zostać zastąpiony hello `--network-security-group` argument za pomocą ciągu pustego (`""`).</span><span class="sxs-lookup"><span data-stu-id="8c467-138">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, again run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="8c467-139">W danych wyjściowych hello hello `networkSecurityGroup` ustawiono toonull klucza.</span><span class="sxs-lookup"><span data-stu-id="8c467-139">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="8c467-140">Kojarzenie grupy NSG podsieci tooa</span><span class="sxs-lookup"><span data-stu-id="8c467-140">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="8c467-141">Witaj tooassociate **frontonu NSG** NSG toohello **frontonu** podsieci ponownie, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="8c467-141">tooassociate hello **NSG-FrontEnd** NSG toohello **FrontEnd** subnet again, run hello following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="8c467-142">W danych wyjściowych hello hello `networkSecurityGroup` klucz ma podobny dla wartości hello:</span><span class="sxs-lookup"><span data-stu-id="8c467-142">In hello output, hello `networkSecurityGroup` key has something similar for hello value:</span></span>

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

## <a name="delete-an-nsg"></a><span data-ttu-id="8c467-143">Usuwanie grupy NSG</span><span class="sxs-lookup"><span data-stu-id="8c467-143">Delete an NSG</span></span>
<span data-ttu-id="8c467-144">Grupy NSG można usuwać tylko, jeśli nie został skojarzony tooany zasobów.</span><span class="sxs-lookup"><span data-stu-id="8c467-144">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="8c467-145">toodelete grupy NSG, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="8c467-145">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="8c467-146">zasoby hello toocheck skojarzony tooan NSG, uruchom hello `azure network nsg show` pokazane [skojarzenia grup NSG widoku](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="8c467-146">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="8c467-147">Jeśli hello grupa NSG jest skojarzona tooany kart sieciowych, uruchom hello `azure network nic set` pokazane [skojarzenie grupy NSG z karty Sieciowej](#Dissociate-an-NSG-from-a-NIC) dla poszczególnych kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="8c467-147">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="8c467-148">Jeśli hello NSG jest skojarzona tooany podsieci, uruchom hello `azure network vnet subnet set` pokazane [skojarzenie grupy NSG z podsiecią](#Dissociate-an-NSG-from-a-subnet) dla każdej podsieci.</span><span class="sxs-lookup"><span data-stu-id="8c467-148">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="8c467-149">Uruchom następujące polecenie hello hello toodelete NSG:</span><span class="sxs-lookup"><span data-stu-id="8c467-149">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="8c467-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8c467-150">Next steps</span></span>
* <span data-ttu-id="8c467-151">[Włącz rejestrowanie](virtual-network-nsg-manage-log.md) dla grup NSG.</span><span class="sxs-lookup"><span data-stu-id="8c467-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

