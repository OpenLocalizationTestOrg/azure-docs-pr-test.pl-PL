---
title: "aaaConfigure SSL odciążania — brama usługi aplikacji Azure — PowerShell | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate bramę aplikacji przy użyciu protokołu SSL Odciążanie przy użyciu usługi Azure Resource Manager"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>Konfigurowanie bramy aplikacji na potrzeby odciążania protokołu SSL przy użyciu usługi Azure Resource Manager

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-ssl-arm.md)
> * [Klasyczny portal Azure — program PowerShell](application-gateway-ssl.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-ssl-cli.md)

Brama aplikacji w Azure może być sesji protokołu Secure Sockets Layer (SSL) hello tooterminate skonfigurowanych na powitania bramy tooavoid kosztowne SSL odszyfrowywania zadania toohappen na powitania kolektywu serwerów sieci web. Odciążanie protokołu SSL także upraszcza powitania serwera frontonu Konfiguracja i zarządzanie hello aplikacji sieci web.

## <a name="before-you-begin"></a>Przed rozpoczęciem

1. Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web. Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).
2. Możesz utworzyć sieć wirtualną i podsieć bramy aplikacji hello. Upewnij się, że nie maszyny wirtualne lub wdrożenia chmury z hello podsieci. Usługa Application Gateway musi sama znajdować się w podsieci sieci wirtualnej.
3. serwery Hello konfigurowania bramy aplikacji hello toouse musi istnieć lub ich punkty końcowe utworzone w sieci wirtualnej hello lub z publicznego adresu IP/VIP przypisane.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Co to jest wymagana toocreate bramę aplikacji?

* **Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello. wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.
* **Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie. Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.
* **Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello. Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.
* **Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te ustawienia są z uwzględnieniem wielkości liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).
* **Reguła:** reguła hello wiąże odbiornika hello i hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika. Obecnie tylko hello *podstawowe* reguła jest obsługiwana. Witaj *podstawowe* reguła jest rozkład obciążenia okrężnego.

**Uwagi dotyczące konfiguracji dodatkowych**

Do konfigurowania certyfikatów SSL, hello protokół **HttpListener** należy zmienić zbyt*Https* (z uwzględnieniem wielkości liter). Witaj **SslCertificate** zbyt dodany element**HttpListener** z wartości zmiennej hello skonfigurowanej dla certyfikatu SSL hello. port frontonu Hello powinien być zaktualizowany too443.

**koligacji na podstawie plików cookie tooenable**: bramy aplikacji może być skonfigurowany tooensure żądania z sesji klienta jest zawsze ukierunkowanej toohello tej samej maszyny Wirtualnej w hello kolektywu serwerów sieci web. W tym scenariuszu odbywa się przez uruchomienie pliku cookie sesji, umożliwiającą hello bramy toodirect ruch odpowiednio. Ustaw koligacji na podstawie plików cookie tooenable **CookieBasedAffinity** za*włączone* w hello **elementu BackendHttpSettings** elementu.

## <a name="create-an-application-gateway"></a>Tworzenie bramy aplikacji

Różnica Hello przy użyciu hello Azure klasycznego modelu wdrażania i usługi Azure Resource Manager jest kolejności hello tworzenie aplikacji bramy i hello elementy toobe skonfigurowany.

Usługa Resource Manager wszystkie składniki bramy aplikacji są konfigurowane osobno, a następnie przekaż razem toocreate zasobów bramy aplikacji.

Oto toocreate kroki niezbędne hello bramę aplikacji:

1. Tworzenie grupy zasobów dla usługi Resource Manager
2. Tworzenie sieci wirtualnej, podsieci i publicznego adresu IP dla bramy aplikacji hello
3. Tworzenie obiektu konfiguracji bramy aplikacji
4. Tworzenie zasobu bramy aplikacji

## <a name="create-a-resource-group-for-resource-manager"></a>Tworzenie grupy zasobów dla usługi Resource Manager

Upewnij się, że przełącznika poleceń cmdlet programu PowerShell tryb toouse hello Azure Resource Manager. Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).

### <a name="step-1"></a>Krok 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Krok 2

Sprawdź subskrypcje hello hello konta.

```powershell
Get-AzureRmSubscription
```

Jesteś zostanie wyświetlony monit o tooauthenticate przy użyciu poświadczeń.

### <a name="step-3"></a>Krok 3

Wybierz z toouse Twojej subskrypcji platformy Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Krok 4

Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. To ustawienie jest używane jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów. Upewnij się, że wszystkie toocreate polecenia używa bramy aplikacji hello same grupy zasobów.

W powyższym przykładzie hello, utworzyliśmy grupę zasobów o nazwie **zarządcy zasobów appgw** i lokalizację **zachodnie stany USA**.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Utwórz sieć wirtualną i podsieć bramy aplikacji hello

powitania po przykładzie pokazano, jak toocreate sieci wirtualnej za pomocą Menedżera zasobów:

### <a name="step-1"></a>Krok 1

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

W tym przykładzie przypisuje hello adres zakresu 10.0.0.0/24 tooa podsieci zmiennej toobe używane toocreate sieci wirtualnej.

### <a name="step-2"></a>Krok 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

Ten przykład tworzy sieć wirtualną o nazwie **appgwvnet** w grupie zasobów **zarządcy zasobów appgw** dla regionu zachodnie stany USA hello pomocą hello 10.0.0.0/16 prefiks podsieci 10.0.0.0/24.

### <a name="step-3"></a>Krok 3

```powershell
$subnet = $vnet.Subnets[0]
```

W tym przykładzie przypisuje hello podsieci obiektu toovariable $subnet hello dalsze czynności.

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Utwórz publiczny adres IP dla konfiguracji frontonu hello

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Ten przykład tworzy zasób publicznego adresu IP **publicIP01** w grupie zasobów **zarządcy zasobów appgw** hello regionu zachodnie stany USA.

## <a name="create-an-application-gateway-configuration-object"></a>Tworzenie obiektu konfiguracji bramy aplikacji

### <a name="step-1"></a>Krok 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Ten przykład tworzy konfigurację IP bramy dla aplikacji o nazwie **gatewayIP01**. Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci hello skonfigurowane i tras adresów IP toohello ruchu sieciowego w puli adresów IP zaplecza hello. Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.

### <a name="step-2"></a>Krok 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

Ten przykład konfiguruje hello zaplecza puli adresów IP o nazwie **pool01** z adresami IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** . Te wartości są adresy IP hello otrzymujących hello ruchu sieciowego, który jest dostarczany z punktu końcowego adresu IP frontonu hello. Zastąp hello adresów IP z hello poprzedzających przykład z adresami IP hello punktów końcowych aplikacji sieci web.

### <a name="step-3"></a>Krok 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

Ten przykład konfiguruje ustawienia bramy aplikacji **poolsetting01** zrównoważonym tooload ruchu sieciowego w puli zaplecza hello.

### <a name="step-4"></a>Krok 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

Ten przykład konfiguruje hello frontonu portu IP o nazwie **frontendport01** dla punktu końcowego hello publicznego adresu IP.

### <a name="step-5"></a>Krok 5

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

Ten przykład konfiguruje hello certyfikatu używanego na potrzeby połączenia SSL. certyfikat Hello musi toobe w formacie pfx, a hello hasło musi zawierać od 4 znaki too12.

### <a name="step-6"></a>Krok 6

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

Ten przykład tworzy hello frontonu konfiguracji IP o nazwie **fipconfig01** i publicznego adresu IP z konfiguracji IP frontonu hello hello współpracowników.

### <a name="step-7"></a>Krok 7

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

Ten przykład tworzy nazwę odbiornika hello **listener01** i skojarzone hello konfiguracji IP frontonu toohello portów frontonu i certyfikatu.

### <a name="step-8"></a>Krok 8

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Ten przykład tworzy hello reguły modułu równoważenia obciążenia routingu o nazwie **rule01** który konfiguruje zachowanie usługi równoważenia obciążenia hello.

### <a name="step-9"></a>Krok 9

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Ten przykład konfiguruje hello rozmiar wystąpienia bramy aplikacji hello.

> [!NOTE]
> Witaj wartości domyślnej dla *InstanceCount* 2, maksymalna wartość 10. Witaj wartości domyślnej dla *GatewaySize* to średni. Możesz wybrać następujące wartości: Standard_Small, Standard_Medium i Standard_Large.

### <a name="step-10"></a>Krok 10

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

W tym kroku definiowana toouse zasad SSL hello na bramie aplikacji hello. Odwiedź stronę [skonfigurować protokół SSL wersje zasad i mechanizmów szyfrowania w bramie aplikacji](application-gateway-configure-ssl-policy-powershell.md) toolearn więcej.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Tworzenie bramy aplikacji przy użyciu polecenia New-AzureApplicationGateway

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

Ten przykład tworzy bramę aplikacji z wszystkich elementów konfiguracji z hello w poprzednich krokach. Przykład Witaj bramy aplikacji hello nosi nazwę **appgwtest**.

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

Jeśli chcesz tooconfigure toouse bramy aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB), zobacz [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).

Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

