---
title: "Konfigurowanie protokołu SSL trasie do bramy aplikacji Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób konfigurowania kompleksowe SSL z bramy aplikacji przy użyciu programu PowerShell usługi Azure Resource Manager"
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
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a>Konfigurowanie protokołu SSL trasie do bramy aplikacji przy użyciu programu PowerShell

## <a name="overview"></a>Omówienie

Brama aplikacji w obsługuje pełnego szyfrowania ruchu. Polega to na tym, że usługa Application Gateway przerywa połączenie SSL na bramie aplikacji. Następnie brama stosuje do ruchu reguły routingu, ponownie szyfruje pakiet i przekazuje pakiet do odpowiedniego serwera zaplecza na podstawie zdefiniowanych reguł routingu. Każda odpowiedź z serwera sieci Web przechodzi przez ten sam proces z powrotem do użytkownika końcowego.

Inna funkcja tej bramy aplikacji obsługuje Określanie niestandardowych opcji protokołu SSL. Brama aplikacji w obsługuje wyłączenie Następująca wersja protokołu; **TLSv1.0**, **TLSv1.1**, i **TLSv1.2** jako również definiowanie którego mechanizmy według priorytetu i szyfrowania.  Aby dowiedzieć się więcej na temat opcji SSL można skonfigurować, odwiedź stronę [Przegląd zasad SSL](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> Protokół SSL 2.0 i 3.0 protokołu SSL są domyślnie wyłączone i nie można włączyć. One są uważane za niebezpieczne i nie będą mogły być używane z bramy aplikacji.

![Scenariusz obrazu][scenario]

## <a name="scenario"></a>Scenariusz

W tym scenariuszu Dowiedz się jak utworzyć bramę aplikacji przy użyciu pełnego protokołu SSL przy użyciu programu PowerShell.

W tym scenariuszu obejmują:

* Utwórz grupę zasobów o nazwie **zarządcy zasobów appgw**
* Tworzenie sieci wirtualnej o nazwie **appgwvnet** z 10.0.0.0/16 przestrzeni adresowej.
* Utwórz dwie podsieci o nazwie **appgwsubnet** i **appsubnet**.
* Utwórz bramę małych aplikacji obsługi pełnego szyfrowania SSL w tej wersji protokołów SSL limity i mechanizmów szyfrowania.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Aby skonfigurować protokół SSL kompleksowe z bramy aplikacji, certyfikat jest wymagany dla bramy i certyfikaty są wymagane dla serwerów zaplecza. Certyfikat bramy jest używany do szyfrowania i odszyfrowywania ruchu wysyłane do niego przy użyciu protokołu SSL. Certyfikat bramy musi mieć format wymiana informacji osobistych (pfx). Ten format pliku umożliwia klucz prywatny można wyeksportować co jest wymagane przez bramę aplikacji do szyfrowania i deszyfrowania ruchu.

Do szyfrowania SSL kompleksowe wewnętrznej bazy danych musi być białej z bramy aplikacji. Jest to realizowane przez przekazywanie publicznego certyfikatu zapleczy na bramie aplikacji. Dzięki temu, że bramy aplikacji komunikuje się wyłącznie z wystąpień znane wewnętrznej bazy danych. To dodatkowe zabezpiecza komunikację pełnego.

Ten proces jest opisane w poniższych krokach:

## <a name="create-the-resource-group"></a>Utwórz grupę zasobów

Ta sekcja przeprowadzi Cię przez proces tworzenia grupy zasobów, zawierającą bramy aplikacji.

### <a name="step-1"></a>Krok 1

Zaloguj się do konta platformy Azure.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Krok 2

Wybierz subskrypcję do użycia na potrzeby tego scenariusza.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>Krok 3

Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a>Tworzenie sieci wirtualnej i podsieci dla bramy aplikacji

Poniższy przykład tworzy sieć wirtualną z dwoma podsieciami. W jednej podsieci jest używany do przechowywania bramy aplikacji. Innych podsieci jest używana do zapleczy hosting aplikacji sieci web.

### <a name="step-1"></a>Krok 1

Przypisz zakres adresów dla tej podsieci, można użyć dla bramy aplikacji.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> Podsieci skonfigurowane dla bramy aplikacji należy ustalać poprawnie. Brama aplikacji można skonfigurować dla maksymalnie 10 wystąpień. Każde wystąpienie ma jeden adres IP z podsieci. Zbyt małe podsieci może niekorzystnie wpłynąć na skalowanie w poziomie bramy aplikacji.
> 
> 

### <a name="step-2"></a>Krok 2

Przypisz zakres adresów do użycia dla puli adresów zaplecza.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>Krok 3

Tworzenie sieci wirtualnej z podsieciami zdefiniowane w powyższych kroków.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>Krok 4

Pobieranie zasobu sieci wirtualnej i zasoby podsieci do użycia w kolejnych krokach:

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a>Tworzenie publicznego adresu IP dla konfiguracji frontonu

Utwórz zasób publicznego adresu IP do użycia dla bramy aplikacji. Ten publiczny adres IP jest używany następujący krok.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Brama aplikacji nie obsługuje korzystanie z publicznego adresu IP utworzony ze zdefiniowaną etykietą domeny. Obsługiwane jest tylko publiczny adres IP z etykietą utworzony dynamicznie domeny. Jeśli potrzebujesz dns przyjazną nazwę bramy aplikacji, zaleca się przy użyciu rekordu CNAME jako alias.

## <a name="create-an-application-gateway-configuration-object"></a>Tworzenie obiektu konfiguracji bramy aplikacji

Wszystkie elementy konfiguracji są ustawiane przed utworzeniem bramy aplikacji. Poniższe kroki umożliwiają utworzenie elementów konfiguracji wymaganych w przypadku zasobu bramy aplikacji.

### <a name="step-1"></a>Krok 1

Utwórz konfigurację IP bramy aplikacji, to ustawienie określa, jakie podsieci używa bramy aplikacji. Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci skonfigurowane i kieruje ruchem sieciowym na adresy IP w puli adresów IP zaplecza. Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>Krok 2

Tworzenie konfiguracji IP frontonu, to ustawienie mapuje adres prywatny lub publiczny ip frontonu bramy aplikacji. Następny krok kojarzy publicznego adresu IP w poprzednim kroku z konfiguracją IP frontonu.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>Krok 3

Skonfiguruj pulę adresów IP zaplecza z adresami IP serwerów sieci web zaplecza. Będą to adresy IP odbierające ruch sieciowy pochodzący z punktu końcowego adresu IP frontonu. Można zastąpić następujące adresy IP, aby dodać własne punkty końcowe adresu IP aplikacji.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> W pełni kwalifikowaną nazwą domeny (FQDN) jest również prawidłową wartość zamiast adresu ip dla serwerów zaplecza za pomocą przełącznika - BackendFqdns. 

### <a name="step-4"></a>Krok 4

Skonfiguruj port IP frontonu publiczny punkt końcowy IP. Jest to port, podłączoną do użytkowników końcowych.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>Krok 5

Konfigurowanie certyfikatu dla bramy aplikacji. Ten certyfikat służy do odszyfrowania i Szyfruj ponownie ruch na bramie aplikacji.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> Ten przykład umożliwia skonfigurowanie certyfikatu używanego na potrzeby połączenia SSL. Certyfikat musi być w formacie PFX, a hasło musi składać się z 4–12 znaków.

### <a name="step-6"></a>Krok 6

Utwórz odbiornik HTTP bramy aplikacji. Przypisywanie konfiguracji ip frontonu, port i certyfikat protokołu SSL.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>Krok 7

Przekaż certyfikat do użycia z włączonym protokołem SSL wewnętrznej bazy danych puli zasobów.

> [!NOTE]
> Domyślnego badania pobiera klucza publicznego z **domyślne** powiązanie SSL na adres IP zaplecza na i porównuje wartość klucza publicznego odbiera wartość klucza publicznego zostanie podana tutaj. Pobrane klucz publiczny nie musi być planowanej lokacji, do których ruch **Jeśli** korzystasz z nagłówkami hosta i SNI na zaplecza. W razie wątpliwości, odwiedź stronę https://127.0.0.1/ na zapleczy, aby potwierdzić, certyfikat, który jest używany dla **domyślne** powiązania SSL. W tej sekcji, Użyj klucza publicznego z tym żądaniem. Jeśli korzystasz z nagłówkami hosta i SNI na powiązania HTTPS i nie otrzymasz odpowiedź i certyfikatu z żądanie przeglądarki ręczne do https://127.0.0.1/ na końcach Wstecz, należy skonfigurować domyślne powiązanie SSL na końcach Wstecz. Jeśli nie zrobisz, sondy i zaplecza, nie jest białej.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> Certyfikat w tym kroku należy klucz publiczny certyfikatu pfx na wewnętrznej bazy danych. Wyeksportuj certyfikat (nie certyfikatu głównego) zainstalowany na serwerze wewnętrznej bazy danych w. CER formatowania i używać go w tym kroku. Ten krok whitelists zaplecza bramy aplikacji.

### <a name="step-8"></a>Krok 8

Konfiguruj ustawienia http zaplecza bramy aplikacji. Przypisać certyfikat przekazany w poprzednim kroku w ustawieniach protokołu http.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>Krok 9

Utwórz regułę routingu usługi równoważenia obciążenia, który konfiguruje zachowanie usługi równoważenia obciążenia. W tym przykładzie jest tworzona reguła podstawowe działanie okrężne.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>Krok 10

Skonfiguruj rozmiar wystąpienia bramy aplikacji.  Dostępne rozmiary są **standardowe\_małych**, **standardowe\_średni**, i **standardowe\_duży**.  Pojemność dostępne wartości to 1 do 10.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> Liczba wystąpień 1 można wybrać do celów testowych. Jest ważne dowiedzieć się, że dowolnej liczby wystąpień w obszarze dwa wystąpienia nie pasuje do żadnego umowy SLA i dlatego nie zaleca się. Mała bramy są używane dla deweloperów testu, a nie do celów produkcyjnych.

### <a name="step-11"></a>Krok 11

Skonfiguruj zasady SSL, który ma być używany dla bramy aplikacji. Brama aplikacji w obsługuje możliwość określenia minimalnej wersji dla wersji protokołu SSL.

Listę wersji protokołów, które mogą być definiowane są następujące wartości.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

Ustawia wersję protokołu minimalna **TLSv1_2** i umożliwia **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**i  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** tylko.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a>Utwórz bramę aplikacji

Przy użyciu powyższych kroków, Utwórz bramę aplikacji. Tworzenie bramy jest długo działające procesu.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>Ograniczenia wersji protokołu SSL na istniejącą bramę aplikacji

Powyższych kroków przejście do tworzenia aplikacji przy użyciu protokołu SSL pełnego i wyłączenie niektórych wersji protokołu SSL. Poniższy przykład powoduje wyłączenie określone zasady SSL na istniejącą bramę aplikacji.

### <a name="step-1"></a>Krok 1

Pobiera bramę aplikacji, aby zaktualizować.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>Krok 2

Definiowanie zasad SSL. W poniższym przykładzie TLSv1.0 i TLSv1.1 są wyłączone i mechanizmów szyfrowania **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, i  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** są jedynymi osobami, które są dozwolone.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>Krok 3

Na koniec zaktualizuj bramy. Należy pamiętać, że ten ostatni krok jest długo działające zadania. Po zakończeniu pełnego SSL jest skonfigurowany na bramie aplikacji.

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a>Pobieranie nazwy DNS bramy aplikacji

Po utworzeniu bramy następnym krokiem jest skonfigurowanie frontonu na potrzeby komunikacji. Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna. Aby upewnić się, że użytkownicy końcowi mogą trafić bramę aplikacji, można użyć rekordu CNAME w celu wskazania publicznego punktu końcowego bramy aplikacji. [Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). Aby to zrobić, pobierz szczegóły bramy aplikacji i skojarzony adres IP oraz nazwę DNS, używając elementu PublicIPAddress dołączonego do bramy aplikacji. Nazwa DNS bramy aplikacji powinna zostać użyta w celu utworzenia rekordu CNAME, który wskazuje dwóm aplikacjom sieci Web tę nazwę DNS. Korzystanie z rekordów A nie jest zalecane, ponieważ adres VIP może ulec zmianie po ponownym uruchomieniu bramy aplikacji.

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

Więcej informacji na temat wzmacniania zabezpieczeń aplikacji sieci web z zapory aplikacji sieci Web za pośrednictwem bramy aplikacji, odwiedzając [Omówienie zapory aplikacji sieci Web](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
