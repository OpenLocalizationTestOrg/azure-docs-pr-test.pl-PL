---
title: "Jak używać usługi Azure API Management w sieci wirtualnej z bramą aplikacji | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie instalacji i konfiguracji usługi Azure API Management w wewnętrznej sieci wirtualnej z aplikacji bramy (WAF) jako serwera sieci Web"
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
ms.openlocfilehash: 8131ded6b74e9c544bf70b1a4659ed07e5def04d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="304d9-103">Zintegrować zarządzanie interfejsami API w wewnętrznej sieci Wirtualnej z bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="304d9-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="304d9-104"><a name="overview"></a> — Omówienie</span><span class="sxs-lookup"><span data-stu-id="304d9-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="304d9-105">Usługi interfejsu API zarządzania można skonfigurować w sieci wirtualnej w trybie wewnętrznej, dzięki czemu dostępny tylko w obrębie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="304d9-105">The API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within the Virtual Network.</span></span> <span data-ttu-id="304d9-106">Bramy aplikacji Azure to usługa PAAS, która udostępnia usługi równoważenia obciążenia warstwy 7.</span><span class="sxs-lookup"><span data-stu-id="304d9-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="304d9-107">Pełni rolę usługi proxy odwrotnie, a udostępnia między oferty zapory aplikacji sieci Web (WAF).</span><span class="sxs-lookup"><span data-stu-id="304d9-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="304d9-108">Łączenie usługi API Management udostępniane w wewnętrznej sieci Wirtualnej z frontonu bramy aplikacji umożliwia następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="304d9-108">Combining API Management provisioned in an internal VNET with the Application Gateway frontend enables the following scenarios:</span></span>

* <span data-ttu-id="304d9-109">Użyj tego samego zasobu interfejsu API zarządzania zużycia zarówno przez użytkowników wewnętrznych i zewnętrznych konsumentów.</span><span class="sxs-lookup"><span data-stu-id="304d9-109">Use the same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="304d9-110">Użyj pojedynczego zasobu interfejsu API zarządzania i podzestawu interfejsów API zdefiniowanych w usłudze API Management dostępne dla użytkowników zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="304d9-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="304d9-111">Umożliwiają gotowe włączenie i wyłączenie z publicznego Internetu dostępu do interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="304d9-111">Provide a turn-key way to switch access to API Management from the public Internet on and off.</span></span> 

##<span data-ttu-id="304d9-112"><a name="scenario"></a> Scenariusza</span><span class="sxs-lookup"><span data-stu-id="304d9-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="304d9-113">W tym artykule opisano sposób używania jednej usługi Zarządzanie interfejsami API dla użytkowników wewnętrznych i zewnętrznych i stał się działać jako pojedynczy frontonu dla obu lokalnego i w chmurze interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="304d9-113">This article will cover how to use a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="304d9-114">Widoczne będzie także sposób ujawniać tylko podzestaw swoje interfejsy API (w tym przykładzie, które są wyróżnione zielony) wykorzystania zewnętrznych za pomocą funkcji PathBasedRouting dostępnych w bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-114">You will also see how to expose only a subset of your APIs (in the example they are highlighted in green) for External Consumption using the PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="304d9-115">W pierwszym przykładzie Instalatora wszystkich interfejsów API są zarządzane tylko z sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="304d9-115">In the first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="304d9-116">Konsumenci wewnętrzny (wyróżniane na kolor pomarańczowy) mogą uzyskiwać dostęp do wszystkich sieci wewnętrznych i zewnętrznych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="304d9-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="304d9-117">Ruch nigdy nie trafia do Internetu, wysokiej wydajności jest dostarczany za pomocą obwodów Express Route.</span><span class="sxs-lookup"><span data-stu-id="304d9-117">Traffic never goes out to Internet a high performance is delivered via Express Route circuits.</span></span>

![trasy adresu URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="304d9-119"><a name="before-you-begin"></a> Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="304d9-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="304d9-120">Zainstaluj najnowszą wersję poleceń cmdlet programu Azure PowerShell za pomocą Instalatora platformy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="304d9-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="304d9-121">Najnowszą wersję można pobrać i zainstalować z sekcji **Windows PowerShell** strony [Pliki do pobrania](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="304d9-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="304d9-122">Tworzenie sieci wirtualnej i Utwórz oddzielne podsieci dla interfejsu API zarządzania i bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="304d9-123">Jeśli chcesz utworzyć niestandardowy serwer DNS dla sieci wirtualnej, zrobić przed rozpoczęciem wdrażania.</span><span class="sxs-lookup"><span data-stu-id="304d9-123">If you intend to create a custom DNS server for the Virtual Network, do so before starting the deployment.</span></span> <span data-ttu-id="304d9-124">Dobrze Sprawdź, czy działa przez zapewnienie im maszyny wirtualnej utworzonej w nową podsieć w sieci wirtualnej można rozwiązać i dostęp do wszystkich punktów końcowych usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="304d9-124">Double check it works by ensuring a virtual machine created in a new subnet in the Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-to-create-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="304d9-125">Co to jest wymagana do utworzenia integracja interfejsu API zarządzania i bramę aplikacji?</span><span class="sxs-lookup"><span data-stu-id="304d9-125">What is required to create an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="304d9-126">**Pula serwerów zaplecza:** wewnętrzny wirtualny adres IP usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="304d9-126">**Back-end server pool:** This is the internal virtual IP address of the API Management service.</span></span>
* <span data-ttu-id="304d9-127">**Ustawienia puli serwerów zaplecza:** każda pula ma ustawienia, takie jak port, protokół i koligacja oparta na plikach cookie.</span><span class="sxs-lookup"><span data-stu-id="304d9-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="304d9-128">Te ustawienia są stosowane do wszystkich serwerów w puli.</span><span class="sxs-lookup"><span data-stu-id="304d9-128">These settings are applied to all servers within the pool.</span></span>
* <span data-ttu-id="304d9-129">**Port frontonu:** jest to port publiczny, który jest otwarty na bramie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-129">**Front-end port:** This is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="304d9-130">Naciśnięcie on ruch jest kierowany do jednego z serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="304d9-130">Traffic hitting it gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="304d9-131">**Odbiornik:** odbiornik ma port frontonu, protokół (Http lub Https, z uwzględnieniem wielkości liter) oraz nazwę certyfikatu SSL (w przypadku konfigurowania odciążania protokołu SSL).</span><span class="sxs-lookup"><span data-stu-id="304d9-131">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="304d9-132">**Reguła:** reguły wiąże odbiornik pulę serwerów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="304d9-132">**Rule:** The rule binds a listener to a back-end server pool.</span></span>
* <span data-ttu-id="304d9-133">**Niestandardowe sondy kondycji:** bramy aplikacji domyślnie używa sond na podstawie adresu IP do ustalenia w BackendAddressPool serwerów, które są aktywne.</span><span class="sxs-lookup"><span data-stu-id="304d9-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes to figure out which servers in the BackendAddressPool are active.</span></span> <span data-ttu-id="304d9-134">Zarządzanie interfejsami API, które usługa tylko odpowiada na żądania, które mają nagłówek hosta poprawne, dlatego sond domyślne zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="304d9-134">The API Management service only responds to requests which have the correct host header, hence the default probes fail.</span></span> <span data-ttu-id="304d9-135">Sondy kondycji niestandardowy musi być zdefiniowana, aby ustalić, że usługa jest aktywne i powinny przekazywania żądań bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-135">A custom health probe needs to be defined to help application gateway determine that the service is alive and it should forward requests.</span></span>
* <span data-ttu-id="304d9-136">**Certyfikat domeny niestandardowej:** dostęp do interfejsu API zarządzania z Internetu, należy utworzyć mapowanie CNAME jego nazwy hosta na nazwę DNS frontonu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-136">**Custom domain certificate:** To access API Management from the internet you need to create a CNAME mapping of its hostname to the Application Gateway front-end DNS name.</span></span> <span data-ttu-id="304d9-137">To zapewnia, że nagłówek nazwy hosta i certyfikatu wysłanego na bramie aplikacji, które jest przekazywane do interfejsu API zarządzania jest jeden APIM rozpoznać jako prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="304d9-137">This ensures that the hostname header and certificate sent to Application Gateway that is forwarded to API Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="304d9-138"><a name="overview-steps"></a> Kroków wymaganych do integracji interfejsu API zarządzania i bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="304d9-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="304d9-139">Utworzenie grupy zasobów dla usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="304d9-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="304d9-140">Tworzenie sieci wirtualnej, podsieci i publicznego adresu IP dla bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-140">Create a Virtual Network, subnet, and public IP for the Application Gateway.</span></span> <span data-ttu-id="304d9-141">Utwórz inną podsieć dla interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="304d9-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="304d9-142">Tworzenie usługi Zarządzanie interfejsami API w podsieci sieci Wirtualnej utworzone powyżej i upewnij się, że w przypadku korzystania z trybu wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="304d9-142">Create an API Management service inside the VNET subnet created above and ensure you use the Internal mode.</span></span>
4. <span data-ttu-id="304d9-143">Konfiguracja niestandardowa nazwa domeny w usłudze API Management.</span><span class="sxs-lookup"><span data-stu-id="304d9-143">Setup the custom domain name in the API Management service.</span></span>
5. <span data-ttu-id="304d9-144">Utwórz obiekt konfiguracji bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="304d9-145">Utwórz zasób aplikacji bramy.</span><span class="sxs-lookup"><span data-stu-id="304d9-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="304d9-146">Utwórz rekord CNAME z bramy aplikacji na nazwę hosta serwera proxy usługi API Management publicznej nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="304d9-146">Create a CNAME from the public DNS name of the Application Gateway to the API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="304d9-147">Tworzenie grupy zasobów dla usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="304d9-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="304d9-148">Upewnij się, że używasz najnowszej wersji programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="304d9-148">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="304d9-149">Więcej informacji znajduje się w artykule [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="304d9-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="304d9-150">Krok 1</span><span class="sxs-lookup"><span data-stu-id="304d9-150">Step 1</span></span>

<span data-ttu-id="304d9-151">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="304d9-151">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="304d9-152">Uwierzytelnianie przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="304d9-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="304d9-153">Krok 2</span><span class="sxs-lookup"><span data-stu-id="304d9-153">Step 2</span></span>

<span data-ttu-id="304d9-154">Sprawdź subskrypcje dla konta i zaznacz go.</span><span class="sxs-lookup"><span data-stu-id="304d9-154">Check the subscriptions for the account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="304d9-155">Krok 3</span><span class="sxs-lookup"><span data-stu-id="304d9-155">Step 3</span></span>

<span data-ttu-id="304d9-156">Utwórz grupę zasobów (ten krok można pominąć, jeśli używasz istniejącej grupy zasobów).</span><span class="sxs-lookup"><span data-stu-id="304d9-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="304d9-157">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="304d9-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="304d9-158">Będzie ona używana jako domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="304d9-158">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="304d9-159">Upewnij się, że wszystkie polecenia, aby utworzyć bramę aplikacji używać tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="304d9-159">Make sure that all commands to create an application gateway use the same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="304d9-160">Utwórz sieć wirtualną i podsieć bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="304d9-160">Create a Virtual Network and a subnet for the application gateway</span></span>

<span data-ttu-id="304d9-161">Poniższy przykład pokazuje, jak utworzyć sieć wirtualną przy użyciu zasobu manager.</span><span class="sxs-lookup"><span data-stu-id="304d9-161">The following example shows how to create a Virtual Network using the resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="304d9-162">Krok 1</span><span class="sxs-lookup"><span data-stu-id="304d9-162">Step 1</span></span>

<span data-ttu-id="304d9-163">Przypisz zakresu adresów 10.0.0.0/24 do zmiennej podsieci do użycia dla bramy aplikacji podczas tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="304d9-163">Assign the address range 10.0.0.0/24 to the subnet variable to be used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="304d9-164">Krok 2</span><span class="sxs-lookup"><span data-stu-id="304d9-164">Step 2</span></span>

<span data-ttu-id="304d9-165">Przypisz 10.0.1.0/24 zakres adresów do zmiennej podsieci do użycia dla interfejsu API zarządzania podczas tworzenia sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="304d9-165">Assign the address range 10.0.1.0/24 to the subnet variable to be used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="304d9-166">Krok 3</span><span class="sxs-lookup"><span data-stu-id="304d9-166">Step 3</span></span>

<span data-ttu-id="304d9-167">Tworzenie sieci wirtualnej o nazwie **appgwvnet** w grupie zasobów **apim-appGw-zarządcy zasobów** dla regionu zachodnie stany USA, przy użyciu 10.0.0.0/16 prefiks podsieci 10.0.0.0/24 i 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="304d9-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for the West US region using the prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="304d9-168">Krok 4</span><span class="sxs-lookup"><span data-stu-id="304d9-168">Step 4</span></span>

<span data-ttu-id="304d9-169">Przypisanie zmiennej podsieci następne kroki</span><span class="sxs-lookup"><span data-stu-id="304d9-169">Assign a subnet variable for the next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="304d9-170">Tworzenie usługi Zarządzanie interfejsami API w sieci Wirtualnej w trybie wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="304d9-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="304d9-171">Poniższy przykład pokazuje, jak można utworzyć usługi Zarządzanie interfejsami API w sieci Wirtualnej skonfigurowana dla tylko wewnętrzny dostępu.</span><span class="sxs-lookup"><span data-stu-id="304d9-171">The following example shows how to create an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="304d9-172">Krok 1</span><span class="sxs-lookup"><span data-stu-id="304d9-172">Step 1</span></span>
<span data-ttu-id="304d9-173">Utwórz obiekt sieci wirtualnej interfejsu API zarządzania za pomocą podsieci $apimsubnetdata utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="304d9-173">Create an API Management Virtual Network object using the subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="304d9-174">Krok 2</span><span class="sxs-lookup"><span data-stu-id="304d9-174">Step 2</span></span>
<span data-ttu-id="304d9-175">Tworzenie usługi Zarządzanie interfejsami API w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="304d9-175">Create an API Management service inside the Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
<span data-ttu-id="304d9-176">Po pomyślnym zainicjowaniu powyższego polecenia dotyczą [konfiguracji DNS wymagany dostęp do wewnętrznych usługi Zarządzanie interfejsami API sieci Wirtualnej](api-management-using-with-internal-vnet.md#apim-dns-configuration) do niego dostęp.</span><span class="sxs-lookup"><span data-stu-id="304d9-176">After the above command succeeds refer to [DNS Configuration required to access internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) to access it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="304d9-177">Ustawienie niestandardowej nazwy domeny w usłudze API Management</span><span class="sxs-lookup"><span data-stu-id="304d9-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="304d9-178">Krok 1</span><span class="sxs-lookup"><span data-stu-id="304d9-178">Step 1</span></span>
<span data-ttu-id="304d9-179">Przekaż certyfikat z kluczem prywatnym w domenie.</span><span class="sxs-lookup"><span data-stu-id="304d9-179">Upload the certificate with private key for the domain.</span></span> <span data-ttu-id="304d9-180">W tym przykładzie będzie `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="304d9-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path to .pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="304d9-181">Krok 2</span><span class="sxs-lookup"><span data-stu-id="304d9-181">Step 2</span></span>
<span data-ttu-id="304d9-182">Po przesłaniu certyfikatu, Utwórz obiekt konfiguracji nazwę hosta dla serwera proxy z nazwą hosta z `api.contoso.net`, ponieważ certyfikat przykład stanowi źródło dla `*.contoso.net` domeny.</span><span class="sxs-lookup"><span data-stu-id="304d9-182">Once the certificate is uploaded, create a hostname configuration object for the proxy with a hostname of `api.contoso.net`, as the example certificate provides authority for the  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="304d9-183">Tworzenie publicznego adresu IP dla konfiguracji frontonu</span><span class="sxs-lookup"><span data-stu-id="304d9-183">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="304d9-184">Utwórz zasób publicznego adresu IP **publicIP01** w grupie zasobów **apim-appGw-zarządcy zasobów** dla regionu zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="304d9-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="304d9-185">Adres IP jest przypisywany do bramy aplikacji w chwili uruchamiania usługi.</span><span class="sxs-lookup"><span data-stu-id="304d9-185">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="304d9-186">Tworzenie konfiguracji bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="304d9-186">Create application gateway configuration</span></span>

<span data-ttu-id="304d9-187">Wszystkie elementy konfiguracji muszą zostać skonfigurowane przed utworzeniem bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-187">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="304d9-188">Poniższe kroki umożliwiają utworzenie elementów konfiguracji wymaganych w przypadku zasobu bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-188">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="304d9-189">Krok 1</span><span class="sxs-lookup"><span data-stu-id="304d9-189">Step 1</span></span>

<span data-ttu-id="304d9-190">Utwórz konfigurację adresu IP bramy aplikacji o nazwie **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="304d9-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="304d9-191">Uruchomiona usługa Application Gateway wybierze adres IP ze skonfigurowanej podsieci i skieruje ruch sieciowy do adresów IP w puli adresów IP zaplecza.</span><span class="sxs-lookup"><span data-stu-id="304d9-191">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="304d9-192">Pamiętaj, że każde wystąpienie będzie mieć jeden adres IP.</span><span class="sxs-lookup"><span data-stu-id="304d9-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="304d9-193">Krok 2</span><span class="sxs-lookup"><span data-stu-id="304d9-193">Step 2</span></span>

<span data-ttu-id="304d9-194">Skonfiguruj port IP frontonu publiczny punkt końcowy IP.</span><span class="sxs-lookup"><span data-stu-id="304d9-194">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="304d9-195">Jest to port, podłączoną do użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="304d9-195">This port is the port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="304d9-196">Krok 3</span><span class="sxs-lookup"><span data-stu-id="304d9-196">Step 3</span></span>

<span data-ttu-id="304d9-197">Skonfiguruj adres IP frontonu z punktem końcowym publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="304d9-197">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="304d9-198">Krok 4</span><span class="sxs-lookup"><span data-stu-id="304d9-198">Step 4</span></span>

<span data-ttu-id="304d9-199">Skonfiguruj certyfikat bramy aplikacji, używane do odszyfrowania i zaszyfrowanie ruchu przechodzącego przez.</span><span class="sxs-lookup"><span data-stu-id="304d9-199">Configure the certificate for the Application Gateway, used to decrypt and re-encrypt the traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="304d9-200">Krok 5</span><span class="sxs-lookup"><span data-stu-id="304d9-200">Step 5</span></span>

<span data-ttu-id="304d9-201">Utwórz odbiornik HTTP bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-201">Create the HTTP listener for the Application Gateway.</span></span> <span data-ttu-id="304d9-202">Przypisać IP frontonu certyfikatu konfiguracji, portu i protokołu ssl.</span><span class="sxs-lookup"><span data-stu-id="304d9-202">Assign the front-end IP configuration, port, and ssl certificate to it.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="304d9-203">Krok 6</span><span class="sxs-lookup"><span data-stu-id="304d9-203">Step 6</span></span>

<span data-ttu-id="304d9-204">Tworzenie niestandardowych sondy do usługi API Management `ContosoApi` punktu końcowego domeny serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="304d9-204">Create a custom probe to the API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="304d9-205">Ścieżka `/status-0123456789abcdef` jest domyślnego kondycji punktu końcowego hostowanych na wszystkie usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="304d9-205">The path `/status-0123456789abcdef` is a default health endpoint hosted on all the API Management services.</span></span> <span data-ttu-id="304d9-206">Ustaw `api.contoso.net` jako nazwę hosta niestandardowego sondy do zabezpiecz ją przy użyciu certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="304d9-206">Set `api.contoso.net` as a custom probe hostname to secure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="304d9-207">Nazwa hosta `contosoapi.azure-api.net` jest nazwą hosta serwera proxy domyślne, które zostały skonfigurowane podczas usługi o nazwie `contosoapi` jest tworzony w publicznej Azure.</span><span class="sxs-lookup"><span data-stu-id="304d9-207">The hostname `contosoapi.azure-api.net` is the default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="304d9-208">Krok 7</span><span class="sxs-lookup"><span data-stu-id="304d9-208">Step 7</span></span>

<span data-ttu-id="304d9-209">Przekaż certyfikat do użycia zasobów puli wewnętrznej bazy danych z włączoną obsługą protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="304d9-209">Upload the certificate to be used on the SSL-enabled backend pool resources.</span></span> <span data-ttu-id="304d9-210">Jest to ten sam certyfikat, który podano w kroku 4 powyżej.</span><span class="sxs-lookup"><span data-stu-id="304d9-210">This is the same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path to .cer file>
```

### <a name="step-8"></a><span data-ttu-id="304d9-211">Krok 8</span><span class="sxs-lookup"><span data-stu-id="304d9-211">Step 8</span></span>

<span data-ttu-id="304d9-212">Skonfiguruj ustawienia HTTP zaplecza bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-212">Configure HTTP backend settings for the Application Gateway.</span></span> <span data-ttu-id="304d9-213">Dotyczy to również ustawienie limitu czasu, po którym są anulowane żądania wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="304d9-213">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="304d9-214">Ta wartość jest inny niż limit czasu sondowania.</span><span class="sxs-lookup"><span data-stu-id="304d9-214">This value is different from the probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="304d9-215">Krok 9</span><span class="sxs-lookup"><span data-stu-id="304d9-215">Step 9</span></span>

<span data-ttu-id="304d9-216">Skonfiguruj pulę adresów IP zaplecza, o nazwie **apimbackend** z wewnętrznego wirtualnego adresu IP adresu usługi Zarządzanie interfejsami API utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="304d9-216">Configure a back-end IP address pool named **apimbackend**  with the internal virtual IP address of the API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="304d9-217">Krok 10</span><span class="sxs-lookup"><span data-stu-id="304d9-217">Step 10</span></span>

<span data-ttu-id="304d9-218">Tworzenie ustawień dla fikcyjnego zaplecza (nieistniejącego).</span><span class="sxs-lookup"><span data-stu-id="304d9-218">Create settings for a dummy (non-existent) backend.</span></span> <span data-ttu-id="304d9-219">Żądania do ścieżki interfejsu API, które nie chcemy ujawniać z interfejsu API zarządzania za pośrednictwem bramy aplikacji będzie trafień tego wewnętrznej bazy danych i zwróć 404.</span><span class="sxs-lookup"><span data-stu-id="304d9-219">Requests to API paths that we do not want to expose from API Management via Application Gateway will hit this backend and return 404.</span></span>

<span data-ttu-id="304d9-220">Skonfiguruj ustawienia HTTP zaplecza zastępczego.</span><span class="sxs-lookup"><span data-stu-id="304d9-220">Configure HTTP settings for the dummy backend.</span></span>

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="304d9-221">Skonfiguruj fikcyjny zaplecza **dummyBackendPool**, który wskazuje adres FQDN **dummybackend.com**. Ten adres FQDN nie istnieje w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="304d9-221">Configure a dummy backend **dummyBackendPool**, which points to a FQDN address **dummybackend.com**. This FQDN address does not exist in the virtual network.</span></span>

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

<span data-ttu-id="304d9-222">Utwórz ustawienie reguł używanego domyślnie wskazujący na wewnętrznej bazy danych nie istnieje bramę aplikacji **dummybackend.com** w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="304d9-222">Create a rule setting that the Application Gateway will use by default which points to the non-existent backend **dummybackend.com** in the Virtual Network.</span></span>

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a><span data-ttu-id="304d9-223">Krok 11</span><span class="sxs-lookup"><span data-stu-id="304d9-223">Step 11</span></span>

<span data-ttu-id="304d9-224">Konfiguruj adres URL reguły ścieżki dla pul zaplecza.</span><span class="sxs-lookup"><span data-stu-id="304d9-224">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="304d9-225">Dzięki temu, wybierając tylko niektóre z interfejsów API z interfejsu API zarządzania dla są udostępniane publicznie.</span><span class="sxs-lookup"><span data-stu-id="304d9-225">This enables selecting only some of the APIs from API Management for being exposed to the public.</span></span> <span data-ttu-id="304d9-226">Na przykład, jeśli istnieją `Echo API` (/ echo /), `Calculator API` (/calc/) itd. Sprawdź tylko `Echo API` dostępny z Internetu).</span><span class="sxs-lookup"><span data-stu-id="304d9-226">For example, if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="304d9-227">Poniższy przykład tworzy Prosta reguła dla "/ echo /" ścieżkę routingu ruchu sieciowego do wewnętrznej "apimProxyBackendPool".</span><span class="sxs-lookup"><span data-stu-id="304d9-227">The following example creates a simple rule for the "/echo/" path routing traffic to the back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="304d9-228">Jeśli ścieżka nie odpowiada reguły ścieżki, chcemy, aby umożliwić z interfejsu API zarządzania, Konfiguracja mapowania ścieżki reguły konfiguruje również domyślną pulę adresów zaplecza o nazwie **dummyBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="304d9-228">If the path doesn't match the path rules we want to enable from API Management, the rule path map configuration also configures a default back-end address pool named **dummyBackendPool**.</span></span> <span data-ttu-id="304d9-229">Na przykład http://api.contoso.net/calc/ * przechodzi do **dummyBackendPool** określone jako domyślna pula cofanie dopasowane ruchu.</span><span class="sxs-lookup"><span data-stu-id="304d9-229">For example, http://api.contoso.net/calc/* goes to **dummyBackendPool** as it is defined as the default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

<span data-ttu-id="304d9-230">Powyższy krok zapewnia, że tylko żądania dla ścieżki "/ echo" są dozwolone przez bramę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-230">The above step ensures that only requests for the path "/echo" are allowed through the Application Gateway.</span></span> <span data-ttu-id="304d9-231">Żądania do innych interfejsów API skonfigurowane w usłudze API Management spowoduje zgłoszenie błędów 404 z bramy aplikacji podczas uzyskiwania dostępu do z Internetu.</span><span class="sxs-lookup"><span data-stu-id="304d9-231">Requests to other APIs configured in API Management will throw 404 errors from Application Gateway when accessed from the Internet.</span></span> 

### <a name="step-12"></a><span data-ttu-id="304d9-232">Krok 12</span><span class="sxs-lookup"><span data-stu-id="304d9-232">Step 12</span></span>

<span data-ttu-id="304d9-233">Utwórz ustawienie reguły dla bramy aplikacji korzystać z routingu na podstawie ścieżki adresu URL.</span><span class="sxs-lookup"><span data-stu-id="304d9-233">Create a rule setting for the Application Gateway to use URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a><span data-ttu-id="304d9-234">Krok 13</span><span class="sxs-lookup"><span data-stu-id="304d9-234">Step 13</span></span>

<span data-ttu-id="304d9-235">Skonfiguruj liczbę wystąpień i rozmiaru bramy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-235">Configure the number of instances and size for the Application Gateway.</span></span> <span data-ttu-id="304d9-236">W tym miejscu używamy [SKU zapory aplikacji sieci Web](../application-gateway/application-gateway-webapplicationfirewall-overview.md) Aby zwiększyć bezpieczeństwo zasobu interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="304d9-236">Here we are using the [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of the API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a><span data-ttu-id="304d9-237">Krok 14</span><span class="sxs-lookup"><span data-stu-id="304d9-237">Step 14</span></span>

<span data-ttu-id="304d9-238">Konfigurowanie zapory aplikacji sieci Web w trybie "Zapobiegania".</span><span class="sxs-lookup"><span data-stu-id="304d9-238">Configure WAF to be in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="304d9-239">Utwórz bramę aplikacji</span><span class="sxs-lookup"><span data-stu-id="304d9-239">Create Application Gateway</span></span>

<span data-ttu-id="304d9-240">Utwórz bramę aplikacji ze wszystkimi obiektami konfiguracji z powyższych kroków.</span><span class="sxs-lookup"><span data-stu-id="304d9-240">Create an Application Gateway with all the configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-the-api-management-proxy-hostname-to-the-public-dns-name-of-the-application-gateway-resource"></a><span data-ttu-id="304d9-241">CNAME nazwy hosta serwera proxy usługi API Management do publicznej nazwy DNS zasobu bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="304d9-241">CNAME the API Management proxy hostname to the public DNS name of the Application Gateway resource</span></span>

<span data-ttu-id="304d9-242">Po utworzeniu bramy następnym krokiem jest skonfigurowanie frontonu na potrzeby komunikacji.</span><span class="sxs-lookup"><span data-stu-id="304d9-242">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="304d9-243">Korzystając z publicznym adresem IP, brama aplikacji wymaga przypisywany dynamicznie nazwy DNS, które nie mogą być łatwe w użyciu.</span><span class="sxs-lookup"><span data-stu-id="304d9-243">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy to use.</span></span> 

<span data-ttu-id="304d9-244">Brama aplikacji w nazwa DNS należy utworzyć rekord CNAME, który wskazuje nazwę hosta serwera proxy APIM (np. `api.contoso.net` w powyższych przykładach) do tej nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="304d9-244">The Application Gateway's DNS name should be used to create a CNAME record which points the APIM proxy host name (e.g. `api.contoso.net` in the examples above) to this DNS name.</span></span> <span data-ttu-id="304d9-245">Aby skonfigurować rekord IP CNAME serwera sieci Web, należy pobrać szczegółów bramy aplikacji i jej skojarzonej nazwy IP DNS za pomocą elementu publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="304d9-245">To configure the frontend IP CNAME record, retrieve the details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element.</span></span> <span data-ttu-id="304d9-246">Użycie rekordów A nie jest zalecane, ponieważ adres VIP może się zmieniać podczas ponownego uruchomienia bramy.</span><span class="sxs-lookup"><span data-stu-id="304d9-246">The use of A-records is not recommended since the VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="304d9-247"><a name="summary"></a> Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="304d9-247"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="304d9-248">Skonfigurowane w sieci Wirtualnej platformy Azure API Management oferuje interfejs pojedyncza brama dla wszystkich skonfigurowanych interfejsów API, czy są one lokalnego hostowanej lub w chmurze.</span><span class="sxs-lookup"><span data-stu-id="304d9-248">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in the cloud.</span></span> <span data-ttu-id="304d9-249">Integrowanie aplikacji bramy z interfejsu API zarządzania zapewnia elastyczność selektywne włączenie określonego interfejsów API, aby być dostępna w Internecie, a także dostarczając zapory aplikacji sieci Web frontonu do Twojego wystąpienia usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="304d9-249">Integrating Application Gateway with API Management provides the flexibility of selectively enabling particular APIs to be accessible on the Internet, as well as providing a Web Application Firewall as a frontend to your API Management instance.</span></span>

##<span data-ttu-id="304d9-250"><a name="next-steps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="304d9-250"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="304d9-251">Dowiedz się więcej na temat bramy aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="304d9-251">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="304d9-252">Omówienie bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="304d9-252">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="304d9-253">Zapora aplikacji sieci Web bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="304d9-253">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="304d9-254">Brama aplikacji przy użyciu routingu na podstawie ścieżki</span><span class="sxs-lookup"><span data-stu-id="304d9-254">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="304d9-255">Dowiedz się więcej o interfejsu API zarządzania i sieci wirtualnych</span><span class="sxs-lookup"><span data-stu-id="304d9-255">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="304d9-256">Za pomocą interfejsu API zarządzania dostępny tylko w ramach sieci Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="304d9-256">Using API Management available only within the VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="304d9-257">Za pomocą interfejsu API zarządzania w sieci Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="304d9-257">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
