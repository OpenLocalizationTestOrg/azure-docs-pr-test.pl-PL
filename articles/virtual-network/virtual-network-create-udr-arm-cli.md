---
title: "aaaControl routingu i wirtualnych urządzeń za pomocą hello Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocontrol routingu i wirtualnych urządzeń za pomocą hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a>Tworzenie trasy zdefiniowane przez użytkownika (przez) przy użyciu hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](virtual-network-create-udr-arm-cli.md)
> * [Szablon](virtual-network-create-udr-arm-template.md)
> * [PowerShell (wdrożenia klasycznego)](virtual-network-create-udr-classic-ps.md)
> * [Interfejs wiersza polecenia (wdrożenia klasycznego)](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia 

Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia: 

- [Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modelami wdrażania 
- [Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania hello zasobów (w tym artykule)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

Poniższe polecenia interfejsu wiersza polecenia Azure próbki Hello oczekiwać środowisku niezłożonym już utworzone w zależności od scenariusza hello powyżej. Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, wdrażając najpierw utworzyć środowisko testowe hello [ten szablon](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów Jeśli to konieczne i wykonaj instrukcje hello hello portalu.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Utwórz hello przez hello podsieci frontonu
tabeli tras hello toocreate i trasy wymagane do podsieci frontonu hello oparta na scenariuszu hello powyżej, wykonaj poniższe kroki hello.

1. Utwórz tabelę tras dla podsieci frontonu hello z hello [utworzyć tabelę tras az sieci](/cli/azure/network/route-table#create) polecenia:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    Dane wyjściowe:

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. Utwórz trasę, która wysyła wszystkie toohello podsieci zaplecza (192.168.2.0/24) toohello ruch kierowany **FW1** maszyny Wirtualnej (192.168.0.4) przy użyciu hello [utwórz trasę tabeli tras sieciowych az](/cli/azure/network/route-table/route#create) polecenia:

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    Dane wyjściowe:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    Parametry:

    * **--Nazwa tabeli tras**. Nazwa tabeli tras hello, gdzie ma zostać dodana hello trasy. W naszym scenariuszu *frontonu przez*.
    * **--address-prefix**. Prefiks adresu podsieci hello, gdy pakiety są przeznaczone do. W naszym scenariuszu *192.168.2.0/24*.
    * **--następnego przeskoku typu**. Typ obiektu ruchu zostaną wysłane do. Możliwe wartości to *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, lub *Brak*.
    * **--dalej przeskoku — adres ip**. Adres IP następnego przeskoku. W naszym scenariuszu *192.168.0.4*.

3. Uruchom hello [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update) tabeli tras hello tooassociate polecenia utworzone powyżej z hello **frontonu** podsieci:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    Dane wyjściowe:

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    Parametry:
    
    * **--vnet-name**. Nazwa sieci wirtualnej, w którym znajduje się podsieci hello hello. W naszym scenariuszu jest to *TestVNet*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Utwórz hello przez hello zaplecza podsieci

Witaj toocreate tabeli tras i trasy, potrzebnego do podsieci wewnętrznej hello oparta na scenariuszu hello powyżej pełną hello następujące kroki:

1. Uruchom następujące polecenie toocreate hello tabelę tras dla podsieci wewnętrznej hello:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. Uruchom następujące polecenia toocreate trasy w toosend tabeli tras hello hello wszystkich ruch kierowany toohello podsieci frontonu (192.168.1.0/24) toohello **FW1** maszyny Wirtualnej (192.168.0.4):

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. Uruchom hello następujących tabeli tras hello tooassociate polecenie z hello **zaplecza** podsieci:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>Włącz przesyłanie dalej IP na FW1

przesyłanie dalej IP tooenable w hello używany przez kartę Sieciową **FW1**pełnego hello następujące kroki:

1. Uruchom hello [Pokaż kart sieciowych az](/cli/azure/network/nic#show) poleceń z bieżącej hello toodisplay filtru JMESPATH **Włącz przesyłanie dalej ip** wartość **przesyłanie dalej IP włączyć**. Powinna być ustawiona zbyt*false*.

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    Dane wyjściowe:

        false

2. Witaj uruchom następujące polecenie tooenable przesyłanie dalej IP:

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    Można przejrzeć konsoli toohello strumienia wyjściowego hello, lub po prostu sprawdź jeszcze raz dla określonych hello **enableIpForwarding** wartość:

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    Dane wyjściowe:

        true

    Parametry:

    **przesyłanie dalej ip —**: *true* lub *false*.

