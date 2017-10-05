---
title: "Konfigurowanie zapory aplikacji sieci web — brama aplikacji w usłudze Azure | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera wskazówki dotyczące sposobu uruchamiania za pomocą zapory aplikacji sieci web w istniejącej lub nowej bramy aplikacji."
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
ms.openlocfilehash: dab489a1c9fb7d4a51b9ccbce543b209bec23575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>Konfigurowanie zapory aplikacji sieci web w nowej lub istniejącej bramy aplikacji

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Interfejs wiersza polecenia platformy Azure](application-gateway-web-application-firewall-cli.md)

Dowiedz się, jak utworzyć aplikację sieci web zapory włączone bramy aplikacji lub dodawanie zapory aplikacji sieci web do istniejącej bramy aplikacji.

Zapora aplikacji sieci web (WAF) w brama aplikacji w usłudze Azure chroni aplikacje sieci web przed wspólnej ataków opartych na sieci web takich jak iniekcja kodu SQL, atakami skryptów między witrynami i hijacks sesji.

Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7. Udostępnia tryb failover, oparty na wydajności routing żądań HTTP między różnymi serwerami — w chmurze i lokalnymi. Brama aplikacji w oferuje wiele funkcji aplikacji dostarczania kontrolera (ADC), w tym HTTP załadować równoważenia, opartych na pliku cookie sesji koligacji, Odciążanie bezpiecznego secure sockets layer (SSL), sondy kondycji niestandardowych, obsługę wielu lokacji i wielu innych. Aby uzyskać pełną listę obsługiwanych funkcji, odwiedź stronę: [brama Omówienie aplikacji](application-gateway-introduction.md).

Następujące artykuł przedstawia sposób [Dodawanie zapory aplikacji sieci web do istniejącej bramy aplikacji](#add-web-application-firewall-to-an-existing-application-gateway) i [Utwórz bramę aplikacji, która używa zapory aplikacji sieci web](#create-an-application-gateway-with-web-application-firewall).

![Scenariusz obrazu][scenario]

## <a name="waf-configuration-differences"></a>Różnice w konfiguracji zapory aplikacji sieci Web

Jeśli znasz [Utwórz bramę aplikacji przy użyciu programu PowerShell](application-gateway-create-gateway-arm.md), zrozumieć ustawienia Jednostka SKU, aby skonfigurować podczas tworzenia bramy aplikacji. Zapory aplikacji sieci Web udostępnia dodatkowe ustawienia, aby zdefiniować podczas konfigurowania jednostka SKU bramy aplikacji. Brak dodatkowych zmian wprowadzonych na bramy aplikacji.

| **Ustawienie** | **Szczegóły**
|---|---|
|**SKU** |Normalne bramy aplikacji nie obsługuje zapory aplikacji sieci Web **standardowe\_małych**, **standardowe\_średni**, i **standardowe\_duży** rozmiary. Wraz z wprowadzeniem zapory aplikacji sieci Web, istnieją dwie dodatkowe jednostki SKU, **WAF\_średni** i **zapory aplikacji sieci Web\_duży**. Zapory aplikacji sieci Web nie jest obsługiwana w małych bramy aplikacji.|
|**Warstwy** | Dostępne wartości to **standardowe** lub **WAF**. Zapora aplikacji sieci web, używając **WAF** musi być wybrany.|
|**Tryb** | To ustawienie jest tryb zapory aplikacji sieci Web. dozwolone wartości to **wykrywania** i **zapobiegania**. Gdy zapory aplikacji sieci Web jest skonfigurowana w trybie wykrywania, wszystkie zagrożenia są przechowywane w pliku dziennika. W trybie zapobiegania zdarzenia są nadal rejestrowane, ale osoba atakująca otrzymuje 403 nieautoryzowanego odpowiedź z bramy aplikacji.|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Dodawanie zapory aplikacji sieci web do istniejącej bramy aplikacji

Upewnij się, że używasz najnowszej wersji programu Azure PowerShell. Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).

1. Zaloguj się do konta platformy Azure.

    ```powershell
    Login-AzureRmAccount
    ```

2. Wybierz subskrypcję do użycia na potrzeby tego scenariusza.

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. Pobrać bramy, które są Dodawanie zapory aplikacji sieci web.

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. Skonfiguruj sku zapory aplikacji sieci web. Dostępne rozmiary są **zapory aplikacji sieci Web\_duży** i **WAF\_średni**. Gdy jest używana Zapora aplikacji sieci web warstwy musi być **WAF**, pojemność muszą zostać potwierdzone przy ustawianiu jednostki sku.

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. Skonfiguruj ustawienia zapory aplikacji sieci Web, zgodnie z definicją w poniższym przykładzie:

   Aby uzyskać **FirewallMode**, dostępne wartości to wykrywania i zapobiegania.

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. Zaktualizuj bramę aplikacji z ustawień zdefiniowanych w poprzednim kroku.

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

To polecenie aktualizuje bramy aplikacji zapory aplikacji sieci web. Odwiedź stronę [diagnostyki bramy aplikacji](application-gateway-diagnostics.md) zrozumienie, jak wyświetlać dzienniki bramy aplikacji. Z powodu zabezpieczeń rodzaj zapory aplikacji sieci Web Dzienniki należy ją sprawdzić regularnie, aby poznać strukturę aplikacji sieci web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Utwórz bramę aplikacji z zapory aplikacji sieci web

Poniższe kroki przedstawiają cały proces od początku do końca Tworzenie bramy aplikacji za pomocą zapory aplikacji sieci web.

Upewnij się, że używasz najnowszej wersji programu Azure PowerShell. Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).

1. Logowanie do platformy Azure, uruchamiając `Login-AzureRmAccount`, zostanie wyświetlony monit o uwierzytelniania przy użyciu poświadczeń.

1. Sprawdź subskrypcje dla konta, uruchamiając`Get-AzureRmSubscription`

1. Wybierz subskrypcję platformy Azure do użycia.

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów dla bramy aplikacji.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Ta lokalizacja będzie używana jako domyślna lokalizacja dla zasobów w danej grupie zasobów. Upewnij się, że wszystkie polecenia, aby utworzyć bramę aplikacji używa tej samej grupie zasobów.

W powyższym przykładzie utworzono grupę zasobów o nazwie "zarządcy zasobów appgw" i lokalizacji "Zachodnie stany USA".

> [!NOTE]
> Jeśli trzeba skonfigurować niestandardowe sondowania dla bramy aplikacji, zobacz [Utwórz bramę aplikacji z niestandardowego sond przy użyciu programu PowerShell](application-gateway-create-probe-ps.md). Aby dowiedzieć się więcej, zapoznaj się z informacjami na temat [sond niestandardowych i monitorowania kondycji](application-gateway-probe-overview.md).

### <a name="configure-virtual-network"></a>Skonfiguruj sieć wirtualną

Brama aplikacji wymaga własnej podsieci. W tym kroku utworzysz sieci wirtualnej przestrzeni adresowej 10.0.0.0/16 z dwoma podsieciami, jeden dla bramy aplikacji i jeden dla członków puli wewnętrznej bazy danych.

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>Skonfiguruj publicznego adresu IP

W celu obsługi żądań zewnętrznych, bramy aplikacji wymaga publicznego adresu IP. Ten publiczny adres IP nie może mieć `DomainNameLabel` definicja ma być używany przez bramę aplikacji.

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a>Konfigurowanie bramy aplikacji

```powershell
# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool to hold the addresses or NICs for the application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload the authenication certificate that will be used to communicate with the backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration to associate the public IP address with the Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure the certificate for the Application Gateway. This certificate is used to decrypt and re-encrypt the traffic on the Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>

# Create the HTTP listener for the Application Gateway. Assign the front-end ip configuration, port, and ssl certificate to use.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU of the Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define the SSL policy to use
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure the waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create the Application Gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> Bramy aplikacji utworzonych za pomocą konfiguracji zapory aplikacji sieci web podstawowe są skonfigurowane z CRS 3.0 do ochrony.

## <a name="get-application-gateway-dns-name"></a>Pobierz nazwę DNS bramy aplikacji

Po utworzeniu bramy następnym krokiem jest skonfigurowanie frontonu na potrzeby komunikacji. Korzystając z publicznym adresem IP, brama aplikacji wymaga przypisywany dynamicznie nazwy DNS, który nie jest przyjazną. Aby zapewnić, że użytkownicy końcowi mogą trafień bramy aplikacji, można rekord CNAME wskaż publiczny punkt końcowy bramy aplikacji. [Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). Aby skonfigurować alias, należy pobrać szczegółów bramy aplikacji i jego skojarzonej nazwy IP DNS za pomocą elementu publicznego adresu IP dołączony na bramie aplikacji. Brama aplikacji w nazwa DNS należy utworzyć rekord CNAME, wskazujący aplikacji dwie sieci web do tej nazwy DNS. Użycie rekordów A nie jest zalecane, ponieważ adres VIP może się zmieniać podczas ponownego uruchomienia bramy aplikacji.

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

Informacje o sposobie konfigurowania rejestrowania diagnostycznego do dziennika zdarzeń, które wykryte lub uniemożliwił z zapory aplikacji sieci web, odwiedzając [diagnostyki bramy aplikacji](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
