---
title: "Wprowadzenie do aplikacji usługi v1 środowiska"
description: "Więcej informacji na temat funkcji v1 środowiska usługi aplikacji, która zawiera jednostki skalowania bezpieczne przyłączone do sieci wirtualnej, dedykowane do uruchamiania wszystkich aplikacji."
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
ms.openlocfilehash: 38cb79eb32bd61cdbfb6da91d50e6713d71a2b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="introduction-to-app-service-environment-v1"></a><span data-ttu-id="87314-103">Wprowadzenie do aplikacji usługi v1 środowiska</span><span class="sxs-lookup"><span data-stu-id="87314-103">Introduction to App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="87314-104">Ten artykuł dotyczy v1 środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87314-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="87314-105">Istnieje nowsza wersja środowiska usługi aplikacji jest łatwiejsza w użyciu, który jest uruchamiany na bardziej zaawansowanych infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="87314-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="87314-106">Aby dowiedzieć się więcej o nowy początek wersji z [wprowadzenie do środowiska usługi aplikacji](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="87314-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="87314-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="87314-107">Overview</span></span>
<span data-ttu-id="87314-108">Środowiska usługi aplikacji jest [Premium] [ PremiumTier] opcji plan usługi aplikacji Azure, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować z aplikacjami Azure App Service na dużą skalę, usługa w tym [aplikacje sieci Web][WebApps], [Mobile Apps][MobileApps], i [aplikacje interfejsu API] [ APIApps].</span><span class="sxs-lookup"><span data-stu-id="87314-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="87314-109">Środowiska usługi aplikacji to idealne rozwiązanie w przypadku obciążeń aplikacji wymagających:</span><span class="sxs-lookup"><span data-stu-id="87314-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="87314-110">Bardzo dużej skali</span><span class="sxs-lookup"><span data-stu-id="87314-110">Very high scale</span></span>
* <span data-ttu-id="87314-111">Izolacja i bezpiecznego dostępu do sieci</span><span class="sxs-lookup"><span data-stu-id="87314-111">Isolation and secure network access</span></span>

<span data-ttu-id="87314-112">Klienci mogą tworzyć wiele środowisk usługi aplikacji w jednym regionie Azure, a także w wielu regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="87314-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="87314-113">Dzięki temu można idealne rozwiązanie w przypadku skalowania w poziomie warstwach aplikacji bez stanu, w związku z wysoką obciążeniami RPS środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="87314-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="87314-114">Środowiska usługi aplikacji są izolowane do uruchamiania tylko jednego odbiorcy aplikacji i zawsze są wdrażane w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="87314-114">App Service Environments are isolated to running only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="87314-115">Klienci mają precyzyjną kontrolę nad zarówno aplikacji dla ruchu przychodzącego i wychodzącego ruchu sieciowego i aplikacji może nawiązywać bezpiecznych połączeń o dużej szybkości za pośrednictwem sieci wirtualnej do zasobów firmy lokalnie.</span><span class="sxs-lookup"><span data-stu-id="87314-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="87314-116">Wszystkie artykuły i w jaki sposób — do obiektu o środowiska usługi aplikacji są dostępne w [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="87314-116">All articles and How-To's about App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="87314-117">Omówienie sposób środowiska usługi App Service włączyć wysoką skalę i zabezpieczania dostępu do sieci, zobacz [nowości AzureCon] [ AzureConDeepDive] na środowiska usługi App Service!</span><span class="sxs-lookup"><span data-stu-id="87314-117">For an overview of how App Service Environments enable high scale and secure network access, see the [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="87314-118">Szczegółowo na poziomie odbierającej za pomocą wielu środowiska usługi App Service w artykule na temat sposobu instalacji [wpływ aplikacja rozproszona geograficznie][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="87314-118">For a deep-dive on horizontally scaling using multiple App Service Environments see the article on how to setup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="87314-119">Aby zobaczyć, jak pokazano nowości AzureCon architektury zabezpieczeń został skonfigurowany, zobacz artykuł na implementacji [warstwie Architektura zabezpieczeń](app-service-app-service-environment-layered-security.md) ze środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="87314-119">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="87314-120">Aplikacje działające w środowisku usługi aplikacji może mieć ich dostęp uzyskiwany za nadrzędnego urządzenia, takie jak zapory aplikacji sieci web (WAF).</span><span class="sxs-lookup"><span data-stu-id="87314-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="87314-121">Artykuł na temat [Konfigurowanie zapory aplikacji sieci Web dla środowiska usługi App Service](app-service-app-service-environment-web-application-firewall.md) obejmuje tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="87314-121">The article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="87314-122">Zasoby obliczeniowe dedykowane</span><span class="sxs-lookup"><span data-stu-id="87314-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="87314-123">Wszystkie zasoby obliczeniowe, w środowisku usługi aplikacji dedykowane wyłącznie jedną subskrypcją i środowiska usługi aplikacji można skonfigurować maksymalnie 50 (50) zasoby obliczeniowe do wyłącznego użytku przez jedną aplikację.</span><span class="sxs-lookup"><span data-stu-id="87314-123">All of the compute resources in an App Service Environment are dedicated exclusively to a single subscription, and an App Service Environment can be configured with up to fifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="87314-124">Środowiska usługi aplikacji składa się z puli zasobów obliczeniowych frontonu, jak również pule zasobów obliczeniowych procesów roboczych jednej do trzech.</span><span class="sxs-lookup"><span data-stu-id="87314-124">An App Service Environment is composed of a front-end compute resource pool, as well as one to three worker compute resource pools.</span></span> 

<span data-ttu-id="87314-125">Frontonu pula zawiera zasoby obliczeniowe odpowiedzialny za kończenia żądań SSL, jak również automatyczne równoważenie obciążenia żądań aplikacji w środowisku usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87314-125">The front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="87314-126">Każda pula procesu roboczego zawiera zasoby obliczeniowe przydzielone do [plany usługi App Service][AppServicePlan], które z kolei zawierają co najmniej jedną aplikację usługi Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="87314-126">Each worker pool contains compute resources allocated to [App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="87314-127">Ponieważ może istnieć maksymalnie trzy pule procesów roboczych różnych w środowisku usługi aplikacji, należy wybrać zasoby obliczeniowe różnych dla każdej puli procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="87314-127">Since there can be up to three different worker pools in an App Service Environment, you have the flexibility to choose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="87314-128">Na przykład dzięki temu można utworzyć jeden puli procesów roboczych z słabszy zasoby obliczeniowe dla plany usługi App Service przeznaczonego dla rozwoju lub testowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87314-128">For example, this allows you to create one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="87314-129">Puli procesów roboczych drugi (lub nawet trzeci) można użyć bardziej zaawansowanych zasoby obliczeniowe, przeznaczony dla plany usługi App Service uruchamianie aplikacji w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="87314-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="87314-130">Aby uzyskać więcej szczegółowych informacji na temat ilości zasobów obliczeniowych dostępnych do pul frontonu i proces roboczy, zobacz [sposobu konfigurowania środowiska usługi aplikacji][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="87314-130">For more details on the quantity of compute resources available to the front-end and worker pools, see [How To Configure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="87314-131">Aby uzyskać więcej informacji na temat rozmiarów zasobów obliczeniowych dostępnych obsługiwane w środowisku usługi aplikacji, zapoznaj się [App Service — ceny] [ AppServicePricing] strony i przejrzyj opcje dostępne dla środowiska usługi aplikacji Warstwa cenowa Premium.</span><span class="sxs-lookup"><span data-stu-id="87314-131">For details on the available compute resource sizes supported in an App Service Environment, consult the [App Service Pricing][AppServicePricing] page and review the available options for App Service Environments in the Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="87314-132">Obsługa sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="87314-132">Virtual Network Support</span></span>
<span data-ttu-id="87314-133">Środowiska usługi aplikacji mogą być tworzone w **albo** sieci wirtualnej platformy Azure Resource Manager **lub** sieci wirtualnej wdrożenia klasycznego modelu ([więcej informacji o sieciach wirtualnych] [MoreInfoOnVirtualNetworks]).</span><span class="sxs-lookup"><span data-stu-id="87314-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="87314-134">Ponieważ środowisko usługi aplikacji istnieje zawsze w sieci wirtualnej, a dokładniej w podsieci sieci wirtualnej, można korzystać z funkcji zabezpieczeń sieci wirtualnych do kontrolowania komunikacji zarówno ruchu przychodzącego i wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="87314-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage the security features of virtual networks to control both inbound and outbound network communications.</span></span>  

<span data-ttu-id="87314-135">Środowiska usługi aplikacji może być albo internetowy, za pomocą publicznego adresu IP lub wewnętrzny ukierunkowane przy użyciu adresu Azure wewnętrznego modułu równoważenia obciążenia (ILB).</span><span class="sxs-lookup"><span data-stu-id="87314-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="87314-136">Można użyć [sieciowej grupy zabezpieczeń] [ NetworkSecurityGroups] do ograniczenia komunikacji sieciowej dla ruchu przychodzącego do podsieci, w której znajduje się środowiska usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87314-136">You can use [network security groups][NetworkSecurityGroups] to restrict inbound network communications to the subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="87314-137">Dzięki temu można korzystać z aplikacji za nadrzędnego urządzeń i usług, takich jak zapory aplikacji sieci web i dostawców SaaS sieci.</span><span class="sxs-lookup"><span data-stu-id="87314-137">This allows you to run apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="87314-138">Aplikacje muszą również często dostępu do zasobów firmy, takich jak wewnętrznej bazy danych i usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="87314-138">Apps also frequently need to access corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="87314-139">Typowym podejściem jest, aby udostępnić te punkty końcowe tylko ruchu w sieci wewnętrznej przepływu w ramach sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="87314-139">A common approach is to make these endpoints available only to internal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="87314-140">Po środowiska usługi aplikacji jest dołączony do tej samej sieci wirtualnej co wewnętrzny usługi, aplikacje działające w środowisku może uzyskiwać do nich dostęp, łącznie z punktów końcowych osiągalne za pomocą [lokacja-lokacja] [ SiteToSite] i [Azure ExpressRoute] [ ExpressRoute] połączenia.</span><span class="sxs-lookup"><span data-stu-id="87314-140">Once an App Service Environment is joined to the same virtual network as the internal services, apps running in the environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="87314-141">Dla więcej szczegółowych informacji na temat środowiska usługi App Service z sieciami wirtualnymi i sieciami lokalnymi zapoznaj się następujące artykuły na [architektury sieci][NetworkArchitectureOverview], [kontrolowanie ruchu przychodzącego Ruch][ControllingInboundTraffic], i [bezpiecznego połączenia Zapleczy][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="87314-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult the following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting to Backends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="87314-142">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="87314-142">Getting started</span></span>
<span data-ttu-id="87314-143">Wprowadzenie do środowiska usługi App Service, zobacz [jak do tworzenia środowiska usługi aplikacji][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="87314-143">To get started with App Service Environments, see [How To Create An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="87314-144">Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="87314-144">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="87314-145">Aby uzyskać więcej informacji o platformie usługi Azure App Service, zobacz [usłudze Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="87314-145">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="87314-146">Omówienie architektury sieci środowiska usługi aplikacji, zobacz [omówienie architektury sieci] [ NetworkArchitectureOverview] artykułu.</span><span class="sxs-lookup"><span data-stu-id="87314-146">For an overview of the App Service Environment network architecture, see the [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="87314-147">Aby uzyskać więcej informacji o używaniu środowiska usługi aplikacji z usługi ExpressRoute, zobacz następujący artykuł w [Express Route i środowiska usługi App Service][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="87314-147">For details on using an App Service Environment with ExpressRoute, see the following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

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


