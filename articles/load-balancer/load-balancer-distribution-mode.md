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
# <a name="configure-hello-distribution-mode-for-load-balancer"></a><span data-ttu-id="65f8e-103">Konfigurowanie trybu dystrybucji powitania dla usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="65f8e-103">Configure hello distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="65f8e-104">Tryb dystrybucji wyznaczania wartości skrótu</span><span class="sxs-lookup"><span data-stu-id="65f8e-104">Hash-based distribution mode</span></span>

<span data-ttu-id="65f8e-105">algorytmem dystrybucji domyślne Hello jest krotka 5 (źródłowy adres IP, port źródłowy, docelowy adres IP, port docelowy protokół typu) skrótów toomap ruchu tooavailable serwerów.</span><span class="sxs-lookup"><span data-stu-id="65f8e-105">hello default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash toomap traffic tooavailable servers.</span></span> <span data-ttu-id="65f8e-106">Zapewnia on lepkości tylko w ramach sesji transportu.</span><span class="sxs-lookup"><span data-stu-id="65f8e-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="65f8e-107">Pakietów hello tej samej sesji zostanie przekierowany toohello wystąpienie tego samego centrum danych adresu IP (DIP) za hello równoważenia obciążenia z punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="65f8e-107">Packets in hello same session will be directed toohello same datacenter IP (DIP) instance behind hello load balanced endpoint.</span></span> <span data-ttu-id="65f8e-108">Po uruchomieniu powitania klienta nowej sesji z hello tego samego źródłowego adresu IP, port źródłowy hello zmiany i powoduje, że hello ruchu toogo tooa różnych DIP punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="65f8e-108">When hello client starts a new session from hello same source IP, hello source port changes and causes hello traffic toogo tooa different DIP endpoint.</span></span>

![skrót na podstawie usługi równoważenia obciążenia](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="65f8e-110">Rysunek 1-5-elementowej dystrybucji</span><span class="sxs-lookup"><span data-stu-id="65f8e-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="65f8e-111">Tryb koligacji IP źródła</span><span class="sxs-lookup"><span data-stu-id="65f8e-111">Source IP affinity mode</span></span>

<span data-ttu-id="65f8e-112">Mamy innego trybu dystrybucji o nazwie koligacji IP źródła (znanej także jako koligacji sesji lub koligacji IP klienta).</span><span class="sxs-lookup"><span data-stu-id="65f8e-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="65f8e-113">Usługi równoważenia obciążenia Azure może być skonfigurowany toouse krotka 2 (źródłowy adres IP, docelowy adres IP) lub 3 parametrów (źródłowy adres IP, docelowy adres IP, protokół) toomap ruchu toohello dostępne serwery.</span><span class="sxs-lookup"><span data-stu-id="65f8e-113">Azure Load Balancer can be configured toouse a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) toomap traffic toohello available servers.</span></span> <span data-ttu-id="65f8e-114">Za pomocą koligacji źródłowy adres IP, połączenia inicjowane z hello sam komputer kliencki przechodzi toohello samego DIP punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="65f8e-114">By using Source IP affinity, connections initiated from hello same client computer goes toohello same DIP endpoint.</span></span>

<span data-ttu-id="65f8e-115">powitania po diagram ilustruje konfiguracji 2-spójnej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="65f8e-115">hello following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="65f8e-116">Zwróć uwagę, jak hello 2-krotki działa za pośrednictwem hello obciążenia równoważenia toovirtual komputera 1 (VM1), który jest następnie kopię zapasową maszyny VM2 i VM3.</span><span class="sxs-lookup"><span data-stu-id="65f8e-116">Notice how hello 2-tuple runs through hello load balancer toovirtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![Koligacja sesji](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="65f8e-118">Rysunek 2 — dystrybucji krotki 2</span><span class="sxs-lookup"><span data-stu-id="65f8e-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="65f8e-119">Koligacja IP źródła rozwiązuje występuje niezgodność między hello modułu równoważenia obciążenia Azure i Brama usług pulpitu zdalnego (RD).</span><span class="sxs-lookup"><span data-stu-id="65f8e-119">Source IP affinity solves an incompatibility between hello Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="65f8e-120">Teraz można utworzyć farmę serwerów bramy usług pulpitu zdalnego w usłudze jednej chmury.</span><span class="sxs-lookup"><span data-stu-id="65f8e-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="65f8e-121">Inny scenariusz użycia jest przekazywanie nośnika hello przekazywania danych odbywa się w ramach protokołu UDP, ale dla których płaszczyzny kontroli hello odbywa się za pośrednictwem protokołu TCP:</span><span class="sxs-lookup"><span data-stu-id="65f8e-121">Another use case scenario is media upload where hello data upload happens through UDP but hello control plane is achieved through TCP:</span></span>

* <span data-ttu-id="65f8e-122">Klient najpierw inicjuje sesję TCP o zrównoważonym obciążeniu toohello publiczny adres, pobiera bezpośrednie tooa, określonych DIP, ten kanał jest kondycja połączenia powitania po lewej stronie toomonitor active</span><span class="sxs-lookup"><span data-stu-id="65f8e-122">A client first initiates a TCP session toohello load balanced public address, gets directed tooa specific DIP, this channel is left active toomonitor hello connection health</span></span>
* <span data-ttu-id="65f8e-123">Nowej sesji UDP z hello, w tym samym komputerze klienckim jest inicjowane toohello publiczny punkt końcowy o zrównoważonym obciążeniu tej samej, tutaj oczekiwania hello jest to połączenie jest również ukierunkowanej toohello tego samego końcowy DIP jako hello poprzednie połączenie TCP, aby przekazać nośnika może być wykonany o wysokiej przepływności, zachowując jednocześnie kanału kontroli, za pośrednictwem protokołu TCP.</span><span class="sxs-lookup"><span data-stu-id="65f8e-123">A new UDP session from hello same client computer is initiated toohello same load balanced public endpoint, hello expectation here is that this connection is also directed toohello same DIP endpoint as hello previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="65f8e-124">W przypadku zmiany zestawu z równoważeniem obciążenia (usuwanie lub dodawanie maszyny wirtualnej), jest przeliczane hello dystrybucji żądań klientów.</span><span class="sxs-lookup"><span data-stu-id="65f8e-124">When a load-balanced set changes (removing or adding a virtual machine), hello distribution of client requests is recomputed.</span></span> <span data-ttu-id="65f8e-125">Nie może zależeć od nowych połączeń z istniejących klientów kończy na powitania sam serwer.</span><span class="sxs-lookup"><span data-stu-id="65f8e-125">You cannot depend on new connections from existing clients ending up at hello same server.</span></span> <span data-ttu-id="65f8e-126">Ponadto użycie źródłowy adres IP trybie dystrybucji koligacji może spowodować nierówne rozkładu ruchu.</span><span class="sxs-lookup"><span data-stu-id="65f8e-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="65f8e-127">Klienci z systemem za serwery proxy mogą być widoczne jako jedną aplikację unikatowych klientów.</span><span class="sxs-lookup"><span data-stu-id="65f8e-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="65f8e-128">Konfigurowanie ustawień koligacji źródłowy adres IP dla modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="65f8e-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="65f8e-129">W przypadku maszyn wirtualnych można użyć ustawienia limitu czasu toochange środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="65f8e-129">For virtual machines, you can use PowerShell toochange timeout settings:</span></span>

<span data-ttu-id="65f8e-130">Dodaj tooa Azure punktu końcowego maszyny wirtualnej i ustaw tryb dystrybucji modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="65f8e-130">Add an Azure endpoint tooa Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="65f8e-131">Dystrybucji modułu równoważenia obciążenia można ustawić toosourceIP równoważenia, sourceIPProtocol równoważenia obciążenia 3 parametrów (źródłowy adres IP, docelowy adres IP, protokół) lub brak Chcąc hello domyślne zachowanie usługi równoważenia obciążenia 5-elementowej obciążenia 2 parametrów (źródłowy adres IP, docelowy adres IP).</span><span class="sxs-lookup"><span data-stu-id="65f8e-131">LoadBalancerDistribution can be set toosourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want hello default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="65f8e-132">Użyj powitania po tooretrieve konfiguracji trybu dystrybucji modułu równoważenia obciążenia punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="65f8e-132">Use hello following tooretrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="65f8e-133">Jeśli nie ma hello element dystrybucji modułu równoważenia obciążenia modułu równoważenia obciążenia Azure hello używa hello domyślny algorytm 5-elementowej.</span><span class="sxs-lookup"><span data-stu-id="65f8e-133">If hello LoadBalancerDistribution element is not present then hello Azure Load balancer uses hello default 5-tuple algorithm.</span></span>

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="65f8e-134">Ustaw tryb dystrybucji hello na zestawu punktów końcowych ze zrównoważonym obciążeniem</span><span class="sxs-lookup"><span data-stu-id="65f8e-134">Set hello Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="65f8e-135">Jeśli punkty końcowe są częścią zestawu punktów końcowych ze zrównoważonym obciążeniem, należy ustawić tryb rozkładu hello zestawu punktów końcowych ze zrównoważonym obciążeniem hello:</span><span class="sxs-lookup"><span data-stu-id="65f8e-135">If endpoints are part of a load balanced endpoint set, hello distribution mode must be set on hello load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a><span data-ttu-id="65f8e-136">Tryb dystrybucji toochange konfiguracji usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="65f8e-136">Cloud Service configuration toochange distribution mode</span></span>

<span data-ttu-id="65f8e-137">Można wykorzystać hello Azure SDK dla platformy .NET 2.5 (toobe wydanej w listopadzie) tooupdate usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="65f8e-137">You can leverage hello Azure SDK for .NET 2.5 (toobe released in November) tooupdate your Cloud Service.</span></span> <span data-ttu-id="65f8e-138">Ustawienia punktu końcowego usługi w chmurze są nawiązywane w hello csdef.</span><span class="sxs-lookup"><span data-stu-id="65f8e-138">Endpoint settings for Cloud Services are made in hello .csdef.</span></span> <span data-ttu-id="65f8e-139">W kolejności tooupdate hello równoważenia trybu rozkładu obciążenia na wdrożenie usługi w chmurze wymagane jest uaktualnienie wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="65f8e-139">In order tooupdate hello load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="65f8e-140">Oto przykład csdef zmiany ustawień punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="65f8e-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="65f8e-141">Przykładowy interfejs API</span><span class="sxs-lookup"><span data-stu-id="65f8e-141">API example</span></span>

<span data-ttu-id="65f8e-142">Można skonfigurować dystrybucji modułu równoważenia obciążenia hello przy użyciu interfejsu API zarządzania usługami hello.</span><span class="sxs-lookup"><span data-stu-id="65f8e-142">You can configure hello load balancer distribution using hello service management API.</span></span> <span data-ttu-id="65f8e-143">Upewnij się, że hello tooadd `x-ms-version` ustawiono nagłówka tooversion `2014-09-01` lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="65f8e-143">Make sure tooadd hello `x-ms-version` header is set tooversion `2014-09-01` or higher.</span></span>

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="65f8e-144">Aktualizacja konfiguracji hello hello określony zestaw o zrównoważonym obciążeniu we wdrożeniu</span><span class="sxs-lookup"><span data-stu-id="65f8e-144">Update hello configuration of hello specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="65f8e-145">Przykładowe żądanie</span><span class="sxs-lookup"><span data-stu-id="65f8e-145">Request example</span></span>

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

<span data-ttu-id="65f8e-146">wartość Hello dystrybucji modułu równoważenia obciążenia może być sourceIP koligacji krotki 2, sourceIPProtocol koligacji krotki 3 lub none (Brak koligacji w przypadku.</span><span class="sxs-lookup"><span data-stu-id="65f8e-146">hello value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="65f8e-147">czyli 5-elementowej)</span><span class="sxs-lookup"><span data-stu-id="65f8e-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="65f8e-148">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="65f8e-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="65f8e-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="65f8e-149">Next Steps</span></span>

[<span data-ttu-id="65f8e-150">Omówienie usługi równoważenia obciążenia wewnętrznego</span><span class="sxs-lookup"><span data-stu-id="65f8e-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="65f8e-151">Przed rozpoczęciem konfigurowania internetowy modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="65f8e-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

<span data-ttu-id="65f8e-152">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="65f8e-152">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
