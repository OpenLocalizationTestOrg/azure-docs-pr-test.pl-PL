---
title: "aaaAzure usługi aplikacji — dla aplikacji interfejsu API, mobilne i sieci web | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa Azure App Service ułatwia opracowywanie i wdrażanie Aplikacji sieci Web i aplikacji mobilnych oraz zarządzanie nimi."
keywords: "app service, azure app service, koszt usługi app service, skala, skalowalny, wdrażanie aplikacji, wdrażanie aplikacji azure, paas, platforma jako usługa, witryna sieci Web, witryna internetowa, usługi mobilne azure"
services: app-service
documentationcenter: 
author: omarkmsft
manager: erikre
editor: cephalin
ms.assetid: 979cafa8-eeb6-4d3b-87cf-764a821c3e4f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: 22f414c7d79092d87406a8d3538b946881fb4580
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-app-service"></a>Co to jest usługa Azure App Service?
*Usługa App Service* to oferta [platformy jako usługi](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS) dostępna w ramach platformy Microsoft Azure. Umożliwia tworzenie aplikacji sieci Web i aplikacji mobilnych dla dowolnej platformy lub urządzenia. Pozwala integrować aplikacje z rozwiązaniami SaaS, nawiązywać połączenia z aplikacjami lokalnymi i automatyzować procesy biznesowe. Na platformie Azure aplikacje są uruchamiane na w pełni zarządzanych maszynach wirtualnych przy użyciu wybranych przez użytkownika udostępnianych zasobów maszyn wirtualnych lub dedykowanych maszyn wirtualnych.

Usługa App Service oferuje hello sieci web i mobilnych możliwości, które były wcześniej dostępne oddzielnie jako witryny sieci Web Azure oraz Azure Mobile Services. Obejmuje ona także nowe funkcje automatyzacji procesów biznesowych i hostowania interfejsów API w chmurze. Usługa App Service jako pojedyncza zintegrowana usługa umożliwia korzystanie z różnych składników — witryn sieci Web, zaplecza aplikacji mobilnych, interfejsów API RESTful i procesów biznesowych — w ramach jednego rozwiązania.

Witaj następujące 4-minutowy film zawiera krótki opis powiązań tooearlier Azure App Service i ofert nowości w nim.

> [!VIDEO https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/app-service-history-lesson/player]
> 
> 

## <a name="why-use-app-service"></a>Dlaczego warto korzystać z usługi App Service?
Poniżej przedstawiono niektóre najważniejszych funkcji i możliwości usługi App Service:

* **Wiele języków i struktur** — usługa App Service oferuje najwyższej jakości pomoc techniczną w zakresie rozwiązań ASP.NET, Node.js, Java, PHP i Python. Na maszynach wirtualnych usługi App Service można również uruchamiać [program Windows PowerShell oraz inne skrypty lub pliki wykonywalne](../app-service-web/web-sites-create-web-jobs.md).
* **Optymalizacja metodyki DevOps** — konfigurowanie [ciągłej integracji i wdrażania](../app-service-web/app-service-continuous-deployment.md) za pomocą usług Visual Studio Team Services, GitHub lub BitBucket. Promowanie aktualizacji za pośrednictwem [środowisk testowych i przejściowych](../app-service-web/web-sites-staged-publishing.md). Wykonywanie [testowania A/B](../app-service-web/app-service-web-test-in-production-get-start.md). Zarządzanie aplikacjami w usłudze App Service przy użyciu [programu Azure PowerShell](/powershell/azureps-cmdlets-docs) lub hello [międzyplatformowego interfejsu wiersza polecenia (CLI)](../cli-install-nodejs.md).
* **Globalne skalowanie i wysoka dostępność** — ręczne lub automatyczne skalowanie [w pionie](../app-service-web/web-sites-scale.md) lub [w poziomie](../monitoring-and-diagnostics/insights-how-to-scale.md). Hostuj aplikacje sieci w dowolnym miejscu firmy Microsoft globalnej infrastruktury centrum danych i usługi aplikacji hello [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) korzystaj z wysokiej dostępności.
* **TooSaaS połączenia danych platformy i lokalnymi** — wybierz jedną z więcej niż 50 [łączniki](../connectors/apis-list.md) obsługujących systemy dla przedsiębiorstw (takie jak SAP, Siebel i Oracle), usługi SaaS (np. Salesforce i Office 365) i internet usług (takich jak Facebook i Twitter). Dostęp do danych lokalnych przy użyciu [połączeń hybrydowych](../biztalk-services/integration-hybrid-connection-overview.md) i [sieci wirtualnych platformy Azure](../app-service-web/web-sites-integrate-with-vnet.md).
* **Bezpieczeństwo i zgodność** — usługa App Service jest [zgodna ze standardami ISO, SOC i PCI](https://www.microsoft.com/TrustCenter/).
* **Szablony aplikacji** — wybierz z obszernej listy szablonów hello [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/) z użyciem kreatora tooinstall popularnego oprogramowania typu open source, takie jak WordPress, Joomla i Drupal.
* **Integracja z programem Visual Studio** — dedykowane narzędzia w programie Visual Studio usprawnić pracę hello tworzenie, wdrażanie i debugowanie.

## <a name="app-types-in-app-service"></a>Typy aplikacji w usłudze App Service
Usługa App Service oferuje kilka *typy aplikacji*, każdy z nich jest zamierzone toohost określonego obciążenia:

* [**Web Apps**](../app-service-web/app-service-web-overview.md) — do hostowania witryn sieci Web i aplikacji sieci Web.
* [**Mobile Apps**](../app-service-mobile/app-service-mobile-value-prop.md) — do hostowania zaplecza aplikacji mobilnych.
* [**API Apps**](../app-service-api/app-service-api-apps-why-best-platform.md) — do hostowania interfejsów API RESTful.
* [**Logic Apps**](../logic-apps/logic-apps-what-are-logic-apps.md) — do automatyzacji procesów biznesowych oraz integrowania systemów i danych między chmurami bez pisania kodu.

Witaj word *aplikacji* toohello hosting zasobów dedykowanych toorunning obciążenia odnosi się tutaj. Biorąc "web app", na przykład, jest prawdopodobnie zapoznanie toothinking aplikacji sieci web, jak zarówno aplikacji, jak i zasoby obliczeniowe hello kodu przeglądarka tooa łącznie zapewnia funkcje. W usłudze App Service *aplikacji sieci web* jest hello zasoby obliczeniowe, które platformę Azure na potrzeby hostowania kodu aplikacji. 

Aplikacja może się składać z wielu aplikacji usługi App Service różnego rodzaju. Jeśli na przykład aplikacja obejmuje fronton sieci Web i zaplecze interfejsu RESTful API, można:

- Wdrażanie zarówno (frontonu i interfejsu api) tooa jednej sieci web aplikacji  
- Wdrażanie aplikacji sieci web tooa kod frontonu i kod zaplecza aplikacji tooan interfejsu API. 



## <a name="app-service-plans"></a>Plany usługi App Service
[Planów usługi App Service](azure-web-sites-web-hosting-plans-in-depth-overview.md) reprezentuje kolekcję hello toohost fizyczne zasoby używane aplikacje.

Plany usługi App Service definiują następujące elementy:

- **Region** (Zachodnie stany USA, Wschodnie stany USA itp.)
- **Wartość licznika skali** (jedno, dwa, trzy wystąpienia itp.)
- **Rozmiar wystąpienia** (mały, średni, duży)
- **Jednostka magazynowa** (Bezpłatna, Współdzielona, Podstawowa, Standardowa, Premium)

Wszystkie aplikacje przypisane tooan **planu usługi aplikacji** udostępnianie zasobów hello zdefiniowana przez nią stosowanie koszt toosave odnośnie do hostowania wielu aplikacji.

Twoje **planu usługi aplikacji** można skalować z **wolne** i **Shared** jednostki SKU zbyt**podstawowe**, **standardowe**, i **Premium** jednostki SKU, umożliwiając dostęp do zasobów toomore i funkcje wzdłuż hello sposób. Po planu usługi aplikacji jest zbyt**podstawowe** lub nowszym można też kontrolować hello **rozmiar** i skalować liczbę hello maszyn wirtualnych.

Witaj **SKU** i **skali** z usługi aplikacji hello plan określa hello kosztów i nie hello liczbę aplikacje znajdujące się w nim. 

Jeśli potrzebujesz większej skalowalności i izolacji sieci, możesz uruchamiać aplikacje w [środowisku usługi App Service](../app-service-web/app-service-app-service-environment-intro.md).

## <a name="pricing"></a>Ceny
Informacje na temat cen usługi App Service można znaleźć w artykule [App Service — ceny](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="test-drive-app-service"></a>Testowanie usługi App Service
[Utwórz przykładową aplikację sieci Web, aplikację mobilną lub aplikację logiki](https://azure.microsoft.com/try/app-service/) i testuj ją przez jedną godzinę bez konieczności podawania danych karty kredytowej, bez zobowiązań i bez problemu.

Możesz też założyć [bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/) i wypróbować jeden z naszych samouczków ułatwiających rozpoczynanie pracy:

* [Samouczek: tworzenie aplikacji sieci Web](../app-service-web/app-service-web-get-started.md)
* [Samouczek: tworzenie aplikacji mobilnej](../app-service-mobile/app-service-mobile-android-get-started.md)
* [Samouczek: tworzenie aplikacji interfejsu API](../app-service-api/app-service-api-dotnet-get-started.md)
* [Samouczek: tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md)

