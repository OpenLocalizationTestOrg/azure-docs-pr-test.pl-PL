---
title: "zasady SSL aaaConfigure na bramie aplikacji Azure — PowerShell | Dokumentacja firmy Microsoft"
description: Ta strona zawiera instrukcje tooconfigure zasady SSL na bramie aplikacji Azure
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7802ad3d3191a2fe9d88dddcb7c65bc4a70a419c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-policy-versions-and-cipher-suites-on-application-gateway"></a><span data-ttu-id="1bb84-103">Konfigurowanie zasad zabezpieczeń SSL w wersjach i mechanizmy w bramie aplikacji szyfrowania</span><span class="sxs-lookup"><span data-stu-id="1bb84-103">Configure SSL policy versions and cipher suites on Application Gateway</span></span>

<span data-ttu-id="1bb84-104">Dowiedz się, jak wersji zasad SSL tooconfigure i mechanizmy w bramie aplikacji szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="1bb84-104">Learn how tooconfigure SSL policy versions and cipher suites on Application Gateway.</span></span> <span data-ttu-id="1bb84-105">Możesz wybrać z [listy wstępnie zdefiniowanych zasad](#predefined-ssl-policies) czy zawierają różne konfiguracje wersji zasad protokołu SSL i włączone mechanizmów szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="1bb84-105">You can select from a [list of predefined policies](#predefined-ssl-policies) that contain different configurations of SSL policy versions and enabled cipher suites.</span></span> <span data-ttu-id="1bb84-106">Masz również hello możliwości toodefine [niestandardowe zasady SSL](#configure-a-custom-ssl-policy) zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="1bb84-106">You also have hello ability toodefine a [custom SSL policy](#configure-a-custom-ssl-policy) based on your requirements.</span></span>

## <a name="get-available-ssl-options"></a><span data-ttu-id="1bb84-107">Dostępne opcje protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="1bb84-107">Get available SSL options</span></span>

<span data-ttu-id="1bb84-108">Witaj `Get-AzureRMApplicationGatewayAvailableSslOptions` polecenie cmdlet udostępnia listę dostępnych wstępnie zdefiniowane zasady, mechanizmów szyfrowania dostępne i wersji protokołu, które można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="1bb84-108">hello `Get-AzureRMApplicationGatewayAvailableSslOptions` cmdlet provides a listing of available pre-defined policies, available cipher suites, and protocol versions that can be configured.</span></span> <span data-ttu-id="1bb84-109">Witaj poniższym przykładzie przedstawiono przykładowe dane wyjściowe z polecenia hello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1bb84-109">hello following example shows an example output from running hello cmdlet.</span></span>

```
DefaultPolicy: AppGwSslPolicy20150501
PredefinedPolicies:
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20150501
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401S

AvailableCipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
    TLS_RSA_WITH_AES_128_GCM_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA256
    TLS_RSA_WITH_AES_128_CBC_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA
    TLS_RSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_3DES_EDE_CBC_SHA
    TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

AvailableProtocols:
    TLSv1_0
    TLSv1_1
    TLSv1_2
```

## <a name="list-pre-defined-ssl-policies"></a><span data-ttu-id="1bb84-110">Lista wstępnie zdefiniowane zasady SSL</span><span class="sxs-lookup"><span data-stu-id="1bb84-110">List pre-defined SSL Policies</span></span>

<span data-ttu-id="1bb84-111">Brama aplikacji jest dostarczany z 3 wstępnie zdefiniowane zasady, które mogą być używane.</span><span class="sxs-lookup"><span data-stu-id="1bb84-111">Application gateway comes with 3 pre-defined policies that can be used.</span></span> <span data-ttu-id="1bb84-112">Witaj `Get-AzureRmApplicationGatewaySslPredefinedPolicy` polecenie cmdlet pobiera tych zasad.</span><span class="sxs-lookup"><span data-stu-id="1bb84-112">hello `Get-AzureRmApplicationGatewaySslPredefinedPolicy` cmdlet retrieves these policies.</span></span> <span data-ttu-id="1bb84-113">Wszystkie zasady mają różnych protokołów i mechanizmów szyfrowania włączone.</span><span class="sxs-lookup"><span data-stu-id="1bb84-113">Each policy has different protocol versions and cipher suites enabled.</span></span> <span data-ttu-id="1bb84-114">Te wstępnie zdefiniowane zasady mogą służyć tooquickly Konfigurowanie zasad dotyczących protokołu SSL na bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1bb84-114">These pre-defined policies can be used tooquickly configure an SSL policy on your application gateway.</span></span> <span data-ttu-id="1bb84-115">Domyślnie **AppGwSslPolicy20170401** jest zaznaczone, jeśli nie określonych SSL zdefiniowano zasad.</span><span class="sxs-lookup"><span data-stu-id="1bb84-115">By default **AppGwSslPolicy20170401** is selected if no specific SSL policy is defined.</span></span>

<span data-ttu-id="1bb84-116">Witaj poniżej przedstawiono przykładowy uruchamiania `Get-AzureRmApplicationGatewaySslPredefinedPolicy`.</span><span class="sxs-lookup"><span data-stu-id="1bb84-116">hello following is an example of running `Get-AzureRmApplicationGatewaySslPredefinedPolicy`.</span></span>

```
Name: AppGwSslPolicy20150501
MinProtocolVersion: TLSv1_0
CipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
 ...
Name: AppGwSslPolicy20170401
MinProtocolVersion: TLSv1_1
CipherSuites:
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
...
```

## <a name="configure-a-custom-ssl-policy"></a><span data-ttu-id="1bb84-117">Skonfiguruj niestandardowe zasady SSL</span><span class="sxs-lookup"><span data-stu-id="1bb84-117">Configure a custom SSL policy</span></span>

<span data-ttu-id="1bb84-118">Poniższy przykład Hello ustawia zasady niestandardowe SSL bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1bb84-118">hello following example sets a custom SSL policy on an application gateway.</span></span> <span data-ttu-id="1bb84-119">Ustawia wersję protocol minimalne hello zbyt`TLSv1_1` i umożliwia hello następujące mechanizmy szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="1bb84-119">It sets hello minimum protocol version too`TLSv1_1` and enables hello following cipher suites:</span></span>

* <span data-ttu-id="1bb84-120">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="1bb84-120">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
* <span data-ttu-id="1bb84-121">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="1bb84-121">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1bb84-122">Mechanizmy szyfrowania co najmniej jeden z następującej listy hello należy wybrać podczas konfigurowania niestandardowych zasad SSL.</span><span class="sxs-lookup"><span data-stu-id="1bb84-122">At least one cipher suite from hello following list must be selected when configuring a custom SSL policy.</span></span> <span data-ttu-id="1bb84-123">Brama aplikacji w używa mechanizmów szyfrowania RSA SHA256 zarządzania wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1bb84-123">Application gateway uses RSA SHA256 cipher suites for backend management.</span></span>
> * <span data-ttu-id="1bb84-124">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="1bb84-124">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
> * <span data-ttu-id="1bb84-125">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="1bb84-125">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
> * <span data-ttu-id="1bb84-126">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="1bb84-126">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
> * <span data-ttu-id="1bb84-127">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="1bb84-127">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
> * <span data-ttu-id="1bb84-128">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="1bb84-128">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
> * <span data-ttu-id="1bb84-129">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="1bb84-129">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

```powershell
# get an application gateway resource
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroup AdatumAppGatewayRG

# set hello SSL policy on hello application gateway
Set-AzureRmApplicationGatewaySslPolicy -ApplicationGateway $gw -PolicyType Custom -MinProtocolVersion TLSv1_1 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-an-application-gateway-with-a-pre-defined-ssl-policy"></a><span data-ttu-id="1bb84-130">Utwórz bramę aplikacji za pomocą wstępnie zdefiniowanych zasad protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="1bb84-130">Create an application gateway with a pre-defined SSL policy</span></span>

<span data-ttu-id="1bb84-131">Witaj poniższy przykład tworzy nową bramę aplikacji za pomocą wstępnie zdefiniowanych zasad SSL.</span><span class="sxs-lookup"><span data-stu-id="1bb84-131">hello following example creates a new application gateway with a pre-defined SSL policy.</span></span>

```powershell
# Create a resource group
$rg = New-AzureRmResourceGroup -Name ContosoRG -Location "East US"
# Create a subnet for hello application gateway
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
# Create a virtual network with a 10.0.0.0/16 address space
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName $rg.ResourceGroupName -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
# Retrieve hello subnet object for later use
$subnet = $vnet.Subnets[0]
# Create a public IP address
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName $rg.ResourceGroupName -name publicIP01 -location "East US" -AllocationMethod Dynamic
# Create a ip configuration object
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
# Create a backend pool for backend web servers
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
# Define hello backend http settings toobe used.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
# Create a new port for SSL
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
# Upload an existing pfx certificate for SSL offload
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile C:\folder\contoso.pfx -Password "P@ssw0rd"
# Create a frontend IP configuration for hello public IP address
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
# Create a new listener with hello certificate, port, and frontend ip.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
# Create a new rule for backend traffic routing
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
# Define hello size of hello application gateway
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
# Configure hello SSL policy toouse a different pre-defined policy
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
# Create hello application gateway.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName $rg.ResourceGroupName -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

## <a name="next-steps"></a><span data-ttu-id="1bb84-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1bb84-132">Next steps</span></span>

<span data-ttu-id="1bb84-133">Odwiedź stronę [omówienie przekierowania aplikacji bramy](application-gateway-redirect-overview.md) toolearn jak tooredirect HTTP ruchu tooa punkt końcowy HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1bb84-133">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) toolearn how tooredirect HTTP traffic tooa HTTPS endpoint.</span></span>
