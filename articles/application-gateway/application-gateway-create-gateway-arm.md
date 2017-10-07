---
title: "aaaCreate i zarządzanie nimi bramę aplikacji Azure — PowerShell | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate, skonfigurować, uruchomić i usunąć bramę aplikacji Azure za pomocą usługi Azure Resource Manager"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: ab98d5f9aa0dc309f8353b7f72591359e1121849
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="b6350-103">Tworzenie, uruchamianie lub usuwanie bramy aplikacji przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b6350-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b6350-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b6350-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="b6350-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6350-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="b6350-106">Klasyczny portal Azure — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6350-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="b6350-107">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b6350-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="b6350-108">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b6350-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="b6350-109">Usługa Azure Application Gateway to moduł równoważenia obciążenia warstwy 7.</span><span class="sxs-lookup"><span data-stu-id="b6350-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="b6350-110">Udostępnia trybu failover i wydajności routingu żądań HTTP między różnymi serwerami, czy znajdują się w chmurze hello lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="b6350-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="b6350-111">Usługa Application Gateway zapewnia wiele funkcji kontrolera dostarczania aplikacji (ADC, Application Delivery Controller), w tym między innymi równoważenie obciążenia HTTP, koligację sesji na podstawie plików cookie, odciążanie protokołu Secure Sockets Layer (SSL), niestandardowe sondy kondycji i obsługę wielu witryn.</span><span class="sxs-lookup"><span data-stu-id="b6350-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="b6350-112">odwiedź toofind pełną listę obsługiwanych funkcji [omówienie bramy aplikacji](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b6350-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="b6350-113">W tym artykule przedstawiono toocreate kroki hello, skonfiguruj start i usunąć bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b6350-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6350-114">Przed rozpoczęciem pracy z zasobów platformy Azure, jest ważne toounderstand, że Azure ma obecnie dwa modele wdrażania: Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="b6350-114">Before you work with Azure resources, it is important toounderstand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="b6350-115">Przed rozpoczęciem pracy z dowolnym zasobem platformy Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="b6350-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="b6350-116">Hello dokumentację dotyczącą różnych narzędzi można wyświetlić, klikając karty hello u góry hello tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="b6350-116">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="b6350-117">W tym dokumencie opisano tworzenie bramy aplikacji przy użyciu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b6350-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="b6350-118">toouse hello klasycznej wersji Przejdź zbyt[tworzenia wdrożenia klasycznego bramy aplikacji przy użyciu programu PowerShell](application-gateway-create-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="b6350-118">toouse hello classic version, go too[Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b6350-119">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="b6350-119">Before you begin</span></span>

1. <span data-ttu-id="b6350-120">Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b6350-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="b6350-121">Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b6350-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="b6350-122">Jeśli masz istniejącą sieć wirtualną, wybierz istniejącą podsieć pusty albo utwórz podsieć w istniejącej sieci wirtualnej wyłącznie do użytku przez bramę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b6350-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="b6350-123">Nie można wdrożyć hello aplikacji bramy tooa innej sieci wirtualnej niż hello zasobów ma toodeploy za hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b6350-123">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway.</span></span>
1. <span data-ttu-id="b6350-124">Skonfigurowanie bramy aplikacji hello toouse serwerów Hello musi istnieć lub mieć przypisane ich punkty końcowe utworzone w sieci wirtualnej hello lub z publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="b6350-124">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="b6350-125">Co to jest wymagana toocreate bramę aplikacji?</span><span class="sxs-lookup"><span data-stu-id="b6350-125">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="b6350-126">**Pula serwerów wewnętrznej bazy danych:** hello listę adresów IP, nazw FQDN lub kart hello serwerów wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b6350-126">**Backend server pool:** hello list of IP addresses, FQDNs, or NICs of hello backend servers.</span></span> <span data-ttu-id="b6350-127">Jeśli używane są adresy IP, albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="b6350-127">If IP addresses are used, they should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="b6350-128">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="b6350-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="b6350-129">Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.</span><span class="sxs-lookup"><span data-stu-id="b6350-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="b6350-130">**port serwera sieci Web:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b6350-130">**frontend port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="b6350-131">Ruch trafienia tego portu, a następnie pobiera przekierowanego tooone hello serwerów wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b6350-131">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="b6350-132">**Odbiornik:** odbiornika hello ma port serwera sieci Web, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="b6350-132">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="b6350-133">**Reguła:** reguły hello wiąże hello odbiornika, puli serwerów wewnętrznej bazy danych hello i określa, jaki ruch hello puli serwera wewnętrznej bazy danych ukierunkowanej toowhen trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="b6350-133">**Rule:** hello rule binds hello listener, hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="b6350-134">Tworzenie grupy zasobów dla usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b6350-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="b6350-135">Upewnij się, że używasz najnowszej wersji programu Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="b6350-135">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="b6350-136">Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="b6350-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="b6350-137">Zaloguj się za tooAzure i wprowadź swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="b6350-137">Log in tooAzure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="b6350-138">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="b6350-138">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="b6350-139">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b6350-139">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="b6350-140">Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="b6350-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="b6350-141">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="b6350-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="b6350-142">Ta lokalizacja jest używana jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="b6350-142">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="b6350-143">Upewnij się, że wszystkie toocreate polecenia używa bramy aplikacji hello same grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b6350-143">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="b6350-144">W powyższym przykładzie hello, utworzyliśmy grupę zasobów o nazwie **ContosoRG** i lokalizację **wschodnie stany USA**.</span><span class="sxs-lookup"><span data-stu-id="b6350-144">In hello example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="b6350-145">Jeśli potrzebujesz tooconfigure sondowania niestandardowych dla bramy aplikacji można znaleźć: [Utwórz bramę aplikacji z niestandardowego sond przy użyciu programu PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b6350-145">If you need tooconfigure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="b6350-146">Aby dowiedzieć się więcej, zapoznaj się z informacjami na temat [sond niestandardowych i monitorowania kondycji](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6350-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-hello-application-gateway-configuration-objects"></a><span data-ttu-id="b6350-147">Utwórz bramę aplikacji hello obiektów konfiguracji</span><span class="sxs-lookup"><span data-stu-id="b6350-147">Create hello application gateway configuration objects</span></span>

<span data-ttu-id="b6350-148">Wszystkie elementy konfiguracji należy skonfigurować przed utworzeniem bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b6350-148">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="b6350-149">Witaj następujące kroki tworzenia hello elementy konfiguracji, które są potrzebne dla zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b6350-149">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign hello address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with hello address space of 10.0.0.0/16 and add hello subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used tooconnect toohello application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. hello gateway picks up an IP addressfrom hello configured subnet and routes network traffic toohello IP addresses in hello backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with hello addresses of your web servers. These backend pool members are all validated toobe healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed toothem when requests come into hello application gateway. Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings toodetermine hello protocol and port that is used when sending traffic toohello backend servers. Cookie-based sessions are also determined by hello backend HTTP settings.  If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used tooconnect toohello application gateway through hello public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure hello frontend IP configuration with hello public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure hello listener.  hello listener is a combination of hello front end IP configuration, protocol, and port and is used tooreceive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used tooroute traffic toohello backend servers. hello backend pool settings, listener, and backend pool created in hello previous steps make up hello rule. Based on hello criteria defined traffic is routed toohello appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU for hello application gateway, this determines hello size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="b6350-150">Po zakończeniu pobrać DNS i adres VIP szczegóły bramy aplikacji hello z hello publicznego adresu IP zasobu toohello dołączone bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b6350-150">When complete, retrieve DNS and VIP details of hello application gateway from hello public IP resource attached toohello application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="b6350-151">Usuń bramę aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="b6350-151">Delete hello application gateway</span></span>

<span data-ttu-id="b6350-152">Witaj poniższy przykład usuwa bramę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b6350-152">hello following example deletes hello application gateway.</span></span>

```powershell
# Retrieve hello application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops hello application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="b6350-153">Witaj **-force** przełącznika może być używane toosuppress hello Usuń potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="b6350-153">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="b6350-154">tooverify, który hello usługi zostały usunięte, możesz użyć hello `Get-AzureRmApplicationGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b6350-154">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="b6350-155">Ten krok nie jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="b6350-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="b6350-156">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="b6350-156">Get application gateway DNS name</span></span>

<span data-ttu-id="b6350-157">Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji.</span><span class="sxs-lookup"><span data-stu-id="b6350-157">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="b6350-158">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="b6350-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="b6350-159">Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b6350-159">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="b6350-160">toodo tego pobierania szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone.</span><span class="sxs-lookup"><span data-stu-id="b6350-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="b6350-161">Można to zrobić z usługi Azure DNS lub innych dostawców DNS przez utworzenie rekordu CNAME, który wskazuje toohello [publicznego adresu IP](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="b6350-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points toohello [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="b6350-162">Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b6350-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="b6350-163">Adres IP jest przypisany toohello bramy aplikacji, po uruchomieniu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="b6350-163">An IP address is assigned toohello application gateway when hello service starts.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
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

## <a name="delete-all-resources"></a><span data-ttu-id="b6350-164">Usuwanie wszystkich zasobów</span><span class="sxs-lookup"><span data-stu-id="b6350-164">Delete all resources</span></span>

<span data-ttu-id="b6350-165">toodelete wszystkie zasoby są tworzone w tym artykule pełną powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="b6350-165">toodelete all resources created in this article, complete hello following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="b6350-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b6350-166">Next steps</span></span>

<span data-ttu-id="b6350-167">Jeśli chcesz tooconfigure odciążanie protokołu SSL można znaleźć: [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b6350-167">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="b6350-168">Jeśli chcesz tooconfigure toouse bramy aplikacji z wewnętrznego modułu równoważenia obciążenia, odwiedź stronę: [Utwórz bramę aplikacji z wewnętrznego modułu równoważenia obciążenia (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="b6350-168">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="b6350-169">Więcej ogólnych informacji na temat opcji równoważenia obciążenia możesz znaleźć, odwiedzając:</span><span class="sxs-lookup"><span data-stu-id="b6350-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="b6350-170">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="b6350-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="b6350-171">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="b6350-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
