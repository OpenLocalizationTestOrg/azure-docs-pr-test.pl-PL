---
title: "Utwórz grupy zabezpieczeń sieci - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć i wdrożyć przy użyciu programu Azure CLI 2.0 grup zabezpieczeń sieci."
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
ms.openlocfilehash: 8efb3ab66d07875b51f723fed5594bcb477ed025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-20"></a><span data-ttu-id="2c776-103">Tworzenie sieci za pomocą 2.0 interfejsu wiersza polecenia Azure grup zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="2c776-103">Create network security groups using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="2c776-104">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="2c776-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="2c776-105">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="2c776-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="2c776-106">[Interfejs wiersza polecenia platformy Azure w wersji 1.0](virtual-networks-create-nsg-cli-nodejs.md) — nasz interfejs wiersza polecenia dla klasycznego modelu wdrażania i modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="2c776-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="2c776-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -naszej nowej generacji interfejsu wiersza polecenia do zarządzania model wdrażania zasobów (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="2c776-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="2c776-108">Przykładowe polecenia 2.0 interfejsu wiersza polecenia platformy Azure po oczekiwać środowisku niezłożonym już utworzone na podstawie w poprzednim scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="2c776-108">The sample Azure CLI 2.0 commands following expect a simple environment already created based on the scenario preceding.</span></span> 

## <a name="create-the-nsg-for-the-frontend-subnet"></a><span data-ttu-id="2c776-109">Tworzenie grupy NSG dla `FrontEnd` podsieci</span><span class="sxs-lookup"><span data-stu-id="2c776-109">Create the NSG for the `FrontEnd` subnet</span></span>

<span data-ttu-id="2c776-110">Aby utworzyć grupy NSG o nazwie *frontonu NSG* oparte na poprzednim scenariuszu, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="2c776-110">To create an NSG named *NSG-FrontEnd* based on the scenario preceding, follow the steps following.</span></span>

1. <span data-ttu-id="2c776-111">Jeśli nie zostało jeszcze, instalowania i konfigurowania najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się do platformy Azure konta przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="2c776-111">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="2c776-112">Tworzenie grupy NSG przy użyciu [utworzyć nsg sieci az](/cli/azure/network/nsg#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="2c776-112">Create an NSG using the [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="2c776-113">Parametry:</span><span class="sxs-lookup"><span data-stu-id="2c776-113">Parameters:</span></span>
   
   * <span data-ttu-id="2c776-114">`--resource-group`: Nazwa grupy zasobów, w którym grupa NSG jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="2c776-114">`--resource-group`: Name of the resource group where the NSG is created.</span></span> <span data-ttu-id="2c776-115">W naszym scenariuszu jest to *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="2c776-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="2c776-116">`--location`: Region platformy azure, gdzie jest tworzona nowa grupa NSG.</span><span class="sxs-lookup"><span data-stu-id="2c776-116">`--location`: Azure region where the new NSG is created.</span></span> <span data-ttu-id="2c776-117">W naszym scenariuszu *westus*.</span><span class="sxs-lookup"><span data-stu-id="2c776-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="2c776-118">`--name`: Nazwa nowej grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="2c776-118">`--name`: Name for the new NSG.</span></span> <span data-ttu-id="2c776-119">W naszym scenariuszu *frontonu NSG*.</span><span class="sxs-lookup"><span data-stu-id="2c776-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="2c776-120">Oczekiwane dane wyjściowe jest dość informacji w tym listę domyślnych reguł.</span><span class="sxs-lookup"><span data-stu-id="2c776-120">The expected output is quite a bit of information including a list of all the default rules.</span></span> <span data-ttu-id="2c776-121">W poniższym przykładzie przedstawiono reguły domyślne przy użyciu JMESPATH filtr zapytania o `table` format wyjściowy:</span><span class="sxs-lookup"><span data-stu-id="2c776-121">The following example shows the default rules using a JMESPATH query filter with the `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="2c776-122">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="2c776-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs to all VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs to Internet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="2c776-123">Utworzyć regułę, która umożliwia uzyskanie dostępu do portu 3389 (RDP) z Internetu z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="2c776-123">Create a rule that allows access to port 3389 (RDP) from the Internet with the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2c776-124">W zależności od powłoki używasz, może być konieczne zmodyfikować `*` znak w argumentach po w celu rozwiń argument przed realizacją.</span><span class="sxs-lookup"><span data-stu-id="2c776-124">Depending on the shell you are using, you might need to modify the `*` character in the arguments following so as not to expand the argument before execution.</span></span>
   
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
   
    <span data-ttu-id="2c776-125">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="2c776-125">Expected output:</span></span>
   
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

    <span data-ttu-id="2c776-126">Parametry:</span><span class="sxs-lookup"><span data-stu-id="2c776-126">Parameters:</span></span>

    * <span data-ttu-id="2c776-127">`--resource-group testrg`: Grupy zasobów do użycia.</span><span class="sxs-lookup"><span data-stu-id="2c776-127">`--resource-group testrg`: The resource group to use.</span></span> <span data-ttu-id="2c776-128">Należy pamiętać, że bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="2c776-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="2c776-129">`--nsg-name NSG-FrontEnd`: Nazwa grupy NSG, w którym jest tworzona reguła.</span><span class="sxs-lookup"><span data-stu-id="2c776-129">`--nsg-name NSG-FrontEnd`: Name of the NSG in which the rule is created.</span></span>
    * <span data-ttu-id="2c776-130">`--name rdp-rule`: Nazwa nowej reguły.</span><span class="sxs-lookup"><span data-stu-id="2c776-130">`--name rdp-rule`: Name for the new rule.</span></span>
    * <span data-ttu-id="2c776-131">`--access Allow`: Poziom dostępu reguły (Deny lub Zezwalaj).</span><span class="sxs-lookup"><span data-stu-id="2c776-131">`--access Allow`: Access level for the rule (Deny or Allow).</span></span>
    * <span data-ttu-id="2c776-132">`--protocol Tcp`: Protocol (Tcp, Udp lub *).</span><span class="sxs-lookup"><span data-stu-id="2c776-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="2c776-133">`--direction Inbound`: Kierunek połączenia (przychodzący lub wychodzący).</span><span class="sxs-lookup"><span data-stu-id="2c776-133">`--direction Inbound`: Direction of the connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="2c776-134">`--priority 100`: Priorytet reguły.</span><span class="sxs-lookup"><span data-stu-id="2c776-134">`--priority 100`: Priority for the rule.</span></span>
    * <span data-ttu-id="2c776-135">`--source-address-prefix Internet`: Prefiks adresu źródłowego CIDR lub przy użyciu znaczników domyślnych.</span><span class="sxs-lookup"><span data-stu-id="2c776-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="2c776-136">`--source-port-range "*"`: Źródła port lub zakres portów.</span><span class="sxs-lookup"><span data-stu-id="2c776-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="2c776-137">Port, który otworzyć połączenia.</span><span class="sxs-lookup"><span data-stu-id="2c776-137">Port that opened the connection.</span></span>
    * <span data-ttu-id="2c776-138">`--destination-address-prefix "*"`: Prefiks adresu docelowego CIDR lub przy użyciu znaczników domyślnych.</span><span class="sxs-lookup"><span data-stu-id="2c776-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="2c776-139">`--destination-port-range 3389`: Miejsce docelowe port lub zakres portów.</span><span class="sxs-lookup"><span data-stu-id="2c776-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="2c776-140">Port, który odbiera żądanie połączenia.</span><span class="sxs-lookup"><span data-stu-id="2c776-140">Port that receives the connection request.</span></span>



4. <span data-ttu-id="2c776-141">Utworzyć regułę, która zezwala na dostęp do portu 80 (HTTP) z Internetu **Tworzenie reguły nsg sieci az** polecenia.</span><span class="sxs-lookup"><span data-stu-id="2c776-141">Create a rule that allows access to port 80 (HTTP) from the Internet **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="2c776-142">Oczekiwano putput:</span><span class="sxs-lookup"><span data-stu-id="2c776-142">Expected putput:</span></span>
   
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

5. <span data-ttu-id="2c776-143">Powiązanie grupy NSG z **frontonu** podsieć o [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update) polecenia.</span><span class="sxs-lookup"><span data-stu-id="2c776-143">Bind the NSG to the **FrontEnd** subnet with the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="2c776-144">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="2c776-144">Expected output:</span></span>
   
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

## <a name="create-the-nsg-for-the-backend-subnet"></a><span data-ttu-id="2c776-145">Tworzenie grupy NSG dla `BackEnd` podsieci</span><span class="sxs-lookup"><span data-stu-id="2c776-145">Create the NSG for the `BackEnd` subnet</span></span>
<span data-ttu-id="2c776-146">Aby utworzyć grupy NSG o nazwie *zaplecza NSG* oparte na poprzednim scenariuszu, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="2c776-146">To create an NSG named *NSG-BackEnd* based on the scenario preceding, follow the steps following.</span></span>

1. <span data-ttu-id="2c776-147">Utwórz `NSG-BackEnd` grupy NSG z **utworzyć nsg sieci az**.</span><span class="sxs-lookup"><span data-stu-id="2c776-147">Create the `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="2c776-148">W kroku 2, poprzedni oczekiwane dane wyjściowe jest dość duży, w tym reguły domyślne.</span><span class="sxs-lookup"><span data-stu-id="2c776-148">As in step 2, preceding, the expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="2c776-149">Utworzyć regułę, która umożliwia uzyskanie dostępu do portu 1433 (SQL) z `FrontEnd` podsieć o **Tworzenie reguły nsg sieci az** polecenia.</span><span class="sxs-lookup"><span data-stu-id="2c776-149">Create a rule that allows access to port 1433 (SQL) from the `FrontEnd` subnet with the **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="2c776-150">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="2c776-150">Expected output:</span></span>

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

3. <span data-ttu-id="2c776-151">Utworzyć regułę, która nie zezwala na dostęp do Internetu za pomocą **Tworzenie reguły nsg sieci az** polecenia.</span><span class="sxs-lookup"><span data-stu-id="2c776-151">Create a rule that denies access to the Internet using the **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="2c776-152">Oczekiwano putput:</span><span class="sxs-lookup"><span data-stu-id="2c776-152">Expected putput:</span></span>
   
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

4. <span data-ttu-id="2c776-153">Powiązanie grupy NSG z `BackEnd` podsieci przy użyciu **zestaw podsieci sieci wirtualnej sieci az** polecenia.</span><span class="sxs-lookup"><span data-stu-id="2c776-153">Bind the NSG to the `BackEnd` subnet using the **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="2c776-154">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="2c776-154">Expected output:</span></span>
   
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
