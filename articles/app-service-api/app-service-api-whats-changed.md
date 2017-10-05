---
title: "Aplikacja interfejsu API usługi aplikacji — informacje o zmianach | Dokumentacja firmy Microsoft"
description: "Poznaj nowe aplikacji interfejsu API w usłudze Azure App Service."
services: app-service\api
documentationcenter: .net
author: mohitsriv
manager: erikre
editor: tdykstra
ms.assetid: a9b58066-e8fd-48b8-a651-4613b1736433
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: rachelap
ms.openlocfilehash: e4e25f2cd1d39bb0113e3fe2bc37120f92227b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="app-service-api-apps---whats-changed"></a>Aplikacja interfejsu API usługi aplikacji — co zostało zmienione
W zdarzeniu Connect() w listopad 2015 r., zostały wiele ulepszeń w usłudze Azure App Service [ogłoszenia](https://azure.microsoft.com/blog/azure-app-service-updates-november-2015/). Te ulepszenia obejmują zmiany podstawowej aplikacji interfejsu API lepiej dostosować Mobile i aplikacje sieci Web, Zmniejsz liczbę koncepcji i zwiększyć wdrożenia i wydajność środowiska uruchomieniowego. Uruchamianie nowej aplikacji interfejsu API 30 listopada 2015 utworzonych za pomocą portalu zarządzania platformy Azure lub najnowsze narzędzia będzie odzwierciedlenia tych zmian. W tym artykule opisano, jak można wdrożyć ponownie istniejących aplikacji, aby skorzystać z możliwości, a także te zmiany.

## <a name="feature-changes"></a>Zmiany funkcji
Najważniejsze funkcje aplikacji API Apps — uwierzytelnianie, CORS i interfejsu API metadanych — został przeniesiony bezpośrednio do usługi aplikacji. Dzięki tej zmianie funkcje są dostępne w aplikacjach interfejsu API, mobilne i sieci Web. W rzeczywistości udziału wszystkich trzech takie same **Microsoft.Web/sites** typu zasobu w Menedżerze zasobów. Brama aplikacji interfejsu API jest już potrzebne lub oferowanych w aplikacjach interfejsu API. Ponadto ułatwia do użycia usługi Azure API Management, ponieważ będzie tylko pojedyncza brama zarządzanie interfejsami API.

![Omówienie aplikacji interfejsu API](./media/app-service-api-whats-changed/api-apps-overview.png)

Zasada projektowania klucza z aktualizacją aplikacji interfejsu API jest umożliwienie można wyświetlić interfejsu API jest dostępna, w wybranym języku.  Interfejs API jest już wdrożony jako aplikacji sieci Web lub aplikacji mobilnej, nie trzeba ponownie wdrożyć aplikację, aby móc korzystać z nowych funkcji. Jeśli jesteś obecnie w aplikacji interfejsu API w wersji zapoznawczej, wskazówki dotyczące migracji została szczegółowo opisana poniżej.

### <a name="authentication"></a>Authentication
Istniejące gotowe API Apps, Mobile Services/aplikacje i aplikacje sieci Web uwierzytelniania funkcji zostały unified i są dostępne w jednym bloku uwierzytelniania usługi Azure App Service w portalu zarządzania. Aby obejrzeć wprowadzenie do usługi uwierzytelniania w usłudze App Service, zobacz [rozwijanie usługi aplikacji uwierzytelniania / autoryzacji](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

W przypadku scenariuszy interfejsu API istnieje szereg nowych możliwości odpowiednich:

* **Obsługa bezpośrednio za pomocą usługi Azure Active Directory**, bez konieczności wymiany tokenu AAD dla tokenu sesji kodu klienta: klient właśnie może zawierać tokeny AAD w nagłówku autoryzacji według specyfikacji tokenu elementu nośnego. Oznacza to również nie specyficzne dla aplikacji usługi SDK jest wymagany po stronie klienta lub serwera. 
* **Dostęp do usługi lub "Internal"**: Jeśli masz procesu demona lub innego klienta wymagające dostępu do interfejsów API bez interfejsu można żądać tokenu przy użyciu nazwy głównej usługi AAD i przekaż go do aplikacji usługi do uwierzytelniania przy użyciu programu aplikacja.
* **Odroczone autoryzacji**: wiele aplikacji ma różne ograniczenia dostępu dla różnych części aplikacji. Możesz określić ma niektórych interfejsów API ma być publicznie dostępne, a inne wymagają logowania. Oryginalny funkcja uwierzytelniania/autoryzacji była all-or-nothing, z całej lokacji wymagające logowania. Ta opcja jest nadal istnieje, ale można też zezwolić na kod aplikacji w celu renderowania dostępem po usługi aplikacji został uwierzytelniony użytkownik.

Aby uzyskać więcej informacji na temat nowych funkcji uwierzytelniania, zobacz [uwierzytelniania i autoryzacji dla aplikacji interfejsu API w usłudze Azure App Service](app-service-api-authentication.md). Aby uzyskać informacje o sposobie migrowania istniejących aplikacji interfejsu API z poprzednim modelu aplikacji interfejsu API do nowego, zobacz [Migrowanie istniejących aplikacji interfejsu API](#migrating-existing-api-apps) dalszej części tego artykułu.

### <a name="cors"></a>CORS
Zamiast rozdzielana przecinkami **MS_CrossDomainOrigins** aplikacji ustawienie, jest teraz blok w portalu zarządzania platformy Azure dla Konfigurowanie mechanizmu CORS. Alternatywnie można skonfigurować, za pomocą narzędzi takich jak Azure PowerShell, interfejsu wiersza polecenia Menedżera zasobów lub [Eksploratora zasobów](https://resources.azure.com/). Ustaw **cors** właściwość **Microsoft.Web/sites/config** typ zasobu dla Twojego  **&lt;nazwa witryny&gt;/web** zasobów. Na przykład:

    {
        "cors": {
            "allowedOrigins": [
                "https://localhost:44300"
            ]
        }
    } 

### <a name="api-metadata"></a>Metadane interfejsu API
Blok definicji interfejsu API jest teraz dostępna w aplikacji interfejsu API, mobilne i sieci Web. W portalu zarządzania można określić względny adres url lub bezwzględny adres url wskazuje punkt końcowy reprezentacja hostów programu Swagger 2.0 tego interfejsu API. Alternatywnie można skonfigurować, za pomocą narzędzia Menedżera zasobów. Ustaw **apiDefinition** właściwość **Microsoft.Web/sites/config** typ zasobu dla Twojego  **&lt;nazwa witryny&gt;/web** zasobów. Na przykład:

    {
        "apiDefinition":
        {
            "url": "https://myStorageAccount.blob.core.windows.net/swagger/apiDefinition.json"
        }
    }

W tej chwili punktu końcowego metadanych musi być dostępny publicznie bez uwierzytelniania dla wielu klientów podrzędne (np. programu Visual Studio interfejsu API REST klienta generowania i rozwiązanie PowerApps "Dodaj interfejsu API" przepływu), użycie go. Oznacza to, jeśli używasz uwierzytelniania usługi aplikacji i udostępnić definicji interfejsu API z samej aplikacji, należy użyć opcji uwierzytelniania odroczone opisana wcześniej, dzięki czemu trasy do metadanych struktury Swagger jest publiczny.

## <a name="management-portal"></a>Portal zarządzania
Wybieranie **nowy > sieci Web i mobilność > Aplikacja interfejsu API** w portalu będzie tworzyć aplikacje interfejsu API, które odzwierciedlać nowych funkcji opisanych w artykule. **Przeglądaj > aplikacje interfejsu API** zostaną wyświetlone tylko te nowe aplikacje interfejsu API. Po przejściu do aplikacji interfejsu API bloku współużytkuje te same układu i możliwości, jak te sieci Web i aplikacji mobilnej. Jedyne różnice są szybkiego startu zawartości i kolejność ustawień.

Istniejące aplikacje interfejsu API (lub Marketplace aplikacje API apps utworzone na podstawie Logic Apps) z poprzednich wersji zapoznawczej możliwości nadal będą widoczne w Projektancie aplikacji logiki i przeglądając wszystkie zasoby w grupie zasobów.

## <a name="visual-studio"></a>Visual Studio
Większość narzędzi aplikacji sieci Web będzie działać z nowej aplikacji interfejsu API, ponieważ mają tego samego podstawowego **Microsoft.Web/sites** typu zasobu. Visual Studio Azure narzędzi, należy jednak uaktualnieni do wersji 2.8.1 lub nowszego ponieważ ujawnia on wiele możliwości specyficznych dla interfejsów API. Pobierz zestaw SDK z [Azure pliki do pobrania](https://azure.microsoft.com/downloads/).

Z racjonalizacja typów usług aplikacji, należy opublikować jest również unified w obszarze **publikowania > Microsoft Azure App Service**:

![Publikowanie aplikacji interfejsu API](./media/app-service-api-whats-changed/api-apps-publish.png)

Aby dowiedzieć się więcej o zestawie SDK 2.8.1, przeczytaj anons [wpis w blogu](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).

Alternatywnie możesz ręcznie zaimportuj profil publikowania z portalu zarządzania, aby umożliwić publikowanie. Jednak wymaga zestawu SDK 2.8.1 w Eksploratorze chmury, generowanie kodu i tworzenia wybór aplikacji interfejsu API lub nowszej.

## <a name="migrating-existing-api-apps"></a>Migrowanie istniejących aplikacji interfejsu API
Jeśli niestandardowego interfejsu API jest wdrażana w poprzedniej wersji zapoznawczej aplikacji interfejsu API, prosimy przeprowadzenie migracji do nowego modelu dla aplikacji interfejsu API przez 31 grudnia 2015 r. Zarówno stary i nowy model jest tworzony na podstawie interfejsów API sieci Web hostowanych w usłudze App Service, większość istniejącego kodu mogą być ponownie używane.

### <a name="hosting-and-redeployment"></a>Hosting i ponowne wdrożenie
Kroki dotyczące ponownego wdrażania są takie same jak wdrażanie wszelkie istniejące interfejsu API sieci Web do usługi App Service. kroki:

1. Utwórz pustą aplikację interfejsu API. Można to zrobić w portalu wraz z nowym > Aplikacja interfejsu API w programie Visual Studio z publikowania lub narzędzia Menedżera zasobów. Jeśli przy użyciu narzędzia Menedżera zasobów lub szablonów, należy ustawić **rodzaj** do wartości **interfejsu api** na **Microsoft.Web/sites** typu zasobu na poradniki Szybki Start i ustawień w portal zarządzania przeznaczonych do scenariuszy interfejsu API.
2. Połącz i wdrażania projektu do pustych aplikacji interfejsu API przy użyciu dowolnego mechanizmu wdrażania obsługiwane przez usługę App Service. Odczyt [dokumentacja wdrażania usługi aplikacji Azure](../app-service-web/web-sites-deploy.md) Aby dowiedzieć się więcej. 

### <a name="authentication"></a>Authentication
Usługi uwierzytelniania usługi App Service obsługuje te same możliwości, które były dostępne w poprzednim modelu aplikacji interfejsu API. Jeśli używasz tokeny sesji i wymagają zestawów SDK, należy użyć następujących zestawów SDK klienta i serwera:

* Klient: [klientów mobilnych Azure SDK](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
* Serwer: [rozszerzenie uwierzytelniania .NET aplikacji mobilnej platformy Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/) 

Jeśli były używane zamiast alfa zestawów SDK z usługi aplikacji, są obecnie są przestarzałe:

* Klient: [zestawu SDK usługi aplikacji platformy Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.AppService)
* Serwer: [Microsoft.Azure.AppService.ApiApps.Service](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service)

W szczególności z usługą Azure Active Directory, jednak nie usługi specyficzny dla aplikacji jest wymagany, jeśli używasz token usługi AAD bezpośrednio.

### <a name="internal-access"></a>Dostęp do
Poprzednim modelu aplikacji interfejsu API uwzględniane na poziomie wbudowanych dostęp do. Użyj zestawu SDK to wymagany do podpisywania żądań. Jak opisano wcześniej, z nowego modelu aplikacji interfejsu API podmiotów zabezpieczeń usługi AAD może służyć jako odpowiednik do usługi uwierzytelniania bez konieczności usługi specyficzny dla aplikacji zestawu SDK. Dowiedz się więcej w [uwierzytelnianie główną usługi dla aplikacji interfejsu API w usłudze Azure App Service](app-service-api-dotnet-service-principal-auth.md).

### <a name="discovery"></a>Odnajdywania
Poprzednim modelu aplikacji interfejsu API miał interfejsy API wykrywania innych aplikacji interfejsu API w czasie wykonywania w tej samej grupie zasobów za tą samą bramą. Jest to szczególnie przydatne w przypadku blokowej architektury, które implementują wzorce mikrousługi. Gdy to nie jest bezpośrednio obsługiwana, dostępnych jest kilka opcji:

1. API Menedżera zasobów Azure używany do odnajdowania.
2. Umieść Azure API Management przed swoje interfejsy API hostowanych usług aplikacji. Azure API Management służy jako fasad i zapewniają stabilna zewnętrznego adresu url połączonej, nawet jeśli zmieni się wewnętrzny topologii.
3. Utworzyć własną aplikację interfejsu API odnajdywania i mają inne aplikacje interfejsu API Zarejestruj aplikacji odnajdywania podczas uruchamiania.
4. W czasie wdrażania umieścić w ustawieniach aplikacji wszystkie aplikacje interfejsu API (i klientów) punkty końcowe w innych aplikacjach interfejsu API. Jest to działało, w przypadku wdrożeń szablonu i ponieważ aplikacje interfejsu API umożliwiają teraz kontroli adresu URL.

## <a name="using-api-apps-with-logic-apps"></a>Przy użyciu aplikacji interfejsu API w usłudze Logic Apps
Nowy model aplikacji interfejsu API dobrze działa z [Logic Apps wersji schematu 2015-08-01](../logic-apps/logic-apps-schema-2015-08-01.md).

## <a name="next-steps"></a>Następne kroki
Aby dowiedzieć się więcej, zapoznaj się z artykułami w [sekcji dokumentacji interfejsu API Apps](https://azure.microsoft.com/documentation/services/app-service/api/). One zostały zaktualizowane w celu uwzględnienia nowego modelu dla aplikacji interfejsu API. Ponadto dotrzeć na forach dodatkowe szczegółowe informacje i wskazówki dotyczące migracji:

* [Forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-api-apps)

