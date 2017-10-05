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
# <a name="configure-the-distribution-mode-for-load-balancer"></a><span data-ttu-id="43bf9-103">Konfigurowanie trybu dystrybucji dla usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="43bf9-103">Configure the distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="43bf9-104">Tryb dystrybucji wyznaczania wartości skrótu</span><span class="sxs-lookup"><span data-stu-id="43bf9-104">Hash-based distribution mode</span></span>

<span data-ttu-id="43bf9-105">Domyślnym algorytmem dystrybucji jest krotka 5 (źródłowy adres IP, port źródłowy, docelowy adres IP, port docelowy protokół typu) skrót do mapowania ruchu na dostępne serwery.</span><span class="sxs-lookup"><span data-stu-id="43bf9-105">The default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash to map traffic to available servers.</span></span> <span data-ttu-id="43bf9-106">Zapewnia on lepkości tylko w ramach sesji transportu.</span><span class="sxs-lookup"><span data-stu-id="43bf9-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="43bf9-107">Pakiety w tej samej sesji zostanie przekierowany do tego samego wystąpienia adres IP (DIP) datacenter za punkt końcowy ze zrównoważonym obciążeniem.</span><span class="sxs-lookup"><span data-stu-id="43bf9-107">Packets in the same session will be directed to the same datacenter IP (DIP) instance behind the load balanced endpoint.</span></span> <span data-ttu-id="43bf9-108">Przy uruchamianiu klienta w nowej sesji z tym samym źródłowy adres IP, port źródłowy zmiany i powoduje, że ruch komunikować się z innym punktem końcowym DIP.</span><span class="sxs-lookup"><span data-stu-id="43bf9-108">When the client starts a new session from the same source IP, the source port changes and causes the traffic to go to a different DIP endpoint.</span></span>

![skrót na podstawie usługi równoważenia obciążenia](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="43bf9-110">Rysunek 1-5-elementowej dystrybucji</span><span class="sxs-lookup"><span data-stu-id="43bf9-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="43bf9-111">Tryb koligacji IP źródła</span><span class="sxs-lookup"><span data-stu-id="43bf9-111">Source IP affinity mode</span></span>

<span data-ttu-id="43bf9-112">Mamy innego trybu dystrybucji o nazwie koligacji IP źródła (znanej także jako koligacji sesji lub koligacji IP klienta).</span><span class="sxs-lookup"><span data-stu-id="43bf9-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="43bf9-113">Moduł równoważenia obciążenia Azure można skonfigurować na potrzeby mapowania ruchu na dostępne serwery 2 parametrów (źródłowy adres IP, docelowy adres IP) lub 3 parametrów (źródłowy adres IP, docelowy adres IP, protokół).</span><span class="sxs-lookup"><span data-stu-id="43bf9-113">Azure Load Balancer can be configured to use a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) to map traffic to the available servers.</span></span> <span data-ttu-id="43bf9-114">Za pomocą koligacji źródłowy adres IP, połączenia inicjowane z tego samego komputera klienckiego prowadzi do tego samego punktu końcowego DIP.</span><span class="sxs-lookup"><span data-stu-id="43bf9-114">By using Source IP affinity, connections initiated from the same client computer goes to the same DIP endpoint.</span></span>

<span data-ttu-id="43bf9-115">Na poniższym diagramie przedstawiono konfiguracji 2-spójnej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="43bf9-115">The following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="43bf9-116">Zwróć uwagę, jak krotki 2 jest uruchamiany za pośrednictwem usługi równoważenia obciążenia do maszyny wirtualnej 1 (VM1), który jest następnie kopię zapasową maszyny VM2 i VM3.</span><span class="sxs-lookup"><span data-stu-id="43bf9-116">Notice how the 2-tuple runs through the load balancer to virtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![Koligacja sesji](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="43bf9-118">Rysunek 2 — dystrybucji krotki 2</span><span class="sxs-lookup"><span data-stu-id="43bf9-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="43bf9-119">Koligacja IP źródła rozwiązuje występuje niezgodność między modułu równoważenia obciążenia Azure i Brama usług pulpitu zdalnego (RD).</span><span class="sxs-lookup"><span data-stu-id="43bf9-119">Source IP affinity solves an incompatibility between the Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="43bf9-120">Teraz można utworzyć farmę serwerów bramy usług pulpitu zdalnego w usłudze jednej chmury.</span><span class="sxs-lookup"><span data-stu-id="43bf9-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="43bf9-121">Inny scenariusz użycia jest przekazywanie nośnika przekazywania danych odbywa się w ramach protokołu UDP, ale dla których płaszczyzny sterowania odbywa się za pośrednictwem protokołu TCP:</span><span class="sxs-lookup"><span data-stu-id="43bf9-121">Another use case scenario is media upload where the data upload happens through UDP but the control plane is achieved through TCP:</span></span>

* <span data-ttu-id="43bf9-122">Klient najpierw inicjuje sesję TCP jako publiczny adres równoważenia obciążenia, pobiera kierowane do określonego adresu DIP, ten kanał pozostaje aktywna do monitorowania kondycji połączenia</span><span class="sxs-lookup"><span data-stu-id="43bf9-122">A client first initiates a TCP session to the load balanced public address, gets directed to a specific DIP, this channel is left active to monitor the connection health</span></span>
* <span data-ttu-id="43bf9-123">Nowa sesja UDP z tego samego komputera klienckiego jest inicjowany do tego samego ze zrównoważonym obciążeniem publicznego punktu końcowego, w tym miejscu oczekuje się, że to połączenie również jest kierowane do tego samego punktu końcowego DIP jak poprzednie połączenie TCP, aby przekazać nośnika mogą być wykonywane na wysoką przepustowość, zachowując jednocześnie kanału kontroli, za pośrednictwem protokołu TCP.</span><span class="sxs-lookup"><span data-stu-id="43bf9-123">A new UDP session from the same client computer is initiated to the same load balanced public endpoint, the expectation here is that this connection is also directed to the same DIP endpoint as the previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="43bf9-124">Gdy zostanie zmieniona zestawu z równoważeniem obciążenia (usuwanie lub dodawanie maszyny wirtualnej), dystrybucji żądań klientów jest przeliczane.</span><span class="sxs-lookup"><span data-stu-id="43bf9-124">When a load-balanced set changes (removing or adding a virtual machine), the distribution of client requests is recomputed.</span></span> <span data-ttu-id="43bf9-125">Nie są zależne od nowych połączeń z istniejących klientów kończące na tym samym serwerze.</span><span class="sxs-lookup"><span data-stu-id="43bf9-125">You cannot depend on new connections from existing clients ending up at the same server.</span></span> <span data-ttu-id="43bf9-126">Ponadto użycie źródłowy adres IP trybie dystrybucji koligacji może spowodować nierówne rozkładu ruchu.</span><span class="sxs-lookup"><span data-stu-id="43bf9-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="43bf9-127">Klienci z systemem za serwery proxy mogą być widoczne jako jedną aplikację unikatowych klientów.</span><span class="sxs-lookup"><span data-stu-id="43bf9-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="43bf9-128">Konfigurowanie ustawień koligacji źródłowy adres IP dla modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="43bf9-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="43bf9-129">Dla maszyn wirtualnych programu PowerShell służy do zmiany ustawienia limitu czasu:</span><span class="sxs-lookup"><span data-stu-id="43bf9-129">For virtual machines, you can use PowerShell to change timeout settings:</span></span>

<span data-ttu-id="43bf9-130">Dodawanie punktu końcowego platformy Azure do maszyny wirtualnej i ustaw tryb dystrybucji modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="43bf9-130">Add an Azure endpoint to a Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="43bf9-131">Dystrybucji modułu równoważenia obciążenia może być równa sourceIP równoważenia, sourceIPProtocol równoważenia obciążenia 3 parametrów (źródłowy adres IP, docelowy adres IP, protokół) lub Brak Jeśli domyślne zachowanie usługi równoważenia obciążenia 5-elementowej obciążenia 2 parametrów (źródłowy adres IP, docelowy adres IP).</span><span class="sxs-lookup"><span data-stu-id="43bf9-131">LoadBalancerDistribution can be set to sourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want the default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="43bf9-132">Aby pobrać konfiguracji trybu dystrybucji modułu równoważenia obciążenia punktu końcowego, skorzystaj z następujących:</span><span class="sxs-lookup"><span data-stu-id="43bf9-132">Use the following to retrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="43bf9-133">Jeśli nie ma elementu dystrybucji modułu równoważenia obciążenia modułu równoważenia obciążenia Azure używa domyślnego algorytmu 5-elementowej.</span><span class="sxs-lookup"><span data-stu-id="43bf9-133">If the LoadBalancerDistribution element is not present then the Azure Load balancer uses the default 5-tuple algorithm.</span></span>

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="43bf9-134">Ustaw tryb dystrybucji na zestawu punktów końcowych ze zrównoważonym obciążeniem</span><span class="sxs-lookup"><span data-stu-id="43bf9-134">Set the Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="43bf9-135">Jeśli punkty końcowe są częścią zestawu punktów końcowych ze zrównoważonym obciążeniem, tryb dystrybucji musi być ustawiona na zestawu punktów końcowych ze zrównoważonym obciążeniem:</span><span class="sxs-lookup"><span data-stu-id="43bf9-135">If endpoints are part of a load balanced endpoint set, the distribution mode must be set on the load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a><span data-ttu-id="43bf9-136">Konfiguracji usługi, aby zmienić tryb dystrybucji w chmurze</span><span class="sxs-lookup"><span data-stu-id="43bf9-136">Cloud Service configuration to change distribution mode</span></span>

<span data-ttu-id="43bf9-137">Zestaw Azure SDK for .NET 2.5 (mają zostać udostępnione w listopadzie) można wykorzystać do aktualizacji usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="43bf9-137">You can leverage the Azure SDK for .NET 2.5 (to be released in November) to update your Cloud Service.</span></span> <span data-ttu-id="43bf9-138">Ustawienia punktu końcowego usługi w chmurze są nawiązywane w csdef.</span><span class="sxs-lookup"><span data-stu-id="43bf9-138">Endpoint settings for Cloud Services are made in the .csdef.</span></span> <span data-ttu-id="43bf9-139">Aby można było zaktualizować tryb dystrybucji modułu równoważenia obciążenia dla wdrożenia usługi w chmurze, wymagane jest uaktualnienie wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="43bf9-139">In order to update the load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="43bf9-140">Oto przykład csdef zmiany ustawień punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="43bf9-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="43bf9-141">Przykładowy interfejs API</span><span class="sxs-lookup"><span data-stu-id="43bf9-141">API example</span></span>

<span data-ttu-id="43bf9-142">Można skonfigurować przy użyciu interfejsu API zarządzania usługami dystrybucji modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="43bf9-142">You can configure the load balancer distribution using the service management API.</span></span> <span data-ttu-id="43bf9-143">Upewnij się dodać `x-ms-version` ustawiono nagłówka do wersji `2014-09-01` lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="43bf9-143">Make sure to add the `x-ms-version` header is set to version `2014-09-01` or higher.</span></span>

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="43bf9-144">Zaktualizuj konfigurację określonego zestawu z równoważeniem obciążenia we wdrożeniu</span><span class="sxs-lookup"><span data-stu-id="43bf9-144">Update the configuration of the specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="43bf9-145">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="43bf9-145">Request example</span></span>

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

<span data-ttu-id="43bf9-146">Wartość dystrybucji modułu równoważenia obciążenia mogą być sourceIP koligacji krotki 2, sourceIPProtocol koligacji krotki 3 lub none (Brak koligacji w przypadku.</span><span class="sxs-lookup"><span data-stu-id="43bf9-146">The value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="43bf9-147">czyli 5-elementowej)</span><span class="sxs-lookup"><span data-stu-id="43bf9-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="43bf9-148">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="43bf9-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="43bf9-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43bf9-149">Next Steps</span></span>

[<span data-ttu-id="43bf9-150">Omówienie usługi równoważenia obciążenia wewnętrznego</span><span class="sxs-lookup"><span data-stu-id="43bf9-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="43bf9-151">Przed rozpoczęciem konfigurowania internetowy modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="43bf9-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

<span data-ttu-id="43bf9-152">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="43bf9-152">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
