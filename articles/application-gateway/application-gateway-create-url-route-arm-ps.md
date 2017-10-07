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
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="9ad4f-103">Utwórz bramę aplikacji przy użyciu routingu opartego na ścieżce</span><span class="sxs-lookup"><span data-stu-id="9ad4f-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ad4f-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9ad4f-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="9ad4f-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ad4f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="9ad4f-106">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="9ad4f-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="9ad4f-107">Na podstawie ścieżki routingu adresów URL umożliwia możesz tooassociate tras na podstawie hello ścieżki adresu URL żądania Http.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="9ad4f-108">Sprawdza, czy jest skonfigurowane dla adresu URL hello przedstawionych w hello brama aplikacji w puli zaplecza tooa trasy.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway.</span></span> <span data-ttu-id="9ad4f-109">Wysyła następnie toohello ruchu sieciowego hello zdefiniowanymi w puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-109">It then sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="9ad4f-110">Użycia routingu opartego na adres URL jest tooload równoważenie żądań dla pul serwerów zaplecza toodifferent różne typy zawartości.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-110">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="9ad4f-111">Na podstawie adresu URL routingu wprowadza nową bramę tooapplication typ reguły.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-111">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="9ad4f-112">Brama aplikacji ma dwa typy zasad: podstawowe i PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-112">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="9ad4f-113">Podstawowe reguły typ zapewnia usługi okrężnego dla zaplecza hello pul podczas PathBasedRouting dodatkowo dystrybucji działania okrężnego tooround, uwzględnia również wzorzec ścieżki adresu URL żądania hello podczas wybierania hello puli wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-113">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="9ad4f-114">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="9ad4f-114">Scenario</span></span>

<span data-ttu-id="9ad4f-115">W hello poniższy przykład, bramy aplikacji jest obsługę ruchu dla domeny contoso.com z dwóch pul serwerów zaplecza: puli serwerów wideo i puli serwerów obrazu.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-115">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="9ad4f-116">Żądania dla http://contoso.com/image * są kierowane puli serwerów tooimage (pool1), a http://contoso.com/video * są kierowane puli serwerów toovideo (pool2).</span><span class="sxs-lookup"><span data-stu-id="9ad4f-116">Requests for http://contoso.com/image* are routed tooimage server pool (pool1), and http://contoso.com/video* are routed toovideo server pool (pool2).</span></span> <span data-ttu-id="9ad4f-117">Jeśli żadna hello ścieżki wzorców, domyślna pula serwera (pool1) jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-117">if none of hello path patterns match, a default server pool (pool1) is selected.</span></span>

![trasy adresu URL](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="9ad4f-119">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="9ad4f-119">Before you begin</span></span>

1. <span data-ttu-id="9ad4f-120">Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="9ad4f-121">Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9ad4f-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="9ad4f-122">Utworzysz sieć wirtualna i podsieć bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-122">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="9ad4f-123">Upewnij się, że nie maszyny wirtualne lub wdrożenia chmury z hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-123">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="9ad4f-124">Brama aplikacji Hello należy samodzielnie w podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-124">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="9ad4f-125">serwery Hello dodać bramę aplikacji hello toouse puli zaplecza toohello musi istnieć lub ich punkty końcowe utworzone w sieci wirtualnej hello lub z publicznego adresu IP/VIP przypisane.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-125">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="9ad4f-126">Co to jest wymagana toocreate bramę aplikacji?</span><span class="sxs-lookup"><span data-stu-id="9ad4f-126">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="9ad4f-127">**Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="9ad4f-128">wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="9ad4f-129">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="9ad4f-130">Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="9ad4f-131">**Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="9ad4f-132">Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="9ad4f-133">**Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="9ad4f-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="9ad4f-134">**Reguła:** reguły hello wiąże hello odbiornika, hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-134">**Rule:** hello rule binds hello listener, hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="9ad4f-135">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="9ad4f-135">Create an application gateway</span></span>

<span data-ttu-id="9ad4f-136">Różnica Hello przy użyciu klasycznego Azure i usługi Azure Resource Manager jest hello kolejność, w którym utworzyć bramę aplikacji hello i elementy hello toobe skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-136">hello difference between using Azure Classic and Azure Resource Manager is hello order in which you create hello application gateway and hello items that need toobe configured.</span></span>

<span data-ttu-id="9ad4f-137">Usługa Resource Manager wszystkie elementy bramy aplikacji są konfigurowane osobno, a następnie przekaż razem zasobu bramy aplikacji hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-137">With Resource Manager, all items that make an application gateway are configured individually and then put together toocreate hello application gateway resource.</span></span>

<span data-ttu-id="9ad4f-138">Poniżej przedstawiono kroki hello, które są potrzebne toocreate bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="9ad4f-138">Here are hello steps that are needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="9ad4f-139">Utworzenie grupy zasobów dla usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="9ad4f-140">Tworzenie sieci wirtualnej, podsieci i publicznego adresu IP dla bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-140">Create a virtual network, subnet, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="9ad4f-141">Utworzenie obiektu konfiguracji bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-141">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="9ad4f-142">Utworzenie zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-142">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="9ad4f-143">Tworzenie grupy zasobów dla usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9ad4f-143">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="9ad4f-144">Upewnij się, że używasz najnowszej wersji programu Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-144">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="9ad4f-145">Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="9ad4f-145">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="9ad4f-146">Krok 1</span><span class="sxs-lookup"><span data-stu-id="9ad4f-146">Step 1</span></span>

<span data-ttu-id="9ad4f-147">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="9ad4f-147">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="9ad4f-148">Jesteś zostanie wyświetlony monit o tooauthenticate przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-148">You are prompted tooauthenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="9ad4f-149">Krok 2</span><span class="sxs-lookup"><span data-stu-id="9ad4f-149">Step 2</span></span>

<span data-ttu-id="9ad4f-150">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-150">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="9ad4f-151">Krok 3</span><span class="sxs-lookup"><span data-stu-id="9ad4f-151">Step 3</span></span>

<span data-ttu-id="9ad4f-152">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-152">Choose which of your Azure subscriptions toouse.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="9ad4f-153">Krok 4</span><span class="sxs-lookup"><span data-stu-id="9ad4f-153">Step 4</span></span>

<span data-ttu-id="9ad4f-154">Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="9ad4f-154">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="9ad4f-155">Alternatywnie można również utworzyć tagi dla grupy zasobów dla bramy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="9ad4f-155">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="9ad4f-156">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-156">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="9ad4f-157">Ta grupa zasobów jest używany jako domyślną lokalizacją plików hello zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-157">This resource group is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="9ad4f-158">Upewnij się, że hello Użyj bramy aplikacji wszystkie polecenia toocreate tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-158">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="9ad4f-159">W powyższym przykładzie hello utworzono grupę zasobów o nazwie "zarządcy zasobów appgw" i lokalizacji "Zachodnie US".</span><span class="sxs-lookup"><span data-stu-id="9ad4f-159">In hello example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> <span data-ttu-id="9ad4f-160">Jeśli potrzebujesz tooconfigure sondowania niestandardowych dla bramy aplikacji, zobacz [Utwórz bramę aplikacji z niestandardowego sond przy użyciu programu PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9ad4f-160">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="9ad4f-161">Aby dowiedzieć się więcej, zapoznaj się z informacjami na temat [sond niestandardowych i monitorowania kondycji](application-gateway-probe-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9ad4f-161">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="9ad4f-162">Utwórz sieć wirtualną i podsieć bramy aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="9ad4f-162">Create a virtual network and a subnet for hello application gateway</span></span>

<span data-ttu-id="9ad4f-163">powitania po przykładzie pokazano, jak toocreate sieci wirtualnej za pomocą Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-163">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="9ad4f-164">W tym przykładzie jest tworzony dla hello brama aplikacji w sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-164">This example creates a VNET for hello Application Gateway.</span></span> <span data-ttu-id="9ad4f-165">Brama aplikacji wymaga jego własnej podsieci z tego powodu podsieci hello utworzone dla bramy aplikacji hello jest mniejszy niż hello przestrzeni adresowej sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-165">Application Gateway requires its own subnet, for this reason hello subnet created for hello Application Gateway is smaller than hello VNET address space.</span></span> <span data-ttu-id="9ad4f-166">Dzięki temu innych zasobów, w tym, ale tooweb innymi serwerami toobe skonfigurowane w hello samo sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-166">This allows for other resources, including but not limited tooweb servers toobe configured in hello same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="9ad4f-167">Krok 1</span><span class="sxs-lookup"><span data-stu-id="9ad4f-167">Step 1</span></span>

<span data-ttu-id="9ad4f-168">Przypisz zakres adresów hello 10.0.0.0/24 toocreate zmiennej toobe używane podsieci toohello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-168">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toocreate a virtual network.</span></span>  <span data-ttu-id="9ad4f-169">Spowoduje to utworzenie obiektu konfiguracji podsieci powitania dla bramy aplikacji, która jest używana w następnym przykładzie hello hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-169">This creates hello subnet configuration object for hello Application Gateway, which is used in hello next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="9ad4f-170">Krok 2</span><span class="sxs-lookup"><span data-stu-id="9ad4f-170">Step 2</span></span>

<span data-ttu-id="9ad4f-171">Tworzenie sieci wirtualnej o nazwie **appgwvnet** w grupie zasobów **zarządcy zasobów appgw** dla regionu zachodnie stany USA hello pomocą hello 10.0.0.0/16 prefiks podsieci 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-171">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="9ad4f-172">Na tym kończy się konfigurację hello hello sieć Wirtualną z jednej podsieci dla tooreside bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-172">This completes hello configuration of hello VNET with a single subnet for hello Application Gateway tooreside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="9ad4f-173">Krok 3</span><span class="sxs-lookup"><span data-stu-id="9ad4f-173">Step 3</span></span>

<span data-ttu-id="9ad4f-174">Przypisywanie zmienna podsieci hello hello kolejne kroki, to jest przekazywany toohello `New-AzureRMApplicationGateway` polecenia cmdlet w przyszłości kroku.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-174">Assign hello subnet variable for hello next steps, this is passed toohello `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="9ad4f-175">Utwórz publiczny adres IP dla konfiguracji frontonu hello</span><span class="sxs-lookup"><span data-stu-id="9ad4f-175">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="9ad4f-176">Utwórz zasób publicznego adresu IP **publicIP01** w grupie zasobów **zarządcy zasobów appgw** hello regionu zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-176">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="9ad4f-177">Brama aplikacji można użyć publicznego adresu IP, wewnętrzny adres IP lub obu żądań tooreceive Równoważenie obciążenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-177">Application Gateway can use a public IP address, internal IP address or both tooreceive requests for load balancing.</span></span>  <span data-ttu-id="9ad4f-178">W tym przykładzie używany jest tylko publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-178">This example only uses a public IP address.</span></span> <span data-ttu-id="9ad4f-179">W hello poniższy przykład Brak nazwy DNS jest skonfigurowany do tworzenia hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-179">In hello following example, no DNS name is configured for creating hello Public IP address.</span></span>  <span data-ttu-id="9ad4f-180">Usługa Application Gateway nie obsługuje niestandardowych nazw DNS dla publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-180">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="9ad4f-181">Jeśli nazwy niestandardowego jest wymagany do hello publiczny punkt końcowy, rekord CNAME powinny być tworzone nazwy DNS są generowane automatycznie toohello toopoint hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-181">If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="9ad4f-182">Adres IP jest przypisany toohello bramy aplikacji, po uruchomieniu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-182">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="9ad4f-183">Tworzenie konfiguracji bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="9ad4f-183">Create application gateway configuration</span></span>

<span data-ttu-id="9ad4f-184">Wszystkie elementy konfiguracji należy skonfigurować przed utworzeniem bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-184">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="9ad4f-185">Witaj następujące kroki tworzenia hello elementy konfiguracji, które są potrzebne dla zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-185">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="9ad4f-186">Krok 1</span><span class="sxs-lookup"><span data-stu-id="9ad4f-186">Step 1</span></span>

<span data-ttu-id="9ad4f-187">Utwórz konfigurację adresu IP bramy aplikacji o nazwie **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-187">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="9ad4f-188">Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci hello skonfigurowane i tras adresów IP toohello ruchu sieciowego w puli adresów IP zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-188">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="9ad4f-189">Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-189">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="9ad4f-190">Krok 2</span><span class="sxs-lookup"><span data-stu-id="9ad4f-190">Step 2</span></span>

<span data-ttu-id="9ad4f-191">Skonfiguruj hello zaplecza puli adresów IP o nazwie **pool01** i **pool2** z adresami IP **pool1** i **pool2**.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-191">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="9ad4f-192">Te adresy IP są adresami IP hello hello zasobów, które prowadzą hosting toobe aplikacji sieci web hello chronione przez bramę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-192">These IP addresses are hello IP addresses of hello resources that are hosting hello web application toobe protected by hello application gateway.</span></span> <span data-ttu-id="9ad4f-193">Tych elementów członkowskich puli wewnętrznej bazy danych są wszystkie zatwierdzone toobe dobrej kondycji przez sond sond podstawowego lub niestandardowego sondy.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-193">These backend pool members are all validated toobe healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="9ad4f-194">Ruch jest następnie przekierowywany toothem podczas żądania wejścia hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-194">Traffic is then routed toothem when requests come into hello application gateway.</span></span> <span data-ttu-id="9ad4f-195">Pul zaplecza mogą być używane przez wiele reguł w ramach bramy aplikacji hello, co oznacza jednej puli wewnętrznej bazy danych można użyć dla wielu aplikacji sieci web, które znajdują się na powitania sam hosta.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-195">Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="9ad4f-196">W tym przykładzie istnieją dwie pule zaplecza tooroute ruchu w sieci na podstawie hello ścieżki adresu URL.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-196">In this example, there are two back-end pools tooroute network traffic based on hello URL path.</span></span> <span data-ttu-id="9ad4f-197">Jedna pula odbiera ruch ze ścieżki adresu URL „/video”, a druga pula odbiera ruch ze ścieżki „/image”.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-197">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="9ad4f-198">Zastąp hello poprzedzających tooadd adresy IP własne punkty końcowe adresu IP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-198">Replace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="9ad4f-199">Krok 3</span><span class="sxs-lookup"><span data-stu-id="9ad4f-199">Step 3</span></span>

<span data-ttu-id="9ad4f-200">Skonfiguruj ustawienia bramy aplikacji **poolsetting01** i **poolsetting02** hello równoważeniem obciążenia ruchu sieciowego w puli zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-200">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="9ad4f-201">W tym przykładzie możesz skonfigurować ustawienia innej puli zaplecza hello pul zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-201">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="9ad4f-202">Każda pula zaplecza może mieć własne ustawienia puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-202">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="9ad4f-203">Ustawienia HTTP zaplecza są używane przez członków puli zaplecza poprawne toohello reguły tooroute ruchu.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-203">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="9ad4f-204">Określa hello protokół i port, który jest używany podczas wysyłania ruchu członków puli zaplecza toohello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-204">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="9ad4f-205">Ustawienia HTTP zaplecza hello również ustala oparte na pliku cookie sesji.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-205">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="9ad4f-206">U możliwia koligacji na podstawie plików cookie sesji wysyła toohello ruch tego samego wewnętrznej bazy danych jako poprzedniego żądania dla każdego pakietu.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-206">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="9ad4f-207">Krok 4</span><span class="sxs-lookup"><span data-stu-id="9ad4f-207">Step 4</span></span>

<span data-ttu-id="9ad4f-208">Skonfiguruj IP frontonu hello publicznego adresu IP punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-208">Configure hello front-end IP with public IP endpoint.</span></span> <span data-ttu-id="9ad4f-209">obiekt konfiguracji IP frontonu Hello służy hello toorelate odbiornika na zewnątrz, skierowane do adresu IP z hello odbiornika.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-209">hello front-end IP configuration object is used by a listener toorelate hello outward facing IP address with hello listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="9ad4f-210">Krok 5</span><span class="sxs-lookup"><span data-stu-id="9ad4f-210">Step 5</span></span>

<span data-ttu-id="9ad4f-211">Skonfiguruj hello portów frontonu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-211">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="9ad4f-212">obiekt konfiguracji portów frontonu Hello jest używany przez toodefine odbiornika, port bramy aplikacji hello nasłuchuje ruchu na powitania odbiornika.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-212">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="9ad4f-213">Krok 6</span><span class="sxs-lookup"><span data-stu-id="9ad4f-213">Step 6</span></span>

<span data-ttu-id="9ad4f-214">Skonfiguruj odbiornik hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-214">Configure hello listener.</span></span> <span data-ttu-id="9ad4f-215">Ten krok obejmuje skonfigurowanie odbiornika hello hello publicznego adresu IP i port używany tooreceive przychodzącego ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-215">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="9ad4f-216">Poniższy przykład Hello przyjmuje konfiguracji IP frontonu hello wcześniej skonfigurowane, Konfiguracja portów frontonu i protokołu (http lub https) i konfiguruje hello odbiornika.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-216">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="9ad4f-217">W tym przykładzie odbiornika hello nasłuchuje tooHTTP ruch na porcie 80 hello publiczny adres IP, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-217">In this example, hello listener listens tooHTTP traffic on port 80 on hello public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="9ad4f-218">Krok 7</span><span class="sxs-lookup"><span data-stu-id="9ad4f-218">Step 7</span></span>

<span data-ttu-id="9ad4f-219">Konfiguruj adres URL reguły ścieżki dla pul zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-219">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="9ad4f-220">Ten krok umożliwia skonfigurowanie ścieżki względnej hello używany przez bramę aplikacji i definiuje mapowanie hello między hello ścieżki adresu URL oraz pulę zaplecza hello jest przypisany toohandle hello przychodzący ruch.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-220">This step configures hello relative path used by application gateway and defines hello mapping between hello URL path and hello back-end pool that is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ad4f-221">Każda ścieżka musi rozpoczynać się od / i miejsce tylko hello "\*" jest dozwolone, znajduje się na końcu hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-221">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="9ad4f-222">Nieprawidłowa przykładów /xyz, /xyz* lub/xyz / *.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-222">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="9ad4f-223">Hello ciąg przekazywani toohello dopasowania ścieżki nie zawiera żadnego tekstu po hello najpierw "?" lub "#", a te znaki są niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-223">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="9ad4f-224">Witaj poniższy przykład tworzy dwie reguły: jeden dla "/ obrazu /" ścieżkę routingu ruchu tooback-end "pool1" a innym dla ścieżki "/ wideo /" routingu ruchu tooback-end "pool2."</span><span class="sxs-lookup"><span data-stu-id="9ad4f-224">hello following example creates two rules: one for "/image/" path routing traffic tooback-end "pool1" and another one for "/video/" path routing traffic tooback-end "pool2."</span></span> <span data-ttu-id="9ad4f-225">Te reguły Sprawdź, czy ruchu dla każdego zestawu adresów URL jest kierowany toohello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-225">These rules ensure that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="9ad4f-226">Na przykład http://contoso.com/image/figure1.jpg przechodzi toopool1 i http://contoso.com/video/example.mp4 przechodzi toopool2.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-226">For example, http://contoso.com/image/figure1.jpg goes toopool1 and http://contoso.com/video/example.mp4 goes toopool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="9ad4f-227">Jeśli ścieżka hello nie odpowiada żadnemu z reguły ścieżki wstępnie zdefiniowane hello, hello reguły ścieżki mapy konfiguracji konfiguruje również domyślna pula adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-227">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="9ad4f-228">Na przykład http://contoso.com/shoppingcart/test.html przechodzi toopool1 określone jako hello domyślnej puli niedopasowane ruchu.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-228">For example, http://contoso.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="9ad4f-229">Krok 8</span><span class="sxs-lookup"><span data-stu-id="9ad4f-229">Step 8</span></span>

<span data-ttu-id="9ad4f-230">Utwórz ustawienie reguły.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-230">Create a rule setting.</span></span> <span data-ttu-id="9ad4f-231">Ten krok obejmuje skonfigurowanie hello aplikacji bramy toouse routingu adresów URL na podstawie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-231">This step configures hello application gateway toouse URL path-based routing.</span></span> <span data-ttu-id="9ad4f-232">Witaj `$urlPathMap` zmiennej zdefiniowanej w hello wcześniejszym kroku jest teraz używane toocreate hello na podstawie ścieżki reguły.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-232">hello `$urlPathMap` variable defined in hello earlier step is now used toocreate hello path-based rule.</span></span> <span data-ttu-id="9ad4f-233">W tym kroku reguły hello powiązane z odbiornika i mapowanie ścieżki adresu url hello utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-233">In this step, we associate hello rule with a listener and hello url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="9ad4f-234">Krok 9</span><span class="sxs-lookup"><span data-stu-id="9ad4f-234">Step 9</span></span>

<span data-ttu-id="9ad4f-235">Konfigurowanie hello liczby wystąpień i rozmiaru bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-235">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="9ad4f-236">Utwórz bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="9ad4f-236">Create Application Gateway</span></span>

<span data-ttu-id="9ad4f-237">Utwórz bramę aplikacji ze wszystkimi obiektami konfiguracji z hello w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-237">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="9ad4f-238">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="9ad4f-238">Get application gateway DNS name</span></span>

<span data-ttu-id="9ad4f-239">Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-239">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="9ad4f-240">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-240">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="9ad4f-241">Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-241">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="9ad4f-242">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9ad4f-242">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="9ad4f-243">tooconfigure hello frontonu rekordu IP CNAME Pobieranie szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-243">tooconfigure hello frontend IP CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="9ad4f-244">Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-244">hello application gateway's DNS name should be used toocreate a CNAME record.</span></span> <span data-ttu-id="9ad4f-245">Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ad4f-245">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9ad4f-246">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9ad4f-246">Next steps</span></span>

<span data-ttu-id="9ad4f-247">Jeśli toolearn odciążanie protokołu Secure Sockets Layer (SSL), zobacz [skonfigurować bramę aplikacji dla odciążania SSL](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9ad4f-247">If you want toolearn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>

