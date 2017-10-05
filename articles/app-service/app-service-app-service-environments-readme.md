---
title: "Środowisko usługi aplikacji | Dokumentacja firmy Microsoft"
description: "Co to jest środowisko usługi aplikacji Azure? Wprowadzenie do środowiska usługi aplikacji."
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
ms.openlocfilehash: 1de3f2c513f4f5ce6fd2ab2b57514122955a9a98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="app-service-environment-documentation"></a>Dokumentacja środowiska usługi aplikacji
Środowiska usługi aplikacji jest [Premium] [ PremiumTier] opcji plan usługi aplikacji Azure, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować z aplikacjami Azure App Service na dużą skalę, usługa w tym [aplikacje sieci Web][WebApps], [Mobile Apps][MobileApps], i [aplikacje interfejsu API] [ APIApps].  

Środowiska usługi aplikacji to idealne rozwiązanie w przypadku obciążeń aplikacji wymagających:

* Bardzo dużej skali
* Izolacja i bezpiecznego dostępu do sieci

Klienci mogą tworzyć wiele środowisk usługi aplikacji w jednym regionie Azure, a także w wielu regionach platformy Azure.  Dzięki temu można idealne rozwiązanie w przypadku skalowania w poziomie warstwach aplikacji bez stanu, w związku z wysoką obciążeniami RPS środowiska usługi App Service.

Środowiska usługi aplikacji są izolowane do uruchamiania tylko jednego odbiorcy aplikacji i zawsze są wdrażane w sieci wirtualnej.  Klienci mają precyzyjną kontrolę nad zarówno dla ruchu przychodzącego i wychodzącego aplikacji sieciowych ruchu przy użyciu [sieciowej grupy zabezpieczeń][NetworkSecurityGroups].  Aplikacje można również ustanowić bezpiecznych połączeń o dużej szybkości za pośrednictwem sieci wirtualnej do zasobów firmy lokalnie.

Aplikacje często muszą uzyskiwać dostęp do zasobów firmy, takich jak wewnętrznej bazy danych i usług sieci web.  Aplikacje działające na środowiska usługi App Service może uzyskiwać dostęp do zasobów osiągalne za pomocą [lokacja-lokacja] [ SiteToSite] sieci VPN i [Azure ExpressRoute] [ ExpressRoute] połączenia.

* [Co to jest środowisko usługi App Service?](../app-service-web/app-service-app-service-environment-intro.md)
* [Tworzenie środowiska usługi App Service](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [Tworzenie aplikacji w środowisku usługi App Service](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Tworzenie i używanie wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [Konfigurowanie środowiska usługi App Service](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [Skalowanie aplikacji w środowisku usługi App Service](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [Zabezpieczenia i architektura sieci](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a>Jak firmy
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a>Filmy wideo
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
