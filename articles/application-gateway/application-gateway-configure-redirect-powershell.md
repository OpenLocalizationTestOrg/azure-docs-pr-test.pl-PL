---
title: "Konfigurowanie przekierowania dla usługi Azure Application Gateway — PowerShell | Microsoft Docs"
description: "Ta strona zawiera scenariusze umożliwiające konfigurowanie przekierowania dla usługi Application Gateway przy użyciu programu PowerShell"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: gwallace
ms.openlocfilehash: 84a25e572a27df2fe46e07c4ab0a4aab5969d68e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="configure-redirection-on-application-gateway-with-powershell"></a><span data-ttu-id="1b406-103">Konfigurowanie przekierowania dla usługi Application Gateway przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b406-103">Configure redirection on Application Gateway with PowerShell</span></span>

<span data-ttu-id="1b406-104">Usługa Application Gateway obsługuje możliwość przekierowywania ruchu sieciowego na podstawie zdefiniowanej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1b406-104">Application gateway supports the ability to redirect traffic based on a defined configuration.</span></span> <span data-ttu-id="1b406-105">Aby uzyskać więcej ogólnych informacji o przekierowywaniu, zobacz [Application Gateway redirect overview](application-gateway-redirect-overview.md) (Przekierowywanie w usłudze Application Gateway — omówienie).</span><span class="sxs-lookup"><span data-stu-id="1b406-105">To learn more about redirection in general visit, [Application Gateway redirect overview](application-gateway-redirect-overview.md).</span></span> <span data-ttu-id="1b406-106">W tym artykule zawarto przykłady przekierowania protokołu HTTP na HTTPS, przekierowań opartych na ścieżkach, przekierowań obejmujących wiele lokacji i przekierowań do lokacji zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="1b406-106">This article provides examples of HTTP to HTTPS redirection, path based redirects, multi-site redirects, and redirects to external sites.</span></span>

## <a name="http-to-https-redirect-on-an-existing-application-gateway"></a><span data-ttu-id="1b406-107">Przekierowanie protokołu HTTP na HTTPS w istniejącej bramie aplikacji</span><span class="sxs-lookup"><span data-stu-id="1b406-107">HTTP to HTTPS redirect on an existing application gateway</span></span>

<span data-ttu-id="1b406-108">Poniższy przykład tworzy nowy odbiornik HTTP na porcie 80 na potrzeby przekierowywania żądań do istniejącego odbiornika na porcie 443.</span><span class="sxs-lookup"><span data-stu-id="1b406-108">The following example creates a new HTTP listener on port 80 to redirect requests to the existing listener on port 443.</span></span>

```powershell
# Get the application gateway
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG

# Get the existing HTTPS listener
$httpslistener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener -ApplicationGateway $gw

# Get the existing front end IP configuration
$fipconfig = Get-AzureRmApplicationGatewayFrontendIPConfig -Name appgatewayfrontendip -ApplicationGateway $gw

# Add a new front end port to support HTTP traffic
Add-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2  -Port 80 -ApplicationGateway $gw

# Get the recently created port
$fp = Get-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2 -ApplicationGateway $gw

# Create a new HTTP listener using the port created earlier
Add-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2  -Protocol Http -FrontendPort $fp -FrontendIPConfiguration $fipconfig -ApplicationGateway $gw 

# Get the new listener
$listener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2 -ApplicationGateway $gw

# Add a redirection configuration using a permanent redirect and targeting the existing listener
Add-AzureRmApplicationGatewayRedirectConfiguration -Name redirectHttptoHttps -RedirectType Permanent -TargetListener $httpslistener -IncludePath $true -IncludeQueryString $true -ApplicationGateway $gw

# Get the redirect configuration
$redirectconfig = Get-AzureRmApplicationGatewayRedirectConfiguration -Name redirectHttptoHttps -ApplicationGateway $gw


# Add a new rule to handle the redirect and use the new listener
Add-AzureRmApplicationGatewayRequestRoutingRule -Name rule02 -RuleType Basic -HttpListener $listener -RedirectConfiguration $redirectconfig -ApplicationGateway $gw

# Update the application gateway
Set-AzureRmApplicationGateway -ApplicationGateway $gw 
```

<span data-ttu-id="1b406-109">Po zaktualizowaniu bramy aplikacji przetestuj nowy odbiornik na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="1b406-109">Once the application gateway is updated, test the new listener on port 80.</span></span>  <span data-ttu-id="1b406-110">W poniższym przykładzie przedstawiono użycie narzędzia `curl` do przetestowania przekierowania.</span><span class="sxs-lookup"><span data-stu-id="1b406-110">The following example shows using `curl` test the redirection.</span></span>

```
curl http://40.69.161.221 -i
HTTP/1.1 301 Moved Permanently
Content-Type: text/html; charset=UTF-8
Location: https://40.69.161.221/
Server: Microsoft-IIS/10.0
Date: Tue, 11 Jul 2017 20:54:00 GMT
Content-Length: 145

<head><title>Document Moved</title></head>
<body><h1>Object Moved</h1>This document may be found <a HREF="https://40.69.161.221/">here</a></body>
```

## <a name="path-based-redirect"></a><span data-ttu-id="1b406-111">Przekierowanie oparte na ścieżce</span><span class="sxs-lookup"><span data-stu-id="1b406-111">Path based redirect</span></span>

<span data-ttu-id="1b406-112">Poniższy przykład tworzy nowy odbiornik i regułę opartą na ścieżce w istniejącej bramie aplikacji oraz przekierowuje tylko ten ruch, który spełnia kryteria konkretnej ścieżki URL.</span><span class="sxs-lookup"><span data-stu-id="1b406-112">The following example creates a new listener and a path based rule on an existing application gateway that redirects only traffic meeting the specific url path.</span></span>

```powershell
# Get the application gateway
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG

# Get the existing HTTPS listener
$httpslistener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener -ApplicationGateway $gw

# Get the existing front end IP configuration
$fipconfig = Get-AzureRmApplicationGatewayFrontendIPConfig -Name appgatewayfrontendip -ApplicationGateway $gw

# Add a new front end port to support HTTP traffic
Add-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2  -Port 80 -ApplicationGateway $gw

# Get the recently created port
$fp = Get-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2 -ApplicationGateway $gw

# Create a new HTTP listener using the port created earlier
Add-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2  -Protocol Http -FrontendPort $fp -FrontendIPConfiguration $fipconfig -ApplicationGateway $gw 

# Get the new listener
$listener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2 -ApplicationGateway $gw

# Add a redirection configuration using a permanent redirect and targeting the existing listener
$redirectconfig = Get-AzureRmApplicationGatewayRedirectConfiguration -Name redirectpath6 -ApplicationGateway $gw

# Retrieve the existing backend http settings to be used
$poolSetting = Get-AzureRmApplicationGatewayBackendHttpSettings -Name "appGatewayBackendHttpSettings" -ApplicationGateway $gw

# Retrieve an existing backend pool
$pool = Get-AzureRmApplicationGatewayBackendAddressPool -Name appGatewayBackendPool -ApplicationGateway $gw

# Create a new path based rule
$pathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule6" -Paths "/image/*" -BackendAddressPool $pool -BackendHttpSettings $poolSetting

# Create a path map to add to the rule
Add-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $pathRule -DefaultBackendAddressPool $pool -DefaultBackendHttpSettings $poolSetting -ApplicationGateway $gw

# Retrieve the url path map created
$urlPathMap = Get-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -ApplicationGateway $gw

# Add a new rule to handle the redirect and use the new listener
Add-AzureRmApplicationGatewayRequestRoutingRule -Name "rule6" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap -RedirectConfiguration $redirectconfig -ApplicationGateway $gw

# Update the application gateway
Set-AzureRmApplicationGateway -ApplicationGateway $gw 
```

## <a name="multi-site-redirect"></a><span data-ttu-id="1b406-113">Przekierowanie obejmujące wiele lokacji</span><span class="sxs-lookup"><span data-stu-id="1b406-113">Multi-site redirect</span></span>

<span data-ttu-id="1b406-114">Poniższy przykład tworzy nową bramę aplikacji z dwoma odbiornikami obejmującymi wiele lokacji na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="1b406-114">The following example creates a new application gateway with 2 multi-site listeners on port 80.</span></span> <span data-ttu-id="1b406-115">Odbiorniki są przeznaczone dla domen adatum.com i adatum.org.</span><span class="sxs-lookup"><span data-stu-id="1b406-115">The listeners are for adatum.com and adatum.org.</span></span> <span data-ttu-id="1b406-116">Do przekierowywania ruchu z domeny adatum.org do domeny adatum.com jest tworzona reguła przekierowania.</span><span class="sxs-lookup"><span data-stu-id="1b406-116">A redirect rule is created to redirect traffic from adatum.org to adatum.com.</span></span> <span data-ttu-id="1b406-117">Wymagane jest dodatkowe skonfigurowanie aliasów CNAME dla publicznego adresu IP bramy aplikacji. Aby uzyskać więcej informacji na temat delegowania domeny do usługi Azure DNS i tworzenia rekordów CNAME dla domeny, odwiedź stronę [Delegowanie domeny do usługi Azure DNS](../dns/dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="1b406-117">Additional configuration is required for configuring CNAME aliases to the application gateway public IP address, for more information on delegating your domain to Azure DNS and creating CNAME records for your domain visit, [Delegate a domain to Azure DNS](../dns/dns-delegate-domain-azure-dns.md).</span></span>

```powershell
# Create a new resource group for the application gateway
New-AzureRmResourceGroup -Name appgw-rg -Location "East US"

# Create a subnet configuration object for the application gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your application gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet

# Create a public IP address for use with the application gateway. Defining the domainnamelabel during creation is not supported for use with application gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "East US" -AllocationMethod Dynamic

# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $vnet.Subnets[0]

# Create a backend pool to hold the addresses or NICs for the application that application gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 80

# Create a frontend IP configuration to associate the public IP address with the application gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Create the HTTP listener for the application gateway for adatum.com. Assign the front-end ip configuration, and port.
$listener1 = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp -HostName adatum.com

# Create the HTTP listener for the application gateway for adatum.org this listener will redirect to the abc.com listener. Assign the front-end ip configuration, and port.
$listener2 = New-AzureRmApplicationGatewayHttpListener -Name listener02 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp -HostName adatum.org

# Create the redirect configuration that will point traffic to the 
$redirectconfig = New-AzureRmApplicationGatewayRedirectConfiguration -Name redirectOrgtoCom -RedirectType Found -TargetListener $listener1 -IncludePath $true -IncludeQueryString $true

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule1 = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -HttpListener $listener1 -BackendHttpSettings $poolSetting -BackendAddressPool $pool

#Create a load balancer routing rule that redirects traffic to the adatum.com listener
$rule2 = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule02 -RuleType Basic -HttpListener $listener2 -RedirectConfiguration $redirectconfig

# Configure the SKU of the application gateway
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Medium -Tier Standard -Capacity 2

# Create the application gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener,$listener2 -RequestRoutingRules $rule1,$rule2 -RedirectConfigurations $redirectconfig -Sku $sku
```

## <a name="redirect-to-an-external-site"></a><span data-ttu-id="1b406-118">Przekierowanie do lokacji zewnętrznej</span><span class="sxs-lookup"><span data-stu-id="1b406-118">Redirect to an external site</span></span>

<span data-ttu-id="1b406-119">Poniższy przykład przekierowuje ruch odbierany przez bramę aplikacji do zewnętrznej witryny internetowej (bing.com).</span><span class="sxs-lookup"><span data-stu-id="1b406-119">The following example redirects traffic coming into the application gateway to an external website (bing.com).</span></span> <span data-ttu-id="1b406-120">W przypadku korzystania z przełącznika `TargetUrl` przełączniki `IncludePath` i `IncludeQuery` nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="1b406-120">When using the `TargetUrl` switch the `IncludePath` and `IncludeQuery` switches are not allowed.</span></span>

```powershell
# Create a new resource group for the application gateway
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"

# Create a subnet configuration object for the application gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your application gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet

# Create a public IP address for use with the application gateway. Defining the domainnamelabel during creation is not supported for use with application gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic

# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $vnet.Subnets[0]

# Create a backend pool to hold the addresses or NICs for the application that application gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 80

# Create a frontend IP configuration to associate the public IP address with the application gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Create the HTTP listener for the application gateway. Assign the front-end ip configuration, and port.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp 

# Create the redirect configuration that will point traffic to the 
$redirectconfig = New-AzureRmApplicationGatewayRedirectConfiguration -Name myredirect -RedirectType Temporary -TargetUrl "http://bing.com" -IncludePath $true -IncludeQueryString $true

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -HttpListener $listener -RedirectConfiguration $redirectconfig 

# Configure the SKU of the application gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Create the application gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -RedirectConfigurations $redirectconfig -Sku $sku
```

## <a name="next-steps"></a><span data-ttu-id="1b406-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b406-121">Next steps</span></span>

<span data-ttu-id="1b406-122">Odwiedź stronę [Configure end to end SSL with application gateway using PowerShell](application-gateway-end-to-end-ssl-powershell.md) (Konfigurowanie kompleksowej usługi SSL i bramy aplikacji przy użyciu programu PowerShell)</span><span class="sxs-lookup"><span data-stu-id="1b406-122">Visit [configure end to end SSL with application gateway using PowerShell](application-gateway-end-to-end-ssl-powershell.md)</span></span>