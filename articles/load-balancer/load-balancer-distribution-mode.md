---
title: "Tryb dystrybucji modułu równoważenia obciążenia aaaConfigure | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure Azure załadować równoważenia dystrybucji tryb toosupport źródła IP koligacji"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 7df27a4d-67a8-47d6-b73e-32c0c6206e6e
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: e745240b733ffc07928d8ed0ae097785ad4f412e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-distribution-mode-for-load-balancer"></a>Konfigurowanie trybu dystrybucji powitania dla usługi równoważenia obciążenia

## <a name="hash-based-distribution-mode"></a>Tryb dystrybucji wyznaczania wartości skrótu

algorytmem dystrybucji domyślne Hello jest krotka 5 (źródłowy adres IP, port źródłowy, docelowy adres IP, port docelowy protokół typu) skrótów toomap ruchu tooavailable serwerów. Zapewnia on lepkości tylko w ramach sesji transportu. Pakietów hello tej samej sesji zostanie przekierowany toohello wystąpienie tego samego centrum danych adresu IP (DIP) za hello równoważenia obciążenia z punktem końcowym. Po uruchomieniu powitania klienta nowej sesji z hello tego samego źródłowego adresu IP, port źródłowy hello zmiany i powoduje, że hello ruchu toogo tooa różnych DIP punktu końcowego.

![skrót na podstawie usługi równoważenia obciążenia](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

Rysunek 1-5-elementowej dystrybucji

## <a name="source-ip-affinity-mode"></a>Tryb koligacji IP źródła

Mamy innego trybu dystrybucji o nazwie koligacji IP źródła (znanej także jako koligacji sesji lub koligacji IP klienta). Usługi równoważenia obciążenia Azure może być skonfigurowany toouse krotka 2 (źródłowy adres IP, docelowy adres IP) lub 3 parametrów (źródłowy adres IP, docelowy adres IP, protokół) toomap ruchu toohello dostępne serwery. Za pomocą koligacji źródłowy adres IP, połączenia inicjowane z hello sam komputer kliencki przechodzi toohello samego DIP punktu końcowego.

powitania po diagram ilustruje konfiguracji 2-spójnej kolekcji. Zwróć uwagę, jak hello 2-krotki działa za pośrednictwem hello obciążenia równoważenia toovirtual komputera 1 (VM1), który jest następnie kopię zapasową maszyny VM2 i VM3.

![Koligacja sesji](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

Rysunek 2 — dystrybucji krotki 2

Koligacja IP źródła rozwiązuje występuje niezgodność między hello modułu równoważenia obciążenia Azure i Brama usług pulpitu zdalnego (RD). Teraz można utworzyć farmę serwerów bramy usług pulpitu zdalnego w usłudze jednej chmury.

Inny scenariusz użycia jest przekazywanie nośnika hello przekazywania danych odbywa się w ramach protokołu UDP, ale dla których płaszczyzny kontroli hello odbywa się za pośrednictwem protokołu TCP:

* Klient najpierw inicjuje sesję TCP o zrównoważonym obciążeniu toohello publiczny adres, pobiera bezpośrednie tooa, określonych DIP, ten kanał jest kondycja połączenia powitania po lewej stronie toomonitor active
* Nowej sesji UDP z hello, w tym samym komputerze klienckim jest inicjowane toohello publiczny punkt końcowy o zrównoważonym obciążeniu tej samej, tutaj oczekiwania hello jest to połączenie jest również ukierunkowanej toohello tego samego końcowy DIP jako hello poprzednie połączenie TCP, aby przekazać nośnika może być wykonany o wysokiej przepływności, zachowując jednocześnie kanału kontroli, za pośrednictwem protokołu TCP.

> [!NOTE]
> W przypadku zmiany zestawu z równoważeniem obciążenia (usuwanie lub dodawanie maszyny wirtualnej), jest przeliczane hello dystrybucji żądań klientów. Nie może zależeć od nowych połączeń z istniejących klientów kończy na powitania sam serwer. Ponadto użycie źródłowy adres IP trybie dystrybucji koligacji może spowodować nierówne rozkładu ruchu. Klienci z systemem za serwery proxy mogą być widoczne jako jedną aplikację unikatowych klientów.

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>Konfigurowanie ustawień koligacji źródłowy adres IP dla modułu równoważenia obciążenia

W przypadku maszyn wirtualnych można użyć ustawienia limitu czasu toochange środowiska PowerShell:

Dodaj tooa Azure punktu końcowego maszyny wirtualnej i ustaw tryb dystrybucji modułu równoważenia obciążenia

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

Dystrybucji modułu równoważenia obciążenia można ustawić toosourceIP równoważenia, sourceIPProtocol równoważenia obciążenia 3 parametrów (źródłowy adres IP, docelowy adres IP, protokół) lub brak Chcąc hello domyślne zachowanie usługi równoważenia obciążenia 5-elementowej obciążenia 2 parametrów (źródłowy adres IP, docelowy adres IP).

Użyj powitania po tooretrieve konfiguracji trybu dystrybucji modułu równoważenia obciążenia punktu końcowego:

    PS C:\> Get-AzureVM –ServiceName MyService –Name MyVM | Get-AzureEndpoint

    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15
    LoadBalancerDistribution : sourceIP

Jeśli nie ma hello element dystrybucji modułu równoważenia obciążenia modułu równoważenia obciążenia Azure hello używa hello domyślny algorytm 5-elementowej.

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a>Ustaw tryb dystrybucji hello na zestawu punktów końcowych ze zrównoważonym obciążeniem

Jeśli punkty końcowe są częścią zestawu punktów końcowych ze zrównoważonym obciążeniem, należy ustawić tryb rozkładu hello zestawu punktów końcowych ze zrównoważonym obciążeniem hello:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a>Tryb dystrybucji toochange konfiguracji usługi w chmurze

Można wykorzystać hello Azure SDK dla platformy .NET 2.5 (toobe wydanej w listopadzie) tooupdate usługi w chmurze. Ustawienia punktu końcowego usługi w chmurze są nawiązywane w hello csdef. W kolejności tooupdate hello równoważenia trybu rozkładu obciążenia na wdrożenie usługi w chmurze wymagane jest uaktualnienie wdrożenia.
Oto przykład csdef zmiany ustawień punktu końcowego:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancerDistribution="sourceIP" />
    </Endpoints>
</WorkerRole>
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
<InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
    <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
</InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="api-example"></a>Przykładowy interfejs API

Można skonfigurować dystrybucji modułu równoważenia obciążenia hello przy użyciu interfejsu API zarządzania usługami hello. Upewnij się, że hello tooadd `x-ms-version` ustawiono nagłówka tooversion `2014-09-01` lub nowszej.

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a>Aktualizacja konfiguracji hello hello określony zestaw o zrównoważonym obciążeniu we wdrożeniu

#### <a name="request-example"></a>Przykładowe żądanie

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>?comp=UpdateLbSet   x-ms-version: 2014-09-01
    Content-Type: application/xml

    <LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <InputEndpoint>
        <LoadBalancedEndpointSetName> endpoint-set-name </LoadBalancedEndpointSetName>
        <LocalPort> local-port-number </LocalPort>
        <Port> external-port-number </Port>
        <LoadBalancerProbe>
          <Port> port-assigned-to-probe </Port>
          <Protocol> probe-protocol </Protocol>
          <IntervalInSeconds> interval-of-probe </IntervalInSeconds>
          <TimeoutInSeconds> timeout-for-probe </TimeoutInSeconds>
        </LoadBalancerProbe>
        <Protocol> endpoint-protocol </Protocol>
        <EnableDirectServerReturn> enable-direct-server-return </EnableDirectServerReturn>
        <IdleTimeoutInMinutes>idle-time-out</IdleTimeoutInMinutes>
        <LoadBalancerDistribution>sourceIP</LoadBalancerDistribution>
      </InputEndpoint>
    </LoadBalancedEndpointList>

wartość Hello dystrybucji modułu równoważenia obciążenia może być sourceIP koligacji krotki 2, sourceIPProtocol koligacji krotki 3 lub none (Brak koligacji w przypadku. czyli 5-elementowej)

#### <a name="response"></a>Odpowiedź

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a>Następne kroki

[Omówienie usługi równoważenia obciążenia wewnętrznego](load-balancer-internal-overview.md)

[Przed rozpoczęciem konfigurowania internetowy modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)
