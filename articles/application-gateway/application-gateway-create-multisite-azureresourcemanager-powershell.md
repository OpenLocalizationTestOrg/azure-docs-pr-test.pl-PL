---
title: "aaaCreate bramę aplikacji dla wielu witryn | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate, skonfiguruj bramę aplikacji Azure do obsługi wielu aplikacji sieci web na powitania tą samą bramą."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a>Utwórz bramę aplikacji do obsługi wielu aplikacji sieci web

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)

Obsługa wielu lokacji pozwala toodeploy więcej niż jednej aplikacji sieci web na powitania tej samej bramy aplikacji. Opiera się na obecność nagłówek hosta w hello przychodzące żądanie HTTP, toodetermine odbiornika, które będzie odbierać dane. odbiornik Hello następnie kieruje ruch puli zaplecza tooappropriate zgodnie z konfiguracją w definicji reguły hello hello bramy. W aplikacji sieci web z włączonym protokołem SSL bramy aplikacji polega na powitania oznaczenia nazwy serwera (SNI) rozszerzenia toochoose hello poprawne odbiornika dla ruchu w sieci web hello. Zazwyczaj jest używane, do obsługi wielu lokacji tooload równoważenie żądań dla pul serwerów zaplecza toodifferent domeny innej witryny sieci web. Podobnie wielu poddomen powitalne tej samej domeny katalogu głównego może być również obsługiwane na hello tej samej bramy aplikacji.

## <a name="scenario"></a>Scenariusz

W hello poniższy przykład, bramy aplikacji jest obsługę ruchu dla domeny contoso.com i fabrikam.com z dwóch pul serwerów zaplecza: contoso puli serwerów i puli serwerów firmy fabrikam. Podobne instalacja może być poddomeny używane toohost jak app.contoso.com i blog.contoso.com.

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a>Przed rozpoczęciem

1. Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web. Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).
2. serwery Hello dodać bramę aplikacji hello toouse puli zaplecza toohello musi istnieć lub ich punkty końcowe utworzone w sieci wirtualnej hello w osobnej podsieci lub publicznego adresu IP/VIP przypisane.

## <a name="requirements"></a>Wymagania

* **Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello. wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP. Można także nazwę FQDN.
* **Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie. Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.
* **Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello. Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.
* **Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL). Dla bramy aplikacji obsługującej obejmujący wiele lokacji nazwy hosta i wskaźniki SNI są również został dodany.
* **Reguła:** reguły hello wiąże hello odbiornika, hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika. Reguły są przetwarzane w kolejności hello, są one wyświetlane, a ruch zostanie skierowany za pośrednictwem hello pierwszą regułę odpowiadającą niezależnie od szczegółowością. Na przykład jeśli masz przy użyciu odbiornika podstawowe reguły i zasady przy użyciu odbiornika obejmujący wiele lokacji zarówno na powitania sam port hello reguły z hello obejmujący wiele lokacji odbiornika musi być wymienione przed reguły hello przy hello odbiornika podstawowych, aby hello toofunction reguły obejmujący wiele lokacji jako Oczekiwano.

## <a name="create-an-application-gateway"></a>Tworzenie bramy aplikacji

następujące Hello są wymagane czynności hello toocreate bramę aplikacji:

1. Utworzenie grupy zasobów dla usługi Resource Manager.
2. Utwórz sieć wirtualną, podsieci i publicznego adresu IP dla bramy aplikacji hello.
3. Utworzenie obiektu konfiguracji bramy aplikacji.
4. Utworzenie zasobu bramy aplikacji.

## <a name="create-a-resource-group-for-resource-manager"></a>Tworzenie grupy zasobów dla usługi Resource Manager

Upewnij się, że używasz najnowszej wersji programu Azure PowerShell hello. Więcej informacji znajduje się w temacie [przy użyciu programu Windows PowerShell z usługą Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Krok 1

Zaloguj się za tooAzure

```powershell
Login-AzureRmAccount
```
Jesteś zostanie wyświetlony monit o tooauthenticate przy użyciu poświadczeń.

### <a name="step-2"></a>Krok 2

Sprawdź subskrypcje hello hello konta.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Krok 3

Wybierz z toouse Twojej subskrypcji platformy Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Krok 4

Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

Alternatywnie można również utworzyć tagi dla grupy zasobów dla bramy aplikacji:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Ta lokalizacja jest używana jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów. Upewnij się, że hello Użyj bramy aplikacji wszystkie polecenia toocreate tej samej grupie zasobów.

W powyższym przykładzie hello, utworzyliśmy grupę zasobów o nazwie **zarządcy zasobów appgw** z lokalizacji **zachodnie stany USA**.

> [!NOTE]
> Jeśli potrzebujesz tooconfigure sondowania niestandardowych dla bramy aplikacji, zobacz [Utwórz bramę aplikacji z niestandardowego sond przy użyciu programu PowerShell](application-gateway-create-probe-ps.md). Odwiedź stronę [monitorowanie kondycji i badania niestandardowych](application-gateway-probe-overview.md) Aby uzyskać więcej informacji.

## <a name="create-a-virtual-network-and-subnets"></a>Tworzenie sieci wirtualnej i podsieci

powitania po przykładzie pokazano, jak toocreate sieci wirtualnej za pomocą Menedżera zasobów. Dwie podsieci są tworzone w tym kroku. jest Hello pierwszej podsieci bramy aplikacji hello samej siebie. Brama aplikacji wymaga własnego toohold podsieci jego wystąpienia. Inne bramy aplikacji można wdrożyć w tej podsieci. Witaj drugiej podsieci jest serwerów wewnętrznej bazy danych aplikacji hello toohold używane.

### <a name="step-1"></a>Krok 1

Przypisz hello adres zakresu 10.0.0.0/24 toohello podsieci zmiennej toobe toohold używane hello bramy aplikacji.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a>Krok 2

Przypisz hello adres zakresu 10.0.1.0/24 toohello podsieć2 zmiennej toobe używany dla pul zaplecza hello.

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a>Krok 3

Tworzenie sieci wirtualnej o nazwie **appgwvnet** w grupie zasobów **zarządcy zasobów appgw** dla regionu zachodnie stany USA hello pomocą hello 10.0.0.0/16 prefiks podsieci 10.0.0.0/24, a 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a>Krok 4

Przypisanie zmiennej podsieci hello dalsze czynności, które tworzy bramę aplikacji.

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Utwórz publiczny adres IP dla konfiguracji frontonu hello

Utwórz zasób publicznego adresu IP **publicIP01** w grupie zasobów **zarządcy zasobów appgw** hello regionu zachodnie stany USA.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Adres IP jest przypisany toohello bramy aplikacji, po uruchomieniu usługi hello.

## <a name="create-application-gateway-configuration"></a>Tworzenie konfiguracji bramy aplikacji

Przed utworzeniem bramy aplikacji hello jest ma tooset wszystkie elementy konfiguracji. Witaj następujące kroki tworzenia hello elementy konfiguracji, które są potrzebne dla zasobu bramy aplikacji.

### <a name="step-1"></a>Krok 1

Utwórz konfigurację adresu IP bramy aplikacji o nazwie **gatewayIP01**. Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci hello skonfigurowane i tras adresów IP toohello ruchu sieciowego w puli adresów IP zaplecza hello. Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a>Krok 2

Skonfiguruj hello zaplecza puli adresów IP o nazwie **pool01** i **pool2** z adresami IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** dla **pool1** i **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  dla **pool2**.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

W tym przykładzie istnieją dwie pule zaplecza tooroute ruchu w sieci oparte na powitania żądanej witryny. Jedna pula odbiera ruch z lokacji "contoso.com" i innych puli odbiera ruch z lokacji "fabrikam.com". Masz hello tooreplace poprzedzających tooadd adresy IP własne punkty końcowe adresu IP aplikacji. Zamiast adresów IP można również użyć publiczne adresy IP, nazwy FQDN lub wirtualna karta sieciowa dla wystąpień wewnętrznej bazy danych. toospecify nazw FQDN, zamiast adresów IP w programie PowerShell Użyj "-BackendFQDNs" parametru.

### <a name="step-3"></a>Krok 3

Skonfiguruj ustawienia bramy aplikacji **poolsetting01** i **poolsetting02** hello równoważeniem obciążenia ruchu sieciowego w puli zaplecza hello. W tym przykładzie możesz skonfigurować ustawienia innej puli zaplecza hello pul zaplecza. Każda pula zaplecza może mieć własne ustawienia puli zaplecza.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Krok 4

Skonfiguruj IP frontonu hello publicznego adresu IP punktu końcowego.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Krok 5

Skonfiguruj hello portów frontonu bramy aplikacji.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a>Krok 6

Skonfiguruj dwa certyfikaty SSL dla witryny sieci Web hello dwa zamierzamy toosupport w tym przykładzie. Jeden certyfikat jest przeznaczona ruchu contoso.com i hello innych fabrikam.com ruchu. Te certyfikaty należy wystawił certyfikaty dla witryny sieci Web urzędu certyfikacji. Certyfikaty z podpisem własnym są obsługiwane, ale nie jest zalecane dla ruchu w środowisku produkcyjnym.

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a>Krok 7

W tym przykładzie, należy skonfigurować dwa odbiorniki dla Witaj dwie witryny sieci web. Ten krok obejmuje skonfigurowanie hello odbiorników dla publicznego adresu IP, portu i hosta tooreceive ruchu przychodzącego. Parametr nazwy hosta należy zestaw toohello odpowiedniej witryny sieci Web dla których hello ruch jest odbierany i jest wymagana do obsługi wielu lokacji. Element RequireServerNameIndication parametr należy ustawić tootrue dla witryn sieci Web, że wymagana jest obsługa protokołu SSL w przypadku wielu hostów. Jeśli wymagana jest obsługa protokołu SSL, należy również toospecify hello SSL certyfikatów czyli ruchu toosecure używanych dla tej aplikacji sieci web. Kombinacja Hello konfiguracji IP frontonu, elementu FrontendPort oraz nazwa hosta musi być unikatowy tooa odbiornika. Każdy odbiornik może obsługiwać jeden certyfikat.

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a>Krok 8

Utwórz dwie reguły ustawienie dla Witaj dwie aplikacje sieci web w tym przykładzie. Reguła wiąże ze sobą odbiorników, pul zaplecza i ustawienia protokołu http. Ten krok obejmuje skonfigurowanie hello aplikacji bramy toouse podstawowe reguły routingu, jeden dla każdej witryny sieci Web. Ruch tooeach witryny sieci Web jest odbierany przez jego skonfigurowany odbiornik i jest następnie przekierowywane tooits skonfigurować pulę zaplecza, za pomocą właściwości hello określone na powitania elementu BackendHttpSettings.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a>Krok 9

Konfigurowanie hello liczby wystąpień i rozmiaru bramy aplikacji hello.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Utwórz bramę aplikacji

Utwórz bramę aplikacji ze wszystkimi obiektami konfiguracji z hello w poprzednich krokach.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> Inicjowanie obsługi bramy aplikacji jest operacją wymagającą dużo czasu i może potrwać kilka toocomplete czas.
> 
> 

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

Dowiedz się, jak tooprotect witryny sieci Web z [Application Gateway - zapory aplikacji sieci Web](application-gateway-webapplicationfirewall-overview.md)

