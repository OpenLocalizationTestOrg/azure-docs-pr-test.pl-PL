---
title: "plik readme programu aaaAzure środowiska usługi aplikacji"
description: "Wyświetla listę dokumentacji hello, który opisuje środowiska usługi aplikacji Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 6edc74804ded7497e70c31c9e08252257add4415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a><span data-ttu-id="6167b-103">Dokumentacja środowiska usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="6167b-103">App Service environment documentation</span></span>
 <span data-ttu-id="6167b-104">Środowiska usługi aplikacji Azure to funkcja usługi Azure App Service, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować aplikacji usługi App Service na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="6167b-104">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="6167b-105">Ta funkcja może obsługiwać Twoje [sieci web apps][webapps], [aplikacji mobilnych][mobileapps], [aplikacje interfejsu API][APIApps], i [funkcje][Functions].</span><span class="sxs-lookup"><span data-stu-id="6167b-105">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIApps], and [functions][Functions].</span></span>

<span data-ttu-id="6167b-106">Środowiska usługi aplikacji (ASEs) są idealne rozwiązanie w przypadku obciążeń aplikacji, które wymagają:</span><span class="sxs-lookup"><span data-stu-id="6167b-106">App Service environments (ASEs) are ideal for application workloads that require:</span></span>

* <span data-ttu-id="6167b-107">Bardzo dużej skali.</span><span class="sxs-lookup"><span data-stu-id="6167b-107">Very high scale.</span></span>
* <span data-ttu-id="6167b-108">Izolacja i bezpiecznego dostępu do sieci.</span><span class="sxs-lookup"><span data-stu-id="6167b-108">Isolation and secure network access.</span></span>

<span data-ttu-id="6167b-109">Klienci mogą tworzyć wiele ASEs w pojedynczym regionie Azure i w różnych regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6167b-109">Customers can create multiple ASEs within a single Azure region and across multiple Azure regions.</span></span> <span data-ttu-id="6167b-110">Ta wszechstronność sprawia, że ASEs nadaje się doskonale dla warstwy aplikacji bezstanowych, w związku z wysoką obciążeniami RPS skalowanie w poziomie.</span><span class="sxs-lookup"><span data-stu-id="6167b-110">This versatility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="6167b-111">ASEs są izolowane toorunning tylko jednego odbiorcy aplikacje i zawsze są wdrażane w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6167b-111">ASEs are isolated toorunning only a single customer's applications and are always deployed into an Azure virtual network.</span></span> <span data-ttu-id="6167b-112">Klienci mają precyzyjną kontrolę nad ruchu sieciowego przychodzącego i wychodzącego aplikacji przy użyciu [grup zabezpieczeń sieci][NSGs].</span><span class="sxs-lookup"><span data-stu-id="6167b-112">Customers have fine-grained control over inbound and outbound application network traffic by using [Network Security Groups][NSGs].</span></span> <span data-ttu-id="6167b-113">Aplikacje można również ustanowić bezpiecznych połączeń o dużej szybkości za pośrednictwem zasobów firmowych tooon lokalnej sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6167b-113">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="6167b-114">Aplikacje muszą często tooaccess zasobów firmowych, takich jak wewnętrznej bazy danych i usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="6167b-114">Apps frequently need tooaccess corporate resources, such as internal databases and web services.</span></span> <span data-ttu-id="6167b-115">Dostęp do zasobów za pomocą aplikacji uruchamianych na ASEs [lokacja lokacja] [ SiteToSite] sieci VPN i [Azure ExpressRoute] [ ExpressRoute] połączenia.</span><span class="sxs-lookup"><span data-stu-id="6167b-115">Apps that run on ASEs can access resources via [site-to-site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* <span data-ttu-id="6167b-116">[Co to jest środowisko usługi aplikacji?][Intro]</span><span class="sxs-lookup"><span data-stu-id="6167b-116">[What is an App Service environment?][Intro]</span></span>
* <span data-ttu-id="6167b-117">[Tworzenie środowiska usługi aplikacji][MakeExternalASE]</span><span class="sxs-lookup"><span data-stu-id="6167b-117">[Create an App Service environment][MakeExternalASE]</span></span>
* <span data-ttu-id="6167b-118">[Utworzyć wewnętrznego modułu równoważenia obciążenia środowiska usługi aplikacji][MakeILBASE]</span><span class="sxs-lookup"><span data-stu-id="6167b-118">[Create an internal load balancer App Service environment][MakeILBASE]</span></span>
* <span data-ttu-id="6167b-119">[Użyj środowiska usługi aplikacji][UsingASE]</span><span class="sxs-lookup"><span data-stu-id="6167b-119">[Use an App Service environment][UsingASE]</span></span>
* <span data-ttu-id="6167b-120">[Zagadnienia dotyczące sieci i hello środowiska usługi aplikacji][ASENetwork]</span><span class="sxs-lookup"><span data-stu-id="6167b-120">[Networking considerations and hello App Service environment][ASENetwork]</span></span>
* <span data-ttu-id="6167b-121">[Tworzenie środowiska usługi aplikacji na podstawie szablonu][MakeASEfromTemplate]</span><span class="sxs-lookup"><span data-stu-id="6167b-121">[Create an App Service environment from a template][MakeASEfromTemplate]</span></span>


## <a name="videos"></a><span data-ttu-id="6167b-122">Filmy wideo</span><span class="sxs-lookup"><span data-stu-id="6167b-122">Videos</span></span>
<span data-ttu-id="6167b-123">Wzorzec Modern PaaS dla hello Enterprise z usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="6167b-123">Master Modern PaaS for hello Enterprise with Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

<span data-ttu-id="6167b-124">Wdrażanie wysoce skalowalnych i bezpiecznych aplikacji</span><span class="sxs-lookup"><span data-stu-id="6167b-124">Deploying Highly Scalable and Secure Apps</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

<span data-ttu-id="6167b-125">Uruchamianie aplikacji internetowych i mobilnych w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6167b-125">Running Enterprise Web and Mobile Apps on Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a><span data-ttu-id="6167b-126">Środowisko usługi App Service — wersja 1</span><span class="sxs-lookup"><span data-stu-id="6167b-126">App Service Environment v1</span></span> ##
<span data-ttu-id="6167b-127">Istnieją dwie wersje środowiska usługi aplikacji: ASEv1 i ASEv2.</span><span class="sxs-lookup"><span data-stu-id="6167b-127">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="6167b-128">Aby uzyskać informacje na ASEv1, zobacz [dokumentacji v1 środowiska usługi aplikacji][ASEv1README].</span><span class="sxs-lookup"><span data-stu-id="6167b-128">For information on ASEv1, see [App Service Environment v1 documentation][ASEv1README].</span></span>


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
