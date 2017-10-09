---
title: "aaaCreate, uruchomić lub usunąć bramę aplikacji | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate, skonfigurować, uruchomić i usunąć bramę aplikacji Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a>Tworzenie, uruchamianie i usuwanie bramy aplikacji przy użyciu programu PowerShell 

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-gateway-arm.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-create-gateway.md)
> * [Szablon usługi Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Interfejs wiersza polecenia platformy Azure](application-gateway-create-gateway-cli.md)

Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7. Zapewnia on trybu failover, wydajności routingu żądań HTTP między różnymi serwerami, czy znajdują się w chmurze hello lub lokalnie. Usługa Application Gateway zapewnia wiele funkcji kontrolera dostarczania aplikacji (ADC, Application Delivery Controller), w tym między innymi równoważenie obciążenia HTTP, koligację sesji na podstawie plików cookie, odciążanie protokołu Secure Sockets Layer (SSL), niestandardowe sondy kondycji i obsługę wielu witryn. odwiedź toofind pełną listę obsługiwanych funkcji [omówienie bramy aplikacji](application-gateway-introduction.md)

W tym artykule przedstawiono toocreate kroki hello, skonfiguruj start i usunąć bramę aplikacji.

## <a name="before-you-begin"></a>Przed rozpoczęciem

1. Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web. Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).
2. Jeśli masz istniejącą sieć wirtualną, wybierz istniejącą podsieć pusty albo utwórz nową podsieć w istniejącej sieci wirtualnej wyłącznie do użytku przez bramę aplikacji hello. Nie można wdrożyć hello aplikacji bramy tooa innej sieci wirtualnej niż hello zasobów ma toodeploy za bramy aplikacji hello chyba że używana jest sieć wirtualną komunikacji równorzędnej. toolearn więcej odwiedź [równorzędna sieci wirtualnej](../virtual-network/virtual-network-peering-overview.md)
3. Sprawdź, czy masz działającą sieć wirtualną z prawidłową podsiecią. Upewnij się, że nie maszyny wirtualne lub wdrożenia chmury z hello podsieci. Brama aplikacji Hello należy samodzielnie w podsieci sieci wirtualnej.
4. Skonfigurowanie bramy aplikacji hello toouse serwerów Hello musi istnieć lub mieć przypisane ich punkty końcowe utworzone w sieci wirtualnej hello lub z publicznego adresu IP/VIP.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Co to jest wymagana toocreate bramę aplikacji?

Jeśli używasz hello `New-AzureApplicationGateway` bramy aplikacji hello toocreate polecenia, konfiguracja nie jest ustawiona na tym etapie i hello nowo utworzony zasób są skonfigurowane przy użyciu XML lub obiekt konfiguracji.

Witaj wartości są następujące:

* **Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello. wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.
* **Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie. Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.
* **Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello. Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.
* **Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).
* **Reguła:** reguła hello wiąże odbiornika hello i hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika.

## <a name="create-an-application-gateway"></a>Tworzenie bramy aplikacji

toocreate bramę aplikacji:

1. Utwórz zasób bramy aplikacji.
2. Utwórz konfiguracyjny plik XML lub obiekt konfiguracji.
3. Zatwierdź toohello konfiguracji hello nowo utworzony zasób bramy aplikacji.

> [!NOTE]
> Jeśli potrzebujesz tooconfigure sondowania niestandardowych dla bramy aplikacji, zobacz [Utwórz bramę aplikacji z niestandardowego sond przy użyciu programu PowerShell](application-gateway-create-probe-classic-ps.md). Aby dowiedzieć się więcej, zapoznaj się z informacjami na temat [sond niestandardowych i monitorowania kondycji](application-gateway-probe-overview.md).

![Przykładowy scenariusz][scenario]

### <a name="create-an-application-gateway-resource"></a>Tworzenie zasobu bramy aplikacji

toocreate hello bramy, użyj hello `New-AzureApplicationGateway` polecenia cmdlet, zastępując wartości hello własne. Karta hello bramy nie rozpoczyna się w tym momencie. Karta rozpoczyna się od w kolejnym kroku hello bramy została pomyślnie uruchomiona.

Witaj poniższy przykład tworzy bramę aplikacji przy użyciu sieci wirtualnej o nazwie "testvnet1" i podsieć o nazwie "podsieć 1":

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

Parametry *Description* (opis), *InstanceCount* (Liczba wystąpień) i *GatewaySize* (Rozmiar bramy) są opcjonalne.

toovalidate, który hello bramy został utworzony, można użyć hello `Get-AzureApplicationGateway` polecenia cmdlet.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> Witaj wartości domyślnej dla *InstanceCount* 2, maksymalna wartość 10. Witaj wartości domyślnej dla *GatewaySize* to średni. Do wyboru są wartości Small (Mała), Medium (Średnia) i Large (Duża).

*VirtualIPs* i *DnsName* są wyświetlane jako puste, ponieważ brama hello nie została jeszcze uruchomiona. Są one tworzone po hello brama jest w hello stanu działania.

## <a name="configure-hello-application-gateway"></a>Brama aplikacji hello

Brama aplikacji hello można skonfigurować za pomocą XML lub obiekt konfiguracji.

### <a name="configure-hello-application-gateway-by-using-xml"></a>Konfigurowanie bramy aplikacji hello za pomocą XML

W hello poniższy przykład użyj tooconfigure pliku XML wszystkie ustawienia bramy aplikacji i je zatwierdzić zasobu bramy toohello aplikacji.  

#### <a name="step-1"></a>Krok 1

Skopiuj powitania po tooNotepad tekstu.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Edytuj wartości hello między nawiasami hello hello elementów konfiguracji. Zapisz plik hello z rozszerzeniem .xml.

> [!IMPORTANT]
> Element protokołu Hello Http lub Https jest rozróżniana wielkość liter.

Witaj poniższy przykład pokazuje, jak toouse konfiguracji pliku tooset się bramy aplikacji hello. obciążenia przykład Hello równoważy ruchu HTTP na port publiczny 80 i wysyła ruch sieciowy tooback-end port 80 między dwoma adresami IP.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a>Krok 2

Następnie ustaw hello bramy aplikacji. Użyj hello `Set-AzureApplicationGatewayConfig` polecenie cmdlet z pliku XML konfiguracji.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a>Konfigurowanie bramy aplikacji hello za pomocą obiektu konfiguracji

Witaj poniższy przykład pokazuje, jak tooconfigure hello bramy aplikacji przy użyciu obiektów konfiguracji. Wszystkie elementy konfiguracji należy skonfigurować osobno i następnie dodany obiekt konfiguracji bramy aplikacji tooan. Po utworzeniu obiektu konfiguracji hello używasz hello `Set-AzureApplicationGateway` polecenia toocommit hello konfiguracji toohello wcześniej utworzony zasób bramy aplikacji.

> [!NOTE]
> Przed przypisaniem obiekt konfiguracji tooeach wartości, należy toodeclare obiektem jakiego rodzaju PowerShell korzysta z magazynu. Witaj pierwszego wiersza toocreate hello poszczególne elementy definiuje, jakie `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` są używane.

#### <a name="step-1"></a>Krok 1

Utwórz wszystkie poszczególne elementy konfiguracji.

Utwórz hello IP frontonu, jak pokazano w hello poniższy przykład.

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

Utworzyć hello portów frontonu, jak pokazano w hello poniższy przykład.

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

Utwórz hello puli serwerów zaplecza.

Zdefiniuj hello adresów IP, które są dodawane do puli serwerów zaplecza toohello, jak pokazano w następnym przykładzie hello.

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

Użyj hello $server tooadd hello wartości toohello puli zaplecza dla obiektu ($pool).

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

Utwórz ustawienie puli serwera zaplecza hello.

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

Utwórz odbiornik hello.

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

Utwórz regułę hello.

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a>Krok 2

Przypisz wszystkich konfiguracji poszczególnych elementów tooan aplikacji konfiguracji obiektu bramy ($appgwconfig).

Dodaj hello konfiguracji IP frontonu w toohello.

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

Dodaj konfigurację toohello portów frontonu hello.

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
Dodaj powitania serwera zaplecza puli toohello konfiguracji.

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

Dodawanie konfiguracji toohello hello puli zaplecza.

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

Dodaj konfigurację toohello odbiornika hello.

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

Dodaj konfigurację toohello reguły hello.

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a>Krok 3
Zatwierdź zasobu bramy aplikacji hello konfiguracji obiektu toohello przy użyciu `Set-AzureApplicationGatewayConfig`.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a>Uruchom hello bramy

Po skonfigurowaniu bramy hello Użyj hello `Start-AzureApplicationGateway` bramy hello toostart polecenia cmdlet. Rozliczeń dla bramy aplikacji rozpocznie się po pomyślnym uruchomieniu hello bramy.

> [!NOTE]
> Witaj `Start-AzureApplicationGateway` polecenie cmdlet może potrwać toofinish too15 20 minut.

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Sprawdź stan bramy hello

Użyj hello `Get-AzureApplicationGateway` polecenia cmdlet toocheck hello stan hello bramy. Jeśli `Start-AzureApplicationGateway` zakończyło się pomyślnie w poprzednim kroku hello *stanu* powinna być uruchomiona, i *Vip* i *DnsName* powinny mieć prawidłowe wpisy.

Witaj poniższy przykład przedstawia bramę aplikacji, która jest włączone, uaktywnione i gotowe tootake ruchu przeznaczony dla `http://<generated-dns-name>.cloudapp.net`.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a>Usuń bramę aplikacji hello

Brama aplikacji hello toodelete:

1. Użyj hello `Stop-AzureApplicationGateway` bramy hello toostop polecenia cmdlet.
2. Użyj hello `Remove-AzureApplicationGateway` bramy hello tooremove polecenia cmdlet.
3. Sprawdź tej bramy hello został usunięty przy użyciu hello `Get-AzureApplicationGateway` polecenia cmdlet.

Witaj poniższy przykład przedstawia hello `Stop-AzureApplicationGateway` polecenia cmdlet na powitania pierwszy wiersz, następuje hello danych wyjściowych.

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Po bramy aplikacji hello jest w stanie zatrzymania, użyj hello `Remove-AzureApplicationGateway` usługi hello tooremove polecenia cmdlet.

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

tooverify, który hello usługi zostały usunięte, możesz użyć hello `Get-AzureApplicationGateway` polecenia cmdlet. Ten krok nie jest wymagany.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a>Następne kroki

Jeśli tooconfigure odciążanie protokołu SSL, zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl.md).

Jeśli chcesz tooconfigure toouse bramy aplikacji z wewnętrznego modułu równoważenia obciążenia, zobacz [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).

Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
