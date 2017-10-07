---
title: "aaaCreate zasady bramę aplikacji przy użyciu routingu adresów URL | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate, skonfiguruj bramę aplikacji Azure przy użyciu reguł routingu adresów URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a>Utwórz bramę aplikacji przy użyciu routingu opartego na ścieżce

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](application-gateway-create-url-route-cli.md)

Na podstawie ścieżki routingu adresów URL umożliwia możesz tooassociate tras na podstawie hello ścieżki adresu URL żądania Http. Sprawdza, czy jest skonfigurowane dla adresu URL hello przedstawionych w hello brama aplikacji w puli zaplecza tooa trasy. Wysyła następnie toohello ruchu sieciowego hello zdefiniowanymi w puli zaplecza. Użycia routingu opartego na adres URL jest tooload równoważenie żądań dla pul serwerów zaplecza toodifferent różne typy zawartości.

Na podstawie adresu URL routingu wprowadza nową bramę tooapplication typ reguły. Brama aplikacji ma dwa typy zasad: podstawowe i PathBasedRouting. Podstawowe reguły typ zapewnia usługi okrężnego dla zaplecza hello pul podczas PathBasedRouting dodatkowo dystrybucji działania okrężnego tooround, uwzględnia również wzorzec ścieżki adresu URL żądania hello podczas wybierania hello puli wewnętrznej bazy danych.

## <a name="scenario"></a>Scenariusz

W hello poniższy przykład, bramy aplikacji jest obsługę ruchu dla domeny contoso.com z dwóch pul serwerów zaplecza: puli serwerów wideo i puli serwerów obrazu.

Żądania dla http://contoso.com/image * są kierowane puli serwerów tooimage (pool1), a http://contoso.com/video * są kierowane puli serwerów toovideo (pool2). Jeśli żadna hello ścieżki wzorców, domyślna pula serwera (pool1) jest zaznaczone.

![trasy adresu URL](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a>Przed rozpoczęciem

1. Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web. Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).
2. Utworzysz sieć wirtualna i podsieć bramy aplikacji. Upewnij się, że nie maszyny wirtualne lub wdrożenia chmury z hello podsieci. Brama aplikacji Hello należy samodzielnie w podsieci sieci wirtualnej.
3. serwery Hello dodać bramę aplikacji hello toouse puli zaplecza toohello musi istnieć lub ich punkty końcowe utworzone w sieci wirtualnej hello lub z publicznego adresu IP/VIP przypisane.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Co to jest wymagana toocreate bramę aplikacji?

* **Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello. wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.
* **Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie. Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.
* **Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello. Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.
* **Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).
* **Reguła:** reguły hello wiąże hello odbiornika, hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika.

## <a name="create-an-application-gateway"></a>Tworzenie bramy aplikacji

Różnica Hello przy użyciu klasycznego Azure i usługi Azure Resource Manager jest hello kolejność, w którym utworzyć bramę aplikacji hello i elementy hello toobe skonfigurowany.

Usługa Resource Manager wszystkie elementy bramy aplikacji są konfigurowane osobno, a następnie przekaż razem zasobu bramy aplikacji hello toocreate.

Poniżej przedstawiono kroki hello, które są potrzebne toocreate bramę aplikacji:

1. Utworzenie grupy zasobów dla usługi Resource Manager.
2. Tworzenie sieci wirtualnej, podsieci i publicznego adresu IP dla bramy aplikacji hello.
3. Utworzenie obiektu konfiguracji bramy aplikacji.
4. Utworzenie zasobu bramy aplikacji.

## <a name="create-a-resource-group-for-resource-manager"></a>Tworzenie grupy zasobów dla usługi Resource Manager

Upewnij się, że używasz najnowszej wersji programu Azure PowerShell hello. Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).

### <a name="step-1"></a>Krok 1

Zaloguj się za tooAzure

```powershell
Login-AzureRmAccount
```

Jesteś zostanie wyświetlony monit o tooauthenticate przy użyciu poświadczeń.<BR>

### <a name="step-2"></a>Krok 2

Sprawdź subskrypcje hello hello konta.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Krok 3

Wybierz z toouse Twojej subskrypcji platformy Azure. <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Krok 4

Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

Alternatywnie można również utworzyć tagi dla grupy zasobów dla bramy aplikacji:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Ta grupa zasobów jest używany jako domyślną lokalizacją plików hello zasobów w danej grupie zasobów. Upewnij się, że hello Użyj bramy aplikacji wszystkie polecenia toocreate tej samej grupie zasobów.

W powyższym przykładzie hello utworzono grupę zasobów o nazwie "zarządcy zasobów appgw" i lokalizacji "Zachodnie US".

> [!NOTE]
> Jeśli potrzebujesz tooconfigure sondowania niestandardowych dla bramy aplikacji, zobacz [Utwórz bramę aplikacji z niestandardowego sond przy użyciu programu PowerShell](application-gateway-create-probe-ps.md). Aby dowiedzieć się więcej, zapoznaj się z informacjami na temat [sond niestandardowych i monitorowania kondycji](application-gateway-probe-overview.md).
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Utwórz sieć wirtualną i podsieć bramy aplikacji hello

powitania po przykładzie pokazano, jak toocreate sieci wirtualnej za pomocą Menedżera zasobów. W tym przykładzie jest tworzony dla hello brama aplikacji w sieci Wirtualnej. Brama aplikacji wymaga jego własnej podsieci z tego powodu podsieci hello utworzone dla bramy aplikacji hello jest mniejszy niż hello przestrzeni adresowej sieci Wirtualnej. Dzięki temu innych zasobów, w tym, ale tooweb innymi serwerami toobe skonfigurowane w hello samo sieci Wirtualnej.

### <a name="step-1"></a>Krok 1

Przypisz zakres adresów hello 10.0.0.0/24 toocreate zmiennej toobe używane podsieci toohello sieci wirtualnej.  Spowoduje to utworzenie obiektu konfiguracji podsieci powitania dla bramy aplikacji, która jest używana w następnym przykładzie hello hello.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a>Krok 2

Tworzenie sieci wirtualnej o nazwie **appgwvnet** w grupie zasobów **zarządcy zasobów appgw** dla regionu zachodnie stany USA hello pomocą hello 10.0.0.0/16 prefiks podsieci 10.0.0.0/24. Na tym kończy się konfigurację hello hello sieć Wirtualną z jednej podsieci dla tooreside bramy aplikacji hello.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a>Krok 3

Przypisywanie zmienna podsieci hello hello kolejne kroki, to jest przekazywany toohello `New-AzureRMApplicationGateway` polecenia cmdlet w przyszłości kroku.

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Utwórz publiczny adres IP dla konfiguracji frontonu hello

Utwórz zasób publicznego adresu IP **publicIP01** w grupie zasobów **zarządcy zasobów appgw** hello regionu zachodnie stany USA. Brama aplikacji można użyć publicznego adresu IP, wewnętrzny adres IP lub obu żądań tooreceive Równoważenie obciążenia sieciowego.  W tym przykładzie używany jest tylko publiczny adres IP. W hello poniższy przykład Brak nazwy DNS jest skonfigurowany do tworzenia hello publicznego adresu IP.  Usługa Application Gateway nie obsługuje niestandardowych nazw DNS dla publicznych adresów IP.  Jeśli nazwy niestandardowego jest wymagany do hello publiczny punkt końcowy, rekord CNAME powinny być tworzone nazwy DNS są generowane automatycznie toohello toopoint hello publicznego adresu IP.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Adres IP jest przypisany toohello bramy aplikacji, po uruchomieniu usługi hello.

## <a name="create-application-gateway-configuration"></a>Tworzenie konfiguracji bramy aplikacji

Wszystkie elementy konfiguracji należy skonfigurować przed utworzeniem bramy aplikacji hello. Witaj następujące kroki tworzenia hello elementy konfiguracji, które są potrzebne dla zasobu bramy aplikacji.

### <a name="step-1"></a>Krok 1

Utwórz konfigurację adresu IP bramy aplikacji o nazwie **gatewayIP01**. Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci hello skonfigurowane i tras adresów IP toohello ruchu sieciowego w puli adresów IP zaplecza hello. Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a>Krok 2

Skonfiguruj hello zaplecza puli adresów IP o nazwie **pool01** i **pool2** z adresami IP **pool1** i **pool2**. Te adresy IP są adresami IP hello hello zasobów, które prowadzą hosting toobe aplikacji sieci web hello chronione przez bramę aplikacji hello. Tych elementów członkowskich puli wewnętrznej bazy danych są wszystkie zatwierdzone toobe dobrej kondycji przez sond sond podstawowego lub niestandardowego sondy.  Ruch jest następnie przekierowywany toothem podczas żądania wejścia hello bramy aplikacji. Pul zaplecza mogą być używane przez wiele reguł w ramach bramy aplikacji hello, co oznacza jednej puli wewnętrznej bazy danych można użyć dla wielu aplikacji sieci web, które znajdują się na powitania sam hosta.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

W tym przykładzie istnieją dwie pule zaplecza tooroute ruchu w sieci na podstawie hello ścieżki adresu URL. Jedna pula odbiera ruch ze ścieżki adresu URL „/video”, a druga pula odbiera ruch ze ścieżki „/image”. Zastąp hello poprzedzających tooadd adresy IP własne punkty końcowe adresu IP aplikacji. 

### <a name="step-3"></a>Krok 3

Skonfiguruj ustawienia bramy aplikacji **poolsetting01** i **poolsetting02** hello równoważeniem obciążenia ruchu sieciowego w puli zaplecza hello. W tym przykładzie możesz skonfigurować ustawienia innej puli zaplecza hello pul zaplecza. Każda pula zaplecza może mieć własne ustawienia puli zaplecza.  Ustawienia HTTP zaplecza są używane przez członków puli zaplecza poprawne toohello reguły tooroute ruchu. Określa hello protokół i port, który jest używany podczas wysyłania ruchu członków puli zaplecza toohello. Ustawienia HTTP zaplecza hello również ustala oparte na pliku cookie sesji.  U możliwia koligacji na podstawie plików cookie sesji wysyła toohello ruch tego samego wewnętrznej bazy danych jako poprzedniego żądania dla każdego pakietu.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Krok 4

Skonfiguruj IP frontonu hello publicznego adresu IP punktu końcowego. obiekt konfiguracji IP frontonu Hello służy hello toorelate odbiornika na zewnątrz, skierowane do adresu IP z hello odbiornika.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Krok 5

Skonfiguruj hello portów frontonu bramy aplikacji. obiekt konfiguracji portów frontonu Hello jest używany przez toodefine odbiornika, port bramy aplikacji hello nasłuchuje ruchu na powitania odbiornika.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a>Krok 6

Skonfiguruj odbiornik hello. Ten krok obejmuje skonfigurowanie odbiornika hello hello publicznego adresu IP i port używany tooreceive przychodzącego ruchu sieciowego. Poniższy przykład Hello przyjmuje konfiguracji IP frontonu hello wcześniej skonfigurowane, Konfiguracja portów frontonu i protokołu (http lub https) i konfiguruje hello odbiornika. W tym przykładzie odbiornika hello nasłuchuje tooHTTP ruch na porcie 80 hello publiczny adres IP, który został utworzony wcześniej.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a>Krok 7

Konfiguruj adres URL reguły ścieżki dla pul zaplecza hello. Ten krok umożliwia skonfigurowanie ścieżki względnej hello używany przez bramę aplikacji i definiuje mapowanie hello między hello ścieżki adresu URL oraz pulę zaplecza hello jest przypisany toohandle hello przychodzący ruch.

> [!IMPORTANT]
> Każda ścieżka musi rozpoczynać się od / i miejsce tylko hello "\*" jest dozwolone, znajduje się na końcu hello. Nieprawidłowa przykładów /xyz, /xyz* lub/xyz / *. Hello ciąg przekazywani toohello dopasowania ścieżki nie zawiera żadnego tekstu po hello najpierw "?" lub "#", a te znaki są niedozwolone. 

Witaj poniższy przykład tworzy dwie reguły: jeden dla "/ obrazu /" ścieżkę routingu ruchu tooback-end "pool1" a innym dla ścieżki "/ wideo /" routingu ruchu tooback-end "pool2." Te reguły Sprawdź, czy ruchu dla każdego zestawu adresów URL jest kierowany toohello wewnętrznej bazy danych. Na przykład http://contoso.com/image/figure1.jpg przechodzi toopool1 i http://contoso.com/video/example.mp4 przechodzi toopool2.

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

Jeśli ścieżka hello nie odpowiada żadnemu z reguły ścieżki wstępnie zdefiniowane hello, hello reguły ścieżki mapy konfiguracji konfiguruje również domyślna pula adresów zaplecza. Na przykład http://contoso.com/shoppingcart/test.html przechodzi toopool1 określone jako hello domyślnej puli niedopasowane ruchu.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a>Krok 8

Utwórz ustawienie reguły. Ten krok obejmuje skonfigurowanie hello aplikacji bramy toouse routingu adresów URL na podstawie ścieżki. Witaj `$urlPathMap` zmiennej zdefiniowanej w hello wcześniejszym kroku jest teraz używane toocreate hello na podstawie ścieżki reguły. W tym kroku reguły hello powiązane z odbiornika i mapowanie ścieżki adresu url hello utworzony wcześniej.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a>Krok 9

Konfigurowanie hello liczby wystąpień i rozmiaru bramy aplikacji hello.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Utwórz bramę aplikacji

Utwórz bramę aplikacji ze wszystkimi obiektami konfiguracji z hello w poprzednich krokach.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a>Pobieranie nazwy DNS bramy aplikacji

Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji. Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna. Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello. [Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure hello frontonu rekordu IP CNAME Pobieranie szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone. Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME. Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.

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

Jeśli toolearn odciążanie protokołu Secure Sockets Layer (SSL), zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl-arm.md).

