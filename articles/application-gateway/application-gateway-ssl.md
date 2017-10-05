---
title: "Skonfiguruj klasycznego środowiska PowerShell odciążania — brama usługi aplikacji Azure — SSL | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera instrukcje, aby utworzyć bramę aplikacji przy użyciu protokołu SSL Odciążanie przy użyciu modelu klasycznego wdrożenia usługi Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2eba6fb24c11add12ac16d04d3445e19a3486216
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-classic-deployment-model"></a>Skonfiguruj bramę aplikacji dla odciążania protokołu SSL przy użyciu klasycznego modelu wdrażania

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-ssl-arm.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-ssl.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-ssl-cli.md)

Usługę Azure Application Gateway można skonfigurować tak, aby przerywała sesję protokołu SSL (Secure Sockets Layer) na poziomie bramy, co pozwoli na uniknięcie wykonywania kosztownych zadań szyfrowania protokołu SSL w kolektywie serwerów sieci Web. Odciążanie protokołu SSL upraszcza również konfigurowanie serwerów frontonu i zarządzanie aplikacją sieci Web.

## <a name="before-you-begin"></a>Przed rozpoczęciem

1. Zainstaluj najnowszą wersję poleceń cmdlet programu Azure PowerShell za pomocą Instalatora platformy sieci Web. Najnowszą wersję można pobrać i zainstalować z sekcji **Windows PowerShell** strony [Pliki do pobrania](https://azure.microsoft.com/downloads/).
2. Sprawdź, czy masz działającą sieć wirtualną z prawidłową podsiecią. Upewnij się, że z podsieci nie korzystają żadne maszyny wirtualne ani wdrożenia w chmurze. Brama aplikacji musi znajdować się w podsieci sieci wirtualnej.
3. Serwery konfigurowane do używania bramy aplikacji muszą być umieszczone w sieci wirtualnej lub z przypisanym adresem IP/VIP lub mieć w niej utworzone punkty końcowe.

Aby skonfigurować bramę aplikacji odciążanie protokołu SSL, wykonaj następujące kroki w podanej kolejności:

1. [Tworzenie bramy aplikacji](#create-an-application-gateway)
2. [Przekaż certyfikaty SSL](#upload-ssl-certificates)
3. [Konfigurowanie bramy](#configure-the-gateway)
4. [Ustaw konfigurację bramy](#set-the-gateway-configuration)
5. [Uruchom bramę](#start-the-gateway)
6. [Sprawdź stan bramy](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Tworzenie bramy aplikacji

Aby utworzyć bramę, użyj polecenia cmdlet `New-AzureApplicationGateway`, zastępując wartości własnymi. Opłaty za bramę nie są jeszcze naliczane. Rozliczanie zaczyna się na późniejszym etapie, po pomyślnym uruchomieniu bramy.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

Aby sprawdzić, czy brama została utworzona, możesz użyć polecenia cmdlet `Get-AzureApplicationGateway`.

W przykładzie *opis*, *InstanceCount*, i *GatewaySize* są opcjonalnymi parametrami. Wartość domyślna parametru *InstanceCount* to 2, a wartość maksymalna — 10. Wartość domyślna parametru *GatewaySize* to Medium (Średnia). Małe i duże są inne dostępne wartości. Parametry *VirtualIPs* (Wirtualne adresy IP) i *DnsName* (Nazwa serwera DNS) są wyświetlane jako puste, ponieważ brama nie została jeszcze uruchomiona. Te wartości są tworzone, gdy brama jest w stanie uruchomienia.

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a>Przekaż certyfikaty SSL

Użyj `Add-AzureApplicationGatewaySslCertificate` można przekazać certyfikatu serwera w *pfx* format na bramie aplikacji. Nazwa certyfikatu jest nazwą wybranych przez użytkownika i muszą być unikatowe w ramach bramy aplikacji. Ten certyfikat jest określane o tej nazwie we wszystkich operacjach zarządzania certyfikatu dla bramy aplikacji.

To w poniższym przykładzie przedstawiono polecenie cmdlet, Zastąp wartości w próbce własnymi.

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path to pfx file>
```

Następnie sprawdź poprawność przekazywanie certyfikatu. Użyj `Get-AzureApplicationGatewayCertificate` polecenia cmdlet.

Przykład obejmuje polecenia cmdlet w pierwszym wierszu, to po danych wyjściowych.

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> Hasło certyfikatu musi należeć do przedziału od 4 do 12 znaków, liter i cyfr. Znaki specjalne nie są akceptowane.

## <a name="configure-the-gateway"></a>Konfigurowanie bramy

Konfiguracja bramy aplikacji składa się z wielu wartości. Wartości mogą być powiązane ze sobą w celu utworzenia konfiguracji.

Potrzebne wartości:

* **Pula serwerów zaplecza:** lista adresów IP serwerów zaplecza. Adresy IP na liście powinny należeć do podsieci sieci wirtualnej lub być publicznymi bądź wirtualnymi adresami IP.
* **Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie. Te ustawienia są powiązane z pulą i są stosowane do wszystkich serwerów w tej puli.
* **Port frontonu:** port publiczny, który jest otwierany w bramie aplikacji. Ruch trafia do tego portu, a następnie jest przekierowywany do jednego z serwerów zaplecza.
* **Odbiornik:** odbiornik ma port frontonu, protokół (Http lub Https, z uwzględnieniem wielkości liter) oraz nazwę certyfikatu SSL (w przypadku konfigurowania odciążania protokołu SSL).
* **Reguła:** reguła wiąże odbiornik z pulą serwerów zaplecza i umożliwia zdefiniowanie, do której puli serwerów zaplecza ma być przekierowywany ruch w przypadku trafienia do określonego odbiornika. Obecnie jest obsługiwana tylko reguła *podstawowa*. Reguła *podstawowa* to dystrybucja obciążenia z działaniem okrężnym.

**Uwagi dotyczące konfiguracji dodatkowych**

W przypadku konfiguracji certyfikatów SSL protokół w polu **HttpListener** należy zmienić na *Https* (z uwzględnieniem wielkości liter). **SslCert** element zostanie dodany do **HttpListener** o wartości do tej samej nazwie w przekazywania poprzedzających SSL certyfikaty sekcji. Port frontonu należy zaktualizować do 443.

**Aby włączyć koligację opartą na plikach cookie**: bramę aplikacji można skonfigurować tak, aby żądanie z sesji klienta było zawsze kierowane do tej samej maszyny wirtualnej w kolektywie serwerów sieci Web. W tym scenariuszu należy wstrzyknąć plik cookie sesji, który umożliwi bramie prawidłowe kierowanie ruchu. Aby włączyć koligację opartą na plikach cookie, ustaw element **CookieBasedAffinity** na wartość *Enabled* w elemencie **BackendHttpSettings**.

Można utworzyć konfiguracji poprzez utworzenie obiektu konfiguracji lub przy użyciu pliku XML konfiguracji.
Aby utworzyć konfigurację za pomocą pliku XML konfiguracji, skorzystaj z poniższego przykładu:

**Przykładowy plik XML konfiguracji**

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-the-gateway-configuration"></a>Ustaw konfigurację bramy

Następnie należy ustawić bramy aplikacji. Można użyć `Set-AzureApplicationGatewayConfig` polecenia cmdlet bez obiekt konfiguracji lub z pliku XML konfiguracji.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-the-gateway"></a>Uruchamianie bramy

Po skonfigurowaniu bramy użyj polecenia cmdlet `Start-AzureApplicationGateway`, aby uruchomić bramę. Naliczanie opłat za bramę aplikacji rozpocznie się po pomyślnym uruchomieniu bramy.

> [!NOTE]
> Wykonanie polecenia cmdlet `Start-AzureApplicationGateway` może zająć do 15–20 minut.
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a>Sprawdzanie stanu bramy

Użyj polecenia cmdlet `Get-AzureApplicationGateway`, aby sprawdzić stan bramy. Jeśli `Start-AzureApplicationGateway` zakończyło się pomyślnie w poprzednim kroku, *stanu* powinna być uruchomiona, i *VirtualIPs* i *DnsName* powinny mieć prawidłowe wpisy.

W tym przykładzie pokazano bramę aplikacji, który, uruchomione i jest gotowa do sporządzenia ruchu.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a>Następne kroki

Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

