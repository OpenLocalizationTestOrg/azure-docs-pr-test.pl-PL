---
title: "sieć wirtualna — Azure CLI 2.0 aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate sieci wirtualnych za pomocą funkcji hello Azure CLI 2.0."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a>Utwórz sieć wirtualną przy użyciu hello Azure CLI 2.0

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Platforma Azure ma dwa modele wdrażania: usługa Azure Resource Manager i wersja klasyczna. Firma Microsoft zaleca utworzenie zasobów za pośrednictwem modelu wdrażania usługi Resource Manager hello. więcej informacji o toolearn hello różnice między modelami hello dwa odczytu hello [modele wdrażania zrozumieć Azure](../azure-resource-manager/resource-manager-deployment-model.md) artykułu.

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modelami wdrażania
- [Azure CLI 2.0](#create-a-virtual-network) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania hello zasobów (w tym artykule) "
 
    Możesz również utworzyć sieć wirtualną za pomocą Menedżera zasobów przy użyciu innych narzędzi lub utworzyć sieć wirtualną przy użyciu hello klasycznego modelu wdrażania, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Portal](virtual-networks-create-vnet-arm-pportal.md)
> * [Program PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [Interfejs wiersza polecenia](virtual-networks-create-vnet-arm-cli.md)
> * [Szablon](virtual-networks-create-vnet-arm-template-click.md)
> * [Portal (klasyczny)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (klasyczny)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [Interfejs wiersza polecenia (klasyczny)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a>Tworzenie sieci wirtualnej

toocreate sieci wirtualnych za pomocą funkcji hello Azure CLI 2.0, pełną hello następujące kroki:

1. Instalowanie i konfigurowanie hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

2. Utwórz grupę zasobów dla sieci wirtualnej przy użyciu hello [Tworzenie grupy az](/cli/azure/group#create) z hello `--name` i `--location` argumentów:

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. Utwórz sieć wirtualną i podsieć:

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    Oczekiwane dane wyjściowe:
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    Użyte parametry:

    - `--name TestVNet`: Nazwa toobe sieci wirtualnej hello utworzony.
    - `--resource-group TestRG`: Nazwa grupy zasobów hello #, kontrolujące hello zasobów. 
    - `--location centralus`: hello lokalizacji, do których toodeploy.
    - `--address-prefix 192.168.0.0/16`: hello prefiksu adresu i bloku.  
    - `--subnet-name FrontEnd`: Nazwa hello hello podsieci.
    - `--subnet-prefix 192.168.1.0/24`: hello prefiksu adresu i bloku.

    toolist hello podstawowe informacje toouse w hello obok polecenia, można badać przy użyciu sieci wirtualnej hello [Filtr kwerendy](/cli/azure/query-az-cli2):

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    Pozwalającą na uzyskanie hello następujące dane wyjściowe:

        Where      Name      Group

        centralus  TestVNet  TestRG

4. Utwórz podsieć:

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    Oczekiwane dane wyjściowe:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    Użyte parametry:

    - `--address-prefix 192.168.2.0/24`: Blok CIDR podsieci.
    - `--name BackEnd`: Nazwa nowej podsieci hello.
    - `--resource-group TestRG`: hello grupy zasobów.
    - `--vnet-name TestVNet`: Nazwa hello hello będący właścicielem sieci wirtualnej.

5. Właściwości hello zapytania hello nowej sieci wirtualnej:

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    Oczekiwane dane wyjściowe:

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. Właściwości hello zapytania hello podsieci:

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    Oczekiwane dane wyjściowe:

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooconnect:

- Sieć wirtualną maszyny wirtualnej (VM) tooa odczytując hello [Utwórz Maszynę wirtualną systemu Linux](../virtual-machines/linux/quick-create-cli.md) artykułu. Zamiast tworzenia sieci wirtualnej i podsieci w krokach hello hello artykułów, możesz wybrać istniejącej sieci wirtualnej i tooconnect podsieci maszyny Wirtualnej, aby.
- Witaj sieci wirtualne sieci wirtualnej tooother odczytując hello [połączyć sieci wirtualnych](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artykułu.
- Witaj sieci wirtualnej tooan sieci lokalnej za pomocą wirtualnej sieci prywatnej (VPN) do lokacji lub obwodu usługi expressroute. Dowiedz się, jak odczytując hello [połączyć sieć lokalną tooan sieci wirtualnej przy użyciu sieci VPN lokacja lokacja](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) i [połączyć sieć wirtualną tooan obwodu ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
