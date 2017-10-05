---
title: "Jak używać usługi Azure API Management z wewnętrznej sieci wirtualnej | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie instalacji i konfiguracji usługi Azure API Management w wewnętrznej sieci wirtualnej."
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 55248387c7e78d05c1cf1afd615b7b921e9669d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="dc339-103">Przy użyciu usługi Azure API Management z wewnętrznej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="dc339-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="dc339-104">Sieci wirtualne Azure (sieci wirtualne) zarządzanie interfejsami API umożliwiają zarządzanie interfejsów API nie jest dostępny w Internecie.</span><span class="sxs-lookup"><span data-stu-id="dc339-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on the Internet.</span></span> <span data-ttu-id="dc339-105">Liczba technologii sieci VPN są dostępne do nawiązania połączenia i zarządzanie interfejsami API może zostać wdrożony w dwóch trybach głównego w sieci Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="dc339-105">A number of VPN technologies are available to make the connection and API Management can be deployed in two main modes inside the VNET:</span></span>
* <span data-ttu-id="dc339-106">Zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="dc339-106">External</span></span>
* <span data-ttu-id="dc339-107">wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="dc339-107">Internal</span></span>

## <span data-ttu-id="dc339-108"><a name="overview"> </a>Omówienie</span><span class="sxs-lookup"><span data-stu-id="dc339-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="dc339-109">Zarządzanie interfejsami API jest wdrażana w trybie sieci wewnętrznej wirtualnym, wszystkie punkty końcowe usługi (bramy, portalu dla deweloperów, portal wydawcy, bezpośrednie zarządzanie i Git) są widoczne w sieci wirtualnej, którą kontrolujesz tylko dostęp do.</span><span class="sxs-lookup"><span data-stu-id="dc339-109">When API Management is deployed in an Internal Virtual network mode, all the service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="dc339-110">Żaden z punktów końcowych usługi nie jest zarejestrowany na publicznym serwerze DNS.</span><span class="sxs-lookup"><span data-stu-id="dc339-110">None of the service endpoints are registered on the Public DNS Server.</span></span>

<span data-ttu-id="dc339-111">Za pomocą interfejsu API zarządzania w trybie wewnętrzny można osiągnąć następujące scenariusze</span><span class="sxs-lookup"><span data-stu-id="dc339-111">Using API Management in Internal mode, you can achieve the following scenarios</span></span>
* <span data-ttu-id="dc339-112">Bezpiecznie należy interfejsów API hostowanych w prywatnej dostępny centrum danych przez 3 strony poza za pomocą połączeń lokacja-lokacja lub sieci VPN usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="dc339-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="dc339-113">Włącz scenariuszach chmur hybrydowych dzięki uwidocznieniu działania sieci opartej na chmurze interfejsów API i interfejsów API lokalnego za pośrednictwem wspólnego bramy.</span><span class="sxs-lookup"><span data-stu-id="dc339-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="dc339-114">Zarządzanie swoje interfejsy API hostowany w wielu lokalizacjach geograficznych przy użyciu jeden punkt końcowy bramy.</span><span class="sxs-lookup"><span data-stu-id="dc339-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="dc339-115"><a name="enable-vpn"></a>Tworzenie zarządzanie interfejsami API w sieci wewnętrznej wirtualnej</span><span class="sxs-lookup"><span data-stu-id="dc339-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="dc339-116">Usługa API Management w sieci wewnętrznej wirtualnej jest hostowany za wewnętrzny Balancer(ILB) obciążenia.</span><span class="sxs-lookup"><span data-stu-id="dc339-116">The API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="dc339-117">Adres IP ILB znajduje się w [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) zakresu.</span><span class="sxs-lookup"><span data-stu-id="dc339-117">The IP Address of the ILB is in the [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="dc339-118">Włącz połączenie sieci Wirtualnej przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="dc339-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="dc339-119">Najpierw utworzyć usługi Zarządzanie interfejsami API, wykonując kroki [utworzyć zarządzanie interfejsami API usługi][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="dc339-119">First create the API Management service by following the steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="dc339-120">Następnie Konfiguracja interfejsu API zarządzania do wdrożenia w ramach sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dc339-120">Then set-up API Management to be deployed inside a Virtual network.</span></span>

![Menu konfigurowania APIM w wewnętrznej sieci wirtualnej][api-management-using-internal-vnet-menu]

<span data-ttu-id="dc339-122">Po wdrożeniu zakończy się powodzeniem, wewnętrznego wirtualnego adresu IP usługi powinny być widoczne na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="dc339-122">After the deployment succeeds, you should see the Internal Virtual IP Address of your service on the dashboard.</span></span>

![Pulpit nawigacyjny zarządzania interfejsu API z wewnętrznej sieci Wirtualnej skonfigurowane][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="dc339-124">Włącz połączenie sieci Wirtualnej przy użyciu poleceń cmdlet programu Powershell</span><span class="sxs-lookup"><span data-stu-id="dc339-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="dc339-125">Można również włączyć łączność sieci Wirtualnej przy użyciu poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc339-125">You can also enable VNET connectivity using the PowerShell cmdlets.</span></span>

* <span data-ttu-id="dc339-126">**Tworzenie usługi Zarządzanie interfejsami API w sieci Wirtualnej**: Użyj polecenia cmdlet [AzureRmApiManagement nowy](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) utworzenia usługi Azure API Management w sieci Wirtualnej i skonfigurować go do używania typu wewnętrznej sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dc339-126">**Create an API Management service inside a VNET**: Use the cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) to create an Azure API Management service inside a VNET and configure it to use the Internal VNET type.</span></span>

* <span data-ttu-id="dc339-127">**Wdrażanie istniejącej usługi Zarządzanie interfejsami API w sieci Wirtualnej**: Użyj polecenia cmdlet [AzureRmApiManagementDeployment aktualizacji](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) Aby przenieść istniejącą usługę Azure API Management w sieci wirtualnej i skonfigurować go do używania Wewnętrzny typ sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dc339-127">**Deploy an existing API Management service inside a VNET**: Use the cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) to move an existing Azure API Management service inside a Virtual network and configure it to use Internal VNET type.</span></span>

## <span data-ttu-id="dc339-128"><a name="apim-dns-configuration"></a>Konfiguracja DNS</span><span class="sxs-lookup"><span data-stu-id="dc339-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="dc339-129">Korzystając z interfejsu API zarządzania w trybie sieci zewnętrznych wirtualnym, DNS jest zarządzana przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="dc339-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="dc339-130">Dla trybu sieciowego wewnętrznego wirtualnego trzeba zarządzać własną DNS.</span><span class="sxs-lookup"><span data-stu-id="dc339-130">For Internal Virtual network mode, you have to manage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="dc339-131">Zarządzanie interfejsami API usługi nie nasłuchiwać żądań przesyłanych na adresy IP.</span><span class="sxs-lookup"><span data-stu-id="dc339-131">API Management service does not listen to requests coming on IP addresses.</span></span> <span data-ttu-id="dc339-132">Tylko odpowiada na żądania nazwa hosta skonfigurowana na jego punktów końcowych usługi (w tym bramy, portalu dla deweloperów wydawcy portalu, bezpośrednie zarządzanie punktu końcowego i git).</span><span class="sxs-lookup"><span data-stu-id="dc339-132">It only responds to requests to the Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="dc339-133">Dostęp do nazw hosta domyślnego:</span><span class="sxs-lookup"><span data-stu-id="dc339-133">Access on default host names:</span></span>
<span data-ttu-id="dc339-134">Podczas tworzenia usługi Zarządzanie interfejsami API w chmurze publicznej Azure, na przykład o nazwie "contoso", następujące punkty końcowe usługi są domyślnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="dc339-134">When you create an API Management service in public Azure cloud, named "contoso" for example, the following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="dc339-135">Bramy / serwera Proxy - contoso.azure api.net</span><span class="sxs-lookup"><span data-stu-id="dc339-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="dc339-136">Portal wydawcy i portalu dla deweloperów - contoso.portal.azure api.net</span><span class="sxs-lookup"><span data-stu-id="dc339-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="dc339-137">Punkt końcowy zarządzania bezpośredniego - contoso.management.azure api.net</span><span class="sxs-lookup"><span data-stu-id="dc339-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="dc339-138">GIT - contoso.scm.azure api.net</span><span class="sxs-lookup"><span data-stu-id="dc339-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="dc339-139">Aby uzyskać dostęp do tych punktów końcowych usługi API Management, należy utworzyć maszynę wirtualną w podsieci podłączone do sieci wirtualnej, w której jest wdrażane zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="dc339-139">To access these API Management service endpoints, you can create a Virtual Machine in a subnet connected to the Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="dc339-140">Zakładając, że wewnętrznego wirtualnego adresu IP dla usługi jest 10.0.0.5, możesz zrobić hosty pliku mapowania (% SystemDrive%\drivers\etc\hosts) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="dc339-140">Assuming the Internal Virtual IP Address for your service is 10.0.0.5, you can do the hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="dc339-141">10.0.0.5 contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="dc339-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="dc339-142">10.0.0.5 contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="dc339-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="dc339-143">10.0.0.5 contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="dc339-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="dc339-144">10.0.0.5 contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="dc339-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="dc339-145">Wszystkie punkty końcowe usługi można następnie uzyskać dostęp z maszyny wirtualnej został utworzony.</span><span class="sxs-lookup"><span data-stu-id="dc339-145">You can then access all the service endpoints from the Virtual Machine you created.</span></span> <span data-ttu-id="dc339-146">Jeśli używany jest serwer niestandardowe DNS w sieci wirtualnej, można również utworzyć rekordy A DNS i uzyskiwać dostęp do tych punktów końcowych z dowolnego miejsca w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dc339-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="dc339-147">Dostęp do niestandardowych nazw domen:</span><span class="sxs-lookup"><span data-stu-id="dc339-147">Access on custom domain names:</span></span>
<span data-ttu-id="dc339-148">Jeśli nie chcesz uzyskać dostęp do usługi API Management z domyślnej nazwy hostów, należy skonfigurować niestandardowe nazwy domen dla wszystkich usług punktów końcowych podobnie jak poniżej</span><span class="sxs-lookup"><span data-stu-id="dc339-148">If you don’t want to access the API Management service with the default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Skonfigurowanie domeny niestandardowej dla interfejsu API zarządzania][api-management-custom-domain-name]

<span data-ttu-id="dc339-150">Następnie można utworzyć rekordów znajdujących się na serwerze DNS, aby dostęp do tych punktów końcowych, które są dostępne jedynie z sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dc339-150">Then you can create A records in your DNS Server to access these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="dc339-151"><a name="related-content"></a>Związane z zawartością</span><span class="sxs-lookup"><span data-stu-id="dc339-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="dc339-152">[Typowe problemy z konfiguracją sieci podczas konfigurowania APIM w sieci Wirtualnej][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="dc339-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="dc339-153">Często zadawane pytania dotyczące sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="dc339-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="dc339-154">Tworzenie rekord w systemie DNS</span><span class="sxs-lookup"><span data-stu-id="dc339-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
