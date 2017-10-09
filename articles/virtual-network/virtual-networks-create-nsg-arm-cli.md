---
title: "aaaCreate sieciowej grupy zabezpieczeń - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i wdrażanie grup zabezpieczeń sieci przy użyciu hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="b8f38-103">Tworzenie sieci za pomocą hello Azure CLI 2.0 grup zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="b8f38-103">Create network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b8f38-104">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="b8f38-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="b8f38-105">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="b8f38-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="b8f38-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modelami wdrażania</span><span class="sxs-lookup"><span data-stu-id="b8f38-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="b8f38-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania hello zasobów (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="b8f38-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="b8f38-108">środowisku niezłożonym już utworzone na podstawie w poprzednim scenariuszu hello spodziewać się następujące polecenia przykładowe Hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="b8f38-108">hello sample Azure CLI 2.0 commands following expect a simple environment already created based on hello scenario preceding.</span></span> 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a><span data-ttu-id="b8f38-109">Utwórz hello NSG dla hello `FrontEnd` podsieci</span><span class="sxs-lookup"><span data-stu-id="b8f38-109">Create hello NSG for hello `FrontEnd` subnet</span></span>

<span data-ttu-id="b8f38-110">grupy NSG o nazwie toocreate *frontonu NSG* oparte na poprzednim scenariuszu hello, wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="b8f38-110">toocreate an NSG named *NSG-FrontEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="b8f38-111">Jeśli nie zostało jeszcze, instalowania i konfigurowania hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b8f38-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="b8f38-112">Tworzenie grupy NSG przy użyciu hello [utworzyć nsg sieci az](/cli/azure/network/nsg#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="b8f38-112">Create an NSG using hello [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="b8f38-113">Parametry:</span><span class="sxs-lookup"><span data-stu-id="b8f38-113">Parameters:</span></span>
   
   * <span data-ttu-id="b8f38-114">`--resource-group`: Nazwa grupy zasobów hello gdzie hello grupa NSG jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="b8f38-114">`--resource-group`: Name of hello resource group where hello NSG is created.</span></span> <span data-ttu-id="b8f38-115">W naszym scenariuszu jest to *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="b8f38-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="b8f38-116">`--location`: Region platformy azure, w którym hello Nowa grupa NSG jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="b8f38-116">`--location`: Azure region where hello new NSG is created.</span></span> <span data-ttu-id="b8f38-117">W naszym scenariuszu *westus*.</span><span class="sxs-lookup"><span data-stu-id="b8f38-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="b8f38-118">`--name`: Nazwa hello Nowa grupa NSG.</span><span class="sxs-lookup"><span data-stu-id="b8f38-118">`--name`: Name for hello new NSG.</span></span> <span data-ttu-id="b8f38-119">W naszym scenariuszu *frontonu NSG*.</span><span class="sxs-lookup"><span data-stu-id="b8f38-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="b8f38-120">Witaj oczekiwanych danych wyjściowych jest dość nieco informacji, łącznie z listą wszystkich reguł domyślnych hello.</span><span class="sxs-lookup"><span data-stu-id="b8f38-120">hello expected output is quite a bit of information including a list of all hello default rules.</span></span> <span data-ttu-id="b8f38-121">Witaj poniższy przykład przedstawia hello domyślnych reguł przy użyciu filtru kwerendy JMESPATH z hello `table` format wyjściowy:</span><span class="sxs-lookup"><span data-stu-id="b8f38-121">hello following example shows hello default rules using a JMESPATH query filter with hello `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="b8f38-122">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="b8f38-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="b8f38-123">Utworzyć regułę, która umożliwia dostęp tooport 3389 (RDP) z hello Internet z hello [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="b8f38-123">Create a rule that allows access tooport 3389 (RDP) from hello Internet with hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b8f38-124">W zależności od powłoki hello używasz, może być konieczne toomodify hello `*` znak w argumentach powitania po nie tooexpand hello argument przed realizacją.</span><span class="sxs-lookup"><span data-stu-id="b8f38-124">Depending on hello shell you are using, you might need toomodify hello `*` character in hello arguments following so as not tooexpand hello argument before execution.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    <span data-ttu-id="b8f38-125">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="b8f38-125">Expected output:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    <span data-ttu-id="b8f38-126">Parametry:</span><span class="sxs-lookup"><span data-stu-id="b8f38-126">Parameters:</span></span>

    * <span data-ttu-id="b8f38-127">`--resource-group testrg`: hello toouse grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b8f38-127">`--resource-group testrg`: hello resource group toouse.</span></span> <span data-ttu-id="b8f38-128">Należy pamiętać, że bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="b8f38-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="b8f38-129">`--nsg-name NSG-FrontEnd`: Nazwa grupy NSG hello, w których hello jest tworzona reguła.</span><span class="sxs-lookup"><span data-stu-id="b8f38-129">`--nsg-name NSG-FrontEnd`: Name of hello NSG in which hello rule is created.</span></span>
    * <span data-ttu-id="b8f38-130">`--name rdp-rule`: Nazwa hello nowej reguły.</span><span class="sxs-lookup"><span data-stu-id="b8f38-130">`--name rdp-rule`: Name for hello new rule.</span></span>
    * <span data-ttu-id="b8f38-131">`--access Allow`: Poziom dostępu hello reguły (Deny lub Zezwalaj).</span><span class="sxs-lookup"><span data-stu-id="b8f38-131">`--access Allow`: Access level for hello rule (Deny or Allow).</span></span>
    * <span data-ttu-id="b8f38-132">`--protocol Tcp`: Protocol (Tcp, Udp lub *).</span><span class="sxs-lookup"><span data-stu-id="b8f38-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="b8f38-133">`--direction Inbound`: Kierunek hello połączenia (przychodzący lub wychodzący).</span><span class="sxs-lookup"><span data-stu-id="b8f38-133">`--direction Inbound`: Direction of hello connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="b8f38-134">`--priority 100`: Priorytet reguły hello.</span><span class="sxs-lookup"><span data-stu-id="b8f38-134">`--priority 100`: Priority for hello rule.</span></span>
    * <span data-ttu-id="b8f38-135">`--source-address-prefix Internet`: Prefiks adresu źródłowego CIDR lub przy użyciu znaczników domyślnych.</span><span class="sxs-lookup"><span data-stu-id="b8f38-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="b8f38-136">`--source-port-range "*"`: Źródła port lub zakres portów.</span><span class="sxs-lookup"><span data-stu-id="b8f38-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="b8f38-137">Port, który otworzyć hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="b8f38-137">Port that opened hello connection.</span></span>
    * <span data-ttu-id="b8f38-138">`--destination-address-prefix "*"`: Prefiks adresu docelowego CIDR lub przy użyciu znaczników domyślnych.</span><span class="sxs-lookup"><span data-stu-id="b8f38-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="b8f38-139">`--destination-port-range 3389`: Miejsce docelowe port lub zakres portów.</span><span class="sxs-lookup"><span data-stu-id="b8f38-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="b8f38-140">Port, który odbiera żądanie połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="b8f38-140">Port that receives hello connection request.</span></span>



4. <span data-ttu-id="b8f38-141">Utworzyć regułę, która umożliwia dostęp tooport 80 (HTTP) z hello Internet **Tworzenie reguły nsg sieci az** polecenia.</span><span class="sxs-lookup"><span data-stu-id="b8f38-141">Create a rule that allows access tooport 80 (HTTP) from hello Internet **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    <span data-ttu-id="b8f38-142">Oczekiwano putput:</span><span class="sxs-lookup"><span data-stu-id="b8f38-142">Expected putput:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. <span data-ttu-id="b8f38-143">Powiąż hello NSG toohello **frontonu** podsieć o hello [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update) polecenia.</span><span class="sxs-lookup"><span data-stu-id="b8f38-143">Bind hello NSG toohello **FrontEnd** subnet with hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="b8f38-144">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="b8f38-144">Expected output:</span></span>
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-hello-nsg-for-hello-backend-subnet"></a><span data-ttu-id="b8f38-145">Utwórz hello NSG dla hello `BackEnd` podsieci</span><span class="sxs-lookup"><span data-stu-id="b8f38-145">Create hello NSG for hello `BackEnd` subnet</span></span>
<span data-ttu-id="b8f38-146">grupy NSG o nazwie toocreate *wewnętrznej bazy danych grupy NSG* oparte na poprzednim scenariuszu hello, wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="b8f38-146">toocreate an NSG named *NSG-BackEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="b8f38-147">Utwórz hello `NSG-BackEnd` grupy NSG z **utworzyć nsg sieci az**.</span><span class="sxs-lookup"><span data-stu-id="b8f38-147">Create hello `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="b8f38-148">W kroku 2, poprzedni hello oczekuje się, że dane wyjściowe są bardzo duże, w tym reguły domyślne.</span><span class="sxs-lookup"><span data-stu-id="b8f38-148">As in step 2, preceding, hello expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="b8f38-149">Utworzyć regułę, która umożliwia dostęp tooport 1433 (SQL) z hello `FrontEnd` podsieć o hello **Tworzenie reguły nsg sieci az** polecenia.</span><span class="sxs-lookup"><span data-stu-id="b8f38-149">Create a rule that allows access tooport 1433 (SQL) from hello `FrontEnd` subnet with hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    <span data-ttu-id="b8f38-150">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="b8f38-150">Expected output:</span></span>

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. <span data-ttu-id="b8f38-151">Utworzyć regułę, która nie zezwala na dostęp toohello Internetu za pomocą hello **Tworzenie reguły nsg sieci az** polecenia.</span><span class="sxs-lookup"><span data-stu-id="b8f38-151">Create a rule that denies access toohello Internet using hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    <span data-ttu-id="b8f38-152">Oczekiwano putput:</span><span class="sxs-lookup"><span data-stu-id="b8f38-152">Expected putput:</span></span>
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. <span data-ttu-id="b8f38-153">Powiąż hello NSG toohello `BackEnd` podsieci przy użyciu hello **zestaw podsieci sieci wirtualnej sieci az** polecenia.</span><span class="sxs-lookup"><span data-stu-id="b8f38-153">Bind hello NSG toohello `BackEnd` subnet using hello **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="b8f38-154">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="b8f38-154">Expected output:</span></span>
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
