---
title: "aaaAbout Mobile Apps w usłudze Azure App Service"
description: Poznaj zalety hello czy App Service oferuje tooyour enterprise aplikacji mobilnych.
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: 4e96cb9d-a632-4cf6-8219-0810d8ade3f9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ab96af11c3df196acfb9ecec1339e7f6093c7066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started"> </a>Informacje o funkcji Mobile Apps w usłudze Azure App Service
Usługa Azure App Service to oferta w pełni zarządzanej [platformy jako usługi](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) dla profesjonalnych deweloperów. Usługa Hello oferuje bogaty zestaw funkcji scenariusze tooweb, mobilnych i umożliwiających integrację. 

funkcji Mobile Apps Hello Azure App Service zapewnia deweloperów w przedsiębiorstwach i platforma programistyczna aplikacji mobile integratory systemu, która jest wysoce skalowalna i dostępnego globalnie.

![Wizualne omówienie funkcji Mobile Apps](./media/app-service-mobile-value-prop/overview.png)

## <a name="why-mobile-apps"></a>Dlaczego warto korzystać z usługi Mobile Apps?
Przy użyciu funkcji Mobile Apps hello można:

* **Kompilować aplikacje natywne i międzyplatformowe** — bez względu na to, czy kompilujesz natywne aplikacje dla systemów iOS, Android i Windows, czy też międzyplatformowe aplikacje platform Xamarin lub Cordova (PhoneGap), możesz korzystać z usługi App Service za pośrednictwem natywnych zestawów SDK.
* **Łączenie systemów przedsiębiorstwa tooyour**: przy użyciu funkcji Mobile Apps hello, można dodać firmowej logowania (w minutach) oraz połączyć tooyour przedsiębiorstwa lokalnie lub zasobów w chmurze.
* **Tworzenie aplikacji w trybie offline gotowe za pomocą synchronizacji danych**: personel mobilny bardziej wydajnej pracy przy tworzeniu aplikacji, które działają w trybie offline, a następnie użyć danych toosync Mobile Apps w tle powitania po nawiązaniu łączności ze wszystkimi źródeł danych przedsiębiorstwa lub oprogramowanie jako usługa (SaaS) interfejsów API.
* **Wypychanie powiadomień toomillions w sekundach**: Uwzględnij z klientami dzięki błyskawicznym powiadomieniom wypychanym z dowolnego urządzenia spersonalizowane tootheir potrzeb i wysyłany, gdy czas hello jest odpowiednia.

## <a name="mobile-apps-features"></a>Funkcje Mobile Apps
Witaj, następujące funkcje są ważne włączone toocloud przenośnych programowanie:

* **Uwierzytelnianie i autoryzacja** — wybieraj z coraz dłuższej listy dostawców tożsamości, obejmującej usługę Azure Active Directory na potrzeby uwierzytelniania w przedsiębiorstwie, a także dostawców sieci społecznościowych, takich jak Facebook, Google, Twitter i konta Microsoft. Funkcja Mobile Apps udostępnia usługę OAuth 2.0 dla każdego dostawcy. Można również zintegrować hello zestawu SDK dla dostawcy tożsamości hello funkcji specyficznych dla dostawcy.

    Dowiedz się więcej na temat naszych [authentication features].

* **Dostęp do danych**: Mobile Apps udostępnia przyjazna OData v3 źródła danych ma połączonych tooAzure bazy danych SQL lub lokalnego programu SQL server. Ponieważ ta usługa może opierać się na platformie Entity Framework, możesz łatwo zintegrować ją z innymi dostawcami danych NoSQL i SQL, w tym [Azure Table Storage], MongoDB i [Azure Cosmos DB], a także dostawcami interfejsów API SaaS, takimi jak Office 365 i Salesforce.com.

* **Synchronizacja w trybie offline**: zestawów SDK klientów była łatwe toobuild niezawodny i elastyczny aplikacji mobilnych korzystających z zestawem danych w trybie offline. Można zsynchronizować ten zestaw danych automatycznie za pomocą danych zaplecza hello, w tym obsługi rozwiązywania konfliktów.

  Dowiedz się więcej na temat naszych [funkcje związane z danymi].

* **Powiadomienia wypychane**: zestawów SDK klientów integrują się z możliwościami rejestracji hello Azure Notification Hubs, więc można wysyłać toomillions powiadomień wypychanych użytkowników jednocześnie.

  Dowiedz się więcej na temat naszych [funkcje powiadomień wypychanych].

* **Zestawy SDK klientów**: oferujemy kompletny pakiet zestawów SDK klientów, które obsługują tworzenie aplikacji natywnych ([iOS], [Android] i [Windows]), międzyplatformowych ([Xamarin.iOS i Xamarin.Android], [Xamarin.Forms]) i hybrydowych ([Apache Cordova]). Każdy zestaw SDK klienta jest dostępny z licencją MIT i jest rozwiązaniem typu open source.

## <a name="azure-app-service-features"></a>Funkcje usługi Azure App Service
Witaj, następujące funkcje platformy są przydatne w przypadku witryn produkcyjnych aplikacji mobilnych:

* **Skalowanie automatyczne**: Z usługi aplikacji, można szybko skalowanie w górę lub skalowanie toohandle dowolnych przychodzących obciążeń klientów. Ręcznie wybierz hello liczby i rozmiarów maszyn wirtualnych lub skonfigurować funkcję skalowania automatycznego tooscale Twojej aplikacji mobilnej zaplecza oparte na obciążenie lub harmonogram.

  Dowiedz się więcej na temat [skalowania automatycznego].

* **Środowiska przejściowe**: usługa App Service może uruchamiać wiele wersji witryny, co umożliwia testowanie A/B, testowanie w środowisku produkcyjnym jako część większego planu metodyki DevOps oraz miejscowe wdrażanie przejściowe nowego zaplecza.

  Dowiedz się więcej na temat [środowiska przejściowe].

* **Ciągłe wdrażanie**: App Service można zintegrować z typowymi systemami zarządzania (SCM) łańcucha dostaw, więc można automatycznie wdrażać nowej wersji z zaplecza przez wypchnięcie tooa gałęzi systemu SCM.

  Dowiedz się więcej na temat [opcje wdrożenia].

* **Sieci wirtualne**: App Service można połączyć zasoby lokalne tooon przy użyciu wirtualnej sieci, usługa Azure ExpressRoute lub połączeń hybrydowych.

  Dowiedz się więcej na temat [połączenia hybrydowe], [sieci wirtualnych] i [ExpressRoute].

* **Środowiska izolowane i dedykowane**: usługę App Service można uruchamiać w dedykowanym, w pełni izolowanym środowisku, aby bezpiecznie pracować z aplikacjami usługi Azure App Service na dużą skalę. To środowisko jest idealne w przypadku obciążeń aplikacji wymagających dużej skali, izolacji lub bezpiecznego dostępu do sieci.

  Dowiedz się więcej na temat [środowisk usługi App Service].

## <a name="next-steps"></a>Następne kroki

tooget pracy z usługą Mobile Apps w usłudze Azure App Service, pełną hello [wprowadzenie] samouczka. Samouczek Hello obejmuje podstawy hello produkcji kończyć przenośnym Wstecz i klienta. Obejmuje on również zagadnienia, takie jak integrowanie uwierzytelniania, synchronizacji w trybie offline i powiadomień wypychanych. Można wykonać samouczek hello wielokrotnie, jeden raz dla każdej aplikacji klienta.

Aby uzyskać więcej informacji o funkcji Mobile Apps, zapoznaj się z naszą [mapą nauki].
Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service].

<!-- URLs. -->
[Migrate your mobile service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[wprowadzenie]: app-service-mobile-ios-get-started.md
[Azure Table storage]:../cosmos-db/table-storage-how-to-use-dotnet.md
[Azure Cosmos DB]: ../cosmos-db/documentdb-get-started.md
[authentication features]: ./app-service-mobile-auth.md
[funkcje związane z danymi]: ./app-service-mobile-offline-data-sync.md
[funkcje powiadomień wypychanych]: ../notification-hubs/notification-hubs-push-notification-overview.md
[iOS]: ./app-service-mobile-ios-how-to-use-client-library.md
[Android]: ./app-service-mobile-android-how-to-use-client-library.md
[Windows]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.iOS i Xamarin.Android]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.Forms]: ./app-service-mobile-xamarin-forms-get-started.md
[Apache Cordova]: ./app-service-mobile-cordova-how-to-use-client-library.md
[skalowanie automatyczne]: ../app-service-web/web-sites-scale.md
[środowiska przejściowe]: ../app-service-web/web-sites-staged-publishing.md
[opcje wdrożenia]: ../app-service-web/web-sites-deploy.md
[połączenia hybrydowe]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[sieci wirtualnych]: ../app-service-web/web-sites-integrate-with-vnet.md
[ExpressRoute]: ../app-service-web/app-service-app-service-environment-network-configuration-expressroute.md
[środowiska usługi App Service]: ../app-service-web/app-service-app-service-environment-intro.md
[mapą nauki]: https://azure.microsoft.com/en-us/documentation/learning-paths/appservice-mobileapps/
