---
title: "aaaCreate wewnętrzne załadować równoważenia - klasycznego wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toocreate usługi równoważenia obciążenia wewnętrznego przy użyciu wiersza polecenia platformy Azure w hello klasycznego modelu wdrażania"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a>Rozpoczynanie pracy tworzenia wewnętrznego modułu równoważenia obciążenia (klasyczne) przy użyciu hello wiersza polecenia platformy Azure

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Usługi w chmurze](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](load-balancer-get-started-ilb-arm-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a>toocreate wewnętrznego modułu równoważenia obciążenia dla maszyn wirtualnych

toocreate wewnętrznego modułu równoważenia obciążenia ustaw i hello serwerów, które będzie wysyłać ich tooit ruchu, należy wykonać następujące hello:

1. Utwórz wystąpienie wewnętrzne Równoważenie obciążenia sieciowego, który będzie hello punkt końcowy przychodzącego ruchu toobe równoważone między serwerami hello zestawu z równoważeniem obciążenia.
2. Dodawanie punktów końcowych odpowiadającego toohello maszyn wirtualnych, które będzie otrzymywał hello ruchu przychodzącego.
3. Konfigurowanie serwerów hello, które będą wysyłane się, że hello ruchu toobe o zrównoważonym obciążeniu toosend ich ruchu toohello wirtualny adres IP (VIP) wystąpienia hello wewnętrzne Równoważenie obciążenia sieciowego.

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a>Szczegółowy opis tworzenia wewnętrznego modułu równoważenia obciążenia przy użyciu interfejsu wiersza polecenia

Ten przewodnik zawiera jak toocreate wewnętrznego modułu równoważenia obciążenia na podstawie scenariusza hello powyżej.

1. Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.
2. Uruchom hello **trybie azure config** polecenia tooswitch tooclassic tryb, jak pokazano poniżej.

    ```azurecli
    azure config mode asm
    ```

    Oczekiwane dane wyjściowe:

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>Tworzenie punktu końcowego i zestawu modułu równoważenia obciążenia

Hello scenariusz zakłada hello maszyn wirtualnych "DB1" i "Bazy danych DB2" w usłudze w chmurze o nazwie "mytestcloud". Obie maszyny wirtualne korzystają z sieci wirtualnej o nazwie „testvnet” z podsiecią o nazwie „subnet-1”.

W tym przewodniku opisano sposób tworzenia zestawu wewnętrznego modułu równoważenia obciążenia przy użyciu portu 1433 jako portu publicznego i lokalnego.

To jest typowy scenariusz, w którym masz SQL maszyn wirtualnych na powitania zaplecza przy użyciu serwerów baz danych hello tooguarantee obciążenia wewnętrznego modułu równoważenia nie będą widoczne, bezpośrednio za pomocą publicznego adresu IP.

### <a name="step-1"></a>Krok 1

Utwórz zestaw wewnętrznego modułu równoważenia obciążenia za pomocą polecenia `azure network service internal-load-balancer add`.

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

Użyj polecenia `azure service internal-load-balancer --help`, aby uzyskać więcej informacji.

Możesz sprawdzić właściwości usługi równoważenia obciążenia wewnętrznego hello za pomocą polecenia hello `azure service internal-load-balancer list` *nazwa usługi w chmurze*.

W tym miejscu następujący przykład danych wyjściowych hello:

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a>Krok 2

Możesz skonfigurować hello wewnętrznego modułu równoważenia obciążenia ustawić po dodaniu hello pierwszym punktem końcowym. Skojarzysz hello punktu końcowego, maszyny wirtualnej i badania portu toohello wewnętrznego modułu równoważenia obciążenia w tym kroku.

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a>Krok 3

Sprawdzić z konfiguracji usługi równoważenia obciążenia hello `azure vm show` *nazwę maszyny wirtualnej*

```azurecli
azure vm show DB1
```

Witaj dane wyjściowe będą mieć:

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>Tworzenie punktu końcowego pulpitu zdalnego maszyny wirtualnej

Ruch sieciowy tooforward zdalny punkt końcowy pulpitu można utworzyć na podstawie port publiczny port lokalny tooa dla określonej maszyny wirtualnej przy użyciu `azure vm endpoint create`.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>Usuwanie maszyny wirtualnej z modułu równoważenia obciążenia

Możesz usunąć maszynę wirtualną z wewnętrznego modułu równoważenia obciążenia ustawione przez usuwanie punktu końcowego hello skojarzone. Po usunięciu punktu końcowego hello hello maszyny wirtualnej nie należą już zestaw modułów równoważenia obciążenia toohello.

Za pomocą powyższego przykładu hello, można usunąć punktu końcowego hello utworzone dla maszyny wirtualnej "DB1" z wewnętrznego modułu równoważenia obciążenia "ilbset" za pomocą polecenia hello `azure vm endpoint delete`.

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

Użyj polecenia `azure vm endpoint --help`, aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki

[Configure a load balancer distribution mode using source IP affinity](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia przy użyciu koligacji źródłowych adresów IP)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
