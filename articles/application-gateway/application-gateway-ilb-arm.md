---
title: "Brama aplikacji Azure z wewnętrznego modułu równoważenia obciążenia - PowerShell aaaUsing | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate, skonfigurować, uruchomić i usunąć bramę aplikacji Azure z wewnętrznego modułu równoważenia obciążenia (ILB) dla usługi Azure Resource Manager"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a>Tworzenie i konfigurowanie bramy aplikacji przy użyciu wewnętrznego modułu równoważenia obciążenia i usługi Azure Resource Manager

> [!div class="op_single_selector"]
> * [Klasyczny portal Azure — program PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager — program PowerShell](application-gateway-ilb-arm.md)

Brama aplikacji w Azure można skonfigurować z adresów VIP połączonych z Internetem lub wewnętrzny punkt końcowy, który nie jest narażonych toohello Internet, znanej także jako punkt końcowy (ILB) usługi równoważenia obciążenia wewnętrznego. Konfigurowanie bramy hello z ILB jest przydatne w przypadku wewnętrznych aplikacji — biznesowych, które nie są uwidocznione toohello Internet. Jest również przydatne w przypadku usług i warstwy aplikacji wielowarstwowych, które znajdują się w granicy zabezpieczeń, który nie jest narażonych toohello Internet, ale nadal wymagają okrężnego obciążenia dystrybucji, lepkości sesji lub zakończenie protokołu Secure Sockets Layer (SSL).

W tym artykule przedstawiono hello kroki tooconfigure bramę aplikacji z ILB.

## <a name="before-you-begin"></a>Przed rozpoczęciem

1. Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web. Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).
2. Utworzysz sieć wirtualną i podsieć dla usługi Application Gateway. Upewnij się, że nie maszyny wirtualne lub wdrożenia chmury z hello podsieci. Usługa Application Gateway musi sama znajdować się w podsieci sieci wirtualnej.
3. Skonfigurowanie bramy aplikacji hello toouse serwerów Hello musi istnieć lub mieć przypisane ich punkty końcowe utworzone w sieci wirtualnej hello lub z publicznego adresu IP/VIP.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Co to jest wymagana toocreate bramę aplikacji?

* **Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello. Witaj wymienionych na liście adresów IP powinien albo należy toohello sieci wirtualnej, ale w innej podsieci bramy aplikacji hello lub powinny być publicznego adresu IP/VIP.
* **Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie. Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.
* **Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello. Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.
* **Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).
* **Reguła:** reguła hello wiąże odbiornika hello i hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika. Obecnie tylko hello *podstawowe* reguła jest obsługiwana. Witaj *podstawowe* reguła jest rozkład obciążenia okrężnego.

## <a name="create-an-application-gateway"></a>Tworzenie bramy aplikacji

Różnica Hello przy użyciu klasycznego Azure i usługi Azure Resource Manager jest hello kolejność, w którym utworzyć bramę aplikacji hello i elementy hello toobe skonfigurowany.
Usługa Resource Manager wszystkie elementy bramy aplikacji jest skonfigurowany oddzielnie, a następnie przekaż razem zasobu bramy aplikacji hello toocreate.

Poniżej przedstawiono kroki hello, które są potrzebne toocreate bramę aplikacji:

1. Tworzenie grupy zasobów dla usługi Resource Manager
2. Utwórz sieć wirtualną i podsieć bramy aplikacji hello
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

Utwórz nową grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Służy to jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów. Upewnij się, że wszystkie toocreate polecenia używa bramy aplikacji hello same grupy zasobów.

Przykład poprzedzających hello utworzyliśmy grupę zasobów o nazwie "Zarządcy zasobów appgw" i lokalizacji "zachodnie stany USA".

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Utwórz sieć wirtualną i podsieć bramy aplikacji hello

powitania po przykładzie pokazano, jak toocreate sieci wirtualnej za pomocą Menedżera zasobów:

### <a name="step-1"></a>Krok 1

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Ten krok przypisuje hello adres zakresu 10.0.0.0/24 tooa podsieci zmiennej toobe używane toocreate sieci wirtualnej.

### <a name="step-2"></a>Krok 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

Spowoduje to utworzenie sieci wirtualnej o nazwie "appgwvnet" w zasobów grupy "appgw-zarządcy zasobów" dla regionu zachodnie stany USA hello pomocą hello 10.0.0.0/16 prefiks podsieci 10.0.0.0/24.

### <a name="step-3"></a>Krok 3

```powershell
$subnet = $vnet.subnets[0]
```

Ten krok przypisuje hello podsieci obiektu toovariable $subnet hello dalsze czynności.

## <a name="create-an-application-gateway-configuration-object"></a>Tworzenie obiektu konfiguracji bramy aplikacji

### <a name="step-1"></a>Krok 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Spowoduje to utworzenie konfiguracji IP bramy dla aplikacji o nazwie "gatewayIP01". Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci hello skonfigurowane i tras adresów IP toohello ruchu sieciowego w puli adresów IP zaplecza hello. Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.

### <a name="step-2"></a>Krok 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

Ten krok obejmuje skonfigurowanie hello zaplecza puli adresów IP o nazwie "pool01" z adresem IP, adresy "10.1.1.8, 10.1.1.9, 10.1.1.10". Są to adresy IP hello otrzymujących hello ruchu sieciowego, który jest dostarczany z punktu końcowego adresu IP frontonu hello. Zastąp hello poprzedzających tooadd adresy IP własne punkty końcowe adresu IP aplikacji.

### <a name="step-3"></a>Krok 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Ten krok obejmuje skonfigurowanie ruchu sieciowego bramy ustawienie "poolsetting01" hello obciążenia zrównoważonym aplikacji w puli zaplecza hello.

### <a name="step-4"></a>Krok 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

Ten krok obejmuje skonfigurowanie hello o nazwie "frontendport01" hello ILB frontonu portów IP.

### <a name="step-5"></a>Krok 5

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

Ten krok hello frontonu konfiguracji IP o nazwie "fipconfig01" tworzy i kojarzy ją z prywatnego adresu IP z hello bieżącej podsieci sieci wirtualnej.

### <a name="step-6"></a>Krok 6

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

Ten krok hello odbiornik o nazwie "listener01" tworzy i kojarzy hello portów frontonu toohello frontonu konfiguracji IP.

### <a name="step-7"></a>Krok 7

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Spowoduje to utworzenie hello reguły modułu równoważenia obciążenia routingu o nazwie "rule01", który konfiguruje zachowanie usługi równoważenia obciążenia hello.

### <a name="step-8"></a>Krok 8

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Ten krok obejmuje skonfigurowanie hello rozmiar wystąpienia bramy aplikacji hello.

> [!NOTE]
> Witaj wartości domyślnej dla *InstanceCount* 2, maksymalna wartość 10. Witaj wartości domyślnej dla *GatewaySize* to średni. Możesz wybrać następujące wartości: Standard_Small, Standard_Medium i Standard_Large.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Tworzenie bramy aplikacji przy użyciu polecenia New-AzureApplicationGateway

Tworzy bramę aplikacji z wszystkich elementów konfiguracji z hello w poprzednich krokach. W tym przykładzie bramy aplikacji hello jest nazywany "appgwtest".

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

Ten krok tworzy bramę aplikacji z wszystkich elementów konfiguracji z hello w poprzednich krokach. Przykład Witaj bramy aplikacji hello jest nazywany "appgwtest".

## <a name="delete-an-application-gateway"></a>Usuwanie bramy aplikacji

toodelete bramę aplikacji należy hello toodo następujące kroki w kolejności:

1. Użyj hello `Stop-AzureRmApplicationGateway` bramy hello toostop polecenia cmdlet.
2. Użyj hello `Remove-AzureRmApplicationGateway` bramy hello tooremove polecenia cmdlet.
3. Sprawdź tej bramy hello został usunięty przy użyciu hello `Get-AzureApplicationGateway` polecenia cmdlet.

### <a name="step-1"></a>Krok 1

Pobierz obiekt bramy aplikacji hello i skojarz go tooa zmiennej "$getgw".

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a>Krok 2

Użyj `Stop-AzureRmApplicationGateway` bramy aplikacji hello toostop. W tym przykładzie pokazano hello `Stop-AzureRmApplicationGateway` polecenia cmdlet na powitania pierwszy wiersz, następuje hello danych wyjściowych.

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Po bramy aplikacji hello jest w stanie zatrzymania, użyj hello `Remove-AzureRmApplicationGateway` usługi hello tooremove polecenia cmdlet.

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> Witaj **-force** przełącznika może być używane toosuppress hello Usuń potwierdzenia.

tooverify, który hello usługi zostały usunięte, możesz użyć hello `Get-AzureRmApplicationGateway` polecenia cmdlet. Ten krok nie jest wymagany.

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a>Następne kroki

Jeśli tooconfigure odciążanie protokołu SSL, zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl.md).

Jeśli chcesz tooconfigure toouse bramy aplikacji z ILB, zobacz [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).

Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć w następujących artykułach:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

