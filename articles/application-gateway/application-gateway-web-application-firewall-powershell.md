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
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="77ad4-103">Konfigurowanie zapory aplikacji sieci web w nowej lub istniejącej bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="77ad4-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="77ad4-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="77ad4-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="77ad4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="77ad4-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="77ad4-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="77ad4-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="77ad4-107">Dowiedz się, jak utworzyć aplikację sieci web zapory włączone bramy aplikacji lub dodawanie zapory aplikacji sieci web do istniejącej bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-107">Learn how to create a web application firewall enabled Application Gateway or add web application firewall to an existing Application Gateway.</span></span>

<span data-ttu-id="77ad4-108">Zapora aplikacji sieci web (WAF) w brama aplikacji w usłudze Azure chroni aplikacje sieci web przed wspólnej ataków opartych na sieci web takich jak iniekcja kodu SQL, atakami skryptów między witrynami i hijacks sesji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="77ad4-109">Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7.</span><span class="sxs-lookup"><span data-stu-id="77ad4-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="77ad4-110">Udostępnia tryb failover, oparty na wydajności routing żądań HTTP między różnymi serwerami — w chmurze i lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="77ad4-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="77ad4-111">Brama aplikacji w oferuje wiele funkcji aplikacji dostarczania kontrolera (ADC), w tym HTTP załadować równoważenia, opartych na pliku cookie sesji koligacji, Odciążanie bezpiecznego secure sockets layer (SSL), sondy kondycji niestandardowych, obsługę wielu lokacji i wielu innych.</span><span class="sxs-lookup"><span data-stu-id="77ad4-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="77ad4-112">Aby uzyskać pełną listę obsługiwanych funkcji, odwiedź stronę: [brama Omówienie aplikacji](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="77ad4-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="77ad4-113">Następujące artykuł przedstawia sposób [Dodawanie zapory aplikacji sieci web do istniejącej bramy aplikacji](#add-web-application-firewall-to-an-existing-application-gateway) i [Utwórz bramę aplikacji, która używa zapory aplikacji sieci web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="77ad4-113">The following article shows how to [add web application firewall to an existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![Scenariusz obrazu][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="77ad4-115">Różnice w konfiguracji zapory aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="77ad4-115">WAF configuration differences</span></span>

<span data-ttu-id="77ad4-116">Jeśli znasz [Utwórz bramę aplikacji przy użyciu programu PowerShell](application-gateway-create-gateway-arm.md), zrozumieć ustawienia Jednostka SKU, aby skonfigurować podczas tworzenia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand the SKU settings to configure when creating an Application Gateway.</span></span> <span data-ttu-id="77ad4-117">Zapory aplikacji sieci Web udostępnia dodatkowe ustawienia, aby zdefiniować podczas konfigurowania jednostka SKU bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-117">WAF provides additional settings to define when configuring the SKU on an Application Gateway.</span></span> <span data-ttu-id="77ad4-118">Brak dodatkowych zmian wprowadzonych na bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-118">There are no additional changes that you make on the Application Gateway itself.</span></span>

| <span data-ttu-id="77ad4-119">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="77ad4-119">**Setting**</span></span> | <span data-ttu-id="77ad4-120">**Szczegóły**</span><span class="sxs-lookup"><span data-stu-id="77ad4-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="77ad4-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="77ad4-121">**SKU**</span></span> |<span data-ttu-id="77ad4-122">Normalne bramy aplikacji nie obsługuje zapory aplikacji sieci Web **standardowe\_małych**, **standardowe\_średni**, i **standardowe\_duży** rozmiary.</span><span class="sxs-lookup"><span data-stu-id="77ad4-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="77ad4-123">Wraz z wprowadzeniem zapory aplikacji sieci Web, istnieją dwie dodatkowe jednostki SKU, **WAF\_średni** i **zapory aplikacji sieci Web\_duży**.</span><span class="sxs-lookup"><span data-stu-id="77ad4-123">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="77ad4-124">Zapory aplikacji sieci Web nie jest obsługiwana w małych bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="77ad4-125">**Warstwy**</span><span class="sxs-lookup"><span data-stu-id="77ad4-125">**Tier**</span></span> | <span data-ttu-id="77ad4-126">Dostępne wartości to **standardowe** lub **WAF**.</span><span class="sxs-lookup"><span data-stu-id="77ad4-126">The available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="77ad4-127">Zapora aplikacji sieci web, używając **WAF** musi być wybrany.</span><span class="sxs-lookup"><span data-stu-id="77ad4-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="77ad4-128">**Tryb**</span><span class="sxs-lookup"><span data-stu-id="77ad4-128">**Mode**</span></span> | <span data-ttu-id="77ad4-129">To ustawienie jest tryb zapory aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="77ad4-129">This setting is the mode of WAF.</span></span> <span data-ttu-id="77ad4-130">dozwolone wartości to **wykrywania** i **zapobiegania**.</span><span class="sxs-lookup"><span data-stu-id="77ad4-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="77ad4-131">Gdy zapory aplikacji sieci Web jest skonfigurowana w trybie wykrywania, wszystkie zagrożenia są przechowywane w pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="77ad4-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="77ad4-132">W trybie zapobiegania zdarzenia są nadal rejestrowane, ale osoba atakująca otrzymuje 403 nieautoryzowanego odpowiedź z bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-132">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the Application Gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="77ad4-133">Dodawanie zapory aplikacji sieci web do istniejącej bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="77ad4-133">Add web application firewall to an existing Application Gateway</span></span>

<span data-ttu-id="77ad4-134">Upewnij się, że używasz najnowszej wersji programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77ad4-134">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="77ad4-135">Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="77ad4-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="77ad4-136">Zaloguj się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77ad4-136">Log in to your Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="77ad4-137">Wybierz subskrypcję do użycia na potrzeby tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="77ad4-137">Select the subscription to use for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="77ad4-138">Pobrać bramy, które są Dodawanie zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="77ad4-138">Retrieve the gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="77ad4-139">Skonfiguruj sku zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="77ad4-139">Configure the web application firewall sku.</span></span> <span data-ttu-id="77ad4-140">Dostępne rozmiary są **zapory aplikacji sieci Web\_duży** i **WAF\_średni**.</span><span class="sxs-lookup"><span data-stu-id="77ad4-140">The available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="77ad4-141">Gdy jest używana Zapora aplikacji sieci web warstwy musi być **WAF**, pojemność muszą zostać potwierdzone przy ustawianiu jednostki sku.</span><span class="sxs-lookup"><span data-stu-id="77ad4-141">When web application firewall is used the tier must be **WAF**, the capacity must be confirmed when setting the sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="77ad4-142">Skonfiguruj ustawienia zapory aplikacji sieci Web, zgodnie z definicją w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="77ad4-142">Configure the WAF settings as defined in the following example:</span></span>

   <span data-ttu-id="77ad4-143">Aby uzyskać **FirewallMode**, dostępne wartości to wykrywania i zapobiegania.</span><span class="sxs-lookup"><span data-stu-id="77ad4-143">For **FirewallMode**, the available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="77ad4-144">Zaktualizuj bramę aplikacji z ustawień zdefiniowanych w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="77ad4-144">Update the Application Gateway with the settings defined in the preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="77ad4-145">To polecenie aktualizuje bramy aplikacji zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="77ad4-145">This command updates the Application Gateway with web application firewall.</span></span> <span data-ttu-id="77ad4-146">Odwiedź stronę [diagnostyki bramy aplikacji](application-gateway-diagnostics.md) zrozumienie, jak wyświetlać dzienniki bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your Application Gateway.</span></span> <span data-ttu-id="77ad4-147">Z powodu zabezpieczeń rodzaj zapory aplikacji sieci Web Dzienniki należy ją sprawdzić regularnie, aby poznać strukturę aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="77ad4-147">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="77ad4-148">Utwórz bramę aplikacji z zapory aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="77ad4-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="77ad4-149">Poniższe kroki przedstawiają cały proces od początku do końca Tworzenie bramy aplikacji za pomocą zapory aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="77ad4-149">The following steps take you through the entire process from beginning to end for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="77ad4-150">Upewnij się, że używasz najnowszej wersji programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77ad4-150">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="77ad4-151">Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="77ad4-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="77ad4-152">Logowanie do platformy Azure, uruchamiając `Login-AzureRmAccount`, zostanie wyświetlony monit o uwierzytelniania przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="77ad4-152">Log in to Azure by running `Login-AzureRmAccount`, you are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="77ad4-153">Sprawdź subskrypcje dla konta, uruchamiając`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="77ad4-153">Check the subscriptions for the account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="77ad4-154">Wybierz subskrypcję platformy Azure do użycia.</span><span class="sxs-lookup"><span data-stu-id="77ad4-154">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="77ad4-155">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="77ad4-155">Create a resource group</span></span>

<span data-ttu-id="77ad4-156">Utwórz grupę zasobów dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-156">Create a resource group for the Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="77ad4-157">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="77ad4-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="77ad4-158">Ta lokalizacja będzie używana jako domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="77ad4-158">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="77ad4-159">Upewnij się, że wszystkie polecenia, aby utworzyć bramę aplikacji używa tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="77ad4-159">Make sure that all commands to create an Application Gateway uses the same resource group.</span></span>

<span data-ttu-id="77ad4-160">W powyższym przykładzie utworzono grupę zasobów o nazwie "zarządcy zasobów appgw" i lokalizacji "Zachodnie stany USA".</span><span class="sxs-lookup"><span data-stu-id="77ad4-160">In the preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="77ad4-161">Jeśli trzeba skonfigurować niestandardowe sondowania dla bramy aplikacji, zobacz [Utwórz bramę aplikacji z niestandardowego sond przy użyciu programu PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="77ad4-161">If you need to configure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="77ad4-162">Aby dowiedzieć się więcej, zapoznaj się z informacjami na temat [sond niestandardowych i monitorowania kondycji](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77ad4-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="77ad4-163">Skonfiguruj sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="77ad4-163">Configure virtual network</span></span>

<span data-ttu-id="77ad4-164">Brama aplikacji wymaga własnej podsieci.</span><span class="sxs-lookup"><span data-stu-id="77ad4-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="77ad4-165">W tym kroku utworzysz sieci wirtualnej przestrzeni adresowej 10.0.0.0/16 z dwoma podsieciami, jeden dla bramy aplikacji i jeden dla członków puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="77ad4-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for the Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="77ad4-166">Skonfiguruj publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="77ad4-166">Configure public IP address</span></span>

<span data-ttu-id="77ad4-167">W celu obsługi żądań zewnętrznych, bramy aplikacji wymaga publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="77ad4-167">In order to handle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="77ad4-168">Ten publiczny adres IP nie może mieć `DomainNameLabel` definicja ma być używany przez bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-168">This public IP address must not have a `DomainNameLabel` defined to be used by the Application Gateway.</span></span>

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a><span data-ttu-id="77ad4-169">Konfigurowanie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="77ad4-169">Configure the Application Gateway</span></span>

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
> <span data-ttu-id="77ad4-170">Bramy aplikacji utworzonych za pomocą konfiguracji zapory aplikacji sieci web podstawowe są skonfigurowane z CRS 3.0 do ochrony.</span><span class="sxs-lookup"><span data-stu-id="77ad4-170">Application Gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="77ad4-171">Pobierz nazwę DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="77ad4-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="77ad4-172">Po utworzeniu bramy następnym krokiem jest skonfigurowanie frontonu na potrzeby komunikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-172">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="77ad4-173">Korzystając z publicznym adresem IP, brama aplikacji wymaga przypisywany dynamicznie nazwy DNS, który nie jest przyjazną.</span><span class="sxs-lookup"><span data-stu-id="77ad4-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="77ad4-174">Aby zapewnić, że użytkownicy końcowi mogą trafień bramy aplikacji, można rekord CNAME wskaż publiczny punkt końcowy bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-174">To ensure end users can hit the Application Gateway, a CNAME record can be used to point to the public endpoint of the Application Gateway.</span></span> <span data-ttu-id="77ad4-175">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="77ad4-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="77ad4-176">Aby skonfigurować alias, należy pobrać szczegółów bramy aplikacji i jego skojarzonej nazwy IP DNS za pomocą elementu publicznego adresu IP dołączony na bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-176">To configure an alias, retrieve details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element attached to the Application Gateway.</span></span> <span data-ttu-id="77ad4-177">Brama aplikacji w nazwa DNS należy utworzyć rekord CNAME, wskazujący aplikacji dwie sieci web do tej nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="77ad4-177">The Application Gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="77ad4-178">Użycie rekordów A nie jest zalecane, ponieważ adres VIP może się zmieniać podczas ponownego uruchomienia bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="77ad4-178">The use of A-records is not recommended since the VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="77ad4-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77ad4-179">Next steps</span></span>

<span data-ttu-id="77ad4-180">Informacje o sposobie konfigurowania rejestrowania diagnostycznego do dziennika zdarzeń, które wykryte lub uniemożliwił z zapory aplikacji sieci web, odwiedzając [diagnostyki bramy aplikacji](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="77ad4-180">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
