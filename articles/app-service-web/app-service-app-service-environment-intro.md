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
# <a name="introduction-tooapp-service-environment-v1"></a>Wprowadzenie tooApp v1 środowiska usługi

> [!NOTE]
> Ten artykuł dotyczy hello v1 środowiska usługi aplikacji.  Istnieje nowsza wersja hello środowiska usługi aplikacji jest łatwiejsze toouse, który jest uruchamiany na bardziej zaawansowanych infrastruktury. więcej informacji na temat nowej wersji hello rozpoczynać hello toolearn [toohello wprowadzenie środowiska usługi aplikacji](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Omówienie
Środowiska usługi aplikacji jest [Premium] [ PremiumTier] opcji plan usługi aplikacji Azure, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować z aplikacjami Azure App Service na dużą skalę, usługa w tym [aplikacje sieci Web][WebApps], [Mobile Apps][MobileApps], i [aplikacje interfejsu API] [ APIApps].  

Środowiska usługi aplikacji to idealne rozwiązanie w przypadku obciążeń aplikacji wymagających:

* Bardzo dużej skali
* Izolacja i bezpiecznego dostępu do sieci

Klienci mogą tworzyć wiele środowisk usługi aplikacji w jednym regionie Azure, a także w wielu regionach platformy Azure.  Dzięki temu można idealne rozwiązanie w przypadku skalowania w poziomie warstwach aplikacji bez stanu, w związku z wysoką obciążeniami RPS środowiska usługi App Service.

Środowiska usługi aplikacji są izolowane toorunning tylko jednego odbiorcy aplikacje i zawsze są wdrażane w sieci wirtualnej.  Klienci mają precyzyjną kontrolę nad zarówno aplikacji dla ruchu przychodzącego i wychodzącego ruchu sieciowego i aplikacji może nawiązywać bezpiecznych połączeń o dużej szybkości za pośrednictwem zasobów firmowych tooon lokalnej sieci wirtualnych.

Wszystkie artykuły i w jaki sposób — do obiektu o środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

Omówienie sposób środowiska usługi App Service włączyć wysoką skalę i zabezpieczania dostępu do sieci, zobacz hello [nowości AzureCon] [ AzureConDeepDive] na środowiska usługi App Service!

Szczegółowo na poziomie odbierającej za pomocą wielu środowiska usługi App Service zawiera artykuł hello na temat toosetup [wpływ aplikacja rozproszona geograficznie][GeodistributedAppFootprint].

toosee, jak pokazano hello nowości AzureCon Architektura zabezpieczeń hello został skonfigurowany, zobacz artykuł hello na implementacji [warstwie Architektura zabezpieczeń](app-service-app-service-environment-layered-security.md) ze środowiska usługi App Service.

Aplikacje działające w środowisku usługi aplikacji może mieć ich dostęp uzyskiwany za nadrzędnego urządzenia, takie jak zapory aplikacji sieci web (WAF).  Artykuł Hello na [Konfigurowanie zapory aplikacji sieci Web dla środowiska usługi App Service](app-service-app-service-environment-web-application-firewall.md) obejmuje tego scenariusza. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a>Zasoby obliczeniowe dedykowane
Wszystkie hello zasobów obliczeniowych, zasobów w środowisku usługi aplikacji są wyłącznie tooa jednej subskrypcji w wersji dedykowanej i środowiska usługi aplikacji można skonfigurować za pomocą zasobów obliczeniowych toofifty (50) do wyłącznego użytku przez jedną aplikację.

Środowiska usługi aplikacji składa się z puli zasobów obliczeniowych frontonu, jak również pul zasobów obliczeniowych proces roboczy co toothree. 

Pula frontonu Hello zawiera zasoby obliczeniowe odpowiedzialny za kończenia żądań SSL, jak również automatyczne równoważenie obciążenia żądań aplikacji w środowisku usługi aplikacji. 

Każda pula procesu roboczego zawiera zasoby obliczeniowe przydzielone za[plany usługi App Service][AppServicePlan], które z kolei zawierają co najmniej jedną aplikację usługi Azure App Service.  Ponieważ może istnieć zapasowej pule procesów roboczych różnych toothree w środowisku usługi aplikacji, masz hello elastyczność toochoose obliczeń różnych zasobów dla każdej puli procesów roboczych.  

Na przykład umożliwia toocreate jednego procesu roboczego puli z słabszy zasoby obliczeniowe dla plany usługi App Service przeznaczonego dla rozwoju lub testowania aplikacji.  Puli procesów roboczych drugi (lub nawet trzeci) można użyć bardziej zaawansowanych zasoby obliczeniowe, przeznaczony dla plany usługi App Service uruchamianie aplikacji w środowisku produkcyjnym.

Więcej szczegółów na powitania ilość obliczeniowego zasoby dostępne toohello frontonu i pule procesów roboczych, zobacz [jak tooConfigure środowiska usługi aplikacji][HowToConfigureanAppServiceEnvironment].  

Aby uzyskać szczegółowe informacje o dostępnych hello obliczeniowe rozmiary zasobów obsługiwane w środowisku usługi aplikacji, zapoznaj się z pomocą techniczną firmy hello [App Service — ceny] [ AppServicePricing] strony i przejrzyj dostępne opcje powitania dla środowiska usługi App Service w warstwie cenowej Premium hello.

## <a name="virtual-network-support"></a>Obsługa sieci wirtualnej
Środowiska usługi aplikacji mogą być tworzone w **albo** sieci wirtualnej platformy Azure Resource Manager **lub** sieci wirtualnej wdrożenia klasycznego modelu ([więcej informacji o sieciach wirtualnych] [MoreInfoOnVirtualNetworks]).  Ponieważ środowisko usługi aplikacji istnieje zawsze w sieci wirtualnej, a dokładniej w podsieci sieci wirtualnej, można wykorzystać funkcje zabezpieczeń hello toocontrol sieci wirtualnych obu komunikacji sieciowej dla ruchu przychodzącego i wychodzącego.  

Środowiska usługi aplikacji może być albo internetowy, za pomocą publicznego adresu IP lub wewnętrzny ukierunkowane przy użyciu adresu Azure wewnętrznego modułu równoważenia obciążenia (ILB).

Można użyć [sieciowej grupy zabezpieczeń] [ NetworkSecurityGroups] toorestrict przychodzącej komunikacji toohello podsieci, z którym znajduje się środowiska usługi aplikacji.  Dzięki temu aplikacje toorun za nadrzędnego urządzeń i usług, takich jak zapory aplikacji sieci web i dostawców SaaS sieci.

Aplikacje muszą również często tooaccess zasobów firmowych, takich jak wewnętrznej bazy danych i usług sieci web.  Typowym podejściem jest toomake te punkty końcowe ruchu sieciowego dostępne tylko toointernal przepływu w ramach sieci wirtualnej platformy Azure.  Środowiska usługi aplikacji po toohello przyłączone do tej samej sieci wirtualnej co wewnętrzny hello usługi, aplikacje działające w środowisku hello można uzyskać dostępu do ich tym osiągalne za pomocą punktów końcowych [lokacja-lokacja] [ SiteToSite]i [Azure ExpressRoute] [ ExpressRoute] połączenia.

Dla więcej szczegółowych informacji na temat środowiska usługi App Service z sieci wirtualnych i sieci lokalnej, zapoznaj się następujące artykuły powitania [architektury sieci][NetworkArchitectureOverview], [kontrolowanie ruchu przychodzącego Ruch][ControllingInboundTraffic], i [bezpiecznego połączenia tooBackends][SecurelyConnectingToBackends]. 

## <a name="getting-started"></a>Wprowadzenie
tooget wprowadzenie do środowiska usługi App Service, zobacz [jak tooCreate środowiska usługi aplikacji][HowToCreateAnAppServiceEnvironment]

Wszystkie artykuły i w jaki sposób — do użytkownika dla środowiska usługi aplikacji są dostępne w hello [Plik README dla środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service][AzureAppService].

Omówienie architektury sieci środowiska usługi aplikacji hello, zobacz hello [omówienie architektury sieci] [ NetworkArchitectureOverview] artykułu.

Szczegółowe informacje o używaniu środowiska usługi aplikacji z usługi ExpressRoute, możesz znaleźć hello poniższego artykułu [Express Route i środowiska usługi App Service][NetworkConfigDetailsForExpressRoute].

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


