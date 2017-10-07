---
title: "Zapora aplikacji sieci web aaaConfigure — brama aplikacji w usłudze Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera wskazówki dotyczące sposobu przy użyciu toostart Zapora aplikacji sieci web w istniejącej lub nowej bramy aplikacji."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>Konfigurowanie zapory aplikacji sieci web w nowej lub istniejącej bramy aplikacji

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure](application-gateway-web-application-firewall-cli.md)

Dowiedz się, jak toocreate zapory aplikacji sieci web włączone bramy aplikacji lub Dodaj tooan zapory aplikacji sieci web istniejącą bramę aplikacji.

Hello zapory aplikacji sieci web (WAF) brama aplikacji w usłudze Azure chroni aplikacje sieci web przed wspólnej ataków opartych na sieci web takich jak iniekcja kodu SQL, ataki skryptów między witrynami i hijacks sesji.

Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7. Zapewnia on trybu failover, wydajności routingu żądań HTTP między różnymi serwerami, czy znajdują się w chmurze hello lub lokalnie. Brama aplikacji w oferuje wiele funkcji aplikacji dostarczania kontrolera (ADC), w tym HTTP załadować równoważenia, opartych na pliku cookie sesji koligacji, Odciążanie bezpiecznego secure sockets layer (SSL), sondy kondycji niestandardowych, obsługę wielu lokacji i wielu innych. toofind pełną listę obsługiwanych funkcji, odwiedź stronę: [brama Omówienie aplikacji](application-gateway-introduction.md).

Hello artykule przedstawiono sposób zbyt[dodać tooan zapory aplikacji sieci web istniejącą bramę aplikacji](#add-web-application-firewall-to-an-existing-application-gateway) i [Utwórz bramę aplikacji, która używa zapory aplikacji sieci web](#create-an-application-gateway-with-web-application-firewall).

![Scenariusz obrazu][scenario]

## <a name="waf-configuration-differences"></a>Różnice w konfiguracji zapory aplikacji sieci Web

Jeśli znasz [Utwórz bramę aplikacji przy użyciu programu PowerShell](application-gateway-create-gateway-arm.md), zrozumieć hello SKU ustawienia tooconfigure podczas tworzenia bramy aplikacji. Zapory aplikacji sieci Web udostępnia dodatkowe ustawienia toodefine podczas konfigurowania hello jednostki SKU bramy aplikacji. Brak dodatkowych zmian wprowadzonych na powitania bramy aplikacji.

| **Ustawienie** | **Szczegóły**
|---|---|
|**SKU** |Normalne bramy aplikacji nie obsługuje zapory aplikacji sieci Web **standardowe\_małych**, **standardowe\_średni**, i **standardowe\_duży** rozmiary. Wprowadzenie hello zapory aplikacji sieci Web, istnieją dwie dodatkowe jednostki SKU, **zapory aplikacji sieci Web\_średni** i **zapory aplikacji sieci Web\_duży**. Zapory aplikacji sieci Web nie jest obsługiwana w małych bramy aplikacji.|
|**Warstwy** | Witaj dostępne wartości to **standardowe** lub **WAF**. Zapora aplikacji sieci web, używając **WAF** musi być wybrany.|
|**Tryb** | To ustawienie jest tryb hello zapory aplikacji sieci Web. dozwolone wartości to **wykrywania** i **zapobiegania**. Gdy zapory aplikacji sieci Web jest skonfigurowana w trybie wykrywania, wszystkie zagrożenia są przechowywane w pliku dziennika. W trybie zapobiegania zdarzenia są nadal rejestrowane, ale osoba atakująca hello odbiera odpowiedź 403 nieautoryzowanego z hello bramy aplikacji.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Dodaj tooan zapory aplikacji sieci web istniejącej bramy aplikacji

Upewnij się, że używasz najnowszej wersji programu Azure PowerShell hello. Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).

1. Zaloguj się za tooyour konto platformy Azure.

    ```powershell
    Login-AzureRmAccount
    ```

2. Wybierz hello toouse subskrypcji dla tego scenariusza.

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. Pobrać bramy hello są Dodawanie zapory aplikacji sieci web.

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. Skonfiguruj sku zapory aplikacji sieci web hello. są dostępne rozmiary Hello **zapory aplikacji sieci Web\_duży** i **WAF\_średni**. Gdy jest używana Zapora aplikacji sieci web musi być warstwy hello **zapory aplikacji sieci Web**, pojemność hello muszą zostać potwierdzone przy ustawianiu hello jednostki sku.

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. Skonfiguruj ustawienia hello zapory aplikacji sieci Web, zgodnie z definicją w hello poniższy przykład:

   Aby uzyskać **FirewallMode**, hello dostępne wartości to wykrywania i zapobiegania.

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. Zaktualizuj hello bramy aplikacji z ustawieniami hello zdefiniowane w hello poprzedzających krok.

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

To polecenie aktualizuje bramy aplikacji hello zapory aplikacji sieci web. Odwiedź stronę [diagnostyki bramy aplikacji](application-gateway-diagnostics.md) toounderstand jak tooview dzienniki bramy aplikacji. Powodu toohello zabezpieczeń rodzaj zapory aplikacji sieci Web dzienniki toobe należy regularnie weryfikowane toounderstand hello stan zabezpieczeń aplikacji sieci web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Utwórz bramę aplikacji z zapory aplikacji sieci web

Hello poniższe kroki przedstawiają cały proces powitania od początku tooend do tworzenia bramy aplikacji z zapory aplikacji sieci web.

Upewnij się, że używasz najnowszej wersji programu Azure PowerShell hello. Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).

1. Zaloguj się za tooAzure uruchamiając `Login-AzureRmAccount`, to zostanie wyświetlony monit o tooauthenticate przy użyciu poświadczeń.

1. Sprawdź, czy hello subskrypcji dla konta hello uruchamiając`Get-AzureRmSubscription`

1. Wybierz z toouse Twojej subskrypcji platformy Azure.

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów dla hello Application Gateway.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Ta lokalizacja jest używana jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów. Upewnij się, że wszystkie polecenia, które używa toocreate jako bramy aplikacji hello tej samej grupie zasobów.

W hello poprzedzających przykład utworzyliśmy grupę zasobów o nazwie "Zarządcy zasobów appgw" i lokalizacji "zachodnie stany USA."

> [!NOTE]
> Jeśli potrzebujesz tooconfigure sondowania niestandardowych dla bramy aplikacji, zobacz [Utwórz bramę aplikacji z niestandardowego sond przy użyciu programu PowerShell](application-gateway-create-probe-ps.md). Aby dowiedzieć się więcej, zapoznaj się z informacjami na temat [sond niestandardowych i monitorowania kondycji](application-gateway-probe-overview.md).

### <a name="configure-virtual-network"></a>Konfigurowanie sieci wirtualnej

Brama aplikacji wymaga własnej podsieci. W tym kroku utworzysz sieci wirtualnej przestrzeni adresowej 10.0.0.0/16 z dwoma podsieciami, jeden dla bramy aplikacji hello i jeden dla członków puli wewnętrznej bazy danych.

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>Skonfiguruj publicznego adresu IP

W kolejności toohandle zewnętrznych żądań bramy aplikacji wymaga publicznego adresu IP. Ten publiczny adres IP nie może mieć `DomainNameLabel` zdefiniowane toobe używany przez bramę aplikacji hello.

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a>Skonfiguruj hello bramy aplikacji

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> Bramy aplikacji utworzonych za pomocą konfiguracji zapory aplikacji sieci web podstawowe hello są skonfigurowane z CRS 3.0 do ochrony.

## <a name="get-application-gateway-dns-name"></a>Pobierz nazwę DNS bramy aplikacji

Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji. Korzystając z publicznym adresem IP, brama aplikacji wymaga przypisywany dynamicznie nazwy DNS, który nie jest przyjazną. tooensure użytkownicy końcowi mogą trafień hello bramy aplikacji, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy hello bramy aplikacji. [Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure aliasu, pobrać szczegółów hello bramy aplikacji i skojarzonej z nią IP DNS nazwy przy użyciu hello publicznego adresu IP elementu dołączony toohello Application Gateway. Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS. Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.

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

Dowiedz się, jak tooconfigure rejestrowania diagnostycznego, toolog hello zdarzenia, które są wykrywane lub zapobiec za pomocą zapory aplikacji sieci web, odwiedzając [diagnostyki bramy aplikacji](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
