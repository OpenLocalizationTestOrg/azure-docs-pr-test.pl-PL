---
title: "Ochrona aplikacji internetowych za pomocą usługi Azure Application Gateway — PowerShell | Microsoft Docs"
description: "Ten artykuł zawiera wskazówki dotyczące sposobu konfigurowania aplikacji internetowych jako hostów zaplecza w istniejącej lub nowej bramie aplikacji."
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
ms.date: 07/25/2017
ms.author: gwallace
ms.openlocfilehash: eab15513e15ea897881edabab38f4d24d7002c04
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-app-service-web-apps-with-application-gateway"></a><span data-ttu-id="f2644-103">Konfigurowanie usługi App Service Web Apps za pomocą usługi Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f2644-103">Configure App Service Web Apps with Application Gateway</span></span> 

<span data-ttu-id="f2644-104">Brama aplikacji umożliwia korzystanie z aplikacji internetowej platformy Azure lub innej usługi wielodostępnej jako elementu członkowskiego puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f2644-104">Application gateway allows you to have an Azure Web App or other multi-tenant service as a back-end pool member.</span></span> <span data-ttu-id="f2644-105">W tym artykule przedstawiono sposób konfigurowania aplikacji internetowej platformy Azure za pomocą usługi Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f2644-105">In this article, to you learn to configure an Azure web app with Application Gateway.</span></span> <span data-ttu-id="f2644-106">W pierwszym przykładzie pokazano, jak skonfigurować istniejącą bramę aplikacji w celu używania aplikacji internetowej jako elementu członkowskiego puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f2644-106">The first example shows you how to configure an existing application gateway to use a web app as a back-end pool member.</span></span> <span data-ttu-id="f2644-107">Drugi przykład pokazuje, jak utworzyć nową bramę aplikacji z aplikacją internetową jako elementem członkowskim puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f2644-107">The second example shows you how to create a new application gateway with a web app as a back-end pool member.</span></span>

## <a name="configure-a-web-app-behind-an-existing-application-gateway"></a><span data-ttu-id="f2644-108">Konfigurowanie aplikacji internetowej za istniejącą bramą aplikacji</span><span class="sxs-lookup"><span data-stu-id="f2644-108">Configure a web app behind an existing application gateway</span></span>

<span data-ttu-id="f2644-109">W poniższym przykładzie aplikacja internetowa jest dodawana jako element członkowski puli zaplecza do istniejącej bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f2644-109">The following example adds a web app as a back-end pool member to an existing application gateway.</span></span> <span data-ttu-id="f2644-110">Aby aplikacje internetowe działały, wymagane jest udostępnienie przełącznika `-PickHostNamefromBackendHttpSettings` w konfiguracji sondowania oraz `-PickHostNameFromBackendAddress` w ustawieniach HTTP zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f2644-110">Both the switch `-PickHostNamefromBackendHttpSettings`on the Probe configuration and `-PickHostNameFromBackendAddress` on the back-end http settings must be provided in order for web apps to work.</span></span>

```powershell
# FQDN of the web app
$webappFQDN = "<enter your webapp FQDN i.e mywebsite.azurewebsites.net>"

# Retrieve an existing application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName $rg.ResourceGroupName

# Define the status codes to match for the probe
$match=New-AzureRmApplicationGatewayProbeHealthResponseMatch -StatusCode 200-399

# Add a new probe to the application gateway
Add-AzureRmApplicationGatewayProbeConfig -name webappprobe2 -ApplicationGateway $gw -Protocol Http -Path / -Interval 30 -Timeout 120 -UnhealthyThreshold 3 -PickHostNameFromBackendHttpSettings -Match $match

# Retrieve the newly added probe
$probe = Get-AzureRmApplicationGatewayProbeConfig -name webappprobe2 -ApplicationGateway $gw

# Configure an existing backend http settings 
Set-AzureRmApplicationGatewayBackendHttpSettings -Name appGatewayBackendHttpSettings -ApplicationGateway $gw -PickHostNameFromBackendAddress -Port 80 -Protocol http -CookieBasedAffinity Disabled -RequestTimeout 30 -Probe $probe

# Add the web app to the backend pool
Set-AzureRmApplicationGatewayBackendAddressPool -Name appGatewayBackendPool -ApplicationGateway $gw -BackendIPAddresses $webappFQDN

# Update the application gateway
Set-AzureRmApplicationGateway -ApplicationGateway $gw
```

## <a name="configure-a-web-application-behind-a-new-application-gateway"></a><span data-ttu-id="f2644-111">Konfigurowanie aplikacji internetowej za nową bramą aplikacji</span><span class="sxs-lookup"><span data-stu-id="f2644-111">Configure a web application behind a new application gateway</span></span>

<span data-ttu-id="f2644-112">W tym scenariuszu aplikacja internetowa jest wdrażana za pomocą witryny internetowej wprowadzenia do platformy ASP.NET oraz bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f2644-112">This scenario deploys a web app with the asp.net getting started website and an application gateway.</span></span>

```powershell
# Defines a variable for a dotnet get started web app repository location
$gitrepo="https://github.com/Azure-Samples/app-service-web-dotnet-get-started.git"

# Unique web app name
$webappname="mywebapp$(Get-Random)"

# Creates a resource group
$rg = New-AzureRmResourceGroup -Name ContosoRG -Location Eastus

# Create an App Service plan in Free tier.
New-AzureRmAppServicePlan -Name $webappname -Location EastUs -ResourceGroupName $rg.ResourceGroupName -Tier Free

# Creates a web app
$webapp = New-AzureRmWebApp -ResourceGroupName $rg.ResourceGroupName -Name $webappname -Location EastUs -AppServicePlan $webappname

# Configure GitHub deployment from your GitHub repo and deploy once to web app.
$PropertiesObject = @{
    repoUrl = "$gitrepo";
    branch = "master";
    isManualIntegration = "true";
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName $rg.ResourceGroupName -ResourceType Microsoft.Web/sites/sourcecontrols -ResourceName $webappname/web -ApiVersion 2015-08-01 -Force

# Creates a subnet for the application gateway
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Creates a vnet for the application gateway
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName $rg.ResourceGroupName -Location EastUs -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve the subnet object for use later
$subnet=$vnet.Subnets[0]

# Create a public IP address
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName $rg.ResourceGroupName -name publicIP01 -location EastUs -AllocationMethod Dynamic

# Create a new IP configuration
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Create a backend pool with the hostname of the web app
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name appGatewayBackendPool -BackendIPAddresses $webapp.HostNames

# Define the status codes to match for the probe
$match = New-AzureRmApplicationGatewayProbeHealthResponseMatch -StatusCode 200-399

# Create a probe with the PickHostNameFromBackendHttpSettings switch for web apps
$probeconfig = New-AzureRmApplicationGatewayProbeConfig -name webappprobe -Protocol Http -Path / -Interval 30 -Timeout 120 -UnhealthyThreshold 3 -PickHostNameFromBackendHttpSettings -Match $match

# Define the backend http settings
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name appGatewayBackendHttpSettings -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120 -PickHostNameFromBackendAddress -Probe $probeconfig

# Create a new front-end port
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Create a new front end IP configuration
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Create a new listener using the front-end ip configuration and port created earlier
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Create a new rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool 

# Define the application gateway SKU to use
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create the application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName $rg.ResourceGroupName -Location EastUs -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -Probes $probeconfig -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="f2644-113">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="f2644-113">Get application gateway DNS name</span></span>

<span data-ttu-id="f2644-114">Po utworzeniu bramy następnym krokiem jest skonfigurowanie frontonu na potrzeby komunikacji.</span><span class="sxs-lookup"><span data-stu-id="f2644-114">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="f2644-115">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="f2644-115">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="f2644-116">Aby upewnić się, że użytkownicy końcowi mogą trafić bramę aplikacji, można użyć rekordu CNAME w celu wskazania publicznego punktu końcowego bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f2644-116">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="f2644-117">Aby utworzyć alias, pobierz szczegóły bramy aplikacji i skojarzony adres IP oraz nazwę DNS, używając elementu PublicIPAddress dołączonego do bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f2644-117">To create the alias, retrieve the details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="f2644-118">Można to zrobić za pomocą usługi Azure DNS lub innych dostawców usługi DNS, tworząc rekord CNAME, który wskazuje [publiczny adres IP](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="f2644-118">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points to the [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="f2644-119">Korzystanie z rekordów A nie jest zalecane, ponieważ adres VIP może ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f2644-119">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : eastus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="f2644-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f2644-120">Next steps</span></span>

<span data-ttu-id="f2644-121">Dowiedz się, jak skonfigurować przekierowanie, odwiedzając stronę [Konfigurowanie przekierowania dla usługi Application Gateway przy użyciu programu PowerShell](application-gateway-configure-redirect-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f2644-121">Learn how to configure redirection by visiting: [Configure redirection on Application Gateway with PowerShell](application-gateway-configure-redirect-powershell.md).</span></span>
