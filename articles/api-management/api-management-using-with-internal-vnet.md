---
title: "aaaHow toouse Azure API Management z wewnętrznej sieci wirtualnej | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i konfigurowanie usługi Azure API Management w wewnętrznej sieci wirtualnej."
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
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a><span data-ttu-id="a9090-103">Przy użyciu usługi Azure API Management z wewnętrznej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a9090-103">Using Azure API Management service with Internal Virtual Network</span></span>
<span data-ttu-id="a9090-104">Sieci wirtualne Azure (sieci wirtualne) zarządzanie interfejsami API umożliwiają zarządzanie interfejsów API nie jest dostępna na powitania Internet.</span><span class="sxs-lookup"><span data-stu-id="a9090-104">With Azure Virtual Networks (VNETs), API Management can manage APIs not accessible on hello Internet.</span></span> <span data-ttu-id="a9090-105">Połączenia hello toomake dostępne są różne technologie sieci VPN i zarządzanie interfejsami API może zostać wdrożony w dwóch trybach głównego wewnątrz hello sieci Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="a9090-105">A number of VPN technologies are available toomake hello connection and API Management can be deployed in two main modes inside hello VNET:</span></span>
* <span data-ttu-id="a9090-106">Zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="a9090-106">External</span></span>
* <span data-ttu-id="a9090-107">wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="a9090-107">Internal</span></span>

## <span data-ttu-id="a9090-108"><a name="overview"> </a>Omówienie</span><span class="sxs-lookup"><span data-stu-id="a9090-108"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="a9090-109">Po wdrożeniu usługi API Management w trybie sieci wewnętrznej wirtualnym wszystkich hello punktów końcowych usługi (bramy, portalu dla deweloperów, portal wydawcy, bezpośrednie zarządzanie i Git) są widoczne tylko w sieci wirtualnej, która umożliwia kontrolę dostępu do.</span><span class="sxs-lookup"><span data-stu-id="a9090-109">When API Management is deployed in an Internal Virtual network mode, all hello service endpoints (gateway, developer portal, publisher portal, direct management and Git) are only visible inside a Virtual network that you control access to.</span></span> <span data-ttu-id="a9090-110">Żaden z punktów końcowych usługi hello nie jest zarejestrowany na powitania publiczny serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="a9090-110">None of hello service endpoints are registered on hello Public DNS Server.</span></span>

<span data-ttu-id="a9090-111">Za pomocą interfejsu API zarządzania w trybie wewnętrzny można osiągnąć następujące scenariusze hello</span><span class="sxs-lookup"><span data-stu-id="a9090-111">Using API Management in Internal mode, you can achieve hello following scenarios</span></span>
* <span data-ttu-id="a9090-112">Bezpiecznie należy interfejsów API hostowanych w prywatnej dostępny centrum danych przez 3 strony poza za pomocą połączeń lokacja-lokacja lub sieci VPN usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a9090-112">Securely make APIs hosted in your private datacenter accessible by 3rd parties outside of it using Site-to-Site or ExpressRoute VPN connections.</span></span>
* <span data-ttu-id="a9090-113">Włącz scenariuszach chmur hybrydowych dzięki uwidocznieniu działania sieci opartej na chmurze interfejsów API i interfejsów API lokalnego za pośrednictwem wspólnego bramy.</span><span class="sxs-lookup"><span data-stu-id="a9090-113">Enable hybrid cloud scenarios by exposing your cloud-based APIs and on-prem APIs through a common gateway.</span></span>
* <span data-ttu-id="a9090-114">Zarządzanie swoje interfejsy API hostowany w wielu lokalizacjach geograficznych przy użyciu jeden punkt końcowy bramy.</span><span class="sxs-lookup"><span data-stu-id="a9090-114">Manage your APIs hosted in multiple geographic locations using a single Gateway endpoint.</span></span> 

## <span data-ttu-id="a9090-115"><a name="enable-vpn"></a>Tworzenie zarządzanie interfejsami API w sieci wewnętrznej wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a9090-115"><a name="enable-vpn"> </a>Creating an API Management in Internal Virtual network</span></span>
<span data-ttu-id="a9090-116">Witaj usługi Zarządzanie interfejsami API w sieci wewnętrznej wirtualnej jest hostowany za wewnętrzny Balancer(ILB) obciążenia.</span><span class="sxs-lookup"><span data-stu-id="a9090-116">hello API Management service in Internal Virtual network is hosted behind an Internal Load Balancer(ILB).</span></span> <span data-ttu-id="a9090-117">Adres IP hello ILB Hello jest hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) zakresu.</span><span class="sxs-lookup"><span data-stu-id="a9090-117">hello IP Address of hello ILB is in hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) range.</span></span>  

### <a name="enable-vnet-connection-using-azure-portal"></a><span data-ttu-id="a9090-118">Włącz połączenie sieci Wirtualnej przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a9090-118">Enable VNET connection using Azure portal</span></span>
<span data-ttu-id="a9090-119">Najpierw utworzyć usługi Zarządzanie interfejsami API hello, wykonując kroki hello [utworzyć zarządzanie interfejsami API usługi][Create API Management service].</span><span class="sxs-lookup"><span data-stu-id="a9090-119">First create hello API Management service by following hello steps [Create API Management service][Create API Management service].</span></span> <span data-ttu-id="a9090-120">Następnie Konfiguracja interfejsu API zarządzania toobe wdrożone w ramach sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9090-120">Then set-up API Management toobe deployed inside a Virtual network.</span></span>

![Menu konfigurowania APIM w wewnętrznej sieci wirtualnej][api-management-using-internal-vnet-menu]

<span data-ttu-id="a9090-122">Po pomyślnym zainicjowaniu wdrażania hello, hello wewnętrznego wirtualnego adresu IP usługi powinny być widoczne na pulpicie nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="a9090-122">After hello deployment succeeds, you should see hello Internal Virtual IP Address of your service on hello dashboard.</span></span>

![Pulpit nawigacyjny zarządzania interfejsu API z wewnętrznej sieci Wirtualnej skonfigurowane][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a><span data-ttu-id="a9090-124">Włącz połączenie sieci Wirtualnej przy użyciu poleceń cmdlet programu Powershell</span><span class="sxs-lookup"><span data-stu-id="a9090-124">Enable VNET connection using Powershell cmdlets</span></span>
<span data-ttu-id="a9090-125">Można również włączyć łączność sieci Wirtualnej przy użyciu poleceń cmdlet programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a9090-125">You can also enable VNET connectivity using hello PowerShell cmdlets.</span></span>

* <span data-ttu-id="a9090-126">**Tworzenie usługi Zarządzanie interfejsami API w sieci Wirtualnej**: Użyj polecenia cmdlet hello [AzureRmApiManagement nowy](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate Azure API Management w sieci Wirtualnej i skonfiguruj go toouse hello wewnętrzna sieć wirtualna typu.</span><span class="sxs-lookup"><span data-stu-id="a9090-126">**Create an API Management service inside a VNET**: Use hello cmdlet [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate an Azure API Management service inside a VNET and configure it toouse hello Internal VNET type.</span></span>

* <span data-ttu-id="a9090-127">**Wdrażanie istniejącej usługi Zarządzanie interfejsami API w sieci Wirtualnej**: Użyj polecenia cmdlet hello [AzureRmApiManagementDeployment aktualizacji](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove istniejącej usługi Azure API Management w sieci wirtualnej i skonfiguruj go toouse Wewnętrzny typ sieci Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9090-127">**Deploy an existing API Management service inside a VNET**: Use hello cmdlet [Update-AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove an existing Azure API Management service inside a Virtual network and configure it toouse Internal VNET type.</span></span>

## <span data-ttu-id="a9090-128"><a name="apim-dns-configuration"></a>Konfiguracja DNS</span><span class="sxs-lookup"><span data-stu-id="a9090-128"><a name="apim-dns-configuration"></a>DNS configuration</span></span>
<span data-ttu-id="a9090-129">Korzystając z interfejsu API zarządzania w trybie sieci zewnętrznych wirtualnym, DNS jest zarządzana przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="a9090-129">When using API Management in External Virtual network mode, DNS is managed by Azure.</span></span> <span data-ttu-id="a9090-130">Tryb sieci wewnętrznej wirtualny należy toomanage własne DNS.</span><span class="sxs-lookup"><span data-stu-id="a9090-130">For Internal Virtual network mode, you have toomanage your own DNS.</span></span>

> [!NOTE]
> <span data-ttu-id="a9090-131">Zarządzanie interfejsami API usługi nie będzie nasłuchiwać toorequests pochodzących z adresami IP.</span><span class="sxs-lookup"><span data-stu-id="a9090-131">API Management service does not listen toorequests coming on IP addresses.</span></span> <span data-ttu-id="a9090-132">Tylko odpowiadały toohello toorequests nazwa hosta skonfigurowana na jego punktów końcowych usługi (w tym bramy, portalu dla deweloperów wydawcy portalu, bezpośrednie zarządzanie punktu końcowego i git).</span><span class="sxs-lookup"><span data-stu-id="a9090-132">It only responds toorequests toohello Hostname configured on its service endpoints (which includes gateway, developer portal, publisher Portal, direct management endpoint, and git).</span></span>

### <a name="access-on-default-host-names"></a><span data-ttu-id="a9090-133">Dostęp do nazw hosta domyślnego:</span><span class="sxs-lookup"><span data-stu-id="a9090-133">Access on default host names:</span></span>
<span data-ttu-id="a9090-134">Podczas tworzenia usługi Zarządzanie interfejsami API w chmurze publicznej Azure, na przykład o nazwie "contoso", hello następujące punkty końcowe usługi są domyślnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="a9090-134">When you create an API Management service in public Azure cloud, named "contoso" for example, hello following service endpoints are configured by default.</span></span>

>   <span data-ttu-id="a9090-135">Bramy / serwera Proxy - contoso.azure api.net</span><span class="sxs-lookup"><span data-stu-id="a9090-135">Gateway / Proxy - contoso.azure-api.net</span></span>

> <span data-ttu-id="a9090-136">Portal wydawcy i portalu dla deweloperów - contoso.portal.azure api.net</span><span class="sxs-lookup"><span data-stu-id="a9090-136">Publisher Portal and Developer Portal - contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="a9090-137">Punkt końcowy zarządzania bezpośredniego - contoso.management.azure api.net</span><span class="sxs-lookup"><span data-stu-id="a9090-137">Direct Management Endpoint - contoso.management.azure-api.net</span></span>

>   <span data-ttu-id="a9090-138">GIT - contoso.scm.azure api.net</span><span class="sxs-lookup"><span data-stu-id="a9090-138">GIT - contoso.scm.azure-api.net</span></span>

<span data-ttu-id="a9090-139">tooaccess tych punktów końcowych usługi Zarządzanie interfejsami API można utworzyć maszyny wirtualnej w sieci wirtualnej toohello podłączone podsieci, w której jest wdrażane zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="a9090-139">tooaccess these API Management service endpoints, you can create a Virtual Machine in a subnet connected toohello Virtual network in which API Management is deployed.</span></span> <span data-ttu-id="a9090-140">Zakładając, że hello wewnętrznego wirtualnego adresu IP dla usługi jest 10.0.0.5, możesz zrobić hello mapowania pliku hostów (% SystemDrive%\drivers\etc\hosts) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a9090-140">Assuming hello Internal Virtual IP Address for your service is 10.0.0.5, you can do hello hosts file mapping (%SystemDrive%\drivers\etc\hosts) as follows:</span></span>

> <span data-ttu-id="a9090-141">10.0.0.5 contoso.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="a9090-141">10.0.0.5    contoso.azure-api.net</span></span>

> <span data-ttu-id="a9090-142">10.0.0.5 contoso.portal.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="a9090-142">10.0.0.5    contoso.portal.azure-api.net</span></span>

> <span data-ttu-id="a9090-143">10.0.0.5 contoso.management.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="a9090-143">10.0.0.5    contoso.management.azure-api.net</span></span>

> <span data-ttu-id="a9090-144">10.0.0.5 contoso.scm.azure-api.net</span><span class="sxs-lookup"><span data-stu-id="a9090-144">10.0.0.5    contoso.scm.azure-api.net</span></span>

<span data-ttu-id="a9090-145">Następnie są dostępne wszystkie punkty końcowe usługi hello hello tworzenia maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9090-145">You can then access all hello service endpoints from hello Virtual Machine you created.</span></span> <span data-ttu-id="a9090-146">Jeśli używany jest serwer niestandardowe DNS w sieci wirtualnej, można również utworzyć rekordy A DNS i uzyskiwać dostęp do tych punktów końcowych z dowolnego miejsca w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9090-146">If using a Custom DNS server in a Virtual network, you can also create A DNS records and access these endpoints from anywhere in your Virtual network.</span></span> 

### <a name="access-on-custom-domain-names"></a><span data-ttu-id="a9090-147">Dostęp do niestandardowych nazw domen:</span><span class="sxs-lookup"><span data-stu-id="a9090-147">Access on custom domain names:</span></span>
<span data-ttu-id="a9090-148">Jeśli nie chcesz hello tooaccess usługi API Management z hello domyślne nazwy hosta, należy skonfigurować niestandardowe nazwy domen dla wszystkich usług punktów końcowych podobnie jak poniżej</span><span class="sxs-lookup"><span data-stu-id="a9090-148">If you don’t want tooaccess hello API Management service with hello default host names, you can setup custom domain names for all your service endpoints like below</span></span>

![Skonfigurowanie domeny niestandardowej dla interfejsu API zarządzania][api-management-custom-domain-name]

<span data-ttu-id="a9090-150">Następnie można utworzyć rekordu w sieci serwer DNS tooaccess te punkty końcowe, które są dostępne jedynie z sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9090-150">Then you can create A records in your DNS Server tooaccess these endpoints which are only accessible from within your Virtual network.</span></span>

## <span data-ttu-id="a9090-151"><a name="related-content"></a>Związane z zawartością</span><span class="sxs-lookup"><span data-stu-id="a9090-151"><a name="related-content"> </a>Related content</span></span>
* <span data-ttu-id="a9090-152">[Typowe problemy z konfiguracją sieci podczas konfigurowania APIM w sieci Wirtualnej][Common Network Configuration Issues]</span><span class="sxs-lookup"><span data-stu-id="a9090-152">[Common Network configuration issues while setting up APIM in VNET][Common Network Configuration Issues]</span></span>
* [<span data-ttu-id="a9090-153">Często zadawane pytania dotyczące sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a9090-153">Virtual Network faqs</span></span>](../virtual-network/virtual-networks-faq.md)
* [<span data-ttu-id="a9090-154">Tworzenie rekord w systemie DNS</span><span class="sxs-lookup"><span data-stu-id="a9090-154">Creating A record in DNS</span></span>](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
