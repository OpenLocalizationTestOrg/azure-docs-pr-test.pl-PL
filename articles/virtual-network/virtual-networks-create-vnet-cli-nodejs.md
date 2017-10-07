---
title: "aaaCreate sieci wirtualnych za pomocą funkcji hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate sieci wirtualnych za pomocą funkcji hello Azure CLI 1.0 | Menedżer zasobów."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a>Utwórz sieć wirtualną przy użyciu hello wiersza polecenia platformy Azure

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Platforma Azure ma dwa modele wdrażania: usługa Azure Resource Manager i wersja klasyczna. Firma Microsoft zaleca utworzenie zasobów za pośrednictwem modelu wdrażania usługi Resource Manager hello. więcej informacji o toolearn hello różnice między modelami hello dwa odczytu hello [modele wdrażania zrozumieć Azure](../azure-resource-manager/resource-manager-deployment-model.md) artykułu.

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello
- [Azure CLI 1.0](#create-a-virtual-network) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>Tworzenie sieci wirtualnej

toocreate sieci wirtualnych za pomocą funkcji hello Azure CLI, pełną hello następujące kroki:

1. Instalowanie i konfigurowanie hello Azure CLI przez hello następujące kroki w hello [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) artykułu.

2. Utwórz sieć wirtualną i podsieć:

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    Oczekiwane dane wyjściowe:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    Użyte parametry:

   * **--vnet**. Nazwa toobe sieci wirtualnej hello utworzony. W naszym scenariuszu jest to *TestVNet*
   * **-e (lub--przestrzeni adresowej)**. Przestrzeń adresowa sieci wirtualnej. W naszym scenariuszu *192.168.0.0*
   * **-i (lub - cidr)**. Maska sieci w formacie CIDR. W naszym scenariuszu *16*.
   * **-n (lub--nazwy podsieci**). Nazwa hello pierwszej podsieci. W naszym scenariuszu jest to *FrontEnd*.
   * **-p (lub--podsieci start-ip)**. Początkowy adres IP dla podsieci lub przestrzeni adresowej podsieci. W naszym scenariuszu *192.168.1.0*.
   * **-r (lub--podsieci cidr)**. Maska sieci w formacie CIDR podsieci. W naszym scenariuszu *24*.
   * **-l (lub --location)**. Region platformy Azure, w której jest tworzony hello sieci wirtualnej. W naszym scenariuszu *środkowe stany USA*.

3. Utwórz podsieć:

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    Oczekiwane dane wyjściowe:

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    Użyte parametry:

   * **-t (lub--vnet-name**. Nazwa sieci wirtualnej, w którym zostanie utworzona podsieć hello hello. W naszym scenariuszu jest to *TestVNet*.
   * **-n (lub --name)**. Nazwa nowej podsieci hello. W naszym scenariuszu *zaplecza*.
   * **-a (lub --address-prefix)**. Blok CIDR podsieci. Cztery naszym scenariuszu *192.168.2.0/24*.
   
4. właściwości hello tooview hello nowej sieci wirtualnej:

    ```azurecli
    azure network vnet show
    ```
   
    Oczekiwane dane wyjściowe:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooconnect:

- Sieć wirtualną maszyny wirtualnej (VM) tooa odczytując hello [Utwórz Maszynę wirtualną systemu Linux](../virtual-machines/linux/quick-create-cli.md) artykułu. Zamiast tworzenia sieci wirtualnej i podsieci w krokach hello hello artykułów, możesz wybrać istniejącej sieci wirtualnej i tooconnect podsieci maszyny Wirtualnej, aby.
- Witaj sieci wirtualne sieci wirtualnej tooother odczytując hello [połączyć sieci wirtualnych](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artykułu.
- Witaj sieci wirtualnej tooan sieci lokalnej za pomocą wirtualnej sieci prywatnej (VPN) do lokacji lub obwodu usługi expressroute. Dowiedz się, jak odczytując hello [połączyć sieć lokalną tooan sieci wirtualnej przy użyciu sieci VPN lokacja lokacja](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) i [połączyć sieć wirtualną tooan obwodu ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
