---
title: "toouse aaaHow Azure API Management w sieci wirtualnej z bramą aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i konfigurowanie usługi Azure API Management w wewnętrznej sieci wirtualnej z aplikacji bramy (WAF) jako serwera sieci Web"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a>Zintegrować zarządzanie interfejsami API w wewnętrznej sieci Wirtualnej z bramy aplikacji 

##<a name="overview"></a> — Omówienie
 
Witaj usługi Zarządzanie interfejsami API można skonfigurować w sieci wirtualnej w trybie wewnętrznej, dzięki czemu dostępny tylko w obrębie hello sieci wirtualnej. Bramy aplikacji Azure to usługa PAAS, która udostępnia usługi równoważenia obciążenia warstwy 7. Pełni rolę usługi proxy odwrotnie, a udostępnia między oferty zapory aplikacji sieci Web (WAF).

Zarządzanie interfejsami API udostępniane w wewnętrznej sieci Wirtualnej z frontonu bramy aplikacji hello łączenie umożliwia hello następujące scenariusze:

* Użyj hello sam zasobu interfejsu API zarządzania zużycia zarówno przez użytkowników wewnętrznych i zewnętrznych konsumentów.
* Użyj pojedynczego zasobu interfejsu API zarządzania i podzestawu interfejsów API zdefiniowanych w usłudze API Management dostępne dla użytkowników zewnętrznych.
* Podaj sposób gotowe tooswitch dostępu tooAPI zarządzania z hello publicznej sieci Internet, włączać i wyłączać. 

##<a name="scenario"></a> Scenariusza
W tym artykule opisano, jak toouse pojedynczego zarządzanie interfejsami API usługi dla użytkowników wewnętrznych i zewnętrznych, a następnie stał się działać jako pojedynczy frontonu dla obu lokalnego i w chmurze interfejsów API. Widoczne będzie także sposób tooexpose tylko podzbiór swoje interfejsy API (w przykładzie hello są wyróżnione zielony) wykorzystania zewnętrznych za pomocą hello PathBasedRouting funkcje dostępne w programie Application Gateway.

W pierwszym przykładzie Instalatora hello swoje interfejsy API są zarządzane tylko z w ramach sieci wirtualnej. Konsumenci wewnętrzny (wyróżniane na kolor pomarańczowy) mogą uzyskiwać dostęp do wszystkich sieci wewnętrznych i zewnętrznych interfejsów API. Ruch nigdy nie trafia tooInternet dostarczenia wysokiej wydajności, za pomocą obwodów Express Route.

![trasy adresu URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <a name="before-you-begin"></a> Przed rozpoczęciem

1. Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web. Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).
2. Tworzenie sieci wirtualnej i Utwórz oddzielne podsieci dla interfejsu API zarządzania i bramy aplikacji. 
3. Jeśli planujesz toocreate niestandardowy serwer DNS dla sieci wirtualnej hello zrobić przed rozpoczęciem powitalne wdrożenia. Dobrze Sprawdź, czy działa przez zapewnienie im maszyny wirtualnej utworzonej w nową podsieć w sieci wirtualnej hello można rozwiązać i dostęp do wszystkich punktów końcowych usługi Azure.

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a>Co to jest wymagane toocreate integracja interfejsu API zarządzania i bramę aplikacji?

* **Pula serwerów zaplecza:** to hello wewnętrznego wirtualnego adresu IP hello usługi Zarządzanie interfejsami API.
* **Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie. Te ustawienia są stosowane tooall serwery w puli hello.
* **Port frontonu:** jest to port publiczny hello, która jest otwarta w bramie aplikacji hello. Ruch naciśnięcie go pobiera tooone przekierowanych z hello serwerów zaplecza.
* **Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).
* **Reguła:** reguły hello wiąże pulę odbiornika tooa serwerów zaplecza.
* **Niestandardowe sondy kondycji:** bramy aplikacji domyślnie używa toofigure sond na podstawie adresu IP limit serwerów, które w hello BackendAddressPool są aktywne. Hello usługi Zarządzanie interfejsami API tylko odpowiada toorequests, która ma nagłówek hosta poprawne hello, dlatego hello domyślnej sondy zakończyć się niepowodzeniem. Sondy kondycji niestandardowych musi toobe zdefiniowane toohelp bramy aplikacji ustalić, czy działa usługa hello i należy przekazywać żądania.
* **Certyfikat domeny niestandardowej:** tooaccess API Management z hello internet należy toocreate mapowanie CNAME hostname toohello bramy aplikacji frontonu nazwy DNS. To zapewnia, że nagłówek hostname hello i tooApplication certyfikatu wysłanego bramy, który jest przesyłany dalej tooAPI zarządzania jest jeden APIM rozpoznać jako prawidłowy.

## <a name="overview-steps"></a> Kroków wymaganych do integracji interfejsu API zarządzania i bramy aplikacji 

1. Utworzenie grupy zasobów dla usługi Resource Manager.
2. Tworzenie sieci wirtualnej, podsieci i publicznego adresu IP dla bramy aplikacji hello. Utwórz inną podsieć dla interfejsu API zarządzania.
3. Tworzenie usługi Zarządzanie interfejsami API w podsieci sieci Wirtualnej hello utworzone powyżej i upewnij się, że używany jest tryb wewnętrzny hello.
4. Instalator hello niestandardowej nazwy domeny w hello usługi Zarządzanie interfejsami API.
5. Utwórz obiekt konfiguracji bramy aplikacji.
6. Utwórz zasób aplikacji bramy.
7. Należy utworzyć rekord CNAME z hello publicznej nazwy DNS nazwy hosta hello bramy aplikacji toohello interfejsu API zarządzania serwera proxy.

## <a name="create-a-resource-group-for-resource-manager"></a>Tworzenie grupy zasobów dla usługi Resource Manager

Upewnij się, że używasz najnowszej wersji programu Azure PowerShell hello. Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).

### <a name="step-1"></a>Krok 1

Zaloguj się za tooAzure

```powershell
Login-AzureRmAccount
```

Uwierzytelnianie przy użyciu poświadczeń.<BR>

### <a name="step-2"></a>Krok 2

Sprawdź subskrypcje hello hello konta i zaznacz go.

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a>Krok 3

Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Służy to jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów. Upewnij się, że hello Użyj bramy aplikacji wszystkie polecenia toocreate tej samej grupie zasobów.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Utwórz sieć wirtualną i podsieć bramy aplikacji hello

Witaj poniższy przykład pokazuje, jak toocreate sieci wirtualnych za pomocą funkcji hello Menedżera zasobów.

### <a name="step-1"></a>Krok 1

Przypisz hello adres zakresu 10.0.0.0/24 toohello podsieci zmiennej toobe używana przez bramę aplikacji podczas tworzenia sieci wirtualnej.

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a>Krok 2

Przypisz hello adres zakresu 10.0.1.0/24 toohello podsieci zmiennej toobe interfejsu API zarządzania używać podczas tworzenia sieci wirtualnej.

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a>Krok 3

Tworzenie sieci wirtualnej o nazwie **appgwvnet** w grupie zasobów **apim-appGw-zarządcy zasobów** dla regionu zachodnie stany USA hello przy użyciu hello 10.0.0.0/16 prefiks podsieci 10.0.0.0/24 i 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a>Krok 4

Przypisanie zmiennej podsieci hello następne kroki

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a>Tworzenie usługi Zarządzanie interfejsami API w sieci Wirtualnej w trybie wewnętrzny

Witaj poniższy przykład przedstawia toocreate usługi Zarządzanie interfejsami API w sieci Wirtualnej konfiguracji tylko wewnętrzny dostępu.

### <a name="step-1"></a>Krok 1
Utwórz obiekt sieci wirtualnej interfejsu API zarządzania za pomocą podsieci hello $apimsubnetdata utworzone powyżej.

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a>Krok 2
Tworzenie usługi Zarządzanie interfejsami API wewnątrz hello sieci wirtualnej.

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
Po pomyślnym zainicjowaniu hello powyżej polecenia można znaleźć zbyt[tooaccess wewnętrzny usługi Zarządzanie interfejsami API sieci Wirtualnej wymagana konfiguracja DNS](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess go.

## <a name="set-up-a-custom-domain-name-in-api-management"></a>Ustawienie niestandardowej nazwy domeny w usłudze API Management

### <a name="step-1"></a>Krok 1
Przekaż hello certyfikat z kluczem prywatnym hello domeny. W tym przykładzie będzie `*.contoso.net`. 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a>Krok 2
Po przekazaniu plików certyfikatów hello utworzenia obiektu konfiguracji nazwę hosta dla serwera proxy hello z nazwą hosta z `api.contoso.net`, ponieważ zapewnia hello przykład certyfikatu urzędu hello `*.contoso.net` domeny. 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Utwórz publiczny adres IP dla konfiguracji frontonu hello

Utwórz zasób publicznego adresu IP **publicIP01** w grupie zasobów **apim-appGw-zarządcy zasobów** hello regionu zachodnie stany USA.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

Adres IP jest przypisany toohello bramy aplikacji, po uruchomieniu usługi hello.

## <a name="create-application-gateway-configuration"></a>Tworzenie konfiguracji bramy aplikacji

Wszystkie elementy konfiguracji należy skonfigurować przed utworzeniem bramy aplikacji hello. Witaj następujące kroki tworzenia hello elementy konfiguracji, które są potrzebne dla zasobu bramy aplikacji.

### <a name="step-1"></a>Krok 1

Utwórz konfigurację adresu IP bramy aplikacji o nazwie **gatewayIP01**. Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci hello skonfigurowane i tras adresów IP toohello ruchu sieciowego w puli adresów IP zaplecza hello. Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a>Krok 2

Skonfiguruj hello frontonu portu IP dla punktu końcowego hello publicznego adresu IP. Jest to port hello użytkownicy połączenie.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a>Krok 3

Skonfiguruj IP frontonu hello publicznego adresu IP punktu końcowego.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a>Krok 4

Skonfigurować certyfikat hello hello bramy aplikacji używane toodecrypt a zaszyfrowanie hello ruchu przechodzącego przez.

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a>Krok 5

Utwórz odbiornik HTTP hello na powitania bramy aplikacji. Przypisywanie konfiguracji IP frontonu hello, port i tooit certyfikatu ssl.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a>Krok 6

Tworzenie niestandardowych sondowania toohello usługi Zarządzanie interfejsami API `ContosoApi` punktu końcowego domeny serwera proxy. Ścieżka Hello `/status-0123456789abcdef` jest domyślnego kondycji punktu końcowego hostowanych na wszystkie usługi Zarządzanie interfejsami API hello. Ustaw `api.contoso.net` jako toosecure hostname sondowania niestandardowych za pomocą certyfikatu SSL.

> [!NOTE]
> Witaj hostname `contosoapi.azure-api.net` jest nazwa hosta serwera proxy domyślne hello konfigurowane podczas usługi o nazwie `contosoapi` jest tworzony w publicznej Azure. 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a>Krok 7

Przekaż certyfikat hello toobe używane hello włączony protokół SSL zaplecza puli zasobów. Jest to hello tego samego certyfikatu, które podano w powyższym kroku 4.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a>Krok 8

Skonfiguruj ustawienia HTTP zaplecza hello bramy aplikacji. Dotyczy to również ustawienie limitu czasu, po którym są anulowane żądania wewnętrznej bazy danych. Ta wartość jest inny niż limit czasu sondowania hello.

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a>Krok 9

Skonfiguruj pulę adresów IP zaplecza, o nazwie **apimbackend** z wewnętrznego wirtualnego adresu IP hello adres hello usługi Zarządzanie interfejsami API utworzone powyżej.

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a>Krok 10

Tworzenie ustawień dla fikcyjnego zaplecza (nieistniejącego). Ścieżki tooAPI żądań, które nie chcemy tooexpose z interfejsu API zarządzania za pośrednictwem bramy aplikacji będzie trafień tego wewnętrznej bazy danych i zwracać 404.

Skonfiguruj ustawienia HTTP zaplecza fikcyjny hello.

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Skonfiguruj fikcyjny wewnętrznej bazy danych **dummyBackendPool**, który wskazuje adres FQDN tooa **dummybackend.com**. Ten adres FQDN nie istnieje w sieci wirtualnej hello.

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

Utwórz regułę ustawienie tego hello bramy aplikacji użyje domyślnie wskazujący toohello nieistniejącą zaplecza **dummybackend.com** w hello sieci wirtualnej.

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a>Krok 11

Konfiguruj adres URL reguły ścieżki dla pul zaplecza hello. Umożliwia wybranie tylko niektóre hello interfejsy API z interfejsu API zarządzania jest udostępniany toohello publicznego. Na przykład, jeśli istnieją `Echo API` (/ echo /), `Calculator API` (/calc/) itd. Sprawdź tylko `Echo API` dostępny z Internetu). 

Witaj poniższy przykład tworzy regułę prostego powitania "/ echo /" ścieżkę routingu ruchu toohello zaplecza "apimProxyBackendPool".

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

Jeśli ścieżka hello jest niezgodny hello ścieżki reguły chcemy tooenable z interfejsu API zarządzania, hello reguły ścieżki mapy konfiguracji konfiguruje również domyślną pulę adresów zaplecza o nazwie **dummyBackendPool**. Na przykład http://api.contoso.net/calc/ * prowadzi zbyt**dummyBackendPool** określone jako hello domyślna pula cofanie dopasowane ruchu.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

Hello powyżej kroku gwarantuje, który żąda tylko dla ścieżki hello "/ echo" są dozwolone przez hello bramy aplikacji. Tooother żądania, interfejsy API skonfigurowane w usłudze API Management spowoduje zgłoszenie błędów 404 z bramy aplikacji, gdy użytkowcy hello Internet. 

### <a name="step-12"></a>Krok 12

Utwórz ustawienie reguły dla hello bramy aplikacji toouse routingu adresów URL na podstawie ścieżki.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a>Krok 13

Skonfiguruj hello liczbę wystąpień i rozmiar hello Application Gateway. W tym miejscu używamy hello [SKU zapory aplikacji sieci Web](../application-gateway/application-gateway-webapplicationfirewall-overview.md) Aby zwiększyć bezpieczeństwo hello zasobu interfejsu API zarządzania.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a>Krok 14

Skonfiguruj toobe zapory aplikacji sieci Web w trybie "Zapobiegania".
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a>Utwórz bramę aplikacji

Utwórz bramę aplikacji na wszystkich obiektach konfiguracji hello hello w poprzednich krokach.

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a>CNAME hello interfejsu API zarządzania serwera proxy hostname toohello publicznej nazwy DNS hello zasobu bramy aplikacji

Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji. Korzystając z publicznym adresem IP, brama aplikacji wymaga przypisywany dynamicznie nazwy DNS, które nie mogą być łatwo toouse. 

Hello nazwa DNS bramy aplikacji powinny być używane toocreate rekord CNAME, który wskazuje nazwę hosta serwera proxy APIM hello (np. `api.contoso.net` w powyższych przykładach hello) toothis nazwy DNS. tooconfigure hello frontonu rekordu IP CNAME pobierać szczegóły hello hello bramy aplikacji i jego skojarzonej nazwy IP DNS za pomocą hello publicznego adresu IP elementu. Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<a name="summary"></a> Podsumowanie
Skonfigurowane w sieci Wirtualnej platformy Azure API Management oferuje interfejs pojedyncza brama dla wszystkich skonfigurowanych interfejsów API, czy są one lokalnego hostowanej w chmurze hello. Integrowanie aplikacji bramy z interfejsu API zarządzania zapewnia elastyczność hello selektywne włączenie określonego dostępne na powitania Internet toobe interfejsów API, a także dostarczanie zapory aplikacji sieci Web jako wystąpienie interfejsu API zarządzania tooyour frontonu.

##<a name="next-steps"></a> Następne kroki
* Dowiedz się więcej na temat bramy aplikacji Azure
  * [Omówienie bramy aplikacji](../application-gateway/application-gateway-introduction.md)
  * [Zapora aplikacji sieci Web bramy aplikacji](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [Brama aplikacji przy użyciu routingu na podstawie ścieżki](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* Dowiedz się więcej o interfejsu API zarządzania i sieci wirtualnych
  * [Za pomocą interfejsu API zarządzania dostępne tylko w obrębie hello sieci Wirtualnej](api-management-using-with-internal-vnet.md)
  * [Za pomocą interfejsu API zarządzania w sieci Wirtualnej](api-management-using-with-vnet.md)
