---
title: "aaaConfigure zakończenia tooend SSL z bramy aplikacji Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconfigure kończyć tooend SSL z bramy aplikacji przy użyciu programu PowerShell usługi Azure Resource Manager"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a>Skonfiguruj tooend końcowych SSL z bramy aplikacji przy użyciu programu PowerShell

## <a name="overview"></a>Omówienie

Aplikacja obsługuje bramy końcowy tooend szyfrowania ruchu. Brama aplikacji w następującym cechom zakończenie połączenia SSL hello na powitania bramy aplikacji. Witaj bramy następnie stosuje hello reguły routingu ruchu toohello ponownie szyfruje pakietów hello i przekazuje hello pakietów toohello odpowiedniej wewnętrznej bazy danych na podstawie reguł routingu hello zdefiniowane. Odpowiedzi z serwera sieci web hello przechodzi przez hello tego samego procesu wstecz toohello użytkownika końcowego.

Inna funkcja tej bramy aplikacji obsługuje Określanie niestandardowych opcji protokołu SSL. Brama aplikacji umożliwia wyłączenie powitania po wersji protokołu; **TLSv1.0**, **TLSv1.1**, i **TLSv1.2** również definiowanie hello, który szyfrowania mechanizmy toouse i hello według priorytetu.  toolearn więcej informacji na temat opcji SSL można skonfigurować, odwiedź stronę [Przegląd zasad SSL](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> Protokół SSL 2.0 i 3.0 protokołu SSL są domyślnie wyłączone i nie można włączyć. One są uważane za niebezpieczne i nie są toobe można używać z bramy aplikacji.

![Scenariusz obrazu][scenario]

## <a name="scenario"></a>Scenariusz

W tym scenariuszu dowiesz się, jak bramy aplikacji przy użyciu toocreate kończyć tooend SSL przy użyciu programu PowerShell.

W tym scenariuszu obejmują:

* Utwórz grupę zasobów o nazwie **zarządcy zasobów appgw**
* Tworzenie sieci wirtualnej o nazwie **appgwvnet** z 10.0.0.0/16 przestrzeni adresowej.
* Utwórz dwie podsieci o nazwie **appgwsubnet** i **appsubnet**.
* Tworzenie aplikacji małych bramy obsługi zakończenia tooend szyfrowania SSL tej wersji protokołów SSL limity i mechanizmów szyfrowania.

## <a name="before-you-begin"></a>Przed rozpoczęciem

tooconfigure zakończenia tooend SSL z bramy aplikacji, certyfikat jest wymagany dla bramy hello i certyfikaty są wymagane do hello serwerów wewnętrznej bazy danych. certyfikat bramy Hello jest używany tooencrypt i odszyfrowywania hello ruch wysyłany tooit przy użyciu protokołu SSL. certyfikat bramy Hello musi toobe Format Wymiana informacji osobistych (pfx). Tego formatu pliku umożliwia dla hello prywatnego klucza toobe wyeksportowane wymaganych przez hello aplikacji bramy tooperform hello szyfrowania i odszyfrowywania ruchu.

W celu tooend protokołu SSL szyfrowania hello wewnętrznej bazy danych musi być białej z bramy aplikacji. Jest to realizowane przez przekazywanie certyfikatu publicznego hello hello zapleczy toohello aplikacji bramy. Dzięki temu tej bramy aplikacji hello komunikuje się tylko z wystąpieniami znane wewnętrznej bazy danych. To dodatkowe zabezpiecza komunikację tooend hello.

Ten proces został opisany w hello następujące kroki:

## <a name="create-hello-resource-group"></a>Utwórz hello grupy zasobów

Ta sekcja przeprowadzi Cię przez proces tworzenia grupy zasobów, zawierającą hello bramy aplikacji.

### <a name="step-1"></a>Krok 1

Zaloguj się za tooyour konto platformy Azure.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Krok 2

Wybierz hello toouse subskrypcji dla tego scenariusza.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>Krok 3

Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Utwórz sieć wirtualną i podsieć bramy aplikacji hello

Witaj poniższy przykład tworzy sieć wirtualną z dwoma podsieciami. Podsieć jest bramy aplikacji hello toohold używane. Witaj innych podsieci jest używana dla aplikacji sieci web hello hostingu zapleczy hello.

### <a name="step-1"></a>Krok 1

Przypisz zakres adresów dla podsieci hello można użyć dla hello bramy aplikacji.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> Podsieci skonfigurowane dla bramy aplikacji należy ustalać poprawnie. Brama aplikacji można skonfigurować dla się too10 wystąpień. Każde wystąpienie ma jeden adres IP z podsieci hello. Zbyt małe podsieci może niekorzystnie wpłynąć na skalowanie w poziomie bramy aplikacji.
> 
> 

### <a name="step-2"></a>Krok 2

Przypisz adres toobe zakres używany do hello puli adresów zaplecza.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>Krok 3

Tworzenie sieci wirtualnej z podsieciami hello zdefiniowany w poprzednich krokach hello.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>Krok 4

Pobrać hello sieci wirtualnej zasobów i podsieć zasobów toobe używane w hello następujące kroki:

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Utwórz publiczny adres IP dla konfiguracji frontonu hello

Utwórz publiczny toobe zasobów adresu IP, używana przez bramę aplikacji hello. Ten publiczny adres IP jest używany następujący krok.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Brama aplikacji nie obsługuje użycia hello utworzony ze zdefiniowaną etykietą domeny publicznego adresu IP. Obsługiwane jest tylko publiczny adres IP z etykietą utworzony dynamicznie domeny. Jeśli potrzebujesz nazwy dns przyjazną dla bramy aplikacji hello, zaleca się zarejestrować toouse rekordu CNAME jako alias.

## <a name="create-an-application-gateway-configuration-object"></a>Tworzenie obiektu konfiguracji bramy aplikacji

Wszystkie elementy konfiguracji są ustawiane przed utworzeniem bramy aplikacji hello. Witaj następujące kroki tworzenia hello elementy konfiguracji, które są potrzebne dla zasobu bramy aplikacji.

### <a name="step-1"></a>Krok 1

Utwórz konfigurację IP bramy aplikacji, to ustawienie określa, jakie podsieci hello aplikacja używa bramy. Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci hello skonfigurowane i kieruje adresy IP toohello ruchu sieciowego w puli adresów IP zaplecza hello. Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>Krok 2

Tworzenie konfiguracji IP frontonu, to ustawienie mapuje ip prywatny lub publiczny adres toohello frontonu bramy aplikacji hello. powitania po kroku kojarzy hello publicznego adresu IP w hello poprzedzających krok konfiguracji IP frontonu hello.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>Krok 3

Skonfiguruj pulę adresów IP zaplecza hello hello adresy IP serwerów sieci web zaplecza hello. Te adresy IP są adresy IP hello otrzymujących hello ruchu sieciowego, który jest dostarczany z punktu końcowego adresu IP frontonu hello. Zastąp powitania po tooadd adresy IP własne punkty końcowe adresu IP aplikacji.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> W pełni kwalifikowaną nazwą domeny (FQDN) jest również prawidłową wartość zamiast adresu ip dla serwerów zaplecza hello za pomocą przełącznika - BackendFqdns hello. 

### <a name="step-4"></a>Krok 4

Skonfiguruj hello frontonu portu IP dla punktu końcowego hello publicznego adresu IP. Jest to port hello użytkownicy połączenie.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>Krok 5

Konfigurowanie certyfikatu hello hello bramy aplikacji. Ten certyfikat jest używany toodecrypt i Szyfruj ponownie ruch hello na bramie aplikacji hello.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> Ten przykład konfiguruje hello certyfikatu używanego na potrzeby połączenia SSL. certyfikat Hello musi toobe w formacie pfx, a hello hasło musi zawierać od 4 znaki too12.

### <a name="step-6"></a>Krok 6

Utwórz odbiornik HTTP hello hello bramy aplikacji. Przypisz hello konfiguracji ip frontonu, port i toouse certyfikatu SSL.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>Krok 7

Przekaż certyfikat hello z obsługą toobe używane na powitania SSL zasobów puli wewnętrznej bazy danych.

> [!NOTE]
> Witaj domyślnego badania pobiera hello klucza publicznego z hello **domyślne** powiązanie SSL na powitania zaplecza na adres IP i porównuje hello wartość klucza publicznego odbiera wartość klucza z publicznego toohello podanych tutaj. Witaj pobrany publiczny klucz może nie koniecznie hello przeznaczone lokacji toowhich ruch **Jeśli** korzystasz z nagłówkami hosta i SNI na powitania zaplecza. W razie wątpliwości, odwiedź stronę https://127.0.0.1/ na powitania zapleczy tooconfirm certyfikat, który jest używany dla hello **domyślne** powiązania SSL. W tej sekcji służą hello klucza publicznego z tym żądaniem. Jeśli korzystasz z nagłówkami hosta i SNI na powiązania HTTPS i z toohttps://127.0.0.1/ żądania ręczne przeglądarki na powitania zapleczy nie otrzymasz odpowiedź i certyfikatów, należy skonfigurować domyślne powiązanie SSL na powitania zapleczy. Jeśli nie zrobisz, sondy i zaplecza hello nie jest białej.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> certyfikat Hello opisane w tym kroku należy hello klucz publiczny certyfikatu pfx hello na powitania wewnętrznej bazy danych. Wyeksportuj certyfikat hello (nie hello certyfikatu głównego) zainstalowany na serwerze wewnętrznej bazy danych hello w. CER formatowania i używać go w tym kroku. Ten krok whitelists hello zaplecza bramy aplikacji hello.

### <a name="step-8"></a>Krok 8

Konfiguruj ustawienia http zaplecza bramy aplikacji hello. Przypisz certyfikat hello przekazany w hello poprzedzających krok toohello http ustawienia.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>Krok 9

Utwórz regułę routingu usługi równoważenia obciążenia, który konfiguruje zachowanie usługi równoważenia obciążenia hello. W tym przykładzie jest tworzona reguła podstawowe działanie okrężne.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>Krok 10

Skonfiguruj rozmiar wystąpienia hello hello bramy aplikacji.  są dostępne rozmiary Hello **standardowe\_małych**, **standardowe\_średni**, i **standardowe\_duży**.  Pojemności, hello dostępne wartości to 1 do 10.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> Liczba wystąpień 1 można wybrać do celów testowych. Ważne jest tooknow, że wszystkie wystąpienia liczba wystąpień w dwóch nie pasuje do żadnego hello umowy dotyczącej poziomu usług i dlatego nie zaleca się. Mała bramy są toobe używane dla deweloperów testu, a nie do celów produkcyjnych.

### <a name="step-11"></a>Krok 11

Skonfiguruj toobe zasad SSL hello używane na powitania Application Gateway. Brama aplikacji w obsługuje hello możliwości tooset minimalnej wersji dla wersji protokołu SSL.

Hello są następujące wartości listy wersji protokołów, które mogą zostać zdefiniowane.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

Ustawia hello wersji protocol minimalne zbyt**TLSv1_2** i umożliwia **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**i **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** tylko.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a>Utwórz hello bramy aplikacji

Za pomocą hello wszystkich poprzednich krokach, Utwórz hello Application Gateway. Tworzenie Hello bramy hello jest długo działające procesu.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>Ograniczenia wersji protokołu SSL na istniejącą bramę aplikacji

Witaj powyższych kroków przejście przez tworzenie aplikacji z tooend końcowych SSL i wyłączanie niektórych wersji protokołu SSL. Witaj poniższy przykład powoduje wyłączenie określone zasady SSL na istniejącą bramę aplikacji.

### <a name="step-1"></a>Krok 1

Pobrać tooupdate bramy aplikacji hello.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>Krok 2

Definiowanie zasad SSL. W hello poniższy przykład, TLSv1.0 i TLSv1.1 są wyłączone i hello mechanizmów szyfrowania **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, i  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** są jedynymi osobami dozwolone hello.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>Krok 3

Na koniec zaktualizuj hello bramy. Jest ważne toonote, że ten ostatni krok jest długo działające zadania. Po zakończeniu tooend końcowych SSL jest skonfigurowany dla bramy aplikacji hello.

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a>Pobieranie nazwy DNS bramy aplikacji

Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji. Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna. Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello. [Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo tego pobierania szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone. Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS. Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a>Następne kroki

Więcej informacji na temat wzmacniania zabezpieczeń hello aplikacji sieci web z zapory aplikacji sieci Web za pośrednictwem bramy aplikacji, odwiedzając [Omówienie zapory aplikacji sieci Web](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
