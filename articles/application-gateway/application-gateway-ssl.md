---
title: "aaaConfigure SSL odciążania klasycznego środowiska PowerShell — brama usługi aplikacji Azure — | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera instrukcje toocreate bramę aplikacji przy użyciu protokołu SSL Odciążanie przy użyciu hello Azure klasycznego modelu wdrażania."
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
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a>Skonfiguruj bramę aplikacji dla odciążania protokołu SSL przy użyciu hello klasycznego modelu wdrażania

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-ssl-arm.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-ssl.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-ssl-cli.md)

Brama aplikacji w Azure może być sesji protokołu Secure Sockets Layer (SSL) hello tooterminate skonfigurowanych na powitania bramy tooavoid kosztowne SSL odszyfrowywania zadania toohappen na powitania kolektywu serwerów sieci web. Odciążanie protokołu SSL także upraszcza powitania serwera frontonu Konfiguracja i zarządzanie hello aplikacji sieci web.

## <a name="before-you-begin"></a>Przed rozpoczęciem

1. Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web. Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).
2. Sprawdź, czy masz działającą sieć wirtualną z prawidłową podsiecią. Upewnij się, że nie maszyny wirtualne lub wdrożenia chmury z hello podsieci. Brama aplikacji Hello należy samodzielnie w podsieci sieci wirtualnej.
3. Skonfigurowanie bramy aplikacji hello toouse serwerów Hello musi istnieć lub mieć przypisane ich punkty końcowe utworzone w sieci wirtualnej hello lub z publicznego adresu IP/VIP.

tooconfigure SSL odciążenia na bramę aplikacji, hello następujące kroki w podanej kolejności hello:

1. [Tworzenie bramy aplikacji](#create-an-application-gateway)
2. [Przekaż certyfikaty SSL](#upload-ssl-certificates)
3. [Konfigurowanie bramy hello](#configure-the-gateway)
4. [Konfiguracja bramy hello zestawu](#set-the-gateway-configuration)
5. [Uruchom hello bramy](#start-the-gateway)
6. [Sprawdź stan bramy hello](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Tworzenie bramy aplikacji

toocreate hello bramy, użyj hello `New-AzureApplicationGateway` polecenia cmdlet, zastępując wartości hello własne. Karta hello bramy nie rozpoczyna się w tym momencie. Karta rozpoczyna się od w kolejnym kroku hello bramy została pomyślnie uruchomiona.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate, który hello bramy został utworzony, można użyć hello `Get-AzureApplicationGateway` polecenia cmdlet.

W przykładowym hello *opis*, *InstanceCount*, i *GatewaySize* są opcjonalnymi parametrami. Witaj wartości domyślnej dla *InstanceCount* 2, maksymalna wartość 10. Witaj wartości domyślnej dla *GatewaySize* to średni. Małe i duże są inne dostępne wartości. *VirtualIPs* i *DnsName* są wyświetlane jako puste, ponieważ brama hello nie została jeszcze uruchomiona. Te wartości są tworzone po hello brama jest w hello stanu działania.

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a>Przekaż certyfikaty SSL

Użyj `Add-AzureApplicationGatewaySslCertificate` certyfikatu serwera hello tooupload w *pfx* brama aplikacji w formacie toohello. Nazwa certyfikatu Hello jest nazwą wybranych przez użytkownika i muszą być unikatowe w ramach bramy aplikacji hello. Ten certyfikat jest określony tooby tej nazwy we wszystkich operacjach zarządzania certyfikatu dla bramy aplikacji hello.

Ta poniższy przykład przedstawia hello polecenia cmdlet, Zamień hello wartości w próbce hello własne.

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

Następnie sprawdź poprawność hello przekazywanie certyfikatu. Użyj hello `Get-AzureApplicationGatewayCertificate` polecenia cmdlet.

To przykładowe przedstawiono polecenie cmdlet hello na powitania pierwszy wiersz, następuje hello danych wyjściowych.

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
> Hasło certyfikatu Hello ma toobe między 4 znaki too12, liter i cyfr. Znaki specjalne nie są akceptowane.

## <a name="configure-hello-gateway"></a>Konfigurowanie bramy hello

Konfiguracja bramy aplikacji składa się z wielu wartości. mogą być związane Hello wartości konfiguracji hello tooconstruct razem.

Witaj wartości są następujące:

* **Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello. wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.
* **Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie. Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.
* **Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello. Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.
* **Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).
* **Reguła:** reguła hello wiąże odbiornika hello i hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika. Obecnie tylko hello *podstawowe* reguła jest obsługiwana. Witaj *podstawowe* reguła jest rozkład obciążenia okrężnego.

**Uwagi dotyczące konfiguracji dodatkowych**

Do konfigurowania certyfikatów SSL, hello protokół **HttpListener** należy zmienić zbyt*Https* (z uwzględnieniem wielkości liter). Witaj **SslCert** zbyt dodany element**HttpListener** z hello wartość toohello takie same nazwy w powyższej sekcji certyfikaty SSL przekazywania hello. port frontonu Hello powinien być zaktualizowany too443.

**koligacji na podstawie plików cookie tooenable**: bramy aplikacji może być skonfigurowany tooensure żądania z sesji klienta jest zawsze ukierunkowanej toohello tej samej maszyny Wirtualnej w hello kolektywu serwerów sieci web. W tym scenariuszu odbywa się przez uruchomienie pliku cookie sesji, umożliwiającą hello bramy toodirect ruch odpowiednio. Ustaw koligacji na podstawie plików cookie tooenable **CookieBasedAffinity** za*włączone* w hello **elementu BackendHttpSettings** elementu.

Można utworzyć konfiguracji poprzez utworzenie obiektu konfiguracji lub przy użyciu pliku XML konfiguracji.
Użyj konfiguracji przy użyciu pliku XML konfiguracji tooconstruct hello następujący przykład:

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

## <a name="set-hello-gateway-configuration"></a>Konfiguracja bramy hello zestawu

Następnie należy ustawić bramę aplikacji hello. Można użyć hello `Set-AzureApplicationGatewayConfig` polecenia cmdlet bez obiekt konfiguracji lub z pliku XML konfiguracji.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a>Uruchom hello bramy

Po skonfigurowaniu bramy hello Użyj hello `Start-AzureApplicationGateway` bramy hello toostart polecenia cmdlet. Rozliczeń dla bramy aplikacji rozpocznie się po pomyślnym uruchomieniu hello bramy.

> [!NOTE]
> Witaj `Start-AzureApplicationGateway` polecenie cmdlet może potrwać toofinish too15 20 minut.
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Sprawdź stan bramy hello

Użyj hello `Get-AzureApplicationGateway` polecenia cmdlet toocheck hello stan hello bramy. Jeśli `Start-AzureApplicationGateway` zakończyło się pomyślnie w poprzednim kroku hello *stanu* powinna być uruchomiona, i *VirtualIPs* i *DnsName* powinny mieć prawidłowe wpisy.

W tym przykładzie pokazano bramę aplikacji, który, uruchomione i jest gotowy tootake ruchu.

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

