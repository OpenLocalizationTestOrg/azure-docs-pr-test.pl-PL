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
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a>Tworzenie sieci za pomocą hello Azure CLI 2.0 grup zabezpieczeń

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia 

Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia: 

- [Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modelami wdrażania 
- [Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania hello zasobów (w tym artykule)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

środowisku niezłożonym już utworzone na podstawie w poprzednim scenariuszu hello spodziewać się następujące polecenia przykładowe Hello Azure CLI 2.0. 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a>Utwórz hello NSG dla hello `FrontEnd` podsieci

grupy NSG o nazwie toocreate *frontonu NSG* oparte na poprzednim scenariuszu hello, wykonaj następujące kroki hello.

1. Jeśli nie zostało jeszcze, instalowania i konfigurowania hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login). 

2. Tworzenie grupy NSG przy użyciu hello [utworzyć nsg sieci az](/cli/azure/network/nsg#create) polecenia. 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    Parametry:
   
   * `--resource-group`: Nazwa grupy zasobów hello gdzie hello grupa NSG jest tworzona. W naszym scenariuszu jest to *TestRG*.
   * `--location`: Region platformy azure, w którym hello Nowa grupa NSG jest tworzona. W naszym scenariuszu *westus*.
   * `--name`: Nazwa hello Nowa grupa NSG. W naszym scenariuszu *frontonu NSG*.

    Witaj oczekiwanych danych wyjściowych jest dość nieco informacji, łącznie z listą wszystkich reguł domyślnych hello. Witaj poniższy przykład przedstawia hello domyślnych reguł przy użyciu filtru kwerendy JMESPATH z hello `table` format wyjściowy:

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   Dane wyjściowe:

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. Utworzyć regułę, która umożliwia dostęp tooport 3389 (RDP) z hello Internet z hello [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) polecenia.

    > [!NOTE]
    > W zależności od powłoki hello używasz, może być konieczne toomodify hello `*` znak w argumentach powitania po nie tooexpand hello argument przed realizacją.
   
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
   
    Oczekiwane dane wyjściowe:
   
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

    Parametry:

    * `--resource-group testrg`: hello toouse grupy zasobów. Należy pamiętać, że bez uwzględniania wielkości liter.
    * `--nsg-name NSG-FrontEnd`: Nazwa grupy NSG hello, w których hello jest tworzona reguła.
    * `--name rdp-rule`: Nazwa hello nowej reguły.
    * `--access Allow`: Poziom dostępu hello reguły (Deny lub Zezwalaj).
    * `--protocol Tcp`: Protocol (Tcp, Udp lub *).
    * `--direction Inbound`: Kierunek hello połączenia (przychodzący lub wychodzący).
    * `--priority 100`: Priorytet reguły hello.
    * `--source-address-prefix Internet`: Prefiks adresu źródłowego CIDR lub przy użyciu znaczników domyślnych.
    * `--source-port-range "*"`: Źródła port lub zakres portów. Port, który otworzyć hello połączenia.
    * `--destination-address-prefix "*"`: Prefiks adresu docelowego CIDR lub przy użyciu znaczników domyślnych.
    * `--destination-port-range 3389`: Miejsce docelowe port lub zakres portów. Port, który odbiera żądanie połączenia hello.



4. Utworzyć regułę, która umożliwia dostęp tooport 80 (HTTP) z hello Internet **Tworzenie reguły nsg sieci az** polecenia.
   
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
   
    Oczekiwano putput:
   
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

5. Powiąż hello NSG toohello **frontonu** podsieć o hello [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update) polecenia.
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    Oczekiwane dane wyjściowe:
   
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

## <a name="create-hello-nsg-for-hello-backend-subnet"></a>Utwórz hello NSG dla hello `BackEnd` podsieci
grupy NSG o nazwie toocreate *wewnętrznej bazy danych grupy NSG* oparte na poprzednim scenariuszu hello, wykonaj następujące kroki hello.

1. Utwórz hello `NSG-BackEnd` grupy NSG z **utworzyć nsg sieci az**.
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    W kroku 2, poprzedni hello oczekuje się, że dane wyjściowe są bardzo duże, w tym reguły domyślne.
   
2. Utworzyć regułę, która umożliwia dostęp tooport 1433 (SQL) z hello `FrontEnd` podsieć o hello **Tworzenie reguły nsg sieci az** polecenia.
   
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
   
    Oczekiwane dane wyjściowe:

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

3. Utworzyć regułę, która nie zezwala na dostęp toohello Internetu za pomocą hello **Tworzenie reguły nsg sieci az** polecenia.
   
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
   
    Oczekiwano putput:
   
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

4. Powiąż hello NSG toohello `BackEnd` podsieci przy użyciu hello **zestaw podsieci sieci wirtualnej sieci az** polecenia.
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    Oczekiwane dane wyjściowe:
   
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
