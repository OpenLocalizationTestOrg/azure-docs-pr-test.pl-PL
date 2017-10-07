---
title: "limit czasu bezczynności TCP usługi równoważenia obciążenia aaaConfigure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 2bf0704b891f708e0a5bd7aa827441930f51cfaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="43694-103">Skonfiguruj ustawienia limitu czasu bezczynności TCP dla usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="43694-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="43694-104">W konfiguracji domyślnej usługi równoważenia obciążenia Azure ma ustawienie limitu czasu bezczynności 4 minut.</span><span class="sxs-lookup"><span data-stu-id="43694-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="43694-105">Jeśli okres aktywności jest dłuższy niż wartość limitu czasu hello, nie ma żadnej gwarancji, że hello TCP lub zachowano sesji HTTP między powitania klienta i usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="43694-105">If a period of inactivity is longer than hello timeout value, there's no guarantee that hello TCP or HTTP session is maintained between hello client and your cloud service.</span></span>

<span data-ttu-id="43694-106">Zamknięcie połączenia hello aplikacji klienta może zostać wyświetlony hello następujący komunikat o błędzie: "hello połączenie podstawowe zostało zamknięte: połączenie, które oczekiwano toobe utrzymywane został zamknięty przez serwer hello."</span><span class="sxs-lookup"><span data-stu-id="43694-106">When hello connection is closed, your client application may receive hello following error message: "hello underlying connection was closed: A connection that was expected toobe kept alive was closed by hello server."</span></span>

<span data-ttu-id="43694-107">Popularną praktyką jest toouse TCP keep-alive.</span><span class="sxs-lookup"><span data-stu-id="43694-107">A common practice is toouse a TCP keep-alive.</span></span> <span data-ttu-id="43694-108">Takie rozwiązanie przechowuje połączenia hello active dłuższy okres.</span><span class="sxs-lookup"><span data-stu-id="43694-108">This practice keeps hello connection active for a longer period.</span></span> <span data-ttu-id="43694-109">Aby uzyskać więcej informacji, zobacz te [przykłady .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="43694-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="43694-110">Włączone keep-alive, pakiety są wysyłane podczas nieaktywności hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="43694-110">With keep-alive enabled, packets are sent during periods of inactivity on hello connection.</span></span> <span data-ttu-id="43694-111">Te pakiety utrzymywania aktywności Sprawdź, czy wartość limitu czasu bezczynności hello jest nie został nigdy osiągnięty i połączenia hello jest obsługiwany przez dłuższy okres.</span><span class="sxs-lookup"><span data-stu-id="43694-111">These keep-alive packets ensure that hello idle timeout value is never reached and hello connection is maintained for a long period.</span></span>

<span data-ttu-id="43694-112">To ustawienie działa tylko w przypadku połączeń przychodzących.</span><span class="sxs-lookup"><span data-stu-id="43694-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="43694-113">tooavoid powoduje utratę połączenia hello, musisz skonfigurować hello TCP keep-alive interwał mniej niż hello limit czasu bezczynności ustawienie lub zwiększ hello bezczynności wartość limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="43694-113">tooavoid losing hello connection, you must configure hello TCP keep-alive with an interval less than hello idle timeout setting or increase hello idle timeout value.</span></span> <span data-ttu-id="43694-114">toosupport takich scenariuszy Dodaliśmy obsługę można skonfigurować limit czasu bezczynności.</span><span class="sxs-lookup"><span data-stu-id="43694-114">toosupport such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="43694-115">Można teraz ustawić czas trwania 4 too30 minut.</span><span class="sxs-lookup"><span data-stu-id="43694-115">You can now set it for a duration of 4 too30 minutes.</span></span>

<span data-ttu-id="43694-116">TCP keep-alive działa dobrze w przypadku scenariuszy, w których czas pracy baterii nie jest ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="43694-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="43694-117">Nie jest zalecane dla aplikacji dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="43694-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="43694-118">Przy użyciu TCP keep-alive w aplikacji mobilnej można szybciej opróżnienia hello baterii urządzenia.</span><span class="sxs-lookup"><span data-stu-id="43694-118">Using a TCP keep-alive in a mobile application can drain hello device battery faster.</span></span>

![Limit czasu TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="43694-120">Witaj następujące sekcje opisują sposób toochange bezczynności ustawienia limitu czasu w przypadku maszyn wirtualnych i usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="43694-120">hello following sections describe how toochange idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a><span data-ttu-id="43694-121">Konfigurowanie limitu czasu TCP hello Twojej poziomie wystąpienia publicznego adresu IP too15 minut</span><span class="sxs-lookup"><span data-stu-id="43694-121">Configure hello TCP timeout for your instance-level public IP too15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="43694-122">Parametr `IdleTimeoutInMinutes` jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="43694-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="43694-123">Jeśli nie jest ustawiona, hello domyślny limit czasu jest 4 minut.</span><span class="sxs-lookup"><span data-stu-id="43694-123">If it is not set, hello default timeout is 4 minutes.</span></span> <span data-ttu-id="43694-124">zakres dopuszczalny limit czasu Hello jest 4 too30 minut.</span><span class="sxs-lookup"><span data-stu-id="43694-124">hello acceptable timeout range is 4 too30 minutes.</span></span>

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="43694-125">Ustaw limit czasu bezczynności hello podczas tworzenia punktu końcowego platformy Azure na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="43694-125">Set hello idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="43694-126">toochange hello limitu czasu dla punktu końcowego, należy użyć następującego hello:</span><span class="sxs-lookup"><span data-stu-id="43694-126">toochange hello timeout setting for an endpoint, use hello following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="43694-127">tooretrieve konfigurację limit czasu bezczynności hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="43694-127">tooretrieve your idle timeout configuration, use hello following command:</span></span>

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="43694-128">Wartość limitu czasu TCP hello na zestaw z równoważeniem obciążenia punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="43694-128">Set hello TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="43694-129">Jeśli punkty końcowe są częścią zestawu o zrównoważonym obciążeniu punktu końcowego, należy ustawić limitu czasu TCP hello hello równoważeniem obciążenia zestawu punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="43694-129">If endpoints are part of a load-balanced endpoint set, hello TCP timeout must be set on hello load-balanced endpoint set.</span></span> <span data-ttu-id="43694-130">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="43694-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="43694-131">Zmień ustawienia limitu czasu dla usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="43694-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="43694-132">Usługi w chmurze można użyć hello tooupdate zestawu Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="43694-132">You can use hello Azure SDK tooupdate your cloud service.</span></span> <span data-ttu-id="43694-133">Wprowadzone ustawienia punktu końcowego usługi w chmurze w pliku csdef hello.</span><span class="sxs-lookup"><span data-stu-id="43694-133">You make endpoint settings for cloud services in hello .csdef file.</span></span> <span data-ttu-id="43694-134">Aktualizowanie limitu czasu TCP hello wdrożenia usługi w chmurze wymaga uaktualnienia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="43694-134">Updating hello TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="43694-135">Wyjątek stanowi, jeśli limit czasu TCP hello jest określony tylko dla publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="43694-135">An exception is if hello TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="43694-136">Ustawienia publicznego adresu IP znajdują się w pliku .cscfg hello i zaktualizować je za pośrednictwem aktualizacji wdrożenia i uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="43694-136">Public IP settings are in hello .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="43694-137">Witaj csdef zmiany ustawień punktu końcowego są:</span><span class="sxs-lookup"><span data-stu-id="43694-137">hello .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="43694-138">zmiany .cscfg Hello hello ustawienia limitu czasu na publiczne adresy IP są następujące:</span><span class="sxs-lookup"><span data-stu-id="43694-138">hello .cscfg changes for hello timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="43694-139">Przykład interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="43694-139">REST API example</span></span>

<span data-ttu-id="43694-140">Limit czasu bezczynności TCP hello można skonfigurować przy użyciu interfejsu API zarządzania usługami hello.</span><span class="sxs-lookup"><span data-stu-id="43694-140">You can configure hello TCP idle timeout by using hello service management API.</span></span> <span data-ttu-id="43694-141">Upewnij się, że hello `x-ms-version` ustawiono nagłówka tooversion `2014-06-01` lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="43694-141">Make sure that hello `x-ms-version` header is set tooversion `2014-06-01` or later.</span></span> <span data-ttu-id="43694-142">Aktualizacja konfiguracji hello hello określony wejściowych punktów końcowych z równoważeniem obciążenia na wszystkich maszynach wirtualnych we wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="43694-142">Update hello configuration of hello specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="43694-143">Żądanie</span><span class="sxs-lookup"><span data-stu-id="43694-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="43694-144">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="43694-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="43694-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43694-145">Next steps</span></span>

[<span data-ttu-id="43694-146">Omówienie usługi równoważenia obciążenia wewnętrznego</span><span class="sxs-lookup"><span data-stu-id="43694-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="43694-147">Przed rozpoczęciem konfigurowania usługi równoważenia obciążenia połączonych z Internetem</span><span class="sxs-lookup"><span data-stu-id="43694-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

<span data-ttu-id="43694-148">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="43694-148">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>
