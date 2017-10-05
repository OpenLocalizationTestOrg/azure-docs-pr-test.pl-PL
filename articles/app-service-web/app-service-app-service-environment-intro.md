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
# <a name="introduction-to-app-service-environment-v1"></a>Wprowadzenie do aplikacji usługi v1 środowiska

> [!NOTE]
> Ten artykuł dotyczy v1 środowiska usługi aplikacji.  Istnieje nowsza wersja środowiska usługi aplikacji jest łatwiejsza w użyciu, który jest uruchamiany na bardziej zaawansowanych infrastruktury. Aby dowiedzieć się więcej o nowy początek wersji z [wprowadzenie do środowiska usługi aplikacji](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Omówienie
Środowiska usługi aplikacji jest [Premium] [ PremiumTier] opcji plan usługi aplikacji Azure, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować z aplikacjami Azure App Service na dużą skalę, usługa w tym [aplikacje sieci Web][WebApps], [Mobile Apps][MobileApps], i [aplikacje interfejsu API] [ APIApps].  

Środowiska usługi aplikacji to idealne rozwiązanie w przypadku obciążeń aplikacji wymagających:

* Bardzo dużej skali
* Izolacja i bezpiecznego dostępu do sieci

Klienci mogą tworzyć wiele środowisk usługi aplikacji w jednym regionie Azure, a także w wielu regionach platformy Azure.  Dzięki temu można idealne rozwiązanie w przypadku skalowania w poziomie warstwach aplikacji bez stanu, w związku z wysoką obciążeniami RPS środowiska usługi App Service.

Środowiska usługi aplikacji są izolowane do uruchamiania tylko jednego odbiorcy aplikacji i zawsze są wdrażane w sieci wirtualnej.  Klienci mają precyzyjną kontrolę nad zarówno aplikacji dla ruchu przychodzącego i wychodzącego ruchu sieciowego i aplikacji może nawiązywać bezpiecznych połączeń o dużej szybkości za pośrednictwem sieci wirtualnej do zasobów firmy lokalnie.

Wszystkie artykuły i w jaki sposób — do obiektu o środowiska usługi aplikacji są dostępne w [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

Omówienie sposób środowiska usługi App Service włączyć wysoką skalę i zabezpieczania dostępu do sieci, zobacz [nowości AzureCon] [ AzureConDeepDive] na środowiska usługi App Service!

Szczegółowo na poziomie odbierającej za pomocą wielu środowiska usługi App Service w artykule na temat sposobu instalacji [wpływ aplikacja rozproszona geograficznie][GeodistributedAppFootprint].

Aby zobaczyć, jak pokazano nowości AzureCon architektury zabezpieczeń został skonfigurowany, zobacz artykuł na implementacji [warstwie Architektura zabezpieczeń](app-service-app-service-environment-layered-security.md) ze środowiska usługi App Service.

Aplikacje działające w środowisku usługi aplikacji może mieć ich dostęp uzyskiwany za nadrzędnego urządzenia, takie jak zapory aplikacji sieci web (WAF).  Artykuł na temat [Konfigurowanie zapory aplikacji sieci Web dla środowiska usługi App Service](app-service-app-service-environment-web-application-firewall.md) obejmuje tego scenariusza. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a>Zasoby obliczeniowe dedykowane
Wszystkie zasoby obliczeniowe, w środowisku usługi aplikacji dedykowane wyłącznie jedną subskrypcją i środowiska usługi aplikacji można skonfigurować maksymalnie 50 (50) zasoby obliczeniowe do wyłącznego użytku przez jedną aplikację.

Środowiska usługi aplikacji składa się z puli zasobów obliczeniowych frontonu, jak również pule zasobów obliczeniowych procesów roboczych jednej do trzech. 

Frontonu pula zawiera zasoby obliczeniowe odpowiedzialny za kończenia żądań SSL, jak również automatyczne równoważenie obciążenia żądań aplikacji w środowisku usługi aplikacji. 

Każda pula procesu roboczego zawiera zasoby obliczeniowe przydzielone do [plany usługi App Service][AppServicePlan], które z kolei zawierają co najmniej jedną aplikację usługi Azure App Service.  Ponieważ może istnieć maksymalnie trzy pule procesów roboczych różnych w środowisku usługi aplikacji, należy wybrać zasoby obliczeniowe różnych dla każdej puli procesów roboczych.  

Na przykład dzięki temu można utworzyć jeden puli procesów roboczych z słabszy zasoby obliczeniowe dla plany usługi App Service przeznaczonego dla rozwoju lub testowania aplikacji.  Puli procesów roboczych drugi (lub nawet trzeci) można użyć bardziej zaawansowanych zasoby obliczeniowe, przeznaczony dla plany usługi App Service uruchamianie aplikacji w środowisku produkcyjnym.

Aby uzyskać więcej szczegółowych informacji na temat ilości zasobów obliczeniowych dostępnych do pul frontonu i proces roboczy, zobacz [sposobu konfigurowania środowiska usługi aplikacji][HowToConfigureanAppServiceEnvironment].  

Aby uzyskać więcej informacji na temat rozmiarów zasobów obliczeniowych dostępnych obsługiwane w środowisku usługi aplikacji, zapoznaj się [App Service — ceny] [ AppServicePricing] strony i przejrzyj opcje dostępne dla środowiska usługi aplikacji Warstwa cenowa Premium.

## <a name="virtual-network-support"></a>Obsługa sieci wirtualnej
Środowiska usługi aplikacji mogą być tworzone w **albo** sieci wirtualnej platformy Azure Resource Manager **lub** sieci wirtualnej wdrożenia klasycznego modelu ([więcej informacji o sieciach wirtualnych] [MoreInfoOnVirtualNetworks]).  Ponieważ środowisko usługi aplikacji istnieje zawsze w sieci wirtualnej, a dokładniej w podsieci sieci wirtualnej, można korzystać z funkcji zabezpieczeń sieci wirtualnych do kontrolowania komunikacji zarówno ruchu przychodzącego i wychodzącego.  

Środowiska usługi aplikacji może być albo internetowy, za pomocą publicznego adresu IP lub wewnętrzny ukierunkowane przy użyciu adresu Azure wewnętrznego modułu równoważenia obciążenia (ILB).

Można użyć [sieciowej grupy zabezpieczeń] [ NetworkSecurityGroups] do ograniczenia komunikacji sieciowej dla ruchu przychodzącego do podsieci, w której znajduje się środowiska usługi aplikacji.  Dzięki temu można korzystać z aplikacji za nadrzędnego urządzeń i usług, takich jak zapory aplikacji sieci web i dostawców SaaS sieci.

Aplikacje muszą również często dostępu do zasobów firmy, takich jak wewnętrznej bazy danych i usług sieci web.  Typowym podejściem jest, aby udostępnić te punkty końcowe tylko ruchu w sieci wewnętrznej przepływu w ramach sieci wirtualnej platformy Azure.  Po środowiska usługi aplikacji jest dołączony do tej samej sieci wirtualnej co wewnętrzny usługi, aplikacje działające w środowisku może uzyskiwać do nich dostęp, łącznie z punktów końcowych osiągalne za pomocą [lokacja-lokacja] [ SiteToSite] i [Azure ExpressRoute] [ ExpressRoute] połączenia.

Dla więcej szczegółowych informacji na temat środowiska usługi App Service z sieciami wirtualnymi i sieciami lokalnymi zapoznaj się następujące artykuły na [architektury sieci][NetworkArchitectureOverview], [kontrolowanie ruchu przychodzącego Ruch][ControllingInboundTraffic], i [bezpiecznego połączenia Zapleczy][SecurelyConnectingToBackends]. 

## <a name="getting-started"></a>Wprowadzenie
Wprowadzenie do środowiska usługi App Service, zobacz [jak do tworzenia środowiska usługi aplikacji][HowToCreateAnAppServiceEnvironment]

Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

Aby uzyskać więcej informacji o platformie usługi Azure App Service, zobacz [usłudze Azure App Service][AzureAppService].

Omówienie architektury sieci środowiska usługi aplikacji, zobacz [omówienie architektury sieci] [ NetworkArchitectureOverview] artykułu.

Aby uzyskać więcej informacji o używaniu środowiska usługi aplikacji z usługi ExpressRoute, zobacz następujący artykuł w [Express Route i środowiska usługi App Service][NetworkConfigDetailsForExpressRoute].

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


