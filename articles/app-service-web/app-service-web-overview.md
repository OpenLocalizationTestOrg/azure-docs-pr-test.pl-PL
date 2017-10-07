---
title: "Omówienie aplikacji aaaWeb | Dokumentacja firmy Microsoft"
description: "Dowiedz się, w jaki sposób usługa Azure App Service ułatwia tworzenie i hostowanie aplikacji sieci Web"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: ce27519bddd62a7fca6ba1fb23c763d0fc378c2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="web-apps-overview"></a>Przegląd usługi Web Apps
*Azure App Service Web Apps* to w pełni zarządzana platforma obliczeniowa zoptymalizowana pod kątem hostowania witryn i aplikacji sieci Web. To [platforma jako usługa](https://en.wikipedia.org/wiki/Platform_as_a_service) oferty (PaaS) platformy Microsoft Azure pozwala skupić się na logice biznesowej, podczas Azure zajmuje się hello toorun infrastruktury i skalowania aplikacji.

powitania po 5-minutowy film wideo przedstawia aplikacje sieci Web usługi aplikacji Azure.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a>Co to jest aplikacja sieci Web w usłudze App Service?
W usłudze App Service *aplikacji sieci web* jest hello zasoby obliczeniowe, które udostępnia Azure do hostowania witryny sieci Web lub aplikacji sieci web.  

Hello zasoby obliczeniowe mogą znajdować się na współdzielonych lub dedykowanych maszynach wirtualnych (VM), w zależności od wybranej warstwy cenowej hello. Kod aplikacji jest uruchamiany na zarządzanej maszynie wirtualnej, która jest odizolowana od innych klientów.

Kod może być tworzony przy użyciu dowolnego języka lub struktury obsługiwanej przez [usługę Azure App Service](../app-service/app-service-value-prop-what-is.md), na przykład ASP.NET, Node.js, Java, PHP lub Python. W aplikacji sieci Web można również uruchamiać skrypty używające [programu PowerShell i innych języków skryptowych](web-sites-create-web-jobs.md#acceptablefiles).

Przykłady typowych scenariuszach służącego aplikacji sieci Web dla zobacz [scenariusze aplikacji w sieci Web](https://azure.microsoft.com/documentation/scenarios/web-app/) i hello **scenariusze i zalecenia** sekcji [usłudze Azure App Service, Virtual Porównanie maszyny, Service Fabric i usług w chmurze](choose-web-site-cloud-service-vm.md#scenarios).

## <a name="why-use-web-apps"></a>Dlaczego warto używać usługi Web Apps?
Oto główne funkcje usługi App Service stosowane tooWeb aplikacji:

* **Wiele języków i struktur** — usługa App Service oferuje najwyższej jakości pomoc techniczną dotyczącą rozwiązań ASP.NET, Node.js, Java, PHP i Python. Na maszynach wirtualnych usługi App Service można również uruchamiać [program PowerShell oraz inne skrypty lub pliki wykonywalne](web-sites-create-web-jobs.md).
* **Optymalizacja metodyki DevOps** — konfigurowanie [ciągłej integracji i wdrażania](app-service-continuous-deployment.md) za pomocą usług Visual Studio Team Services, GitHub lub BitBucket. Promowanie aktualizacji za pośrednictwem [środowisk testowych i przejściowych](web-sites-staged-publishing.md). Wykonywanie [testowania A/B](app-service-web-test-in-production-get-start.md). Zarządzanie aplikacjami w usłudze App Service przy użyciu [programu Azure PowerShell](/powershell/azureps-cmdlets-docs) lub hello [międzyplatformowego interfejsu wiersza polecenia (CLI)](../cli-install-nodejs.md).
* **Globalne skalowanie i wysoka dostępność** — ręczne lub automatyczne skalowanie [w pionie](web-sites-scale.md) lub [w poziomie](../monitoring-and-diagnostics/insights-how-to-scale.md). Hostuj aplikacje sieci w dowolnym miejscu firmy Microsoft globalnej infrastruktury centrum danych i usługi aplikacji hello [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) korzystaj z wysokiej dostępności.
* **TooSaaS połączenia danych platformy i lokalnymi** — wybierz jedną z więcej niż 50 [łączniki](../connectors/apis-list.md) obsługujących systemy dla przedsiębiorstw (takie jak SAP, Siebel i Oracle), usługi SaaS (np. Salesforce i Office 365) i internet usług (takich jak Facebook i Twitter). Dostęp do danych lokalnych przy użyciu [połączeń hybrydowych](../biztalk-services/integration-hybrid-connection-overview.md) i [sieci wirtualnych platformy Azure](web-sites-integrate-with-vnet.md).
* **Bezpieczeństwo i zgodność** — usługa App Service jest [zgodna ze standardami ISO, SOC i PCI](https://www.microsoft.com/TrustCenter/).
* **Szablony aplikacji** — wybierz z obszernej listy szablonów aplikacji hello [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/) z użyciem kreatora tooinstall popularnego oprogramowania typu open source, takie jak WordPress, Joomla i Drupal.
* **Integracja z programem Visual Studio** — dedykowane narzędzia w programie Visual Studio usprawnić pracę hello tworzenie, wdrażanie i debugowanie.

Ponadto aplikacja sieci Web może korzystać z funkcji oferowanych przez usługi [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) (na przykład obsługa mechanizmu CORS) i [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) (na przykład powiadomienia wypychane). Aby uzyskać więcej informacji na temat typów aplikacji w usłudze App Service, zobacz [omówienie usługi Azure App Service](../app-service/app-service-value-prop-what-is.md).

Oprócz usługi Web Apps w usłudze App Service platforma Azure oferuje inne usługi, które mogą służyć do hostowania witryn i aplikacji sieci Web. W przypadku większości scenariuszy hello najlepszym rozwiązaniem jest aplikacji sieci Web.  W przypadku architektury mikrousługi należy wziąć pod uwagę [sieci szkieletowej usług](https://azure.microsoft.com/documentation/services/service-fabric)i większą kontrolę nad hello maszyn wirtualnych, które działa kod, należy wziąć pod uwagę [maszyny wirtualne Azure](https://azure.microsoft.com/documentation/services/virtual-machines/). Aby uzyskać więcej informacji o tym, jak toochoose między usługami Azure, zobacz [porównanie usługi Azure App Service, maszyn wirtualnych, sieci szkieletowej usług i usługi w chmurze](choose-web-site-cloud-service-vm.md).

## <a name="getting-started"></a>Wprowadzenie
tooget uruchomiona przez wdrożenie przykładowy kod tooa nowej aplikacji sieci web w usłudze App Service, wykonaj jedną z samouczki hello w hello następujące pole listy rozwijanej. Konieczne będzie posiadanie bezpłatnego konta platformy Azure.

> [!div class="op_single_selector"]
> * [Wdrażanie pierwszego tooAzure aplikacji sieci web ASP.NET w ciągu 5 minut](app-service-web-get-started-dotnet.md)
> * [Wdrażanie pierwszego tooAzure aplikacji sieci web PHP w ciągu 5 minut](app-service-web-get-started-php.md)
> * [Wdrażanie pierwszego tooAzure aplikacji sieci web Node.js w ciągu 5 minut](app-service-web-get-started-nodejs.md)
> * [Wdrażanie pierwszego tooAzure aplikacji sieci web Java w ciągu 5 minut](app-service-web-get-started-java.md)
> * [Wdrażanie pierwszego tooAzure aplikacji sieci web języka Python w ciągu 5 minut](app-service-web-get-started-python.md)
> * [Wdrażanie Twojego pierwszego tooAzure lokacji HTML w ciągu 5 minut](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> Usługę [App Service](https://azure.microsoft.com/try/app-service/) możesz wypróbować, nie mając konta platformy Azure. Utwórz początkową aplikację i odtworzyć na temat godzinę tooan — bez karty kredytowej i bez zobowiązań.
> 
> 
