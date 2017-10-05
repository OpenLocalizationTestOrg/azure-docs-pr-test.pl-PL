---
title: "Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia | Dokumentacja firmy Microsoft"
description: "Jak skonfigurować tryb dystrybucji modułu równoważenia obciążenia Azure do obsługi koligacji IP źródła"
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
ms.openlocfilehash: 4cb000c8ee1bb2e267dc0813dab23a77a46080ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-distribution-mode-for-load-balancer"></a>Konfigurowanie trybu dystrybucji dla usługi równoważenia obciążenia

## <a name="hash-based-distribution-mode"></a>Tryb dystrybucji wyznaczania wartości skrótu

Domyślnym algorytmem dystrybucji jest krotka 5 (źródłowy adres IP, port źródłowy, docelowy adres IP, port docelowy protokół typu) skrót do mapowania ruchu na dostępne serwery. Zapewnia on lepkości tylko w ramach sesji transportu. Pakiety w tej samej sesji zostanie przekierowany do tego samego wystąpienia adres IP (DIP) datacenter za punkt końcowy ze zrównoważonym obciążeniem. Przy uruchamianiu klienta w nowej sesji z tym samym źródłowy adres IP, port źródłowy zmiany i powoduje, że ruch komunikować się z innym punktem końcowym DIP.

![skrót na podstawie usługi równoważenia obciążenia](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

Rysunek 1-5-elementowej dystrybucji

## <a name="source-ip-affinity-mode"></a>Tryb koligacji IP źródła

Mamy innego trybu dystrybucji o nazwie koligacji IP źródła (znanej także jako koligacji sesji lub koligacji IP klienta). Moduł równoważenia obciążenia Azure można skonfigurować na potrzeby mapowania ruchu na dostępne serwery 2 parametrów (źródłowy adres IP, docelowy adres IP) lub 3 parametrów (źródłowy adres IP, docelowy adres IP, protokół). Za pomocą koligacji źródłowy adres IP, połączenia inicjowane z tego samego komputera klienckiego prowadzi do tego samego punktu końcowego DIP.

Na poniższym diagramie przedstawiono konfiguracji 2-spójnej kolekcji. Zwróć uwagę, jak krotki 2 jest uruchamiany za pośrednictwem usługi równoważenia obciążenia do maszyny wirtualnej 1 (VM1), który jest następnie kopię zapasową maszyny VM2 i VM3.

![Koligacja sesji](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

Rysunek 2 — dystrybucji krotki 2

Koligacja IP źródła rozwiązuje występuje niezgodność między modułu równoważenia obciążenia Azure i Brama usług pulpitu zdalnego (RD). Teraz można utworzyć farmę serwerów bramy usług pulpitu zdalnego w usłudze jednej chmury.

Inny scenariusz użycia jest przekazywanie nośnika przekazywania danych odbywa się w ramach protokołu UDP, ale dla których płaszczyzny sterowania odbywa się za pośrednictwem protokołu TCP:

* Klient najpierw inicjuje sesję TCP jako publiczny adres równoważenia obciążenia, pobiera kierowane do określonego adresu DIP, ten kanał pozostaje aktywna do monitorowania kondycji połączenia
* Nowa sesja UDP z tego samego komputera klienckiego jest inicjowany do tego samego ze zrównoważonym obciążeniem publicznego punktu końcowego, w tym miejscu oczekuje się, że to połączenie również jest kierowane do tego samego punktu końcowego DIP jak poprzednie połączenie TCP, aby przekazać nośnika mogą być wykonywane na wysoką przepustowość, zachowując jednocześnie kanału kontroli, za pośrednictwem protokołu TCP.

> [!NOTE]
> Gdy zostanie zmieniona zestawu z równoważeniem obciążenia (usuwanie lub dodawanie maszyny wirtualnej), dystrybucji żądań klientów jest przeliczane. Nie są zależne od nowych połączeń z istniejących klientów kończące na tym samym serwerze. Ponadto użycie źródłowy adres IP trybie dystrybucji koligacji może spowodować nierówne rozkładu ruchu. Klienci z systemem za serwery proxy mogą być widoczne jako jedną aplikację unikatowych klientów.

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>Konfigurowanie ustawień koligacji źródłowy adres IP dla modułu równoważenia obciążenia

Dla maszyn wirtualnych programu PowerShell służy do zmiany ustawienia limitu czasu:

Dodawanie punktu końcowego platformy Azure do maszyny wirtualnej i ustaw tryb dystrybucji modułu równoważenia obciążenia

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

Dystrybucji modułu równoważenia obciążenia może być równa sourceIP równoważenia, sourceIPProtocol równoważenia obciążenia 3 parametrów (źródłowy adres IP, docelowy adres IP, protokół) lub Brak Jeśli domyślne zachowanie usługi równoważenia obciążenia 5-elementowej obciążenia 2 parametrów (źródłowy adres IP, docelowy adres IP).

Aby pobrać konfiguracji trybu dystrybucji modułu równoważenia obciążenia punktu końcowego, skorzystaj z następujących:

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

Jeśli nie ma elementu dystrybucji modułu równoważenia obciążenia modułu równoważenia obciążenia Azure używa domyślnego algorytmu 5-elementowej.

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a>Ustaw tryb dystrybucji na zestawu punktów końcowych ze zrównoważonym obciążeniem

Jeśli punkty końcowe są częścią zestawu punktów końcowych ze zrównoważonym obciążeniem, tryb dystrybucji musi być ustawiona na zestawu punktów końcowych ze zrównoważonym obciążeniem:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a>Konfiguracji usługi, aby zmienić tryb dystrybucji w chmurze

Zestaw Azure SDK for .NET 2.5 (mają zostać udostępnione w listopadzie) można wykorzystać do aktualizacji usługi w chmurze. Ustawienia punktu końcowego usługi w chmurze są nawiązywane w csdef. Aby można było zaktualizować tryb dystrybucji modułu równoważenia obciążenia dla wdrożenia usługi w chmurze, wymagane jest uaktualnienie wdrożenia.
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

Można skonfigurować przy użyciu interfejsu API zarządzania usługami dystrybucji modułu równoważenia obciążenia. Upewnij się dodać `x-ms-version` ustawiono nagłówka do wersji `2014-09-01` lub nowszej.

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a>Zaktualizuj konfigurację określonego zestawu z równoważeniem obciążenia we wdrożeniu

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

Wartość dystrybucji modułu równoważenia obciążenia mogą być sourceIP koligacji krotki 2, sourceIPProtocol koligacji krotki 3 lub none (Brak koligacji w przypadku. czyli 5-elementowej)

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
