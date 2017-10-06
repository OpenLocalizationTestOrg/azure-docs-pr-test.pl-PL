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
# <a name="app-service-environment-documentation"></a>Dokumentacja środowiska usługi aplikacji
 Środowiska usługi aplikacji Azure to funkcja usługi Azure App Service, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować aplikacji usługi App Service na dużą skalę. Ta funkcja może obsługiwać Twoje [sieci web apps][webapps], [aplikacji mobilnych][mobileapps], [aplikacje interfejsu API][APIApps], i [funkcje][Functions].

Środowiska usługi aplikacji (ASEs) są idealne rozwiązanie w przypadku obciążeń aplikacji, które wymagają:

* Bardzo dużej skali.
* Izolacja i bezpiecznego dostępu do sieci.

Klienci mogą tworzyć wiele ASEs w pojedynczym regionie Azure i w różnych regionach platformy Azure. Ta wszechstronność sprawia, że ASEs nadaje się doskonale dla warstwy aplikacji bezstanowych, w związku z wysoką obciążeniami RPS skalowanie w poziomie.

ASEs są izolowane toorunning tylko jednego odbiorcy aplikacje i zawsze są wdrażane w sieci wirtualnej platformy Azure. Klienci mają precyzyjną kontrolę nad ruchu sieciowego przychodzącego i wychodzącego aplikacji przy użyciu [grup zabezpieczeń sieci][NSGs]. Aplikacje można również ustanowić bezpiecznych połączeń o dużej szybkości za pośrednictwem zasobów firmowych tooon lokalnej sieci wirtualnych.

Aplikacje muszą często tooaccess zasobów firmowych, takich jak wewnętrznej bazy danych i usług sieci web. Dostęp do zasobów za pomocą aplikacji uruchamianych na ASEs [lokacja lokacja] [ SiteToSite] sieci VPN i [Azure ExpressRoute] [ ExpressRoute] połączenia.

* [Co to jest środowisko usługi aplikacji?][Intro]
* [Tworzenie środowiska usługi aplikacji][MakeExternalASE]
* [Utworzyć wewnętrznego modułu równoważenia obciążenia środowiska usługi aplikacji][MakeILBASE]
* [Użyj środowiska usługi aplikacji][UsingASE]
* [Zagadnienia dotyczące sieci i hello środowiska usługi aplikacji][ASENetwork]
* [Tworzenie środowiska usługi aplikacji na podstawie szablonu][MakeASEfromTemplate]


## <a name="videos"></a>Filmy wideo
Wzorzec Modern PaaS dla hello Enterprise z usługi aplikacji Azure
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

Wdrażanie wysoce skalowalnych i bezpiecznych aplikacji
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

Uruchamianie aplikacji internetowych i mobilnych w usłudze Azure App Service
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a>Środowisko usługi App Service — wersja 1 ##
Istnieją dwie wersje środowiska usługi aplikacji: ASEv1 i ASEv2. Aby uzyskać informacje na ASEv1, zobacz [dokumentacji v1 środowiska usługi aplikacji][ASEv1README].


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
