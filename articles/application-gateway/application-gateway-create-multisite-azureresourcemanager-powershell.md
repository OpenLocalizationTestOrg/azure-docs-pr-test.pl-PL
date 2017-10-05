---
title: "Utwórz bramę aplikacji dla wielu witryn | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje dotyczące tworzenia, konfigurowania bramy aplikacji Azure obsługi wielu aplikacji sieci web na tej samej bramy."
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
ms.openlocfilehash: d42efa7d359f5c87c14afbfd138328b37c8ae6c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="fca9d-103">Utwórz bramę aplikacji do obsługi wielu aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="fca9d-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fca9d-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fca9d-104">Azure portal</span></span>](application-gateway-create-multisite-portal.md)
> * [<span data-ttu-id="fca9d-105">Azure Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="fca9d-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="fca9d-106">Obsługujący wiele lokacji umożliwia wdrożenie więcej niż jednej aplikacji sieci web na tej samej bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="fca9d-107">Opiera się na obecność nagłówek hosta w przychodzące żądanie HTTP, aby określić, które odbiornika będzie odbierać dane.</span><span class="sxs-lookup"><span data-stu-id="fca9d-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="fca9d-108">Odbiornik następnie kieruje ruch do puli zaplecza odpowiednie zgodnie z konfiguracją w definicji reguły bramy.</span><span class="sxs-lookup"><span data-stu-id="fca9d-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="fca9d-109">Brama aplikacji w aplikacji sieci web z włączonym protokołem SSL, opiera się rozszerzenia oznaczenia nazwy serwera (SNI), aby wybrać poprawny odbiornika dla ruchu w sieci web.</span><span class="sxs-lookup"><span data-stu-id="fca9d-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="fca9d-110">Zazwyczaj do obsługi wielu lokacji jest używane w celu zrównoważenia obciążenia żądaniami dla domen z innej witryny sieci web do innego serwera zaplecza pul.</span><span class="sxs-lookup"><span data-stu-id="fca9d-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="fca9d-111">Podobnie wielu domen podrzędnych tej samej domeny katalogu głównego może być hostowana na tę samą bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="fca9d-112">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="fca9d-112">Scenario</span></span>

<span data-ttu-id="fca9d-113">W poniższym przykładzie brama aplikacji jest obsługę ruchu dla domeny contoso.com i fabrikam.com z dwóch pul serwerów zaplecza: contoso puli serwerów i puli serwerów firmy fabrikam.</span><span class="sxs-lookup"><span data-stu-id="fca9d-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="fca9d-114">Podobnych konfiguracji może posłużyć do hosta poddomen, takich jak app.contoso.com i blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="fca9d-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="fca9d-116">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="fca9d-116">Before you begin</span></span>

1. <span data-ttu-id="fca9d-117">Zainstaluj najnowszą wersję poleceń cmdlet programu Azure PowerShell za pomocą Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fca9d-117">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="fca9d-118">Najnowszą wersję można pobrać i zainstalować z sekcji **Windows PowerShell** strony [Pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fca9d-118">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="fca9d-119">Musi istnieć serwerów dodanych do puli zaplecza, aby użyć bramy aplikacji lub ich punkty końcowe utworzone w sieci wirtualnej w osobnej podsieci lub publicznego adresu IP/VIP przypisane.</span><span class="sxs-lookup"><span data-stu-id="fca9d-119">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="fca9d-120">Wymagania</span><span class="sxs-lookup"><span data-stu-id="fca9d-120">Requirements</span></span>

* <span data-ttu-id="fca9d-121">**Pula serwerów zaplecza:** lista adresów IP serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="fca9d-121">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="fca9d-122">Adresy IP na liście powinny należeć do podsieci sieci wirtualnej lub być publicznymi bądź wirtualnymi adresami IP.</span><span class="sxs-lookup"><span data-stu-id="fca9d-122">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="fca9d-123">Można także nazwę FQDN.</span><span class="sxs-lookup"><span data-stu-id="fca9d-123">FQDN can also be used.</span></span>
* <span data-ttu-id="fca9d-124">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="fca9d-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="fca9d-125">Te ustawienia są powiązane z pulą i są stosowane do wszystkich serwerów w tej puli.</span><span class="sxs-lookup"><span data-stu-id="fca9d-125">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="fca9d-126">**Port frontonu:** port publiczny, który jest otwierany w bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-126">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="fca9d-127">Ruch trafia do tego portu, a następnie jest przekierowywany do jednego z serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="fca9d-127">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="fca9d-128">**Odbiornik:** odbiornik ma port frontonu, protokół (Http lub Https, z uwzględnieniem wielkości liter) oraz nazwę certyfikatu SSL (w przypadku konfigurowania odciążania protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="fca9d-128">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="fca9d-129">Dla bramy aplikacji obsługującej obejmujący wiele lokacji nazwy hosta i wskaźniki SNI są również został dodany.</span><span class="sxs-lookup"><span data-stu-id="fca9d-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="fca9d-130">**Reguła:** reguły wiąże odbiornika puli serwera zaplecza i definiuje puli serwera zaplecza, których ruch powinny być kierowane do, gdy trafienia w szczególności odbiornika.</span><span class="sxs-lookup"><span data-stu-id="fca9d-130">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="fca9d-131">Reguły są przetwarzane w kolejności, w jakiej występują, a ruch zostanie skierowany przez pierwszą regułę odpowiadającą niezależnie od szczegółowością.</span><span class="sxs-lookup"><span data-stu-id="fca9d-131">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="fca9d-132">Na przykład jeśli utworzono regułę przy użyciu odbiornika podstawowe i regułę przy użyciu odbiornika obejmujący wiele lokacji zarówno w tym samym porcie, reguły z wieloma lokacjami odbiornika musi być wymieniona przed regułę przy użyciu podstawowego odbiornika w kolejności reguły obejmujący wiele lokacji, aby działać zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="fca9d-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="fca9d-133">Tworzenie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="fca9d-133">Create an application gateway</span></span>

<span data-ttu-id="fca9d-134">Poniżej przedstawiono kroki potrzebne do utworzenia bramy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="fca9d-134">The following are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="fca9d-135">Utworzenie grupy zasobów dla usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fca9d-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="fca9d-136">Utwórz sieć wirtualną, podsieci i publicznego adresu IP dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-136">Create a virtual network, subnets, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="fca9d-137">Utworzenie obiektu konfiguracji bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="fca9d-138">Utworzenie zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="fca9d-139">Tworzenie grupy zasobów dla usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fca9d-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="fca9d-140">Upewnij się, że używasz najnowszej wersji programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fca9d-140">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="fca9d-141">Więcej informacji znajduje się w temacie [przy użyciu programu Windows PowerShell z usługą Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="fca9d-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="fca9d-142">Krok 1</span><span class="sxs-lookup"><span data-stu-id="fca9d-142">Step 1</span></span>

<span data-ttu-id="fca9d-143">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fca9d-143">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="fca9d-144">Zostanie wyświetlony monit o uwierzytelnienie przy użyciu własnych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="fca9d-144">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="fca9d-145">Krok 2</span><span class="sxs-lookup"><span data-stu-id="fca9d-145">Step 2</span></span>

<span data-ttu-id="fca9d-146">Sprawdź subskrypcje dostępne na koncie.</span><span class="sxs-lookup"><span data-stu-id="fca9d-146">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="fca9d-147">Krok 3</span><span class="sxs-lookup"><span data-stu-id="fca9d-147">Step 3</span></span>

<span data-ttu-id="fca9d-148">Wybierz subskrypcję platformy Azure do użycia.</span><span class="sxs-lookup"><span data-stu-id="fca9d-148">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="fca9d-149">Krok 4</span><span class="sxs-lookup"><span data-stu-id="fca9d-149">Step 4</span></span>

<span data-ttu-id="fca9d-150">Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="fca9d-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="fca9d-151">Alternatywnie można również utworzyć tagi dla grupy zasobów dla bramy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="fca9d-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="fca9d-152">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="fca9d-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="fca9d-153">Ta lokalizacja będzie używana jako domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="fca9d-153">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="fca9d-154">Upewnij się, że wszystkie polecenia, aby utworzyć bramę aplikacji używać tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="fca9d-154">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="fca9d-155">W powyższym przykładzie utworzono grupę zasobów o nazwie **zarządcy zasobów appgw** z lokalizacji **zachodnie stany USA**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-155">In the example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> <span data-ttu-id="fca9d-156">Jeśli musisz skonfigurować niestandardową sondę bramy aplikacji, zobacz artykuł [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md) (Tworzenie bramy aplikacji z sondami niestandardowymi przy użyciu programu PowerShell).</span><span class="sxs-lookup"><span data-stu-id="fca9d-156">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="fca9d-157">Odwiedź stronę [monitorowanie kondycji i badania niestandardowych](application-gateway-probe-overview.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-157">Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="fca9d-158">Tworzenie sieci wirtualnej i podsieci</span><span class="sxs-lookup"><span data-stu-id="fca9d-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="fca9d-159">W poniższym przykładzie pokazano, jak utworzyć sieć wirtualną przy użyciu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fca9d-159">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="fca9d-160">Dwie podsieci są tworzone w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="fca9d-160">Two subnets are created in this step.</span></span> <span data-ttu-id="fca9d-161">Jest pierwszą podsieć dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-161">The first subnet is for the application gateway itself.</span></span> <span data-ttu-id="fca9d-162">Brama aplikacji wymaga jego własnej podsieci, aby pomieścić jego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="fca9d-162">Application gateway requires its own subnet to hold its instances.</span></span> <span data-ttu-id="fca9d-163">Inne bramy aplikacji można wdrożyć w tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="fca9d-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="fca9d-164">Drugi podsieci służy do przechowywania serwerów wewnętrznej bazy danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-164">The second subnet is used to hold the application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="fca9d-165">Krok 1</span><span class="sxs-lookup"><span data-stu-id="fca9d-165">Step 1</span></span>

<span data-ttu-id="fca9d-166">Przypisz zakresu adresów 10.0.0.0/24 do zmiennej podsieci ma być używany do przechowywania bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to hold the application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="fca9d-167">Krok 2</span><span class="sxs-lookup"><span data-stu-id="fca9d-167">Step 2</span></span>

<span data-ttu-id="fca9d-168">Przypisz 10.0.1.0/24 zakres adresów do zmiennej podsieć2 służący do pul zaplecza.</span><span class="sxs-lookup"><span data-stu-id="fca9d-168">Assign the address range 10.0.1.0/24 to the subnet2 variable to be used for the backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="fca9d-169">Krok 3</span><span class="sxs-lookup"><span data-stu-id="fca9d-169">Step 3</span></span>

<span data-ttu-id="fca9d-170">Tworzenie sieci wirtualnej o nazwie **appgwvnet** w grupie zasobów **zarządcy zasobów appgw** dla regionu zachodnie stany USA, przy użyciu 10.0.0.0/16 prefiks z podsieci 10.0.0.0/24, a 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="fca9d-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="fca9d-171">Krok 4</span><span class="sxs-lookup"><span data-stu-id="fca9d-171">Step 4</span></span>

<span data-ttu-id="fca9d-172">Przypisanie zmiennej podsieci dalsze czynności, które tworzy bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-172">Assign a subnet variable for the next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="fca9d-173">Tworzenie publicznego adresu IP dla konfiguracji frontonu</span><span class="sxs-lookup"><span data-stu-id="fca9d-173">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="fca9d-174">Utwórz zasób publicznego adresu IP **publicIP01** w grupie zasobów **appgw-rg** dla regionu Zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="fca9d-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="fca9d-175">Adres IP jest przypisywany do bramy aplikacji w chwili uruchamiania usługi.</span><span class="sxs-lookup"><span data-stu-id="fca9d-175">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="fca9d-176">Tworzenie konfiguracji bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="fca9d-176">Create application gateway configuration</span></span>

<span data-ttu-id="fca9d-177">Musisz skonfigurować wszystkie elementy konfiguracji przed utworzeniem bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-177">You have to set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="fca9d-178">Poniższe kroki umożliwiają utworzenie elementów konfiguracji wymaganych w przypadku zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-178">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="fca9d-179">Krok 1</span><span class="sxs-lookup"><span data-stu-id="fca9d-179">Step 1</span></span>

<span data-ttu-id="fca9d-180">Utwórz konfigurację adresu IP bramy aplikacji o nazwie **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="fca9d-181">Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci skonfigurowane i kierować ruchem sieciowym na adresy IP w puli adresów IP zaplecza.</span><span class="sxs-lookup"><span data-stu-id="fca9d-181">When application gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="fca9d-182">Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.</span><span class="sxs-lookup"><span data-stu-id="fca9d-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="fca9d-183">Krok 2</span><span class="sxs-lookup"><span data-stu-id="fca9d-183">Step 2</span></span>

<span data-ttu-id="fca9d-184">Skonfiguruj pulę adresów IP zaplecza o nazwie **pool01** i **pool2** z adresami IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** dla **pool1** i **134.170.186.46**, **134.170.189.221**, **134.170.186.50** dla **pool2**.</span><span class="sxs-lookup"><span data-stu-id="fca9d-184">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="fca9d-185">W tym przykładzie istnieją dwie pule zaplecza, można kierować ruchem sieciowym w oparciu o żądanej witryny.</span><span class="sxs-lookup"><span data-stu-id="fca9d-185">In this example, there are two back-end pools to route network traffic based on the requested site.</span></span> <span data-ttu-id="fca9d-186">Jedna pula odbiera ruch z lokacji "contoso.com" i innych puli odbiera ruch z lokacji "fabrikam.com".</span><span class="sxs-lookup"><span data-stu-id="fca9d-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="fca9d-187">Należy zastąpić poprzedniego adresy IP, aby dodać własne punkty końcowe adresu IP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-187">You have to replace the preceding IP addresses to add your own application IP address endpoints.</span></span> <span data-ttu-id="fca9d-188">Zamiast adresów IP można również użyć publiczne adresy IP, nazwy FQDN lub wirtualna karta sieciowa dla wystąpień wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="fca9d-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="fca9d-189">Aby określić nazwy FQDN, zamiast adresów IP w programie PowerShell Użyj "-BackendFQDNs" parametru.</span><span class="sxs-lookup"><span data-stu-id="fca9d-189">To specify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="fca9d-190">Krok 3</span><span class="sxs-lookup"><span data-stu-id="fca9d-190">Step 3</span></span>

<span data-ttu-id="fca9d-191">Skonfiguruj ustawienia bramy aplikacji **poolsetting01** i **poolsetting02** dla ruchu sieciowego z równoważeniem obciążenia w puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="fca9d-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="fca9d-192">W tym przykładzie możesz skonfigurować ustawienia innej puli zaplecza dla pul zaplecza.</span><span class="sxs-lookup"><span data-stu-id="fca9d-192">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="fca9d-193">Każda pula zaplecza może mieć własne ustawienia puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="fca9d-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="fca9d-194">Krok 4</span><span class="sxs-lookup"><span data-stu-id="fca9d-194">Step 4</span></span>

<span data-ttu-id="fca9d-195">Skonfiguruj adres IP frontonu z punktem końcowym publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="fca9d-195">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="fca9d-196">Krok 5</span><span class="sxs-lookup"><span data-stu-id="fca9d-196">Step 5</span></span>

<span data-ttu-id="fca9d-197">Skonfiguruj port frontonu dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-197">Configure the front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="fca9d-198">Krok 6</span><span class="sxs-lookup"><span data-stu-id="fca9d-198">Step 6</span></span>

<span data-ttu-id="fca9d-199">Skonfiguruj dwa certyfikaty SSL dwie witryny sieci Web w się, że firma Microsoft będzie obsługiwany w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="fca9d-199">Configure two SSL certificates for the two websites we are going to support in this example.</span></span> <span data-ttu-id="fca9d-200">Jeden certyfikat jest przeznaczona ruchu contoso.com i drugą dla ruchu fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="fca9d-200">One certificate is for contoso.com traffic and the other is for fabrikam.com traffic.</span></span> <span data-ttu-id="fca9d-201">Te certyfikaty należy wystawił certyfikaty dla witryny sieci Web urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="fca9d-202">Certyfikaty z podpisem własnym są obsługiwane, ale nie jest zalecane dla ruchu w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="fca9d-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="fca9d-203">Krok 7</span><span class="sxs-lookup"><span data-stu-id="fca9d-203">Step 7</span></span>

<span data-ttu-id="fca9d-204">W tym przykładzie, należy skonfigurować dwa odbiorniki dla dwóch witryn sieci web.</span><span class="sxs-lookup"><span data-stu-id="fca9d-204">Configure two listeners for the two web sites in this example.</span></span> <span data-ttu-id="fca9d-205">Ten krok obejmuje skonfigurowanie odbiorników dla publicznego adresu IP, portu i hosta używany do odbierania ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="fca9d-205">This step configures the listeners for public IP address, port, and host used to receive incoming traffic.</span></span> <span data-ttu-id="fca9d-206">Parametr Nazwa hosta jest wymagana do obsługi wielu lokacji i należy ustawić odpowiednie witryny sieci Web, dla którego zostanie odebrany ruch.</span><span class="sxs-lookup"><span data-stu-id="fca9d-206">HostName parameter is required for multiple site support and should be set to the appropriate website for which the traffic is received.</span></span> <span data-ttu-id="fca9d-207">Element RequireServerNameIndication parametr powinien być ustawiony na wartość true dla witryn sieci Web, że wymagana jest obsługa protokołu SSL w przypadku wielu hostów.</span><span class="sxs-lookup"><span data-stu-id="fca9d-207">RequireServerNameIndication parameter should be set to true for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="fca9d-208">Jeśli wymagana jest obsługa protokołu SSL, należy określić certyfikat SSL, który służy do zabezpieczania ruchu dla tej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="fca9d-208">If SSL support is required, you also need to specify the SSL certificate that is used to secure traffic for that web application.</span></span> <span data-ttu-id="fca9d-209">Kombinacja konfiguracji IP frontonu, elementu FrontendPort oraz nazwa hosta musi być unikatowy w odbiorniku.</span><span class="sxs-lookup"><span data-stu-id="fca9d-209">The combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique to a listener.</span></span> <span data-ttu-id="fca9d-210">Każdy odbiornik może obsługiwać jeden certyfikat.</span><span class="sxs-lookup"><span data-stu-id="fca9d-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="fca9d-211">Krok 8</span><span class="sxs-lookup"><span data-stu-id="fca9d-211">Step 8</span></span>

<span data-ttu-id="fca9d-212">Utwórz dwa ustawienia reguł dla aplikacji sieci web dwóch w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="fca9d-212">Create two rule setting for the two web applications in this example.</span></span> <span data-ttu-id="fca9d-213">Reguła wiąże ze sobą odbiorników, pul zaplecza i ustawienia protokołu http.</span><span class="sxs-lookup"><span data-stu-id="fca9d-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="fca9d-214">Ten krok obejmuje skonfigurowanie bramy aplikacji należy używać podstawowe reguły routingu, jeden dla każdej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fca9d-214">This step configures the application gateway to use Basic routing rule, one for each website.</span></span> <span data-ttu-id="fca9d-215">Ruch do każdej witryny sieci Web jest odbierany przez jego skonfigurowany odbiornik i jest następnie przekierowywane do jego puli zaplecza skonfigurowane przy użyciu właściwości określony w elementu BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="fca9d-215">Traffic to each website is received by its configured listener, and is then directed to its configured backend pool, using the properties specified in the BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="fca9d-216">Krok 9</span><span class="sxs-lookup"><span data-stu-id="fca9d-216">Step 9</span></span>

<span data-ttu-id="fca9d-217">Skonfiguruj liczbę wystąpień i rozmiar bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-217">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="fca9d-218">Utwórz bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="fca9d-218">Create application gateway</span></span>

<span data-ttu-id="fca9d-219">Utwórz bramę aplikacji ze wszystkimi obiektami konfiguracji z powyższych kroków.</span><span class="sxs-lookup"><span data-stu-id="fca9d-219">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> <span data-ttu-id="fca9d-220">Inicjowanie obsługi bramy aplikacji jest operacją wymagającą dużo czasu i może zająć trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="fca9d-220">Application Gateway provisioning is a long running operation and may take some time to complete.</span></span>
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="fca9d-221">Pobieranie nazwy DNS bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="fca9d-221">Get application gateway DNS name</span></span>

<span data-ttu-id="fca9d-222">Po utworzeniu bramy następnym krokiem jest skonfigurowanie frontonu na potrzeby komunikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-222">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="fca9d-223">Gdy jest używany publiczny adres IP, brama aplikacji wymaga dynamicznie przypisywanej nazwy DNS, która nie jest przyjazna.</span><span class="sxs-lookup"><span data-stu-id="fca9d-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="fca9d-224">Aby upewnić się, że użytkownicy końcowi mogą trafić bramę aplikacji, można użyć rekordu CNAME w celu wskazania publicznego punktu końcowego bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-224">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="fca9d-225">[Konfigurowanie niestandardowej nazwy domeny dla platformy Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fca9d-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="fca9d-226">Aby to zrobić, pobierz szczegóły bramy aplikacji i skojarzony adres IP oraz nazwę DNS, używając elementu PublicIPAddress dołączonego do bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-226">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="fca9d-227">Nazwa DNS bramy aplikacji powinna zostać użyta w celu utworzenia rekordu CNAME, który wskazuje dwóm aplikacjom sieci Web tę nazwę DNS.</span><span class="sxs-lookup"><span data-stu-id="fca9d-227">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="fca9d-228">Korzystanie z rekordów A nie jest zalecane, ponieważ adres VIP może ulec zmianie po ponownym uruchomieniu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fca9d-228">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fca9d-229">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fca9d-229">Next steps</span></span>

<span data-ttu-id="fca9d-230">Dowiedz się, jak chronić witryny sieci Web z [Application Gateway - zapory aplikacji sieci Web](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="fca9d-230">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>

