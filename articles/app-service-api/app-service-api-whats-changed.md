---
title: "aaaApp usługi API Apps — informacje o zmianach | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 79df54f1dae91d7c5d3b66d208d0d1c1d7d55ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps---whats-changed"></a>Aplikacja interfejsu API usługi aplikacji — co zostało zmienione
W zdarzeniu Connect() hello w listopada 2015 roku, liczba tooAzure ulepszenia usługi aplikacji zostały [ogłoszenia](https://azure.microsoft.com/blog/azure-app-service-updates-november-2015/). Te ulepszenia obejmują zmiany podstawowego tooAPI toobetter aplikacji Dopasuj Mobile i aplikacji sieci Web, Zmniejsz liczbę koncepcji i zwiększyć wydajność wdrażania i obsługi. Uruchamianie nowej aplikacji interfejsu API 30 listopada 2015 utworzonych za pomocą portalu zarządzania Azure hello lub hello najnowsze narzędzia będzie odzwierciedlać te zmiany. W tym artykule opisano te zmiany, a także sposobu tooredeploy istniejące aplikacje tootake korzystać z funkcji hello.

## <a name="feature-changes"></a>Zmiany funkcji
Witaj najważniejsze funkcje aplikacji API Apps — uwierzytelnianie, CORS i interfejsu API metadanych — został przeniesiony bezpośrednio do usługi aplikacji. Dzięki tej zmianie hello funkcje są dostępne w aplikacjach interfejsu API, mobilne i sieci Web. W rzeczywistości wszystkie trzy udziału hello sam **Microsoft.Web/sites** typu zasobu w Menedżerze zasobów. Brama aplikacji interfejsu API Hello jest już potrzebne lub oferowanych w aplikacjach interfejsu API. Ułatwia to też go toouse łatwiejsze zarządzanie interfejsami API Azure od zostaną tylko hello pojedynczą interfejsu API zarządzania bramą.

![Omówienie aplikacji interfejsu API](./media/app-service-api-whats-changed/api-apps-overview.png)

Zasada projektowania klucza z hello aktualizacji aplikacji interfejsu API jest tooenable toobring jest interfejs API jako, w wybranym języku.  Jeśli Twój interfejs API jest już wdrożony jako aplikacji sieci Web lub aplikacji mobilnej, nie masz tooredeploy korzyści tootake aplikacji hello nowych funkcji. Jeśli jesteś obecnie w aplikacji interfejsu API w wersji zapoznawczej, wskazówki dotyczące migracji została szczegółowo opisana poniżej.

### <a name="authentication"></a>Authentication
Hello istniejących gotowe API Apps, Mobile Services/aplikacje i aplikacje sieci Web uwierzytelniania funkcje zostały unified i są dostępne w jednym bloku uwierzytelniania usługi Azure App Service w portalu zarządzania hello. Wprowadzenie tooauthentication usług w usłudze App Service, zobacz [rozwijanie usługi aplikacji uwierzytelniania / autoryzacji](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

W przypadku scenariuszy interfejsu API istnieje szereg nowych możliwości odpowiednich:

* **Obsługa bezpośrednio za pomocą usługi Azure Active Directory**, bez konieczności token usługi AAD hello tooexchange dla tokenu sesji kodu klienta: klienta może tylko zawierać tokeny AAD hello w nagłówku autoryzacji hello, zgodnie z tokenu elementu nośnego toohello Specyfikacja. Oznacza to również nie specyficzne dla aplikacji usługi SDK jest wymagany na powitania po stronie klienta lub serwera. 
* **Dostęp do usługi lub "Internal"**: Jeśli masz procesu demona lub innego klienta wymagające tooAPIs dostępu bez interfejsu można żądania tokenu przy użyciu nazwy głównej usługi AAD i przekaż go tooApp usługi uwierzytelniania z sieci aplikacja.
* **Odroczone autoryzacji**: wiele aplikacji ma różne ograniczenia dostępu dla różnych części aplikacji hello. Możesz określić ma niektórych interfejsów API toobe publicznie dostępne, a inne wymagają logowania. Hello oryginalnego funkcji uwierzytelniania/autoryzacji all-or-nothing, została wykonana z użyciem hello całej lokacji wymagające logowania. Ta opcja jest nadal istnieje, ale można też zezwolić na kod aplikacji toorender dostępem po usługi aplikacji został uwierzytelniony użytkownik hello.

Aby uzyskać więcej informacji na temat nowych funkcji uwierzytelniania hello zobacz [uwierzytelniania i autoryzacji dla aplikacji interfejsu API w usłudze Azure App Service](app-service-api-authentication.md). Aby dowiedzieć się jak toomigrate istniejących aplikacji interfejsu API z poprzedniej aplikacji interfejsu API hello modelu toohello nowe jeden, zobacz [Migrowanie istniejących aplikacji interfejsu API](#migrating-existing-api-apps) dalszej części tego artykułu.

### <a name="cors"></a>CORS
Zamiast rozdzielana przecinkami **MS_CrossDomainOrigins** aplikacji ustawienie, jest teraz blok w portalu zarządzania Azure hello konfigurowania CORS. Alternatywnie można skonfigurować, za pomocą narzędzi takich jak Azure PowerShell, interfejsu wiersza polecenia Menedżera zasobów lub [Eksploratora zasobów](https://resources.azure.com/). Zestaw hello **cors** właściwość hello **Microsoft.Web/sites/config** typ zasobu dla Twojej  **&lt;nazwa witryny&gt;/web** zasobów. Na przykład:

    {
        "cors": {
            "allowedOrigins": [
                "https://localhost:44300"
            ]
        }
    } 

### <a name="api-metadata"></a>Metadane interfejsu API
Blok definicji interfejsu API Hello jest teraz dostępna w aplikacji interfejsu API, mobilne i sieci Web. W portalu zarządzania hello można określić względny adres url lub bezwzględny adres url wskazuje punkt końcowy tooan reprezentacja hostów programu Swagger 2.0 tego interfejsu API. Alternatywnie można skonfigurować, za pomocą narzędzia Menedżera zasobów. Zestaw hello **apiDefinition** właściwość hello **Microsoft.Web/sites/config** typ zasobu dla Twojej  **&lt;nazwa witryny&gt;/web** zasobów. Na przykład:

    {
        "apiDefinition":
        {
            "url": "https://myStorageAccount.blob.core.windows.net/swagger/apiDefinition.json"
        }
    }

W tej chwili hello metadanych punkt końcowy musi mieć toobe publicznie bez uwierzytelniania dla wielu tooconsume podrzędne klientów (np. programu Visual Studio interfejsu API REST Generowanie klienta i rozwiązanie PowerApps "Dodaj interfejsu API" przepływu) go. Oznacza to, jeśli używasz uwierzytelniania usługi aplikacji i chcesz definicji interfejsu API hello tooexpose z samej aplikacji, konieczne będzie opcja uwierzytelniania odroczone hello toouse opisana wcześniej, dzięki czemu metadanych struktury Swagger tooyour trasy hello jest publiczny.

## <a name="management-portal"></a>Portal zarządzania
Wybranie **nowe > sieci Web i mobilność > Aplikacja interfejsu API** hello portalu spowoduje utworzenie aplikacji interfejsu API, które odzwierciedlać hello nowych funkcji opisanych w artykule hello. **Przeglądaj > aplikacje interfejsu API** zostaną wyświetlone tylko te nowe aplikacje interfejsu API. Po przejściu do aplikacji interfejsu API udziałów bloku hello hello sam układ i możliwości jak sieci Web i aplikacji mobilnej. tylko różnice Hello są szybkiego startu zawartości i kolejność ustawień.

Istniejące aplikacje interfejsu API (lub Marketplace aplikacje API apps utworzone na podstawie Logic Apps) z hello możliwości poprzedniej wersji zapoznawczej nadal będą widoczne w Projektancie aplikacji logiki hello i podczas przeglądania wszystkie zasoby w grupie zasobów.

## <a name="visual-studio"></a>Visual Studio
Witaj większości aplikacji sieci Web narzędzi będzie działać z nowej aplikacji interfejsu API, ponieważ mają tego samego podstawowego **Microsoft.Web/sites** typu zasobu. Hello narzędzi Azure Visual Studio, należy jednak uaktualnionego tooversion 2.8.1 lub nowsze od jej eksponuje pewną liczbę tooAPIs określonych funkcji. Pobierz hello zestawu SDK z hello [Azure pliki do pobrania](https://azure.microsoft.com/downloads/).

Z racjonalizacja hello hello typy usług aplikacji, należy opublikować jest również unified w obszarze **publikowania > Microsoft Azure App Service**:

![Publikowanie aplikacji interfejsu API](./media/app-service-api-whats-changed/api-apps-publish.png)

więcej informacji na temat zestawu SDK 2.8.1, anons odczytu hello toolearn [wpis w blogu](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).

Alternatywnie można ręcznie zaimportować hello profilu z tooenable portalu zarządzania hello publikowania publikowania. Jednak wymaga zestawu SDK 2.8.1 w Eksploratorze chmury, generowanie kodu i tworzenia wybór aplikacji interfejsu API lub nowszej.

## <a name="migrating-existing-api-apps"></a>Migrowanie istniejących aplikacji interfejsu API
Niestandardowy interfejs API w przypadku poprzedniej wersji Preview toohello wdrożonej aplikacji interfejsu API, prosimy migracji toohello nowego modelu dla aplikacji interfejsu API przez 31 grudnia 2015 r. Zarówno hello stary i nowy model jest tworzony na podstawie interfejsów API sieci Web hostowanych w usłudze App Service, większość hello istniejącego kodu mogą być ponownie używane.

### <a name="hosting-and-redeployment"></a>Hosting i ponowne wdrożenie
kroki Hello ponownego wdrażania są hello taki sam jak wdrażanie wszelkie istniejące tooApp interfejsu API sieci Web usługi. kroki:

1. Utwórz pustą aplikację interfejsu API. Można to zrobić w portalu hello z nowy > Aplikacja interfejsu API w programie Visual Studio z publikowania lub narzędzia Menedżera zasobów. Jeśli przy użyciu narzędzia Menedżera zasobów lub szablonów, należy ustawić hello **rodzaj** wartość zbyt**interfejsu api** na powitania **Microsoft.Web/sites** zasobów typu toohave hello poradniki Szybki Start i ustawień w programie portal zarządzania Hello przeznaczonych do scenariuszy interfejsu API.
2. Połącz i Wdróż projekt toohello pusta aplikacja interfejsu API przy użyciu dowolnego hello mechanizmów wdrażania obsługiwane przez usługę App Service. Odczyt [dokumentacja wdrażania usługi aplikacji Azure](../app-service-web/web-sites-deploy.md) toolearn więcej. 

### <a name="authentication"></a>Authentication
Witaj obsługę usług uwierzytelniania usługi aplikacji hello takie same możliwości, które były dostępne z hello poprzedniej aplikacji interfejsu API modelu. Jeśli używasz tokeny sesji i wymagają zestawów SDK, użyj hello następujące zestawy SDK klienta i serwera:

* Klient: [klientów mobilnych Azure SDK](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
* Serwer: [rozszerzenie uwierzytelniania .NET aplikacji mobilnej platformy Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/) 

Jeśli były używane zamiast hello alfa usługi aplikacji zestawów SDK, są obecnie są przestarzałe:

* Klient: [zestawu SDK usługi aplikacji platformy Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.AppService)
* Serwer: [Microsoft.Azure.AppService.ApiApps.Service](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service)

W szczególności z usługą Azure Active Directory, jednak nie usługi specyficzny dla aplikacji jest wymagany, jeśli używasz token usługi AAD hello bezpośrednio.

### <a name="internal-access"></a>Dostęp do
Hello poprzedniej aplikacji interfejsu API modelu uwzględniane na poziomie wbudowanych dostęp do. Użyj hello zestawu SDK to wymagany do podpisywania żądań. Jak opisano wcześniej, z hello nowej aplikacji interfejsu API modelu jednostki usługi AAD może służyć jako odpowiednik do usługi uwierzytelniania bez konieczności usługi specyficzny dla aplikacji zestawu SDK. Dowiedz się więcej w [uwierzytelnianie główną usługi dla aplikacji interfejsu API w usłudze Azure App Service](app-service-api-dotnet-service-principal-auth.md).

### <a name="discovery"></a>Odnajdywania
Witaj poprzedniej aplikacji interfejsu API modelu ma interfejsy API wykrywania innych aplikacji interfejsu API w czasie wykonywania w hello tej samej grupie zasobów za hello tą samą bramą. Jest to szczególnie przydatne w przypadku blokowej architektury, które implementują wzorce mikrousługi. Gdy to nie jest bezpośrednio obsługiwana, dostępnych jest kilka opcji:

1. Witaj API Azure Resource Manager używane do odnajdowania.
2. Umieść Azure API Management przed swoje interfejsy API hostowanych usług aplikacji. Azure API Management służy jako fasad i zapewniają stabilna zewnętrznego adresu url połączonej, nawet jeśli zmieni się wewnętrzny topologii.
3. Tworzenie własnych aplikacji interfejsu API odnajdywania i mają inne aplikacje interfejsu API Zarejestruj hello odnajdywania aplikacji podczas uruchamiania.
4. W czasie wdrażania wypełnić ustawienia aplikacji hello wszystkich hello interfejsu API apps (i klientów) z punktów końcowych hello hello innych aplikacji interfejsu API. Jest to działało, w przypadku wdrożeń szablonu i ponieważ aplikacje interfejsu API umożliwiają teraz kontroli hello adresu URL.

## <a name="using-api-apps-with-logic-apps"></a>Przy użyciu aplikacji interfejsu API w usłudze Logic Apps
Witaj nowego modelu aplikacji interfejsu API dobrze działa z [Logic Apps wersji schematu 2015-08-01](../logic-apps/logic-apps-schema-2015-08-01.md).

## <a name="next-steps"></a>Następne kroki
toolearn więcej, zapoznaj się z artykułami hello w hello [sekcji dokumentacji interfejsu API Apps](https://azure.microsoft.com/documentation/services/app-service/api/). Zostały zaktualizowane tooreflect hello nowego modelu dla aplikacji interfejsu API. Ponadto dotrzeć na forach hello dodatkowe szczegółowe informacje i wskazówki dotyczące migracji:

* [Forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-api-apps)

