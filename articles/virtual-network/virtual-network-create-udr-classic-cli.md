---
title: aaaControl routingu w klasycznym Azure Virtual Network - CLI - | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak hello toocontrol routingu w sieci wirtualnych za pomocą wiersza polecenia platformy Azure w hello klasycznego modelu wdrażania"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a>Formant routingu i użyj wirtualnych urządzeń (klasyczne) przy użyciu interfejsu wiersza polecenia Azure hello

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](virtual-network-create-udr-arm-cli.md)
> * [Szablon](virtual-network-create-udr-arm-template.md)
> * [PowerShell (klasyczny)](virtual-network-create-udr-classic-ps.md)
> * [Interfejs wiersza polecenia (klasyczny)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

W tym artykule omówiono hello klasycznego modelu wdrażania. Możesz również [kontrolować routingu i używaniu urządzeń wirtualnych w modelu wdrażania usługi Resource Manager hello](virtual-network-create-udr-arm-cli.md).

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

Poniższe polecenia interfejsu wiersza polecenia Azure próbki Hello oczekiwać środowisku niezłożonym już utworzone w zależności od scenariusza hello powyżej. Polecenia hello toorun wyświetlaną w tym dokumencie, utworzyć środowisko hello pokazano [Utwórz sieć wirtualną (klasyczne) przy użyciu interfejsu wiersza polecenia Azure hello](virtual-networks-create-vnet-classic-cli.md).

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Utwórz hello przez dla podsieci frontonu hello
tabeli tras hello toocreate i trasy wymagane do podsieci frontonu hello oparta na scenariuszu hello powyżej, wykonaj poniższe kroki hello.

1. Witaj uruchom następujące polecenie Tryb tooclassic tooswitch:

    ```azurecli
    azure config mode asm
    ```

    Dane wyjściowe:

        info:    New mode is asm

2. Uruchom następujące polecenie toocreate hello tabelę tras dla podsieci frontonu hello:

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    Dane wyjściowe:
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    Parametry:
   
   * **-l (lub --location)**. Region platformy Azure, której hello Nowa grupa NSG zostanie utworzona. W naszym scenariuszu *westus*.
   * **-n (lub --name)**. Nazwa hello Nowa grupa NSG. W naszym scenariuszu *frontonu NSG*.
3. Uruchom następujące polecenie toocreate trasy w toosend tabeli tras hello hello wszystkich toohello podsieci zaplecza (192.168.2.0/24) toohello ruch kierowany **FW1** maszyny Wirtualnej (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    Dane wyjściowe:
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    Parametry:
   
   * **-r (lub--nazwa tabeli tras)**. Nazwa tabeli tras hello, gdzie ma zostać dodana hello trasy. W naszym scenariuszu *frontonu przez*.
   * **-a (lub --address-prefix)**. Prefiks adresu podsieci hello, gdy pakiety są przeznaczone do. W naszym scenariuszu *192.168.2.0/24*.
   * **-t (lub--następnego przeskoku typu)**. Typ obiektu ruchu zostaną wysłane do. Możliwe wartości to *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, lub *Brak*.
   * **-p (lub--dalej przeskoku — adres ip**). Adres IP następnego przeskoku. W naszym scenariuszu *192.168.0.4*.
4. Witaj uruchom następujące polecenie tabeli tras hello tooassociate utworzone za pomocą hello **frontonu** podsieci:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    Dane wyjściowe:
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    Parametry:
   
   * **-t (lub--vnet-name)**. Nazwa sieci wirtualnej, w którym znajduje się podsieci hello hello. W naszym scenariuszu jest to *TestVNet*.
   * **-n (lub--nazwy podsieci**. Nazwa tabeli tras hello podsieci hello zostaną dodane do. W naszym scenariuszu jest to *FrontEnd*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Utwórz hello przez hello zaplecza podsieci
Tabela tras hello toocreate i trasy wymagane do podsieci wewnętrznej hello oparta na scenariuszu hello pełną hello następujące kroki:

1. Uruchom następujące polecenie toocreate hello tabelę tras dla podsieci wewnętrznej hello:

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. Uruchom następujące polecenia toocreate trasy w toosend tabeli tras hello hello wszystkich ruch kierowany toohello podsieci frontonu (192.168.1.0/24) toohello **FW1** maszyny Wirtualnej (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. Uruchom hello następujących tabeli tras hello tooassociate polecenie z hello **zaplecza** podsieci:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

