---
title: "aaaCreate bramę aplikacji dla wielu witryn | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje toocreate, skonfiguruj bramę aplikacji Azure do obsługi wielu aplikacji sieci web na powitania tą samą bramą."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="9c7f2-103">Utwórz bramę aplikacji do obsługi wielu aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="9c7f2-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c7f2-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9c7f2-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="9c7f2-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c7f2-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="9c7f2-106">Obsługa wielu lokacji pozwala toodeploy więcej niż jednej aplikacji sieci web na powitania tej samej bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-106">Multiple site hosting allows you toodeploy more than one web application on hello same application gateway.</span></span> <span data-ttu-id="9c7f2-107">Opiera się na obecność nagłówek hosta w hello przychodzące żądanie HTTP, toodetermine odbiornika, które będzie odbierać dane.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-107">It relies on presence of host header in hello incoming HTTP request, toodetermine which listener would receive traffic.</span></span> <span data-ttu-id="9c7f2-108">odbiornik Hello następnie kieruje ruch puli zaplecza tooappropriate zgodnie z konfiguracją w definicji reguły hello hello bramy.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-108">hello listener then directs traffic tooappropriate backend pool as configured in hello rules definition of hello gateway.</span></span> <span data-ttu-id="9c7f2-109">W aplikacji sieci web z włączonym protokołem SSL bramy aplikacji polega na powitania oznaczenia nazwy serwera (SNI) rozszerzenia toochoose hello poprawne odbiornika dla ruchu w sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-109">In SSL enabled web applications, application gateway relies on hello Server Name Indication (SNI) extension toochoose hello correct listener for hello web traffic.</span></span> <span data-ttu-id="9c7f2-110">Zazwyczaj jest używane, do obsługi wielu lokacji tooload równoważenie żądań dla pul serwerów zaplecza toodifferent domeny innej witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-110">A common use for multiple site hosting is tooload balance requests for different web domains toodifferent back-end server pools.</span></span> <span data-ttu-id="9c7f2-111">Podobnie wielu poddomen powitalne tej samej domeny katalogu głównego może być również obsługiwane na hello tej samej bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-111">Similarly multiple subdomains of hello same root domain could also be hosted on hello same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="9c7f2-112">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="9c7f2-112">Scenario</span></span>

<span data-ttu-id="9c7f2-113">W hello poniższy przykład, bramy aplikacji jest obsługę ruchu dla domeny contoso.com i fabrikam.com z dwóch pul serwerów zaplecza: contoso puli serwerów i puli serwerów firmy fabrikam.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-113">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="9c7f2-114">Podobne instalacja może być poddomeny używane toohost jak app.contoso.com i blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-114">Similar setup could be used toohost subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="9c7f2-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="9c7f2-116">Before you begin</span></span>

1. <span data-ttu-id="9c7f2-117">Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-117">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="9c7f2-118">Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9c7f2-118">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="9c7f2-119">serwery Hello dodać bramę aplikacji hello toouse puli zaplecza toohello musi istnieć lub ich punkty końcowe utworzone w sieci wirtualnej hello w osobnej podsieci lub publicznego adresu IP/VIP przypisane.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-119">hello servers added toohello back-end pool toouse hello application gateway must exist or have their endpoints created either in hello virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="9c7f2-120">Wymagania</span><span class="sxs-lookup"><span data-stu-id="9c7f2-120">Requirements</span></span>

* <span data-ttu-id="9c7f2-121">**Pula serwerów zaplecza:** hello listę adresów IP serwerów wewnętrznych hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-121">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="9c7f2-122">wymienionych na liście adresów IP Hello albo powinny należeć toohello podsieć sieci wirtualnej lub powinny być publicznego adresu IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-122">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="9c7f2-123">Można także nazwę FQDN.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-123">FQDN can also be used.</span></span>
* <span data-ttu-id="9c7f2-124">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="9c7f2-125">Te ustawienia są wiązanej tooa puli i są stosowane tooall serwery w puli hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-125">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="9c7f2-126">**Port frontonu:** ten port jest port publiczny hello, która jest otwarta w bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-126">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="9c7f2-127">Ruch trafienia tego portu, a następnie pobiera przekierowanie tooone serwerami zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-127">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="9c7f2-128">**Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="9c7f2-128">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="9c7f2-129">Dla bramy aplikacji obsługującej obejmujący wiele lokacji nazwy hosta i wskaźniki SNI są również został dodany.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="9c7f2-130">**Reguła:** reguły hello wiąże hello odbiornika, hello puli serwerów zaplecza i określa, jaki ruch hello puli serwera zaplecza ukierunkowanej toowhen trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-130">**Rule:** hello rule binds hello listener, hello back-end server pool, and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="9c7f2-131">Reguły są przetwarzane w kolejności hello, są one wyświetlane, a ruch zostanie skierowany za pośrednictwem hello pierwszą regułę odpowiadającą niezależnie od szczegółowością.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-131">Rules are processed in hello order they are listed, and traffic will be directed via hello first rule that matches regardless of specificity.</span></span> <span data-ttu-id="9c7f2-132">Na przykład jeśli masz przy użyciu odbiornika podstawowe reguły i zasady przy użyciu odbiornika obejmujący wiele lokacji zarówno na powitania sam port hello reguły z hello obejmujący wiele lokacji odbiornika musi być wymienione przed reguły hello przy hello odbiornika podstawowych, aby hello toofunction reguły obejmujący wiele lokacji jako Oczekiwano.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on hello same port, hello rule with hello multi-site listener must be listed before hello rule with hello basic listener in order for hello multi-site rule toofunction as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="9c7f2-133">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="9c7f2-133">Create an application gateway</span></span>

<span data-ttu-id="9c7f2-134">następujące Hello są wymagane czynności hello toocreate bramę aplikacji:</span><span class="sxs-lookup"><span data-stu-id="9c7f2-134">hello following are hello steps needed toocreate an application gateway:</span></span>

1. <span data-ttu-id="9c7f2-135">Utworzenie grupy zasobów dla usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="9c7f2-136">Utwórz sieć wirtualną, podsieci i publicznego adresu IP dla bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-136">Create a virtual network, subnets, and public IP for hello application gateway.</span></span>
3. <span data-ttu-id="9c7f2-137">Utworzenie obiektu konfiguracji bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="9c7f2-138">Utworzenie zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="9c7f2-139">Tworzenie grupy zasobów dla usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9c7f2-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="9c7f2-140">Upewnij się, że używasz najnowszej wersji programu Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-140">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="9c7f2-141">Więcej informacji znajduje się w temacie [przy użyciu programu Windows PowerShell z usługą Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9c7f2-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="9c7f2-142">Krok 1</span><span class="sxs-lookup"><span data-stu-id="9c7f2-142">Step 1</span></span>

<span data-ttu-id="9c7f2-143">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="9c7f2-143">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="9c7f2-144">Jesteś zostanie wyświetlony monit o tooauthenticate przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-144">You are prompted tooauthenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="9c7f2-145">Krok 2</span><span class="sxs-lookup"><span data-stu-id="9c7f2-145">Step 2</span></span>

<span data-ttu-id="9c7f2-146">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-146">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="9c7f2-147">Krok 3</span><span class="sxs-lookup"><span data-stu-id="9c7f2-147">Step 3</span></span>

<span data-ttu-id="9c7f2-148">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-148">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="9c7f2-149">Krok 4</span><span class="sxs-lookup"><span data-stu-id="9c7f2-149">Step 4</span></span>

<span data-ttu-id="9c7f2-150">Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="9c7f2-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="9c7f2-151">Alternatywnie można również utworzyć tagi dla grupy zasobów dla bramy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="9c7f2-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="9c7f2-152">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="9c7f2-153">Ta lokalizacja jest używana jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-153">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="9c7f2-154">Upewnij się, że hello Użyj bramy aplikacji wszystkie polecenia toocreate tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-154">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="9c7f2-155">W powyższym przykładzie hello, utworzyliśmy grupę zasobów o nazwie **zarządcy zasobów appgw** z lokalizacji **zachodnie stany USA**.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-155">In hello example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="9c7f2-156">Jeśli potrzebujesz tooconfigure sondowania niestandardowych dla bramy aplikacji, zobacz [Utwórz bramę aplikacji z niestandardowego sond przy użyciu programu PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9c7f2-156">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="9c7f2-157">Odwiedź stronę [monitorowanie kondycji i badania niestandardowych](application-gateway-probe-overview.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="9c7f2-158">Tworzenie sieci wirtualnej i podsieci</span><span class="sxs-lookup"><span data-stu-id="9c7f2-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="9c7f2-159">powitania po przykładzie pokazano, jak toocreate sieci wirtualnej za pomocą Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-159">hello following example shows how toocreate a virtual network by using Resource Manager.</span></span> <span data-ttu-id="9c7f2-160">Dwie podsieci są tworzone w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-160">Two subnets are created in this step.</span></span> <span data-ttu-id="9c7f2-161">jest Hello pierwszej podsieci bramy aplikacji hello samej siebie.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-161">hello first subnet is for hello application gateway itself.</span></span> <span data-ttu-id="9c7f2-162">Brama aplikacji wymaga własnego toohold podsieci jego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-162">Application gateway requires its own subnet toohold its instances.</span></span> <span data-ttu-id="9c7f2-163">Inne bramy aplikacji można wdrożyć w tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="9c7f2-164">Witaj drugiej podsieci jest serwerów wewnętrznej bazy danych aplikacji hello toohold używane.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-164">hello second subnet is used toohold hello application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="9c7f2-165">Krok 1</span><span class="sxs-lookup"><span data-stu-id="9c7f2-165">Step 1</span></span>

<span data-ttu-id="9c7f2-166">Przypisz hello adres zakresu 10.0.0.0/24 toohello podsieci zmiennej toobe toohold używane hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-166">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used toohold hello application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="9c7f2-167">Krok 2</span><span class="sxs-lookup"><span data-stu-id="9c7f2-167">Step 2</span></span>

<span data-ttu-id="9c7f2-168">Przypisz hello adres zakresu 10.0.1.0/24 toohello podsieć2 zmiennej toobe używany dla pul zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-168">Assign hello address range 10.0.1.0/24 toohello subnet2 variable toobe used for hello backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="9c7f2-169">Krok 3</span><span class="sxs-lookup"><span data-stu-id="9c7f2-169">Step 3</span></span>

<span data-ttu-id="9c7f2-170">Tworzenie sieci wirtualnej o nazwie **appgwvnet** w grupie zasobów **zarządcy zasobów appgw** dla regionu zachodnie stany USA hello pomocą hello 10.0.0.0/16 prefiks podsieci 10.0.0.0/24, a 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="9c7f2-171">Krok 4</span><span class="sxs-lookup"><span data-stu-id="9c7f2-171">Step 4</span></span>

<span data-ttu-id="9c7f2-172">Przypisanie zmiennej podsieci hello dalsze czynności, które tworzy bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-172">Assign a subnet variable for hello next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="9c7f2-173">Utwórz publiczny adres IP dla konfiguracji frontonu hello</span><span class="sxs-lookup"><span data-stu-id="9c7f2-173">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="9c7f2-174">Utwórz zasób publicznego adresu IP **publicIP01** w grupie zasobów **zarządcy zasobów appgw** hello regionu zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="9c7f2-175">Adres IP jest przypisany toohello bramy aplikacji, po uruchomieniu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-175">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="9c7f2-176">Tworzenie konfiguracji bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="9c7f2-176">Create application gateway configuration</span></span>

<span data-ttu-id="9c7f2-177">Przed utworzeniem bramy aplikacji hello jest ma tooset wszystkie elementy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-177">You have tooset up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="9c7f2-178">Witaj następujące kroki tworzenia hello elementy konfiguracji, które są potrzebne dla zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-178">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="9c7f2-179">Krok 1</span><span class="sxs-lookup"><span data-stu-id="9c7f2-179">Step 1</span></span>

<span data-ttu-id="9c7f2-180">Utwórz konfigurację adresu IP bramy aplikacji o nazwie **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="9c7f2-181">Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci hello skonfigurowane i tras adresów IP toohello ruchu sieciowego w puli adresów IP zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-181">When application gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="9c7f2-182">Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="9c7f2-183">Krok 2</span><span class="sxs-lookup"><span data-stu-id="9c7f2-183">Step 2</span></span>

<span data-ttu-id="9c7f2-184">Skonfiguruj hello zaplecza puli adresów IP o nazwie **pool01** i **pool2** z adresami IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** dla **pool1** i **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  dla **pool2**.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-184">Configure hello back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="9c7f2-185">W tym przykładzie istnieją dwie pule zaplecza tooroute ruchu w sieci oparte na powitania żądanej witryny.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-185">In this example, there are two back-end pools tooroute network traffic based on hello requested site.</span></span> <span data-ttu-id="9c7f2-186">Jedna pula odbiera ruch z lokacji "contoso.com" i innych puli odbiera ruch z lokacji "fabrikam.com".</span><span class="sxs-lookup"><span data-stu-id="9c7f2-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="9c7f2-187">Masz hello tooreplace poprzedzających tooadd adresy IP własne punkty końcowe adresu IP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-187">You have tooreplace hello preceding IP addresses tooadd your own application IP address endpoints.</span></span> <span data-ttu-id="9c7f2-188">Zamiast adresów IP można również użyć publiczne adresy IP, nazwy FQDN lub wirtualna karta sieciowa dla wystąpień wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="9c7f2-189">toospecify nazw FQDN, zamiast adresów IP w programie PowerShell Użyj "-BackendFQDNs" parametru.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-189">toospecify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="9c7f2-190">Krok 3</span><span class="sxs-lookup"><span data-stu-id="9c7f2-190">Step 3</span></span>

<span data-ttu-id="9c7f2-191">Skonfiguruj ustawienia bramy aplikacji **poolsetting01** i **poolsetting02** hello równoważeniem obciążenia ruchu sieciowego w puli zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="9c7f2-192">W tym przykładzie możesz skonfigurować ustawienia innej puli zaplecza hello pul zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-192">In this example, you configure different back-end pool settings for hello back-end pools.</span></span> <span data-ttu-id="9c7f2-193">Każda pula zaplecza może mieć własne ustawienia puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="9c7f2-194">Krok 4</span><span class="sxs-lookup"><span data-stu-id="9c7f2-194">Step 4</span></span>

<span data-ttu-id="9c7f2-195">Skonfiguruj IP frontonu hello publicznego adresu IP punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-195">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="9c7f2-196">Krok 5</span><span class="sxs-lookup"><span data-stu-id="9c7f2-196">Step 5</span></span>

<span data-ttu-id="9c7f2-197">Skonfiguruj hello portów frontonu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-197">Configure hello front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="9c7f2-198">Krok 6</span><span class="sxs-lookup"><span data-stu-id="9c7f2-198">Step 6</span></span>

<span data-ttu-id="9c7f2-199">Skonfiguruj dwa certyfikaty SSL dla witryny sieci Web hello dwa zamierzamy toosupport w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-199">Configure two SSL certificates for hello two websites we are going toosupport in this example.</span></span> <span data-ttu-id="9c7f2-200">Jeden certyfikat jest przeznaczona ruchu contoso.com i hello innych fabrikam.com ruchu.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-200">One certificate is for contoso.com traffic and hello other is for fabrikam.com traffic.</span></span> <span data-ttu-id="9c7f2-201">Te certyfikaty należy wystawił certyfikaty dla witryny sieci Web urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="9c7f2-202">Certyfikaty z podpisem własnym są obsługiwane, ale nie jest zalecane dla ruchu w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="9c7f2-203">Krok 7</span><span class="sxs-lookup"><span data-stu-id="9c7f2-203">Step 7</span></span>

<span data-ttu-id="9c7f2-204">W tym przykładzie, należy skonfigurować dwa odbiorniki dla Witaj dwie witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-204">Configure two listeners for hello two web sites in this example.</span></span> <span data-ttu-id="9c7f2-205">Ten krok obejmuje skonfigurowanie hello odbiorników dla publicznego adresu IP, portu i hosta tooreceive ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-205">This step configures hello listeners for public IP address, port, and host used tooreceive incoming traffic.</span></span> <span data-ttu-id="9c7f2-206">Parametr nazwy hosta należy zestaw toohello odpowiedniej witryny sieci Web dla których hello ruch jest odbierany i jest wymagana do obsługi wielu lokacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-206">HostName parameter is required for multiple site support and should be set toohello appropriate website for which hello traffic is received.</span></span> <span data-ttu-id="9c7f2-207">Element RequireServerNameIndication parametr należy ustawić tootrue dla witryn sieci Web, że wymagana jest obsługa protokołu SSL w przypadku wielu hostów.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-207">RequireServerNameIndication parameter should be set tootrue for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="9c7f2-208">Jeśli wymagana jest obsługa protokołu SSL, należy również toospecify hello SSL certyfikatów czyli ruchu toosecure używanych dla tej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-208">If SSL support is required, you also need toospecify hello SSL certificate that is used toosecure traffic for that web application.</span></span> <span data-ttu-id="9c7f2-209">Kombinacja Hello konfiguracji IP frontonu, elementu FrontendPort oraz nazwa hosta musi być unikatowy tooa odbiornika.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-209">hello combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique tooa listener.</span></span> <span data-ttu-id="9c7f2-210">Każdy odbiornik może obsługiwać jeden certyfikat.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="9c7f2-211">Krok 8</span><span class="sxs-lookup"><span data-stu-id="9c7f2-211">Step 8</span></span>

<span data-ttu-id="9c7f2-212">Utwórz dwie reguły ustawienie dla Witaj dwie aplikacje sieci web w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-212">Create two rule setting for hello two web applications in this example.</span></span> <span data-ttu-id="9c7f2-213">Reguła wiąże ze sobą odbiorników, pul zaplecza i ustawienia protokołu http.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="9c7f2-214">Ten krok obejmuje skonfigurowanie hello aplikacji bramy toouse podstawowe reguły routingu, jeden dla każdej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-214">This step configures hello application gateway toouse Basic routing rule, one for each website.</span></span> <span data-ttu-id="9c7f2-215">Ruch tooeach witryny sieci Web jest odbierany przez jego skonfigurowany odbiornik i jest następnie przekierowywane tooits skonfigurować pulę zaplecza, za pomocą właściwości hello określone na powitania elementu BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-215">Traffic tooeach website is received by its configured listener, and is then directed tooits configured backend pool, using hello properties specified in hello BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="9c7f2-216">Krok 9</span><span class="sxs-lookup"><span data-stu-id="9c7f2-216">Step 9</span></span>

<span data-ttu-id="9c7f2-217">Konfigurowanie hello liczby wystąpień i rozmiaru bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-217">Configure hello number of instances and size for hello application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="9c7f2-218">Utwórz bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="9c7f2-218">Create application gateway</span></span>

<span data-ttu-id="9c7f2-219">Utwórz bramę aplikacji ze wszystkimi obiektami konfiguracji z hello w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-219">Create an application gateway with all configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="9c7f2-220">Inicjowanie obsługi bramy aplikacji jest operacją wymagającą dużo czasu i może potrwać kilka toocomplete czas.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-220">Application Gateway provisioning is a long running operation and may take some time toocomplete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="9c7f2-221">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="9c7f2-221">Get application gateway DNS name</span></span>

<span data-ttu-id="9c7f2-222">Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-222">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="9c7f2-223">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="9c7f2-224">Użytkownicy końcowi tooensure można trafień bramy aplikacji hello, rekord CNAME mogą być używane toopoint toohello publiczny punkt końcowy bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-224">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="9c7f2-225">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9c7f2-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="9c7f2-226">toodo tego pobierania szczegółów bramy aplikacji hello i skojarzonej z nią IP DNS nazwy przy użyciu bramy aplikacji hello publicznego adresu IP elementu toohello dołączone.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-226">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="9c7f2-227">Brama aplikacji Hello DNS nazwa powinna być używana toocreate rekord CNAME, która nazwa punktów Witaj dwie sieci web aplikacji toothis DNS.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-227">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="9c7f2-228">Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9c7f2-228">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9c7f2-229">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9c7f2-229">Next steps</span></span>

<span data-ttu-id="9c7f2-230">Dowiedz się, jak tooprotect witryny sieci Web z [Application Gateway - zapory aplikacji sieci Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9c7f2-230">Learn how tooprotect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

