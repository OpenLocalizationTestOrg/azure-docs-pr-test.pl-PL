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
# <a name="create-network-security-groups-using-the-azure-cli-20"></a>Tworzenie sieci za pomocą 2.0 interfejsu wiersza polecenia Azure grup zabezpieczeń

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a>Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania 

Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia: 

- [Interfejs wiersza polecenia platformy Azure w wersji 1.0](virtual-networks-create-nsg-cli-nodejs.md) — nasz interfejs wiersza polecenia dla klasycznego modelu wdrażania i modelu wdrażania na potrzeby zarządzania zasobami 
- [Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -naszej nowej generacji interfejsu wiersza polecenia do zarządzania model wdrażania zasobów (w tym artykule)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

Przykładowe polecenia 2.0 interfejsu wiersza polecenia platformy Azure po oczekiwać środowisku niezłożonym już utworzone na podstawie w poprzednim scenariuszu. 

## <a name="create-the-nsg-for-the-frontend-subnet"></a>Tworzenie grupy NSG dla `FrontEnd` podsieci

Aby utworzyć grupy NSG o nazwie *frontonu NSG* oparte na poprzednim scenariuszu, wykonaj następujące kroki.

1. Jeśli nie zostało jeszcze, instalowania i konfigurowania najnowszej [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się do platformy Azure konta przy użyciu [logowania az](/cli/azure/#login). 

2. Tworzenie grupy NSG przy użyciu [utworzyć nsg sieci az](/cli/azure/network/nsg#create) polecenia. 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    Parametry:
   
   * `--resource-group`: Nazwa grupy zasobów, w którym grupa NSG jest tworzona. W naszym scenariuszu jest to *TestRG*.
   * `--location`: Region platformy azure, gdzie jest tworzona nowa grupa NSG. W naszym scenariuszu *westus*.
   * `--name`: Nazwa nowej grupy NSG. W naszym scenariuszu *frontonu NSG*.

    Oczekiwane dane wyjściowe jest dość informacji w tym listę domyślnych reguł. W poniższym przykładzie przedstawiono reguły domyślne przy użyciu JMESPATH filtr zapytania o `table` format wyjściowy:

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
        Allow     Allow outbound traffic from all VMs to all VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs to Internet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. Utworzyć regułę, która umożliwia uzyskanie dostępu do portu 3389 (RDP) z Internetu z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) polecenia.

    > [!NOTE]
    > W zależności od powłoki używasz, może być konieczne zmodyfikować `*` znak w argumentach po w celu rozwiń argument przed realizacją.
   
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

    * `--resource-group testrg`: Grupy zasobów do użycia. Należy pamiętać, że bez uwzględniania wielkości liter.
    * `--nsg-name NSG-FrontEnd`: Nazwa grupy NSG, w którym jest tworzona reguła.
    * `--name rdp-rule`: Nazwa nowej reguły.
    * `--access Allow`: Poziom dostępu reguły (Deny lub Zezwalaj).
    * `--protocol Tcp`: Protocol (Tcp, Udp lub *).
    * `--direction Inbound`: Kierunek połączenia (przychodzący lub wychodzący).
    * `--priority 100`: Priorytet reguły.
    * `--source-address-prefix Internet`: Prefiks adresu źródłowego CIDR lub przy użyciu znaczników domyślnych.
    * `--source-port-range "*"`: Źródła port lub zakres portów. Port, który otworzyć połączenia.
    * `--destination-address-prefix "*"`: Prefiks adresu docelowego CIDR lub przy użyciu znaczników domyślnych.
    * `--destination-port-range 3389`: Miejsce docelowe port lub zakres portów. Port, który odbiera żądanie połączenia.



4. Utworzyć regułę, która zezwala na dostęp do portu 80 (HTTP) z Internetu **Tworzenie reguły nsg sieci az** polecenia.
   
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

5. Powiązanie grupy NSG z **frontonu** podsieć o [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update) polecenia.
        
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

## <a name="create-the-nsg-for-the-backend-subnet"></a>Tworzenie grupy NSG dla `BackEnd` podsieci
Aby utworzyć grupy NSG o nazwie *zaplecza NSG* oparte na poprzednim scenariuszu, wykonaj następujące kroki.

1. Utwórz `NSG-BackEnd` grupy NSG z **utworzyć nsg sieci az**.
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    W kroku 2, poprzedni oczekiwane dane wyjściowe jest dość duży, w tym reguły domyślne.
   
2. Utworzyć regułę, która umożliwia uzyskanie dostępu do portu 1433 (SQL) z `FrontEnd` podsieć o **Tworzenie reguły nsg sieci az** polecenia.
   
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

3. Utworzyć regułę, która nie zezwala na dostęp do Internetu za pomocą **Tworzenie reguły nsg sieci az** polecenia.
   
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

4. Powiązanie grupy NSG z `BackEnd` podsieci przy użyciu **zestaw podsieci sieci wirtualnej sieci az** polecenia.
   
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
