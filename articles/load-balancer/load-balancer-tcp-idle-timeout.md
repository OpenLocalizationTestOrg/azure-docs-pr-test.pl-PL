---
title: "Skonfiguruj limit czasu bezczynności TCP usługi równoważenia obciążenia | Dokumentacja firmy Microsoft"
description: "Skonfiguruj limit czasu bezczynności TCP usługi równoważenia obciążenia"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 4625c6a8-5725-47ce-81db-4fa3bd055891
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: d040fe6580b8ae777aecc9dd385ed33861530c38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="49d45-103">Skonfiguruj ustawienia limitu czasu bezczynności TCP dla usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="49d45-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="49d45-104">W konfiguracji domyślnej usługi równoważenia obciążenia Azure ma ustawienie limitu czasu bezczynności 4 minut.</span><span class="sxs-lookup"><span data-stu-id="49d45-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="49d45-105">Jeśli okres aktywności jest dłuższy niż wartość limitu czasu, nie ma żadnej gwarancji, sesji TCP lub HTTP jest zachowywane między klientem i usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="49d45-105">If a period of inactivity is longer than the timeout value, there's no guarantee that the TCP or HTTP session is maintained between the client and your cloud service.</span></span>

<span data-ttu-id="49d45-106">Gdy połączenie jest zamknięte, aplikacja kliencka może zostać wyświetlony następujący komunikat o błędzie: "Połączenie podstawowe zostało zakończone: połączenie, które miało być aktywne zostało zamknięte przez serwer."</span><span class="sxs-lookup"><span data-stu-id="49d45-106">When the connection is closed, your client application may receive the following error message: "The underlying connection was closed: A connection that was expected to be kept alive was closed by the server."</span></span>

<span data-ttu-id="49d45-107">Popularną praktyką jest Użyj TCP keep-alive.</span><span class="sxs-lookup"><span data-stu-id="49d45-107">A common practice is to use a TCP keep-alive.</span></span> <span data-ttu-id="49d45-108">Takie rozwiązanie pozostawia połączenie jako aktywne przez dłuższy czas.</span><span class="sxs-lookup"><span data-stu-id="49d45-108">This practice keeps the connection active for a longer period.</span></span> <span data-ttu-id="49d45-109">Aby uzyskać więcej informacji, zobacz te [przykłady .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="49d45-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="49d45-110">Włączone keep-alive, pakiety są wysyłane podczas nieaktywności dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="49d45-110">With keep-alive enabled, packets are sent during periods of inactivity on the connection.</span></span> <span data-ttu-id="49d45-111">Te pakiety utrzymywania aktywności Sprawdź, czy wartość limitu czasu bezczynności został nigdy osiągnięty i połączenie jest obsługiwany przez dłuższy okres.</span><span class="sxs-lookup"><span data-stu-id="49d45-111">These keep-alive packets ensure that the idle timeout value is never reached and the connection is maintained for a long period.</span></span>

<span data-ttu-id="49d45-112">To ustawienie działa tylko w przypadku połączeń przychodzących.</span><span class="sxs-lookup"><span data-stu-id="49d45-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="49d45-113">Aby uniknąć utraty połączenia, możesz skonfigurować interwał mniejsza niż wartość ustawienia limit czasu bezczynności keep-alive TCP lub zwiększ wartość limitu czasu bezczynności.</span><span class="sxs-lookup"><span data-stu-id="49d45-113">To avoid losing the connection, you must configure the TCP keep-alive with an interval less than the idle timeout setting or increase the idle timeout value.</span></span> <span data-ttu-id="49d45-114">Do obsługi tych scenariuszy, dodano obsługę można skonfigurować limit czasu bezczynności.</span><span class="sxs-lookup"><span data-stu-id="49d45-114">To support such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="49d45-115">Można teraz ustawić czas od 4 do 30 minut.</span><span class="sxs-lookup"><span data-stu-id="49d45-115">You can now set it for a duration of 4 to 30 minutes.</span></span>

<span data-ttu-id="49d45-116">TCP keep-alive działa dobrze w przypadku scenariuszy, w których czas pracy baterii nie jest ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="49d45-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="49d45-117">Nie jest zalecane dla aplikacji dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="49d45-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="49d45-118">Przy użyciu TCP keep-alive w aplikacji mobilnej można szybciej opróżnienia baterii urządzenia.</span><span class="sxs-lookup"><span data-stu-id="49d45-118">Using a TCP keep-alive in a mobile application can drain the device battery faster.</span></span>

![Limit czasu TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="49d45-120">W poniższych sekcjach opisano sposób zmienić ustawienia limitu czasu bezczynności w przypadku maszyn wirtualnych i usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="49d45-120">The following sections describe how to change idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-the-tcp-timeout-for-your-instance-level-public-ip-to-15-minutes"></a><span data-ttu-id="49d45-121">Konfigurowanie limitu czasu protokołu TCP dla Twojego poziomie wystąpienia publicznego adresu IP na 15 minut</span><span class="sxs-lookup"><span data-stu-id="49d45-121">Configure the TCP timeout for your instance-level public IP to 15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="49d45-122">Parametr `IdleTimeoutInMinutes` jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="49d45-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="49d45-123">Jeśli nie jest ustawiona, domyślny limit czasu jest 4 minut.</span><span class="sxs-lookup"><span data-stu-id="49d45-123">If it is not set, the default timeout is 4 minutes.</span></span> <span data-ttu-id="49d45-124">Zakres dopuszczalny limit czasu wynosi 4 do 30 minut.</span><span class="sxs-lookup"><span data-stu-id="49d45-124">The acceptable timeout range is 4 to 30 minutes.</span></span>

## <a name="set-the-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="49d45-125">Ustaw limit czasu bezczynności podczas tworzenia punktu końcowego platformy Azure na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="49d45-125">Set the idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="49d45-126">Aby zmienić ustawienia limitu czasu dla punktu końcowego, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="49d45-126">To change the timeout setting for an endpoint, use the following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="49d45-127">Aby uzyskać konfigurację limit czasu bezczynności, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="49d45-127">To retrieve your idle timeout configuration, use the following command:</span></span>

    PS C:\> Get-AzureVM -ServiceName "MyService" -Name "MyVM" | Get-AzureEndpoint
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

## <a name="set-the-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="49d45-128">Ustawianie limitu czasu TCP na zestaw z równoważeniem obciążenia punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="49d45-128">Set the TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="49d45-129">Jeśli punkty końcowe są częścią zestawu o zrównoważonym obciążeniu punktu końcowego, należy ustawić limitu czasu TCP zestaw z równoważeniem obciążenia punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="49d45-129">If endpoints are part of a load-balanced endpoint set, the TCP timeout must be set on the load-balanced endpoint set.</span></span> <span data-ttu-id="49d45-130">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="49d45-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="49d45-131">Zmień ustawienia limitu czasu dla usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="49d45-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="49d45-132">Zestaw SDK usługi Azure można użyć do aktualizacji usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="49d45-132">You can use the Azure SDK to update your cloud service.</span></span> <span data-ttu-id="49d45-133">Wprowadzone ustawienia punktu końcowego usługi w chmurze w pliku csdef.</span><span class="sxs-lookup"><span data-stu-id="49d45-133">You make endpoint settings for cloud services in the .csdef file.</span></span> <span data-ttu-id="49d45-134">Aktualizowanie limitu czasu protokołu TCP dla wdrożenia usługi w chmurze wymaga uaktualnienia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="49d45-134">Updating the TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="49d45-135">Wyjątek stanowi, jeśli limit czasu protokołu TCP jest określony tylko dla publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="49d45-135">An exception is if the TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="49d45-136">Ustawienia publicznego adresu IP znajdują się w pliku .cscfg i zaktualizować je za pośrednictwem aktualizacji wdrożenia i uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="49d45-136">Public IP settings are in the .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="49d45-137">Zmiany csdef ustawień punktu końcowego są następujące:</span><span class="sxs-lookup"><span data-stu-id="49d45-137">The .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="49d45-138">Zmiany .cscfg ustawienia limitu czasu na publiczne adresy IP są następujące:</span><span class="sxs-lookup"><span data-stu-id="49d45-138">The .cscfg changes for the timeout setting on public IPs are:</span></span>

```xml
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

## <a name="rest-api-example"></a><span data-ttu-id="49d45-139">Przykład interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="49d45-139">REST API example</span></span>

<span data-ttu-id="49d45-140">Limit czasu bezczynności TCP można skonfigurować przy użyciu interfejsu API zarządzania usługami.</span><span class="sxs-lookup"><span data-stu-id="49d45-140">You can configure the TCP idle timeout by using the service management API.</span></span> <span data-ttu-id="49d45-141">Upewnij się, że `x-ms-version` ustawiono nagłówka do wersji `2014-06-01` lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="49d45-141">Make sure that the `x-ms-version` header is set to version `2014-06-01` or later.</span></span> <span data-ttu-id="49d45-142">Zaktualizuj konfigurację określonego równoważeniem obciążenia wejściowych punktów końcowych na wszystkich maszynach wirtualnych we wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="49d45-142">Update the configuration of the specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="49d45-143">Żądanie</span><span class="sxs-lookup"><span data-stu-id="49d45-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="49d45-144">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="49d45-144">Response</span></span>

```xml
<LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <InputEndpoint>
    <LoadBalancedEndpointSetName>endpoint-set-name</LoadBalancedEndpointSetName>
    <LocalPort>local-port-number</LocalPort>
    <Port>external-port-number</Port>
    <LoadBalancerProbe>
        <Path>path-of-probe</Path>
        <Port>port-assigned-to-probe</Port>
        <Protocol>probe-protocol</Protocol>
        <IntervalInSeconds>interval-of-probe</IntervalInSeconds>
        <TimeoutInSeconds>timeout-for-probe</TimeoutInSeconds>
    </LoadBalancerProbe>
    <LoadBalancerName>name-of-internal-loadbalancer</LoadBalancerName>
    <Protocol>endpoint-protocol</Protocol>
    <IdleTimeoutInMinutes>15</IdleTimeoutInMinutes>
    <EnableDirectServerReturn>enable-direct-server-return</EnableDirectServerReturn>
    <EndpointACL>
        <Rules>
        <Rule>
            <Order>priority-of-the-rule</Order>
            <Action>permit-rule</Action>
            <RemoteSubnet>subnet-of-the-rule</RemoteSubnet>
            <Description>description-of-the-rule</Description>
        </Rule>
        </Rules>
    </EndpointACL>
    </InputEndpoint>
</LoadBalancedEndpointList>
```

## <a name="next-steps"></a><span data-ttu-id="49d45-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="49d45-145">Next steps</span></span>

[<span data-ttu-id="49d45-146">Omówienie usługi równoważenia obciążenia wewnętrznego</span><span class="sxs-lookup"><span data-stu-id="49d45-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="49d45-147">Przed rozpoczęciem konfigurowania usługi równoważenia obciążenia połączonych z Internetem</span><span class="sxs-lookup"><span data-stu-id="49d45-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

<span data-ttu-id="49d45-148">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="49d45-148">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>
