---
title: "aaaApp środowiska usługi | Dokumentacja firmy Microsoft"
description: "Co to jest środowisko usługi aplikacji Azure? TooApp wprowadzenie środowiska usługi."
keywords: "środowiska usługi aplikacji Azure, sieci wirtualnej, bezpieczeństwo operacji sieciowych"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 1db5c057-3c56-4537-b580-cdd21fe3f3a7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: stefsch
ms.openlocfilehash: 1b59fed4e5a72d4c4805e1dca203747e07e77103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="3cb77-105">Dokumentacja środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="3cb77-105">App Service Environment Documentation</span></span>
<span data-ttu-id="3cb77-106">Środowiska usługi aplikacji jest [Premium] [ PremiumTier] opcji plan usługi aplikacji Azure, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować z aplikacjami Azure App Service na dużą skalę, usługa w tym [aplikacje sieci Web][WebApps], [Mobile Apps][MobileApps], i [aplikacje interfejsu API] [ APIApps].</span><span class="sxs-lookup"><span data-stu-id="3cb77-106">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="3cb77-107">Środowiska usługi aplikacji to idealne rozwiązanie w przypadku obciążeń aplikacji wymagających:</span><span class="sxs-lookup"><span data-stu-id="3cb77-107">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="3cb77-108">Bardzo dużej skali</span><span class="sxs-lookup"><span data-stu-id="3cb77-108">Very high scale</span></span>
* <span data-ttu-id="3cb77-109">Izolacja i bezpiecznego dostępu do sieci</span><span class="sxs-lookup"><span data-stu-id="3cb77-109">Isolation and secure network access</span></span>

<span data-ttu-id="3cb77-110">Klienci mogą tworzyć wiele środowisk usługi aplikacji w jednym regionie Azure, a także w wielu regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3cb77-110">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="3cb77-111">Dzięki temu można idealne rozwiązanie w przypadku skalowania w poziomie warstwach aplikacji bez stanu, w związku z wysoką obciążeniami RPS środowiska usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="3cb77-111">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="3cb77-112">Środowiska usługi aplikacji są izolowane toorunning tylko jednego odbiorcy aplikacje i zawsze są wdrażane w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3cb77-112">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="3cb77-113">Klienci mają precyzyjną kontrolę nad zarówno dla ruchu przychodzącego i wychodzącego aplikacji sieciowych ruchu przy użyciu [sieciowej grupy zabezpieczeń][NetworkSecurityGroups].</span><span class="sxs-lookup"><span data-stu-id="3cb77-113">Customers have fine-grained control over both inbound and outbound application network traffic using [network security groups][NetworkSecurityGroups].</span></span>  <span data-ttu-id="3cb77-114">Aplikacje można również ustanowić bezpiecznych połączeń o dużej szybkości za pośrednictwem zasobów firmowych tooon lokalnej sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3cb77-114">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="3cb77-115">Aplikacje muszą często tooaccess zasobów firmowych, takich jak wewnętrznej bazy danych i usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="3cb77-115">Apps frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="3cb77-116">Aplikacje działające na środowiska usługi App Service może uzyskiwać dostęp do zasobów osiągalne za pomocą [lokacja-lokacja] [ SiteToSite] sieci VPN i [Azure ExpressRoute] [ ExpressRoute] połączenia.</span><span class="sxs-lookup"><span data-stu-id="3cb77-116">Apps running on App Service Environments can access resources reachable via [Site-to-Site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* [<span data-ttu-id="3cb77-117">Co to jest środowisko usługi App Service?</span><span class="sxs-lookup"><span data-stu-id="3cb77-117">What is an App Service Environment?</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
* [<span data-ttu-id="3cb77-118">Tworzenie środowiska usługi App Service</span><span class="sxs-lookup"><span data-stu-id="3cb77-118">Creating an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="3cb77-119">Tworzenie aplikacji w środowisku usługi App Service</span><span class="sxs-lookup"><span data-stu-id="3cb77-119">Creating Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="3cb77-120">Tworzenie i używanie wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="3cb77-120">Creating and Using an Internal Load Balancer with App Service Environments</span></span>](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [<span data-ttu-id="3cb77-121">Konfigurowanie środowiska usługi App Service</span><span class="sxs-lookup"><span data-stu-id="3cb77-121">Configuring an App Service Environment</span></span>](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [<span data-ttu-id="3cb77-122">Skalowanie aplikacji w środowisku usługi App Service</span><span class="sxs-lookup"><span data-stu-id="3cb77-122">Scaling Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [<span data-ttu-id="3cb77-123">Zabezpieczenia i architektura sieci</span><span class="sxs-lookup"><span data-stu-id="3cb77-123">Network Security and Architecture</span></span>](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a><span data-ttu-id="3cb77-124">Jak firmy</span><span class="sxs-lookup"><span data-stu-id="3cb77-124">How To's</span></span>
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a><span data-ttu-id="3cb77-125">Filmy wideo</span><span class="sxs-lookup"><span data-stu-id="3cb77-125">Videos</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]



<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
