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
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a>Skonfiguruj ustawienia limitu czasu bezczynności TCP dla usługi równoważenia obciążenia Azure

W konfiguracji domyślnej usługi równoważenia obciążenia Azure ma ustawienie limitu czasu bezczynności 4 minut. Jeśli okres aktywności jest dłuższy niż wartość limitu czasu hello, nie ma żadnej gwarancji, że hello TCP lub zachowano sesji HTTP między powitania klienta i usługi w chmurze.

Zamknięcie połączenia hello aplikacji klienta może zostać wyświetlony hello następujący komunikat o błędzie: "hello połączenie podstawowe zostało zamknięte: połączenie, które oczekiwano toobe utrzymywane został zamknięty przez serwer hello."

Popularną praktyką jest toouse TCP keep-alive. Takie rozwiązanie przechowuje połączenia hello active dłuższy okres. Aby uzyskać więcej informacji, zobacz te [przykłady .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx). Włączone keep-alive, pakiety są wysyłane podczas nieaktywności hello połączenia. Te pakiety utrzymywania aktywności Sprawdź, czy wartość limitu czasu bezczynności hello jest nie został nigdy osiągnięty i połączenia hello jest obsługiwany przez dłuższy okres.

To ustawienie działa tylko w przypadku połączeń przychodzących. tooavoid powoduje utratę połączenia hello, musisz skonfigurować hello TCP keep-alive interwał mniej niż hello limit czasu bezczynności ustawienie lub zwiększ hello bezczynności wartość limitu czasu. toosupport takich scenariuszy Dodaliśmy obsługę można skonfigurować limit czasu bezczynności. Można teraz ustawić czas trwania 4 too30 minut.

TCP keep-alive działa dobrze w przypadku scenariuszy, w których czas pracy baterii nie jest ograniczenie. Nie jest zalecane dla aplikacji dla urządzeń przenośnych. Przy użyciu TCP keep-alive w aplikacji mobilnej można szybciej opróżnienia hello baterii urządzenia.

![Limit czasu TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

Witaj następujące sekcje opisują sposób toochange bezczynności ustawienia limitu czasu w przypadku maszyn wirtualnych i usług w chmurze.

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a>Konfigurowanie limitu czasu TCP hello Twojej poziomie wystąpienia publicznego adresu IP too15 minut

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

Parametr `IdleTimeoutInMinutes` jest opcjonalny. Jeśli nie jest ustawiona, hello domyślny limit czasu jest 4 minut. zakres dopuszczalny limit czasu Hello jest 4 too30 minut.

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a>Ustaw limit czasu bezczynności hello podczas tworzenia punktu końcowego platformy Azure na maszynie wirtualnej

toochange hello limitu czasu dla punktu końcowego, należy użyć następującego hello:

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

tooretrieve konfigurację limit czasu bezczynności hello Użyj następującego polecenia:

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a>Wartość limitu czasu TCP hello na zestaw z równoważeniem obciążenia punktu końcowego

Jeśli punkty końcowe są częścią zestawu o zrównoważonym obciążeniu punktu końcowego, należy ustawić limitu czasu TCP hello hello równoważeniem obciążenia zestawu punktów końcowych. Na przykład:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a>Zmień ustawienia limitu czasu dla usług w chmurze

Usługi w chmurze można użyć hello tooupdate zestawu Azure SDK. Wprowadzone ustawienia punktu końcowego usługi w chmurze w pliku csdef hello. Aktualizowanie limitu czasu TCP hello wdrożenia usługi w chmurze wymaga uaktualnienia wdrożenia. Wyjątek stanowi, jeśli limit czasu TCP hello jest określony tylko dla publicznego adresu IP. Ustawienia publicznego adresu IP znajdują się w pliku .cscfg hello i zaktualizować je za pośrednictwem aktualizacji wdrożenia i uaktualnienia.

Witaj csdef zmiany ustawień punktu końcowego są:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

zmiany .cscfg Hello hello ustawienia limitu czasu na publiczne adresy IP są następujące:

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

## <a name="rest-api-example"></a>Przykład interfejsu API REST

Limit czasu bezczynności TCP hello można skonfigurować przy użyciu interfejsu API zarządzania usługami hello. Upewnij się, że hello `x-ms-version` ustawiono nagłówka tooversion `2014-06-01` lub nowszym. Aktualizacja konfiguracji hello hello określony wejściowych punktów końcowych z równoważeniem obciążenia na wszystkich maszynach wirtualnych we wdrożeniu.

### <a name="request"></a>Żądanie

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a>Odpowiedź

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

## <a name="next-steps"></a>Następne kroki

[Omówienie usługi równoważenia obciążenia wewnętrznego](load-balancer-internal-overview.md)

[Przed rozpoczęciem konfigurowania usługi równoważenia obciążenia połączonych z Internetem](load-balancer-get-started-internet-arm-ps.md)

[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)
