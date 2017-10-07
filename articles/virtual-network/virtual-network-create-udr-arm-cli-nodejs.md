---
title: "aaaControl routingu i wirtualnych urządzeń za pomocą hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocontrol routingu i wirtualnych urządzeń za pomocą hello Azure CLI w wersji 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a>Tworzenie trasy zdefiniowane przez użytkownika (przez) przy użyciu hello Azure CLI w wersji 1.0

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](virtual-network-create-udr-arm-cli.md)
> * [Szablon](virtual-network-create-udr-arm-template.md)
> * [PowerShell (klasyczny)](virtual-network-create-udr-classic-ps.md)
> * [Interfejs wiersza polecenia (klasyczny)](virtual-network-create-udr-classic-cli.md)

Utwórz niestandardowy routing i wirtualnych urządzeń przy użyciu hello wiersza polecenia platformy Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia 

Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia: 

- [Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

Poniższe polecenia interfejsu wiersza polecenia Azure próbki Hello oczekiwać środowisku niezłożonym już utworzone w zależności od scenariusza hello powyżej. Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, wdrażając najpierw utworzyć środowisko testowe hello [ten szablon](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów Jeśli to konieczne i wykonaj instrukcje hello hello portalu.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Utwórz hello przez hello podsieci frontonu
tabeli tras hello toocreate i trasy wymagane do podsieci frontonu hello oparta na scenariuszu hello powyżej, wykonaj poniższe kroki hello.

1. Uruchom następujące polecenie toocreate hello tabelę tras dla podsieci frontonu hello:

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    Dane wyjściowe:
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    Parametry:
   
   * **-g (lub --resource-group)**. Nazwa grupy zasobów hello której zostanie utworzona przez hello. W naszym scenariuszu jest to *TestRG*.
   * **-l (lub --location)**. Region platformy Azure, której hello przez nowe zostanie utworzona. W naszym scenariuszu *westus*.
   * **-n (lub --name)**. Nazwa hello przez nowe. W naszym scenariuszu *frontonu przez*.
2. Uruchom następujące polecenie toocreate trasy w toosend tabeli tras hello hello wszystkich toohello podsieci zaplecza (192.168.2.0/24) toohello ruch kierowany **FW1** maszyny Wirtualnej (192.168.0.4):

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    Dane wyjściowe:
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    Parametry:
   
   * **-r (lub--nazwa tabeli tras)**. Nazwa tabeli tras hello, gdzie ma zostać dodana hello trasy. W naszym scenariuszu *frontonu przez*.
   * **-a (lub --address-prefix)**. Prefiks adresu podsieci hello, gdy pakiety są przeznaczone do. W naszym scenariuszu *192.168.2.0/24*.
   * **-y (lub--następnego przeskoku typu)**. Typ obiektu ruchu zostaną wysłane do. Możliwe wartości to *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, lub *Brak*.
   * **-p (lub--dalej przeskoku — adres ip**). Adres IP następnego przeskoku. W naszym scenariuszu *192.168.0.4*.
3. Witaj uruchom następujące polecenie tabeli tras hello tooassociate utworzone powyżej z hello **frontonu** podsieci:

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    Dane wyjściowe:
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    Parametry:
   
   * **-e (lub--vnet-name)**. Nazwa sieci wirtualnej, w którym znajduje się podsieci hello hello. W naszym scenariuszu jest to *TestVNet*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Utwórz hello przez hello zaplecza podsieci
Witaj toocreate tabeli tras i trasy, potrzebnego do podsieci wewnętrznej hello oparta na scenariuszu hello powyżej pełną hello następujące kroki:

1. Uruchom następujące polecenie toocreate hello tabelę tras dla podsieci wewnętrznej hello:

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. Uruchom następujące polecenia toocreate trasy w toosend tabeli tras hello hello wszystkich ruch kierowany toohello podsieci frontonu (192.168.1.0/24) toohello **FW1** maszyny Wirtualnej (192.168.0.4):

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. Uruchom hello następujących tabeli tras hello tooassociate polecenie z hello **zaplecza** podsieci:

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>Włącz przesyłanie dalej IP na FW1
przesyłanie dalej IP tooenable w hello używany przez kartę Sieciową **FW1**pełnego hello następujące kroki:

1. Uruchom polecenie hello, i zwróć uwagę, wartość hello **przesyłanie dalej IP włączyć**. Powinna być ustawiona zbyt*false*.

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    Dane wyjściowe:
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. Witaj uruchom następujące polecenie tooenable przesyłanie dalej IP:

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    Dane wyjściowe:
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    Parametry:
   
   * **-f (lub--Włącz przesyłanie dalej ip)**. *wartość true,* lub *false*.

