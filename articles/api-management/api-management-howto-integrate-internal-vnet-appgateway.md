---
title: "toouse aaaHow Azure API Management w sieci wirtualnej z bramą aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i konfigurowanie usługi Azure API Management w wewnętrznej sieci wirtualnej z aplikacji bramy (WAF) jako serwera sieci Web"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="a8e89-103">Zintegrować zarządzanie interfejsami API w wewnętrznej sieci Wirtualnej z bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8e89-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="a8e89-104"><a name="overview"></a> — Omówienie</span><span class="sxs-lookup"><span data-stu-id="a8e89-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="a8e89-105">Witaj usługi Zarządzanie interfejsami API można skonfigurować w sieci wirtualnej w trybie wewnętrznej, dzięki czemu dostępny tylko w obrębie hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a8e89-105">hello API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within hello Virtual Network.</span></span> <span data-ttu-id="a8e89-106">Bramy aplikacji Azure to usługa PAAS, która udostępnia usługi równoważenia obciążenia warstwy 7.</span><span class="sxs-lookup"><span data-stu-id="a8e89-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="a8e89-107">Pełni rolę usługi proxy odwrotnie, a udostępnia między oferty zapory aplikacji sieci Web (WAF).</span><span class="sxs-lookup"><span data-stu-id="a8e89-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="a8e89-108">Zarządzanie interfejsami API udostępniane w wewnętrznej sieci Wirtualnej z frontonu bramy aplikacji hello łączenie umożliwia hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="a8e89-108">Combining API Management provisioned in an internal VNET with hello Application Gateway frontend enables hello following scenarios:</span></span>

* <span data-ttu-id="a8e89-109">Użyj hello sam zasobu interfejsu API zarządzania zużycia zarówno przez użytkowników wewnętrznych i zewnętrznych konsumentów.</span><span class="sxs-lookup"><span data-stu-id="a8e89-109">Use hello same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="a8e89-110">Użyj pojedynczego zasobu interfejsu API zarządzania i podzestawu interfejsów API zdefiniowanych w usłudze API Management dostępne dla użytkowników zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="a8e89-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="a8e89-111">Podaj sposób gotowe tooswitch dostępu tooAPI zarządzania z hello publicznej sieci Internet, włączać i wyłączać.</span><span class="sxs-lookup"><span data-stu-id="a8e89-111">Provide a turn-key way tooswitch access tooAPI Management from hello public Internet on and off.</span></span> 

##<span data-ttu-id="a8e89-112"><a name="scenario"></a> Scenariusza</span><span class="sxs-lookup"><span data-stu-id="a8e89-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="a8e89-113">W tym artykule opisano, jak toouse pojedynczego zarządzanie interfejsami API usługi dla użytkowników wewnętrznych i zewnętrznych, a następnie stał się działać jako pojedynczy frontonu dla obu lokalnego i w chmurze interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a8e89-113">This article will cover how toouse a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="a8e89-114">Widoczne będzie także sposób tooexpose tylko podzbiór swoje interfejsy API (w przykładzie hello są wyróżnione zielony) wykorzystania zewnętrznych za pomocą hello PathBasedRouting funkcje dostępne w programie Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="a8e89-114">You will also see how tooexpose only a subset of your APIs (in hello example they are highlighted in green) for External Consumption using hello PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="a8e89-115">W pierwszym przykładzie Instalatora hello swoje interfejsy API są zarządzane tylko z w ramach sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a8e89-115">In hello first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="a8e89-116">Konsumenci wewnętrzny (wyróżniane na kolor pomarańczowy) mogą uzyskiwać dostęp do wszystkich sieci wewnętrznych i zewnętrznych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a8e89-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="a8e89-117">Ruch nigdy nie trafia tooInternet dostarczenia wysokiej wydajności, za pomocą obwodów Express Route.</span><span class="sxs-lookup"><span data-stu-id="a8e89-117">Traffic never goes out tooInternet a high performance is delivered via Express Route circuits.</span></span>

![trasy adresu URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="a8e89-119"><a name="before-you-begin"></a> Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="a8e89-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="a8e89-120">Zainstaluj najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell, za pomocą hello Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a8e89-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="a8e89-121">Można pobrać i zainstalować najnowszą wersję hello z hello **programu Windows PowerShell** sekcji hello [pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a8e89-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="a8e89-122">Tworzenie sieci wirtualnej i Utwórz oddzielne podsieci dla interfejsu API zarządzania i bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8e89-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="a8e89-123">Jeśli planujesz toocreate niestandardowy serwer DNS dla sieci wirtualnej hello zrobić przed rozpoczęciem powitalne wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a8e89-123">If you intend toocreate a custom DNS server for hello Virtual Network, do so before starting hello deployment.</span></span> <span data-ttu-id="a8e89-124">Dobrze Sprawdź, czy działa przez zapewnienie im maszyny wirtualnej utworzonej w nową podsieć w sieci wirtualnej hello można rozwiązać i dostęp do wszystkich punktów końcowych usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e89-124">Double check it works by ensuring a virtual machine created in a new subnet in hello Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="a8e89-125">Co to jest wymagane toocreate integracja interfejsu API zarządzania i bramę aplikacji?</span><span class="sxs-lookup"><span data-stu-id="a8e89-125">What is required toocreate an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="a8e89-126">**Pula serwerów zaplecza:** to hello wewnętrznego wirtualnego adresu IP hello usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="a8e89-126">**Back-end server pool:** This is hello internal virtual IP address of hello API Management service.</span></span>
* <span data-ttu-id="a8e89-127">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="a8e89-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="a8e89-128">Te ustawienia są stosowane tooall serwery w puli hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-128">These settings are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="a8e89-129">**Port frontonu:** jest to port publiczny hello, która jest otwarta w bramie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-129">**Front-end port:** This is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="a8e89-130">Ruch naciśnięcie go pobiera tooone przekierowanych z hello serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="a8e89-130">Traffic hitting it gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="a8e89-131">**Odbiornik:** odbiornika hello ma port frontonu, protokół (Http lub Https, te wartości jest rozróżniana wielkość liter), a hello nazwa certyfikatu SSL (jeśli odciążania Konfigurowanie protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="a8e89-131">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="a8e89-132">**Reguła:** reguły hello wiąże pulę odbiornika tooa serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="a8e89-132">**Rule:** hello rule binds a listener tooa back-end server pool.</span></span>
* <span data-ttu-id="a8e89-133">**Niestandardowe sondy kondycji:** bramy aplikacji domyślnie używa toofigure sond na podstawie adresu IP limit serwerów, które w hello BackendAddressPool są aktywne.</span><span class="sxs-lookup"><span data-stu-id="a8e89-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes toofigure out which servers in hello BackendAddressPool are active.</span></span> <span data-ttu-id="a8e89-134">Hello usługi Zarządzanie interfejsami API tylko odpowiada toorequests, która ma nagłówek hosta poprawne hello, dlatego hello domyślnej sondy zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="a8e89-134">hello API Management service only responds toorequests which have hello correct host header, hence hello default probes fail.</span></span> <span data-ttu-id="a8e89-135">Sondy kondycji niestandardowych musi toobe zdefiniowane toohelp bramy aplikacji ustalić, czy działa usługa hello i należy przekazywać żądania.</span><span class="sxs-lookup"><span data-stu-id="a8e89-135">A custom health probe needs toobe defined toohelp application gateway determine that hello service is alive and it should forward requests.</span></span>
* <span data-ttu-id="a8e89-136">**Certyfikat domeny niestandardowej:** tooaccess API Management z hello internet należy toocreate mapowanie CNAME hostname toohello bramy aplikacji frontonu nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="a8e89-136">**Custom domain certificate:** tooaccess API Management from hello internet you need toocreate a CNAME mapping of its hostname toohello Application Gateway front-end DNS name.</span></span> <span data-ttu-id="a8e89-137">To zapewnia, że nagłówek hostname hello i tooApplication certyfikatu wysłanego bramy, który jest przesyłany dalej tooAPI zarządzania jest jeden APIM rozpoznać jako prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="a8e89-137">This ensures that hello hostname header and certificate sent tooApplication Gateway that is forwarded tooAPI Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="a8e89-138"><a name="overview-steps"></a> Kroków wymaganych do integracji interfejsu API zarządzania i bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8e89-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="a8e89-139">Utworzenie grupy zasobów dla usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a8e89-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="a8e89-140">Tworzenie sieci wirtualnej, podsieci i publicznego adresu IP dla bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-140">Create a Virtual Network, subnet, and public IP for hello Application Gateway.</span></span> <span data-ttu-id="a8e89-141">Utwórz inną podsieć dla interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="a8e89-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="a8e89-142">Tworzenie usługi Zarządzanie interfejsami API w podsieci sieci Wirtualnej hello utworzone powyżej i upewnij się, że używany jest tryb wewnętrzny hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-142">Create an API Management service inside hello VNET subnet created above and ensure you use hello Internal mode.</span></span>
4. <span data-ttu-id="a8e89-143">Instalator hello niestandardowej nazwy domeny w hello usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="a8e89-143">Setup hello custom domain name in hello API Management service.</span></span>
5. <span data-ttu-id="a8e89-144">Utwórz obiekt konfiguracji bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8e89-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="a8e89-145">Utwórz zasób aplikacji bramy.</span><span class="sxs-lookup"><span data-stu-id="a8e89-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="a8e89-146">Należy utworzyć rekord CNAME z hello publicznej nazwy DNS nazwy hosta hello bramy aplikacji toohello interfejsu API zarządzania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="a8e89-146">Create a CNAME from hello public DNS name of hello Application Gateway toohello API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="a8e89-147">Tworzenie grupy zasobów dla usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8e89-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="a8e89-148">Upewnij się, że używasz najnowszej wersji programu Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-148">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="a8e89-149">Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="a8e89-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="a8e89-150">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a8e89-150">Step 1</span></span>

<span data-ttu-id="a8e89-151">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="a8e89-151">Log in tooAzure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="a8e89-152">Uwierzytelnianie przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="a8e89-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="a8e89-153">Krok 2</span><span class="sxs-lookup"><span data-stu-id="a8e89-153">Step 2</span></span>

<span data-ttu-id="a8e89-154">Sprawdź subskrypcje hello hello konta i zaznacz go.</span><span class="sxs-lookup"><span data-stu-id="a8e89-154">Check hello subscriptions for hello account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="a8e89-155">Krok 3</span><span class="sxs-lookup"><span data-stu-id="a8e89-155">Step 3</span></span>

<span data-ttu-id="a8e89-156">Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="a8e89-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="a8e89-157">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="a8e89-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="a8e89-158">Służy to jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="a8e89-158">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="a8e89-159">Upewnij się, że hello Użyj bramy aplikacji wszystkie polecenia toocreate tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="a8e89-159">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a><span data-ttu-id="a8e89-160">Utwórz sieć wirtualną i podsieć bramy aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="a8e89-160">Create a Virtual Network and a subnet for hello application gateway</span></span>

<span data-ttu-id="a8e89-161">Witaj poniższy przykład pokazuje, jak toocreate sieci wirtualnych za pomocą funkcji hello Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="a8e89-161">hello following example shows how toocreate a Virtual Network using hello resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="a8e89-162">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a8e89-162">Step 1</span></span>

<span data-ttu-id="a8e89-163">Przypisz hello adres zakresu 10.0.0.0/24 toohello podsieci zmiennej toobe używana przez bramę aplikacji podczas tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a8e89-163">Assign hello address range 10.0.0.0/24 toohello subnet variable toobe used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="a8e89-164">Krok 2</span><span class="sxs-lookup"><span data-stu-id="a8e89-164">Step 2</span></span>

<span data-ttu-id="a8e89-165">Przypisz hello adres zakresu 10.0.1.0/24 toohello podsieci zmiennej toobe interfejsu API zarządzania używać podczas tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a8e89-165">Assign hello address range 10.0.1.0/24 toohello subnet variable toobe used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="a8e89-166">Krok 3</span><span class="sxs-lookup"><span data-stu-id="a8e89-166">Step 3</span></span>

<span data-ttu-id="a8e89-167">Tworzenie sieci wirtualnej o nazwie **appgwvnet** w grupie zasobów **apim-appGw-zarządcy zasobów** dla regionu zachodnie stany USA hello przy użyciu hello 10.0.0.0/16 prefiks podsieci 10.0.0.0/24 i 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="a8e89-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for hello West US region using hello prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="a8e89-168">Krok 4</span><span class="sxs-lookup"><span data-stu-id="a8e89-168">Step 4</span></span>

<span data-ttu-id="a8e89-169">Przypisanie zmiennej podsieci hello następne kroki</span><span class="sxs-lookup"><span data-stu-id="a8e89-169">Assign a subnet variable for hello next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="a8e89-170">Tworzenie usługi Zarządzanie interfejsami API w sieci Wirtualnej w trybie wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="a8e89-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="a8e89-171">Witaj poniższy przykład przedstawia toocreate usługi Zarządzanie interfejsami API w sieci Wirtualnej konfiguracji tylko wewnętrzny dostępu.</span><span class="sxs-lookup"><span data-stu-id="a8e89-171">hello following example shows how toocreate an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="a8e89-172">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a8e89-172">Step 1</span></span>
<span data-ttu-id="a8e89-173">Utwórz obiekt sieci wirtualnej interfejsu API zarządzania za pomocą podsieci hello $apimsubnetdata utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="a8e89-173">Create an API Management Virtual Network object using hello subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="a8e89-174">Krok 2</span><span class="sxs-lookup"><span data-stu-id="a8e89-174">Step 2</span></span>
<span data-ttu-id="a8e89-175">Tworzenie usługi Zarządzanie interfejsami API wewnątrz hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a8e89-175">Create an API Management service inside hello Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="a8e89-176">Po pomyślnym zainicjowaniu hello powyżej polecenia można znaleźć zbyt[tooaccess wewnętrzny usługi Zarządzanie interfejsami API sieci Wirtualnej wymagana konfiguracja DNS](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess go.</span><span class="sxs-lookup"><span data-stu-id="a8e89-176">After hello above command succeeds refer too[DNS Configuration required tooaccess internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="a8e89-177">Ustawienie niestandardowej nazwy domeny w usłudze API Management</span><span class="sxs-lookup"><span data-stu-id="a8e89-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="a8e89-178">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a8e89-178">Step 1</span></span>
<span data-ttu-id="a8e89-179">Przekaż hello certyfikat z kluczem prywatnym hello domeny.</span><span class="sxs-lookup"><span data-stu-id="a8e89-179">Upload hello certificate with private key for hello domain.</span></span> <span data-ttu-id="a8e89-180">W tym przykładzie będzie `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="a8e89-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="a8e89-181">Krok 2</span><span class="sxs-lookup"><span data-stu-id="a8e89-181">Step 2</span></span>
<span data-ttu-id="a8e89-182">Po przekazaniu plików certyfikatów hello utworzenia obiektu konfiguracji nazwę hosta dla serwera proxy hello z nazwą hosta z `api.contoso.net`, ponieważ zapewnia hello przykład certyfikatu urzędu hello `*.contoso.net` domeny.</span><span class="sxs-lookup"><span data-stu-id="a8e89-182">Once hello certificate is uploaded, create a hostname configuration object for hello proxy with a hostname of `api.contoso.net`, as hello example certificate provides authority for hello  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="a8e89-183">Utwórz publiczny adres IP dla konfiguracji frontonu hello</span><span class="sxs-lookup"><span data-stu-id="a8e89-183">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="a8e89-184">Utwórz zasób publicznego adresu IP **publicIP01** w grupie zasobów **apim-appGw-zarządcy zasobów** hello regionu zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="a8e89-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for hello West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="a8e89-185">Adres IP jest przypisany toohello bramy aplikacji, po uruchomieniu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-185">An IP address is assigned toohello application gateway when hello service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="a8e89-186">Tworzenie konfiguracji bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8e89-186">Create application gateway configuration</span></span>

<span data-ttu-id="a8e89-187">Wszystkie elementy konfiguracji należy skonfigurować przed utworzeniem bramy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-187">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="a8e89-188">Witaj następujące kroki tworzenia hello elementy konfiguracji, które są potrzebne dla zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8e89-188">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="a8e89-189">Krok 1</span><span class="sxs-lookup"><span data-stu-id="a8e89-189">Step 1</span></span>

<span data-ttu-id="a8e89-190">Utwórz konfigurację adresu IP bramy aplikacji o nazwie **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="a8e89-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="a8e89-191">Po uruchomieniu aplikacji bramy przejmuje adresu IP z podsieci hello skonfigurowane i tras adresów IP toohello ruchu sieciowego w puli adresów IP zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-191">When Application Gateway starts, it picks up an IP address from hello subnet configured and route network traffic toohello IP addresses in hello back-end IP pool.</span></span> <span data-ttu-id="a8e89-192">Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.</span><span class="sxs-lookup"><span data-stu-id="a8e89-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="a8e89-193">Krok 2</span><span class="sxs-lookup"><span data-stu-id="a8e89-193">Step 2</span></span>

<span data-ttu-id="a8e89-194">Skonfiguruj hello frontonu portu IP dla punktu końcowego hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="a8e89-194">Configure hello front-end IP port for hello public IP endpoint.</span></span> <span data-ttu-id="a8e89-195">Jest to port hello użytkownicy połączenie.</span><span class="sxs-lookup"><span data-stu-id="a8e89-195">This port is hello port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="a8e89-196">Krok 3</span><span class="sxs-lookup"><span data-stu-id="a8e89-196">Step 3</span></span>

<span data-ttu-id="a8e89-197">Skonfiguruj IP frontonu hello publicznego adresu IP punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="a8e89-197">Configure hello front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="a8e89-198">Krok 4</span><span class="sxs-lookup"><span data-stu-id="a8e89-198">Step 4</span></span>

<span data-ttu-id="a8e89-199">Skonfigurować certyfikat hello hello bramy aplikacji używane toodecrypt a zaszyfrowanie hello ruchu przechodzącego przez.</span><span class="sxs-lookup"><span data-stu-id="a8e89-199">Configure hello certificate for hello Application Gateway, used toodecrypt and re-encrypt hello traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="a8e89-200">Krok 5</span><span class="sxs-lookup"><span data-stu-id="a8e89-200">Step 5</span></span>

<span data-ttu-id="a8e89-201">Utwórz odbiornik HTTP hello na powitania bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8e89-201">Create hello HTTP listener for hello Application Gateway.</span></span> <span data-ttu-id="a8e89-202">Przypisywanie konfiguracji IP frontonu hello, port i tooit certyfikatu ssl.</span><span class="sxs-lookup"><span data-stu-id="a8e89-202">Assign hello front-end IP configuration, port, and ssl certificate tooit.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="a8e89-203">Krok 6</span><span class="sxs-lookup"><span data-stu-id="a8e89-203">Step 6</span></span>

<span data-ttu-id="a8e89-204">Tworzenie niestandardowych sondowania toohello usługi Zarządzanie interfejsami API `ContosoApi` punktu końcowego domeny serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="a8e89-204">Create a custom probe toohello API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="a8e89-205">Ścieżka Hello `/status-0123456789abcdef` jest domyślnego kondycji punktu końcowego hostowanych na wszystkie usługi Zarządzanie interfejsami API hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-205">hello path `/status-0123456789abcdef` is a default health endpoint hosted on all hello API Management services.</span></span> <span data-ttu-id="a8e89-206">Ustaw `api.contoso.net` jako toosecure hostname sondowania niestandardowych za pomocą certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="a8e89-206">Set `api.contoso.net` as a custom probe hostname toosecure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="a8e89-207">Witaj hostname `contosoapi.azure-api.net` jest nazwa hosta serwera proxy domyślne hello konfigurowane podczas usługi o nazwie `contosoapi` jest tworzony w publicznej Azure.</span><span class="sxs-lookup"><span data-stu-id="a8e89-207">hello hostname `contosoapi.azure-api.net` is hello default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="a8e89-208">Krok 7</span><span class="sxs-lookup"><span data-stu-id="a8e89-208">Step 7</span></span>

<span data-ttu-id="a8e89-209">Przekaż certyfikat hello toobe używane hello włączony protokół SSL zaplecza puli zasobów.</span><span class="sxs-lookup"><span data-stu-id="a8e89-209">Upload hello certificate toobe used on hello SSL-enabled backend pool resources.</span></span> <span data-ttu-id="a8e89-210">Jest to hello tego samego certyfikatu, które podano w powyższym kroku 4.</span><span class="sxs-lookup"><span data-stu-id="a8e89-210">This is hello same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a><span data-ttu-id="a8e89-211">Krok 8</span><span class="sxs-lookup"><span data-stu-id="a8e89-211">Step 8</span></span>

<span data-ttu-id="a8e89-212">Skonfiguruj ustawienia HTTP zaplecza hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8e89-212">Configure HTTP backend settings for hello Application Gateway.</span></span> <span data-ttu-id="a8e89-213">Dotyczy to również ustawienie limitu czasu, po którym są anulowane żądania wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a8e89-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="a8e89-214">Ta wartość jest inny niż limit czasu sondowania hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-214">This value is different from hello probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="a8e89-215">Krok 9</span><span class="sxs-lookup"><span data-stu-id="a8e89-215">Step 9</span></span>

<span data-ttu-id="a8e89-216">Skonfiguruj pulę adresów IP zaplecza, o nazwie **apimbackend** z wewnętrznego wirtualnego adresu IP hello adres hello usługi Zarządzanie interfejsami API utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="a8e89-216">Configure a back-end IP address pool named **apimbackend**  with hello internal virtual IP address of hello API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="a8e89-217">Krok 10</span><span class="sxs-lookup"><span data-stu-id="a8e89-217">Step 10</span></span>

<span data-ttu-id="a8e89-218">Tworzenie ustawień dla fikcyjnego zaplecza (nieistniejącego).</span><span class="sxs-lookup"><span data-stu-id="a8e89-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="a8e89-219">Ścieżki tooAPI żądań, które nie chcemy tooexpose z interfejsu API zarządzania za pośrednictwem bramy aplikacji będzie trafień tego wewnętrznej bazy danych i zwracać 404.</span><span class="sxs-lookup"><span data-stu-id="a8e89-219">Requests tooAPI paths that we do not want tooexpose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="a8e89-220">Skonfiguruj ustawienia HTTP zaplecza fikcyjny hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-220">Configure HTTP settings for hello dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="a8e89-221">Skonfiguruj fikcyjny wewnętrznej bazy danych **dummyBackendPool**, który wskazuje adres FQDN tooa **dummybackend.com**. Ten adres FQDN nie istnieje w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-221">Configure a dummy backend **dummyBackendPool**, which points tooa FQDN address **dummybackend.com**. This FQDN address does not exist in hello virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="a8e89-222">Utwórz regułę ustawienie tego hello bramy aplikacji użyje domyślnie wskazujący toohello nieistniejącą zaplecza **dummybackend.com** w hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a8e89-222">Create a rule setting that hello Application Gateway will use by default which points toohello non-existent backend **dummybackend.com** in hello Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="a8e89-223">Krok 11</span><span class="sxs-lookup"><span data-stu-id="a8e89-223">Step 11</span></span>

<span data-ttu-id="a8e89-224">Konfiguruj adres URL reguły ścieżki dla pul zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-224">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="a8e89-225">Umożliwia wybranie tylko niektóre hello interfejsy API z interfejsu API zarządzania jest udostępniany toohello publicznego.</span><span class="sxs-lookup"><span data-stu-id="a8e89-225">This enables selecting only some of hello APIs from API Management for being exposed toohello public.</span></span> <span data-ttu-id="a8e89-226">Na przykład, jeśli istnieją `Echo API` (/ echo /), `Calculator API` (/calc/) itd. Sprawdź tylko `Echo API` dostępny z Internetu).</span><span class="sxs-lookup"><span data-stu-id="a8e89-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="a8e89-227">Witaj poniższy przykład tworzy regułę prostego powitania "/ echo /" ścieżkę routingu ruchu toohello zaplecza "apimProxyBackendPool".</span><span class="sxs-lookup"><span data-stu-id="a8e89-227">hello following example creates a simple rule for hello "/echo/" path routing traffic toohello back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="a8e89-228">Jeśli ścieżka hello jest niezgodny hello ścieżki reguły chcemy tooenable z interfejsu API zarządzania, hello reguły ścieżki mapy konfiguracji konfiguruje również domyślną pulę adresów zaplecza o nazwie **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="a8e89-228">If hello path doesn't match hello path rules we want tooenable from API Management, hello rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="a8e89-229">Na przykład http://api.contoso.net/calc/ * prowadzi zbyt**dummyBackendPool** określone jako hello domyślna pula cofanie dopasowane ruchu.</span><span class="sxs-lookup"><span data-stu-id="a8e89-229">For example, http://api.contoso.net/calc/* goes too**dummyBackendPool** as it is defined as hello default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="a8e89-230">Hello powyżej kroku gwarantuje, który żąda tylko dla ścieżki hello "/ echo" są dozwolone przez hello bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a8e89-230">hello above step ensures that only requests for hello path "/echo" are allowed through hello Application Gateway.</span></span> <span data-ttu-id="a8e89-231">Tooother żądania, interfejsy API skonfigurowane w usłudze API Management spowoduje zgłoszenie błędów 404 z bramy aplikacji, gdy użytkowcy hello Internet.</span><span class="sxs-lookup"><span data-stu-id="a8e89-231">Requests tooother APIs configured in API Management will throw 404 errors from Application Gateway when accessed from hello Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="a8e89-232">Krok 12</span><span class="sxs-lookup"><span data-stu-id="a8e89-232">Step 12</span></span>

<span data-ttu-id="a8e89-233">Utwórz ustawienie reguły dla hello bramy aplikacji toouse routingu adresów URL na podstawie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="a8e89-233">Create a rule setting for hello Application Gateway toouse URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="a8e89-234">Krok 13</span><span class="sxs-lookup"><span data-stu-id="a8e89-234">Step 13</span></span>

<span data-ttu-id="a8e89-235">Skonfiguruj hello liczbę wystąpień i rozmiar hello Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="a8e89-235">Configure hello number of instances and size for hello Application Gateway.</span></span> <span data-ttu-id="a8e89-236">W tym miejscu używamy hello [SKU zapory aplikacji sieci Web](../application-gateway/application-gateway-webapplicationfirewall-overview.md) Aby zwiększyć bezpieczeństwo hello zasobu interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="a8e89-236">Here we are using hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of hello API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="a8e89-237">Krok 14</span><span class="sxs-lookup"><span data-stu-id="a8e89-237">Step 14</span></span>

<span data-ttu-id="a8e89-238">Skonfiguruj toobe zapory aplikacji sieci Web w trybie "Zapobiegania".</span><span class="sxs-lookup"><span data-stu-id="a8e89-238">Configure WAF toobe in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="a8e89-239">Utwórz bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8e89-239">Create Application Gateway</span></span>

<span data-ttu-id="a8e89-240">Utwórz bramę aplikacji na wszystkich obiektach konfiguracji hello hello w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="a8e89-240">Create an Application Gateway with all hello configuration objects from hello preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a><span data-ttu-id="a8e89-241">CNAME hello interfejsu API zarządzania serwera proxy hostname toohello publicznej nazwy DNS hello zasobu bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8e89-241">CNAME hello API Management proxy hostname toohello public DNS name of hello Application Gateway resource</span></span>

<span data-ttu-id="a8e89-242">Po utworzeniu bramy hello hello następnym krokiem jest tooconfigure hello frontonu dla komunikacji.</span><span class="sxs-lookup"><span data-stu-id="a8e89-242">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="a8e89-243">Korzystając z publicznym adresem IP, brama aplikacji wymaga przypisywany dynamicznie nazwy DNS, które nie mogą być łatwo toouse.</span><span class="sxs-lookup"><span data-stu-id="a8e89-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy toouse.</span></span> 

<span data-ttu-id="a8e89-244">Hello nazwa DNS bramy aplikacji powinny być używane toocreate rekord CNAME, który wskazuje nazwę hosta serwera proxy APIM hello (np. `api.contoso.net` w powyższych przykładach hello) toothis nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="a8e89-244">hello Application Gateway's DNS name should be used toocreate a CNAME record which points hello APIM proxy host name (e.g. `api.contoso.net` in hello examples above) toothis DNS name.</span></span> <span data-ttu-id="a8e89-245">tooconfigure hello frontonu rekordu IP CNAME pobierać szczegóły hello hello bramy aplikacji i jego skojarzonej nazwy IP DNS za pomocą hello publicznego adresu IP elementu.</span><span class="sxs-lookup"><span data-stu-id="a8e89-245">tooconfigure hello frontend IP CNAME record, retrieve hello details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element.</span></span> <span data-ttu-id="a8e89-246">Użycie Hello rekordów A nie jest zalecane, ponieważ hello wirtualne adresy IP mogą ulec zmianie po ponownym uruchomieniu bramy.</span><span class="sxs-lookup"><span data-stu-id="a8e89-246">hello use of A-records is not recommended since hello VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="a8e89-247"><a name="summary"></a> Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a8e89-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="a8e89-248">Skonfigurowane w sieci Wirtualnej platformy Azure API Management oferuje interfejs pojedyncza brama dla wszystkich skonfigurowanych interfejsów API, czy są one lokalnego hostowanej w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="a8e89-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in hello cloud.</span></span> <span data-ttu-id="a8e89-249">Integrowanie aplikacji bramy z interfejsu API zarządzania zapewnia elastyczność hello selektywne włączenie określonego dostępne na powitania Internet toobe interfejsów API, a także dostarczanie zapory aplikacji sieci Web jako wystąpienie interfejsu API zarządzania tooyour frontonu.</span><span class="sxs-lookup"><span data-stu-id="a8e89-249">Integrating Application Gateway with API Management provides hello flexibility of selectively enabling particular APIs toobe accessible on hello Internet, as well as providing a Web Application Firewall as a frontend tooyour API Management instance.</span></span>

##<span data-ttu-id="a8e89-250"><a name="next-steps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a8e89-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="a8e89-251">Dowiedz się więcej na temat bramy aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="a8e89-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="a8e89-252">Omówienie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8e89-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="a8e89-253">Zapora aplikacji sieci Web bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="a8e89-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="a8e89-254">Brama aplikacji przy użyciu routingu na podstawie ścieżki</span><span class="sxs-lookup"><span data-stu-id="a8e89-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="a8e89-255">Dowiedz się więcej o interfejsu API zarządzania i sieci wirtualnych</span><span class="sxs-lookup"><span data-stu-id="a8e89-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="a8e89-256">Za pomocą interfejsu API zarządzania dostępne tylko w obrębie hello sieci Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a8e89-256">Using API Management available only within hello VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="a8e89-257">Za pomocą interfejsu API zarządzania w sieci Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a8e89-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
