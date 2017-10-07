---
title: "aaaCreate internetowy załadować równoważenia - klasycznego wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Internet równoważenia obciążenia przy użyciu modelu wdrażania klasycznego hello wiersza polecenia platformy Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a>Rozpocząć tworzenie internetowy modułu równoważenia obciążenia (klasyczne) w hello wiersza polecenia platformy Azure

> [!div class="op_single_selector"]
> * [Klasyczna witryna Azure Portal](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [Program PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Przed rozpoczęciem pracy z zasobów platformy Azure, jest ważne toounderstand, że Azure ma obecnie dwa modele wdrażania: usługi Azure Resource Manager i model klasyczny. Przed rozpoczęciem pracy z dowolnym zasobem Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-classic-rm.md). Hello dokumentację dotyczącą różnych narzędzi można wyświetlić, klikając karty hello u góry hello tego artykułu. W tym artykule omówiono hello klasycznego modelu wdrażania. Możesz również [Dowiedz się, jak usługa równoważenia przy użyciu usługi Azure Resource Manager obciążenia toocreate Internetem](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a>Szczegółowy opis tworzenia modułu równoważenia obciążenia dostępnego z Internetu przy użyciu interfejsu wiersza polecenia

W tym przewodniku pokazuje, jak toocreate Internet równoważenia obciążenia na powitania scenariusz powyżej.

1. Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.
2. Uruchom hello **trybie azure config** polecenia tooswitch tooclassic tryb, jak pokazano poniżej.

    ```azurecli
    azure config mode asm
    ```

    Oczekiwane dane wyjściowe:

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>Tworzenie punktu końcowego i zestawu modułu równoważenia obciążenia

Utworzono "sieci Web 2" i Hello scenariusz zakłada hello maszyn wirtualnych "sieci Web 1".
W tym przewodniku opisano sposób tworzenia modułu równoważenia obciążenia przy użyciu portu 80 jako portu publicznego i lokalnego. Port sondy jest również konfigurowany na porcie 80, a moduł równoważenia obciążenia o nazwie hello ustawić "lbset".

### <a name="step-1"></a>Krok 1

Tworzenie pierwszego punktu końcowego hello i ustawić za pomocą modułu równoważenia obciążenia `azure network vm endpoint create` dla maszyny wirtualnej "sieci Web 1".

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a>Krok 2

Dodaj drugi zestaw usługi równoważenia obciążenia toohello maszyny wirtualnej "sieci Web 2".

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a>Krok 3

Sprawdzić z konfiguracji usługi równoważenia obciążenia hello `azure vm show` .

```azurecli
azure vm show web1
```

Witaj dane wyjściowe będą mieć:

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>Tworzenie punktu końcowego pulpitu zdalnego maszyny wirtualnej

Ruch sieciowy tooforward zdalny punkt końcowy pulpitu można utworzyć na podstawie port publiczny port lokalny tooa dla określonej maszyny wirtualnej przy użyciu `azure vm endpoint create`.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>Usuwanie maszyny wirtualnej z modułu równoważenia obciążenia

Masz toohello punkt końcowym skojarzony hello toodelete załadować zestawu modułu równoważenia z hello maszyny wirtualnej. Po usunięciu punktu końcowego hello hello maszyny wirtualnej nie należy już zestaw modułów równoważenia obciążenia toohello.

Za pomocą powyższego przykładu hello, można usunąć punktu końcowego hello utworzone dla maszyny wirtualnej "sieci Web 1" z modułu równoważenia obciążenia "lbset" za pomocą polecenia hello `azure vm endpoint delete`.

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> Można eksplorować więcej opcji toomanage punktów końcowych przy użyciu polecenia hello`azure vm endpoint --help`

## <a name="next-steps"></a>Następne kroki

[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-ps.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)

[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
