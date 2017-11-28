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
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="0303d-103">Konfigurowanie zapory aplikacji sieci web w nowej lub istniejącej bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="0303d-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0303d-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0303d-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="0303d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0303d-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="0303d-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0303d-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="0303d-107">Dowiedz się, jak toocreate zapory aplikacji sieci web włączone bramy aplikacji lub Dodaj tooan zapory aplikacji sieci web istniejącą bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0303d-107">Learn how toocreate a web application firewall enabled Application Gateway or add web application firewall tooan existing Application Gateway.</span></span>

<span data-ttu-id="0303d-108">Hello zapory aplikacji sieci web (WAF) brama aplikacji w usłudze Azure chroni aplikacje sieci web przed wspólnej ataków opartych na sieci web takich jak iniekcja kodu SQL, ataki skryptów między witrynami i hijacks sesji.</span><span class="sxs-lookup"><span data-stu-id="0303d-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="0303d-109">Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7.</span><span class="sxs-lookup"><span data-stu-id="0303d-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="0303d-110">Zapewnia on trybu failover, wydajności routingu żądań HTTP między różnymi serwerami, czy znajdują się w chmurze hello lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="0303d-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="0303d-111">Brama aplikacji w oferuje wiele funkcji aplikacji dostarczania kontrolera (ADC), w tym HTTP załadować równoważenia, opartych na pliku cookie sesji koligacji, Odciążanie bezpiecznego secure sockets layer (SSL), sondy kondycji niestandardowych, obsługę wielu lokacji i wielu innych.</span><span class="sxs-lookup"><span data-stu-id="0303d-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="0303d-112">toofind pełną listę obsługiwanych funkcji, odwiedź stronę: [brama Omówienie aplikacji](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0303d-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="0303d-113">Hello artykule przedstawiono sposób zbyt[dodać tooan zapory aplikacji sieci web istniejącą bramę aplikacji](#add-web-application-firewall-to-an-existing-application-gateway) i [Utwórz bramę aplikacji, która używa zapory aplikacji sieci web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="0303d-113">hello following article shows how too[add web application firewall tooan existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![Scenariusz obrazu][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="0303d-115">Różnice w konfiguracji zapory aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="0303d-115">WAF configuration differences</span></span>

<span data-ttu-id="0303d-116">Jeśli znasz [Utwórz bramę aplikacji przy użyciu programu PowerShell](application-gateway-create-gateway-arm.md), zrozumieć hello SKU ustawienia tooconfigure podczas tworzenia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0303d-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand hello SKU settings tooconfigure when creating an Application Gateway.</span></span> <span data-ttu-id="0303d-117">Zapory aplikacji sieci Web udostępnia dodatkowe ustawienia toodefine podczas konfigurowania hello jednostki SKU bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0303d-117">WAF provides additional settings toodefine when configuring hello SKU on an Application Gateway.</span></span> <span data-ttu-id="0303d-118">Brak dodatkowych zmian wprowadzonych na powitania bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0303d-118">There are no additional changes that you make on hello Application Gateway itself.</span></span>

| <span data-ttu-id="0303d-119">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="0303d-119">**Setting**</span></span> | <span data-ttu-id="0303d-120">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="0303d-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="0303d-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="0303d-121">**SKU**</span></span> |<span data-ttu-id="0303d-122">Normalne bramy aplikacji nie obsługuje zapory aplikacji sieci Web **standardowe\_małych**, **standardowe\_średni**, i **standardowe\_duży** rozmiary.</span><span class="sxs-lookup"><span data-stu-id="0303d-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="0303d-123">Wprowadzenie hello zapory aplikacji sieci Web, istnieją dwie dodatkowe jednostki SKU, **zapory aplikacji sieci Web\_średni** i **zapory aplikacji sieci Web\_duży**.</span><span class="sxs-lookup"><span data-stu-id="0303d-123">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="0303d-124">Zapory aplikacji sieci Web nie jest obsługiwana w małych bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0303d-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="0303d-125">**Warstwy**</span><span class="sxs-lookup"><span data-stu-id="0303d-125">**Tier**</span></span> | <span data-ttu-id="0303d-126">Witaj dostępne wartości to **standardowe** lub **WAF**.</span><span class="sxs-lookup"><span data-stu-id="0303d-126">hello available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="0303d-127">Zapora aplikacji sieci web, używając **WAF** musi być wybrany.</span><span class="sxs-lookup"><span data-stu-id="0303d-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="0303d-128">**Tryb**</span><span class="sxs-lookup"><span data-stu-id="0303d-128">**Mode**</span></span> | <span data-ttu-id="0303d-129">To ustawienie jest tryb hello zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0303d-129">This setting is hello mode of WAF.</span></span> <span data-ttu-id="0303d-130">dozwolone wartości to **wykrywania** i **zapobiegania**.</span><span class="sxs-lookup"><span data-stu-id="0303d-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="0303d-131">Gdy zapory aplikacji sieci Web jest skonfigurowana w trybie wykrywania, wszystkie zagrożenia są przechowywane w pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="0303d-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="0303d-132">W trybie zapobiegania zdarzenia są nadal rejestrowane, ale osoba atakująca hello odbiera odpowiedź 403 nieautoryzowanego z hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0303d-132">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello Application Gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="0303d-133">Dodaj tooan zapory aplikacji sieci web istniejącej bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="0303d-133">Add web application firewall tooan existing Application Gateway</span></span>

<span data-ttu-id="0303d-134">Upewnij się, że używasz najnowszej wersji programu Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0303d-134">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="0303d-135">Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="0303d-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="0303d-136">Zaloguj się za tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0303d-136">Log in tooyour Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="0303d-137">Wybierz hello toouse subskrypcji dla tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="0303d-137">Select hello subscription toouse for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="0303d-138">Pobrać bramy hello są Dodawanie zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="0303d-138">Retrieve hello gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="0303d-139">Skonfiguruj sku zapory aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="0303d-139">Configure hello web application firewall sku.</span></span> <span data-ttu-id="0303d-140">są dostępne rozmiary Hello **zapory aplikacji sieci Web\_duży** i **WAF\_średni**.</span><span class="sxs-lookup"><span data-stu-id="0303d-140">hello available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="0303d-141">Gdy jest używana Zapora aplikacji sieci web musi być warstwy hello **zapory aplikacji sieci Web**, pojemność hello muszą zostać potwierdzone przy ustawianiu hello jednostki sku.</span><span class="sxs-lookup"><span data-stu-id="0303d-141">When web application firewall is used hello tier must be **WAF**, hello capacity must be confirmed when setting hello sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="0303d-142">Skonfiguruj ustawienia hello zapory aplikacji sieci Web, zgodnie z definicją w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="0303d-142">Configure hello WAF settings as defined in hello following example:</span></span>

   <span data-ttu-id="0303d-143">Aby uzyskać **FirewallMode**, hello dostępne wartości to wykrywania i zapobiegania.</span><span class="sxs-lookup"><span data-stu-id="0303d-143">For **FirewallMode**, hello available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="0303d-144">Zaktualizuj hello bramy aplikacji z ustawieniami hello zdefiniowane w hello poprzedzających krok.</span><span class="sxs-lookup"><span data-stu-id="0303d-144">Update hello Application Gateway with hello settings defined in hello preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="0303d-145">To polecenie aktualizuje bramy aplikacji hello zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="0303d-145">This command updates hello Application Gateway with web application firewall.</span></span> <span data-ttu-id="0303d-146">Odwiedź stronę [diagnostyki bramy aplikacji](application-gateway-diagnostics.md) toounderstand jak tooview dzienniki bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0303d-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your Application Gateway.</span></span> <span data-ttu-id="0303d-147">Powodu toohello zabezpieczeń rodzaj zapory aplikacji sieci Web dzienniki toobe należy regularnie weryfikowane toounderstand hello stan zabezpieczeń aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="0303d-147">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="0303d-148">Utwórz bramę aplikacji z zapory aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="0303d-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="0303d-149">Hello poniższe kroki przedstawiają cały proces powitania od początku tooend do tworzenia bramy aplikacji z zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="0303d-149">hello following steps take you through hello entire process from beginning tooend for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="0303d-150">Upewnij się, że używasz najnowszej wersji programu Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0303d-150">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="0303d-151">Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="0303d-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="0303d-152">Zaloguj się za tooAzure uruchamiając `Login-AzureRmAccount`, to zostanie wyświetlony monit o tooauthenticate przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="0303d-152">Log in tooAzure by running `Login-AzureRmAccount`, you are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="0303d-153">Sprawdź, czy hello subskrypcji dla konta hello uruchamiając`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="0303d-153">Check hello subscriptions for hello account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="0303d-154">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0303d-154">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="0303d-155">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="0303d-155">Create a resource group</span></span>

<span data-ttu-id="0303d-156">Utwórz grupę zasobów dla hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="0303d-156">Create a resource group for hello Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="0303d-157">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="0303d-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="0303d-158">Ta lokalizacja jest używana jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="0303d-158">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="0303d-159">Upewnij się, że wszystkie polecenia, które używa toocreate jako bramy aplikacji hello tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="0303d-159">Make sure that all commands toocreate an Application Gateway uses hello same resource group.</span></span>

<span data-ttu-id="0303d-160">W hello poprzedzających przykład utworzyliśmy grupę zasobów o nazwie "Zarządcy zasobów appgw" i lokalizacji "zachodnie stany USA."</span><span class="sxs-lookup"><span data-stu-id="0303d-160">In hello preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="0303d-161">Jeśli potrzebujesz tooconfigure sondowania niestandardowych dla bramy aplikacji, zobacz [Utwórz bramę aplikacji z niestandardowego sond przy użyciu programu PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0303d-161">If you need tooconfigure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="0303d-162">Aby dowiedzieć się więcej, zapoznaj się z informacjami na temat [sond niestandardowych i monitorowania kondycji](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0303d-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="0303d-163">Konfigurowanie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0303d-163">Configure virtual network</span></span>

<span data-ttu-id="0303d-164">Brama aplikacji wymaga własnej podsieci.</span><span class="sxs-lookup"><span data-stu-id="0303d-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="0303d-165">W tym kroku utworzysz sieci wirtualnej przestrzeni adresowej 10.0.0.0/16 z dwoma podsieciami, jeden dla bramy aplikacji hello i jeden dla członków puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0303d-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for hello Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="0303d-166">Skonfiguruj publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="0303d-166">Configure public IP address</span></span>

<span data-ttu-id="0303d-167">W kolejności toohandle zewnętrznych żądań bramy aplikacji wymaga publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="0303d-167">In order toohandle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="0303d-168">Ten publiczny adres IP nie może mieć `DomainNameLabel` zdefiniowane toobe używany przez bramę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0303d-168">This public IP address must not have a `DomainNameLabel` defined toobe used by hello Application Gateway.</span></span>

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a><span data-ttu-id="0303d-169">Skonfiguruj hello bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="0303d-169">Configure hello Application Gateway</span></span>

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
> <span data-ttu-id="0303d-170">Bramy aplikacji utworzonych za pomocą konfiguracji zapory aplikacji sieci web podstawowe hello są skonfigurowane z CRS 3.0 do ochrony.</span><span class="sxs-lookup"><span data-stu-id="0303d-170">Application Gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="0303d-171">Pobierz nazwę DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="0303d-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="0303d-172">Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji.</span><span class="sxs-lookup"><span data-stu-id="0303d-172">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="0303d-173">Korzystając z publicznym adresem IP, brama aplikacji wymaga przypisywany dynamicznie nazwy DNS, który nie jest przyjazną.</span><span class="sxs-lookup"><span data-stu-id="0303d-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="0303d-174">tooensure użytkownicy końcowi mogą trafień hello bramy aplikacji, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0303d-174">tooensure end users can hit hello Application Gateway, a CNAME record can be used toopoint toohello public endpoint of hello Application Gateway.</span></span> <span data-ttu-id="0303d-175">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0303d-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="0303d-176">tooconfigure aliasu, pobrać szczegółów hello bramy aplikacji i skojarzonej z nią IP DNS nazwy przy użyciu hello publicznego adresu IP elementu dołączony toohello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="0303d-176">tooconfigure an alias, retrieve details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello Application Gateway.</span></span> <span data-ttu-id="0303d-177">Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS.</span><span class="sxs-lookup"><span data-stu-id="0303d-177">hello Application Gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="0303d-178">Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0303d-178">hello use of A-records is not recommended since hello VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0303d-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0303d-179">Next steps</span></span>

<span data-ttu-id="0303d-180">Dowiedz się, jak tooconfigure rejestrowania diagnostycznego, toolog hello zdarzenia, które są wykrywane lub zapobiec za pomocą zapory aplikacji sieci web, odwiedzając [diagnostyki bramy aplikacji](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="0303d-180">Learn how tooconfigure diagnostic logging, toolog hello events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
