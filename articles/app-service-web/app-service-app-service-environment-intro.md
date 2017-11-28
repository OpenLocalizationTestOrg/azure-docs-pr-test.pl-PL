---
title: "tooApp aaaIntroduction v1 środowiska usługi"
description: "Więcej informacji na temat funkcji hello v1 środowiska usługi aplikacji, która zawiera jednostki skalowania bezpieczne przyłączone do sieci wirtualnej, dedykowane do uruchamiania wszystkich aplikacji."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a><span data-ttu-id="6e3a9-103">Wprowadzenie tooApp v1 środowiska usługi</span><span class="sxs-lookup"><span data-stu-id="6e3a9-103">Introduction tooApp Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="6e3a9-104">Ten artykuł dotyczy hello v1 środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="6e3a9-105">Istnieje nowsza wersja hello środowiska usługi aplikacji jest łatwiejsze toouse, który jest uruchamiany na bardziej zaawansowanych infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="6e3a9-106">więcej informacji na temat nowej wersji hello rozpoczynać hello toolearn [toohello wprowadzenie środowiska usługi aplikacji](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="6e3a9-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="6e3a9-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6e3a9-107">Overview</span></span>
<span data-ttu-id="6e3a9-108">Środowiska usługi aplikacji jest [Premium] [ PremiumTier] opcji plan usługi aplikacji Azure, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować z aplikacjami Azure App Service na dużą skalę, usługa w tym [aplikacje sieci Web][WebApps], [Mobile Apps][MobileApps], i [aplikacje interfejsu API] [ APIApps].</span><span class="sxs-lookup"><span data-stu-id="6e3a9-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="6e3a9-109">Środowiska usługi aplikacji to idealne rozwiązanie w przypadku obciążeń aplikacji wymagających:</span><span class="sxs-lookup"><span data-stu-id="6e3a9-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="6e3a9-110">Bardzo dużej skali</span><span class="sxs-lookup"><span data-stu-id="6e3a9-110">Very high scale</span></span>
* <span data-ttu-id="6e3a9-111">Izolacja i bezpiecznego dostępu do sieci</span><span class="sxs-lookup"><span data-stu-id="6e3a9-111">Isolation and secure network access</span></span>

<span data-ttu-id="6e3a9-112">Klienci mogą tworzyć wiele środowisk usługi aplikacji w jednym regionie Azure, a także w wielu regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="6e3a9-113">Dzięki temu można idealne rozwiązanie w przypadku skalowania w poziomie warstwach aplikacji bez stanu, w związku z wysoką obciążeniami RPS środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="6e3a9-114">Środowiska usługi aplikacji są izolowane toorunning tylko jednego odbiorcy aplikacje i zawsze są wdrażane w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-114">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="6e3a9-115">Klienci mają precyzyjną kontrolę nad zarówno aplikacji dla ruchu przychodzącego i wychodzącego ruchu sieciowego i aplikacji może nawiązywać bezpiecznych połączeń o dużej szybkości za pośrednictwem zasobów firmowych tooon lokalnej sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="6e3a9-116">Wszystkie artykuły i w jaki sposób — do obiektu o środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="6e3a9-116">All articles and How-To's about App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="6e3a9-117">Omówienie sposób środowiska usługi App Service włączyć wysoką skalę i zabezpieczania dostępu do sieci, zobacz hello [nowości AzureCon] [ AzureConDeepDive] na środowiska usługi App Service!</span><span class="sxs-lookup"><span data-stu-id="6e3a9-117">For an overview of how App Service Environments enable high scale and secure network access, see hello [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="6e3a9-118">Szczegółowo na poziomie odbierającej za pomocą wielu środowiska usługi App Service zawiera artykuł hello na temat toosetup [wpływ aplikacja rozproszona geograficznie][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="6e3a9-118">For a deep-dive on horizontally scaling using multiple App Service Environments see hello article on how toosetup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="6e3a9-119">toosee, jak pokazano hello nowości AzureCon Architektura zabezpieczeń hello został skonfigurowany, zobacz artykuł hello na implementacji [warstwie Architektura zabezpieczeń](app-service-app-service-environment-layered-security.md) ze środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-119">toosee how hello security architecture shown in hello AzureCon Deep Dive was configured, see hello article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="6e3a9-120">Aplikacje działające w środowisku usługi aplikacji może mieć ich dostęp uzyskiwany za nadrzędnego urządzenia, takie jak zapory aplikacji sieci web (WAF).</span><span class="sxs-lookup"><span data-stu-id="6e3a9-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="6e3a9-121">Artykuł Hello na [Konfigurowanie zapory aplikacji sieci Web dla środowiska usługi App Service](app-service-app-service-environment-web-application-firewall.md) obejmuje tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-121">hello article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="6e3a9-122">Zasoby obliczeniowe dedykowane</span><span class="sxs-lookup"><span data-stu-id="6e3a9-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="6e3a9-123">Wszystkie hello zasobów obliczeniowych, zasobów w środowisku usługi aplikacji są wyłącznie tooa jednej subskrypcji w wersji dedykowanej i środowiska usługi aplikacji można skonfigurować za pomocą zasobów obliczeniowych toofifty (50) do wyłącznego użytku przez jedną aplikację.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-123">All of hello compute resources in an App Service Environment are dedicated exclusively tooa single subscription, and an App Service Environment can be configured with up toofifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="6e3a9-124">Środowiska usługi aplikacji składa się z puli zasobów obliczeniowych frontonu, jak również pul zasobów obliczeniowych proces roboczy co toothree.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-124">An App Service Environment is composed of a front-end compute resource pool, as well as one toothree worker compute resource pools.</span></span> 

<span data-ttu-id="6e3a9-125">Pula frontonu Hello zawiera zasoby obliczeniowe odpowiedzialny za kończenia żądań SSL, jak również automatyczne równoważenie obciążenia żądań aplikacji w środowisku usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-125">hello front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="6e3a9-126">Każda pula procesu roboczego zawiera zasoby obliczeniowe przydzielone za[plany usługi App Service][AppServicePlan], które z kolei zawierają co najmniej jedną aplikację usługi Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-126">Each worker pool contains compute resources allocated too[App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="6e3a9-127">Ponieważ może istnieć zapasowej pule procesów roboczych różnych toothree w środowisku usługi aplikacji, masz hello elastyczność toochoose obliczeń różnych zasobów dla każdej puli procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-127">Since there can be up toothree different worker pools in an App Service Environment, you have hello flexibility toochoose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="6e3a9-128">Na przykład umożliwia toocreate jednego procesu roboczego puli z słabszy zasoby obliczeniowe dla plany usługi App Service przeznaczonego dla rozwoju lub testowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-128">For example, this allows you toocreate one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="6e3a9-129">Puli procesów roboczych drugi (lub nawet trzeci) można użyć bardziej zaawansowanych zasoby obliczeniowe, przeznaczony dla plany usługi App Service uruchamianie aplikacji w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="6e3a9-130">Więcej szczegółów na powitania ilość obliczeniowego zasoby dostępne toohello frontonu i pule procesów roboczych, zobacz [jak tooConfigure środowiska usługi aplikacji][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="6e3a9-130">For more details on hello quantity of compute resources available toohello front-end and worker pools, see [How tooConfigure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="6e3a9-131">Aby uzyskać szczegółowe informacje o dostępnych hello obliczeniowe rozmiary zasobów obsługiwane w środowisku usługi aplikacji, zapoznaj się z pomocą techniczną firmy hello [App Service — ceny] [ AppServicePricing] strony i przejrzyj dostępne opcje powitania dla środowiska usługi App Service w warstwie cenowej Premium hello.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-131">For details on hello available compute resource sizes supported in an App Service Environment, consult hello [App Service Pricing][AppServicePricing] page and review hello available options for App Service Environments in hello Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="6e3a9-132">Obsługa sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="6e3a9-132">Virtual Network Support</span></span>
<span data-ttu-id="6e3a9-133">Środowiska usługi aplikacji mogą być tworzone w **albo** sieci wirtualnej platformy Azure Resource Manager **lub** sieci wirtualnej wdrożenia klasycznego modelu ([więcej informacji o sieciach wirtualnych] [MoreInfoOnVirtualNetworks]).</span><span class="sxs-lookup"><span data-stu-id="6e3a9-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="6e3a9-134">Ponieważ środowisko usługi aplikacji istnieje zawsze w sieci wirtualnej, a dokładniej w podsieci sieci wirtualnej, można wykorzystać funkcje zabezpieczeń hello toocontrol sieci wirtualnych obu komunikacji sieciowej dla ruchu przychodzącego i wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage hello security features of virtual networks toocontrol both inbound and outbound network communications.</span></span>  

<span data-ttu-id="6e3a9-135">Środowiska usługi aplikacji może być albo internetowy, za pomocą publicznego adresu IP lub wewnętrzny ukierunkowane przy użyciu adresu Azure wewnętrznego modułu równoważenia obciążenia (ILB).</span><span class="sxs-lookup"><span data-stu-id="6e3a9-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="6e3a9-136">Można użyć [sieciowej grupy zabezpieczeń] [ NetworkSecurityGroups] toorestrict przychodzącej komunikacji toohello podsieci, z którym znajduje się środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-136">You can use [network security groups][NetworkSecurityGroups] toorestrict inbound network communications toohello subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="6e3a9-137">Dzięki temu aplikacje toorun za nadrzędnego urządzeń i usług, takich jak zapory aplikacji sieci web i dostawców SaaS sieci.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-137">This allows you toorun apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="6e3a9-138">Aplikacje muszą również często tooaccess zasobów firmowych, takich jak wewnętrznej bazy danych i usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-138">Apps also frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="6e3a9-139">Typowym podejściem jest toomake te punkty końcowe ruchu sieciowego dostępne tylko toointernal przepływu w ramach sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-139">A common approach is toomake these endpoints available only toointernal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="6e3a9-140">Środowiska usługi aplikacji po toohello przyłączone do tej samej sieci wirtualnej co wewnętrzny hello usługi, aplikacje działające w środowisku hello można uzyskać dostępu do ich tym osiągalne za pomocą punktów końcowych [lokacja-lokacja] [ SiteToSite]i [Azure ExpressRoute] [ ExpressRoute] połączenia.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-140">Once an App Service Environment is joined toohello same virtual network as hello internal services, apps running in hello environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="6e3a9-141">Dla więcej szczegółowych informacji na temat środowiska usługi App Service z sieci wirtualnych i sieci lokalnej, zapoznaj się następujące artykuły powitania [architektury sieci][NetworkArchitectureOverview], [kontrolowanie ruchu przychodzącego Ruch][ControllingInboundTraffic], i [bezpiecznego połączenia tooBackends][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="6e3a9-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult hello following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting tooBackends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="6e3a9-142">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="6e3a9-142">Getting started</span></span>
<span data-ttu-id="6e3a9-143">tooget wprowadzenie do środowiska usługi App Service, zobacz [jak tooCreate środowiska usługi aplikacji][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="6e3a9-143">tooget started with App Service Environments, see [How tooCreate An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="6e3a9-144">Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="6e3a9-144">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="6e3a9-145">Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="6e3a9-145">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="6e3a9-146">Omówienie architektury sieci środowiska usługi aplikacji hello, zobacz hello [omówienie architektury sieci] [ NetworkArchitectureOverview] artykułu.</span><span class="sxs-lookup"><span data-stu-id="6e3a9-146">For an overview of hello App Service Environment network architecture, see hello [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="6e3a9-147">Szczegółowe informacje o używaniu środowiska usługi aplikacji z usługi ExpressRoute, możesz znaleźć hello poniższego artykułu [Express Route i środowiska usługi App Service][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="6e3a9-147">For details on using an App Service Environment with ExpressRoute, see hello following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


