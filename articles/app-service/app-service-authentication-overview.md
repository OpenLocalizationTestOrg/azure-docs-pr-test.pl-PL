---
title: "aaaAuthentication i autoryzację w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Odwołanie koncepcyjne i przegląd hello uwierzytelniania / autoryzacji funkcji Azure App Service"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: b7151b57-09e5-4c77-a10c-375a262f17e5
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/29/2016
ms.author: mahender
ms.openlocfilehash: dc2074b16cce47b72b78ea7afeda89dbc4832166
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-app-service"></a>Uwierzytelnianie i autoryzacja w usłudze Azure App Service
## <a name="what-is-app-service-authentication--authorization"></a>Co to jest aplikacja usługi uwierzytelniania / autoryzacji?
Uwierzytelnianie usługi aplikacji / autoryzacja to funkcja umożliwiająca sposób dla twojej aplikacji toosign wśród użytkowników, dzięki czemu nie trzeba toochange kodu aplikacji hello wewnętrznej bazy danych. Zapewnia prosty sposób tooprotect aplikacji i pracy z danymi użytkownika.

Tożsamości federacyjnych, w którym dostawca tożsamości innych firm przechowuje konta i uwierzytelnia użytkowników korzysta z usługi aplikacji. aplikacji Hello zależy od informacji o tożsamości dostawcy hello tak, aby hello aplikacji nie ma toostore tego samych informacji. Usługi aplikacji obsługuje pięć dostawców tożsamości fabrycznej hello: Azure Active Directory, Facebook, Google, Microsoft Account i Twitter. Aplikacji można używać dowolnej liczby te tooprovide dostawców tożsamości użytkowników z opcjami dla sposób logowania się w. wbudowana obsługa hello tooexpand można zintegrować innego dostawcy tożsamości lub [rozwiązania tożsamość niestandardowa][custom-auth].

Jeśli chcesz tooget pracę już teraz, zobacz jedną z następujących samouczków hello:

* [Dodawanie aplikacji dla systemu iOS tooyour uwierzytelniania] [ iOS] (lub [Android], [Windows], [Xamarin.iOS], [ Xamarin.Android], [platformy Xamarin.Forms], lub [Cordova])
* [Uwierzytelnianie użytkownika dla aplikacji interfejsu API w usłudze Azure App Service][apia-user]
* [Wprowadzenie do usługi Azure App Service — część 2][web-getstarted]

## <a name="how-authentication-works-in-app-service"></a>Jak działa uwierzytelniania w usłudze App Service
W kolejności tooauthenticate za pomocą jednego z dostawców tożsamości hello musisz najpierw tooknow dostawcy tożsamości hello tooconfigure dotyczące Twojej aplikacji. Dostawca tożsamości Hello będzie dostarczać identyfikatory i hasła, musisz zapewnić tooApp usługi. Relacja zaufania hello na tym kończy się tak, aby sprawdzić potwierdzenia użytkownika, takich jak tokeny uwierzytelniania z hello dostawcy tożsamości usługi aplikacji.

toosign użytkownika przy użyciu jednej z tych dostawców, hello użytkownik musi być punkt końcowy przekierowanego tooan, który loguje się użytkowników dla tego dostawcy. Jeśli klienci używają przeglądarki sieci web, może mieć usługi aplikacji — automatyczne kierowanie wszystkich endpoint toohello użytkownikom nieuwierzytelnionym użytkownikom zalogowanie się. W przeciwnym razie trzeba będzie toodirect klientów za`{your App Service base URL}/.auth/login/<provider>`, gdzie `<provider>` jest jednym z hello następujące wartości: aad, facebook, google, microsoft lub twitter. Scenariusze mobilnych i interfejsu API opisano szczegółowo w sekcji w dalszej części tego artykułu.

Użytkownicy, którzy korzystają z Twojej aplikacji za pośrednictwem przeglądarki sieci web ma plik cookie skonfigurować tak, aby może pozostawać uwierzytelniony jako przeglądania aplikacji. Dla innych typów klientów, takie jak telefon komórkowy, tokenu web JSON (JWT), które powinny być prezentowane w hello `X-ZUMO-AUTH` nagłówka, które zostaną wystawione toohello klienta. powitania klienta Mobile Apps SDK obsłuży to dla Ciebie. Alternatywnie token tożsamości usługi Azure Active Directory lub token dostępu może być bezpośrednio zawarta w hello `Authorization` nagłówek jako [tokenu elementu nośnego](https://tools.ietf.org/html/rfc6750).

Usługi aplikacji — zostanie przeprowadzona Weryfikacja dowolnego pliku cookie lub token, że aplikacja wystawia tooauthenticate użytkowników. toorestrict, kto ma dostęp do aplikacji, zobacz hello [autoryzacji](#authorization) sekcji w dalszej części tego artykułu.

### <a name="mobile-authentication-with-a-provider-sdk"></a>Przenośne uwierzytelniania za pomocą dostawcy zestawu SDK
Po skonfigurowaniu wszystkich hello wewnętrznej bazy danych można zmodyfikować toosign klientów mobilnych za pomocą usługi aplikacji. Istnieją dwie metody w tym miejscu:

* Korzystanie z zestawu SDK, że dostawca tożsamości danego publikuje tooestablish tożsamości i uzyskać dostęp tooApp usługi.
* Użyj pojedynczy wiersz kodu, aby zalogować się użytkowników powitania klienta Mobile Apps SDK.

> [!TIP]
> Większość aplikacji, należy użyć dostawcy zestawu SDK tooget więcej spójne środowisko podczas logowania, obsługa odświeżania toouse i tooget określa tego dostawcę hello inne korzyści.
> 
> 

Podczas używania dostawcy SDK, użytkownicy mogą rejestrować środowisko tooan, bardziej ściśle zintegrowana z systemem operacyjnym hello, aplikacja hello jest uruchomiona na. Zapewnia to również token dostawcy i niektóre informacje użytkownika na powitania klienta, co pozwala znacznie łatwiejsze wykres tooconsume interfejsów API i dostosować hello środowisko użytkownika. Czasami blogi i fora, zostanie wyświetlony ten hello tooas określonego "przebieg klienta" lub "przepływ skierowane do klienta", ponieważ kod na powitania klienta logowania użytkowników i kod klienta hello ma dostęp tooa dostawcy tokenu.

Po uzyskaniu tokenu dostawcy musi toobe wysyłane tooApp usługi do sprawdzania poprawności. Po usługi aplikacji weryfikuje hello token, usługi aplikacji — tworzy nowy token usługi aplikacji, zwracana toohello klienta. powitania klienta Mobile Apps SDK ma toomanage metody pomocnika tego programu exchange i automatyczne dołączanie hello token tooall żądania toohello aplikacji zaplecza. Deweloperzy mogą również zachować dostawcy tokenu toohello odwołanie, jeśli wybiera on.

### <a name="mobile-authentication-without-a-provider-sdk"></a>Przenośne uwierzytelniania bez dostawcy zestawu SDK
Jeśli nie chcesz, aby tooset się dostawcy SDK, można zezwolić funkcji Mobile Apps hello toosign usłudze Azure App Service w automatycznie. powitania klienta Mobile Apps SDK będzie Otwórz wybrane dostawca toohello widoku sieci web i zaloguj hello użytkownika. Od czasu do czasu na blogi i fora, zobaczysz tego określonego tooas hello "serwera przepływ" lub "przepływ skierowane do serwera" ponieważ powitania serwera zarządza procesem hello, który loguje się użytkowników i powitania klienta SDK nigdy nie otrzyma tokenu dostawcy hello.

Kod toostart, których ten przepływ jest uwzględniona w samouczku uwierzytelniania powitania dla każdej platformy. W końcu hello przepływu hello powitania klienta SDK ma token usługi aplikacji, a hello token jest automatycznie dołączone tooall żądań toohello aplikacji zaplecza.

### <a name="service-to-service-authentication"></a>Uwierzytelnianie między usługami
Mimo że można udzielać użytkownikom dostępu tooyour aplikacji, można również ufać innego toocall aplikacji własnego interfejsu API. Na przykład można mieć jednej aplikacji sieci web wywołania interfejsu API w innej aplikacji sieci web. W tym scenariuszu można używać poświadczeń dla konta usługi zamiast tooget poświadczenia użytkownika tokenu. Konto usługi jest także znana jako *nazwy głównej usługi* w terminologii usługi Azure Active Directory i uwierzytelniania przy użyciu tego konta jest także znana jako scenariusza service-to-service.

> [!IMPORTANT]
> Ponieważ aplikacje mobilne są uruchamiane na urządzeniach klienckich, czy aplikacje mobilne *nie* są liczone jako zaufane aplikacje i nie należy używać przepływu główną usługi. Zamiast tego powinny używać przepływu użytkownika, który został wcześniej szczegółowe.
> 
> 

W przypadku scenariuszy usług usługi aplikacji może chronić aplikacji za pomocą usługi Azure Active Directory. aplikacja wywołująca Hello wystarczy tooprovide token autoryzacji podmiotu zabezpieczeń usługi Azure Active Directory, uzyskany przez podanie Identyfikatora klienta hello i klienta w usłudze Azure Active Directory. Ten scenariusz, który korzysta z aplikacji interfejsu API platformy ASP.NET przykładem tłumaczy samouczek hello [uwierzytelnianie główną usługi dla aplikacji interfejsu API][apia-service].

Jeśli chcesz toouse toohandle uwierzytelniania usługi aplikacji — scenariusz service-to-service, można użyć uwierzytelniania podstawowego lub certyfikatów klienta. Aby uzyskać informacje o certyfikatach klientów na platformie Azure, zobacz [jak tooConfigure TLS wzajemnego uwierzytelniania dla aplikacji sieci Web](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Aby dowiedzieć się, uwierzytelnianie podstawowe w programie ASP.NET, zobacz [filtry uwierzytelniania w ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters).

Uwierzytelnianie konta usługi z usługi aplikacji — logika aplikację tooan interfejsu API aplikacji jest szczegółowo w przypadku specjalne [przy użyciu niestandardowego interfejsu API hostowanych w usłudze aplikacji z usługą Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="authorization"></a>Jak działa autoryzacji w usłudze App Service
Masz pełną kontrolę nad żądań hello, którzy mają dostęp do aplikacji. Aplikacja usługi uwierzytelniania / autoryzacji można skonfigurować za pomocą dowolnego z hello następujące zachowania:

* Zezwalaj tylko tooreach uwierzytelnianych żądań aplikacji.
  
    Jeśli przeglądarka odbierze żądania od użytkowników anonimowych, usługi aplikacji przekieruje strony tooa dla dostawcy tożsamości hello wybranego przez użytkownika, dzięki czemu użytkownicy mogą rejestrować. Jeśli Żądanie hello pochodzi z urządzenia przenośnego, hello zwrócony odpowiedzi HTTP *401 nieautoryzowane* odpowiedzi.
  
    Po wybraniu tej opcji nie ma potrzeby toowrite żadnego kodu uwierzytelniania na wszystkich w aplikacji. Aby uzyskać bardziej precyzyjną autoryzacji, informacje o użytkowniku hello jest dostępne tooyour kodu.
* Zezwalaj na wszystkie tooreach żądań aplikacji, ale poprawności żądań uwierzytelnionych i przekazują informacje o uwierzytelnianiu w nagłówkach hello HTTP.
  
    Opcja ta różni się kod aplikacji tooyour decyzji dotyczących autoryzacji. Większa elastyczność w obsłudze żądań anonimowych, ale masz kod toowrite.
* Zezwalaj na wszystkie tooreach żądań aplikacji, a nie podejmuj żadnej akcji na informacje dotyczące uwierzytelniania w żądaniach hello.
  
    W takim przypadku hello uwierzytelniania / autoryzacji funkcja jest wyłączona. zadania Hello uwierzytelniania i autoryzacji są całkowicie się tooyour kodu aplikacji.

zachowania poprzedniej Hello są kontrolowane przez hello **tootake akcji w przypadku nieuwierzytelnionego żądania** opcję hello portalu Azure. Jeśli wybierzesz ** Zaloguj się przy użyciu *Nazwa dostawcy* **, wszystkie żądania ma toobe uwierzytelniony. **Zezwalaj na żądanie (żadnej akcji)** różni się hello autoryzacji decyzji tooyour kodu, ale nadal zawierają informacje dotyczące uwierzytelniania. Jeśli chcesz toohave swój kod obsługi wszystkich, możesz wyłączyć hello uwierzytelniania / autoryzacji funkcji.

## <a name="working-with-user-identities-in-your-application"></a>Praca z tożsamościami użytkowników w aplikacji
Niektórych aplikacji tooyour informacje użytkownika są przekazywane przez usługę aplikacji za pomocą specjalnych nagłówków. Zewnętrzne żądań Zabroń używania tych nagłówków i zostanie tylko jeśli obecne ustawiona przez aplikację usługi uwierzytelniania / autoryzacji. Niektóre nagłówki przykład obejmują:

* X-MS-KLIENTA-— NAZWA GŁÓWNA
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

Kodu napisanego w dowolnego języka lub platformy można uzyskać informacji hello wymaganych z tych nagłówków. Dla aplikacji platformy ASP.NET 4.6 hello **ClaimsPrincipal** jest ustawiany automatycznie z hello odpowiednie wartości.

Aplikację można również uzyskać szczegóły użytkownika dodatkowe za pośrednictwem HTTP GET na powitania `/.auth/me` punkt końcowy aplikacji. Prawidłowy token, który wchodzi w skład żądania hello będzie zwracać ładunek JSON o szczegółowe informacje dotyczące dostawcy hello, który jest używany, hello podstawowego dostawcy tokenu i inne informacje użytkownika. Witaj serwera Mobile Apps SDK zapewniają metody pomocnicze toowork przy użyciu tych danych. Aby uzyskać więcej informacji, zobacz [jak toouse hello zestaw SDK usługi Azure Mobile Apps Node.js](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-getidentity), i [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#user-info).

## <a name="documentation-and-additional-resources"></a>Dokumentacja i dodatkowe zasoby
### <a name="identity-providers"></a>Dostawców tożsamości
Witaj, jak następujące samouczki Pokaż dostawców uwierzytelniania różnych toouse usługi aplikacji tooconfigure:

* [Jak tooconfigure Logowanie usługi Azure Active Directory toouse aplikacji][AAD]
* [Jak tooconfigure logowanie Facebook toouse aplikacji][Facebook]
* [Jak tooconfigure logowanie Google toouse aplikacji][Google]
* [Jak tooconfigure logowanie Account Microsoft toouse aplikacji][MSA]
* [Jak tooconfigure logowanie Twitter toouse aplikacji][Twitter]

Jeśli chcesz toouse systemu tożsamości inne niż hello te podane w tym miejscu można również użyć hello [obsługę uwierzytelniania niestandardowego w powitania serwera Mobile Apps .NET SDK w wersji preview][custom-auth], której można użyć w aplikacji sieci web aplikacje mobilne lub aplikacje interfejsu API.

### <a name="web-applications"></a>Aplikacje sieci Web
następujące samouczki Hello pokazują, jak jest tooadd tooa uwierzytelniania aplikacji sieci web:

* [Wprowadzenie do usługi Azure App Service — część 2][web-getstarted]

### <a name="mobile-applications"></a>Aplikacje mobilne
następujące samouczki Hello pokazują, jak klientów mobilnych tooyour uwierzytelniania tooadd przy użyciu hello przepływu skierowane do serwera:

* [Dodawanie aplikacji dla systemu iOS tooyour uwierzytelniania][iOS]
* [Dodawanie aplikacji dla systemu Android tooyour uwierzytelniania][Android]
* [Dodawanie aplikacji dla systemu Windows tooyour uwierzytelniania][Windows]
* [Dodaj aplikację platformy Xamarin.iOS tooyour uwierzytelniania][Xamarin.iOS]
* [Dodawanie aplikacji platformy Xamarin.Android tooyour uwierzytelniania][ Xamarin.Android]
* [Dodaj aplikację platformy Xamarin.Forms tooyour uwierzytelniania][platformy Xamarin.Forms]
* [Dodaj aplikację Cordova tooyour uwierzytelniania][Cordova]

Użyj następujących zasobów, jeśli chcesz, aby toouse hello klient skierowany przepływu dla usługi Azure Active Directory hello:

* [Użyj hello biblioteki uwierzytelniania usługi Active Directory dla systemu iOS][ADAL-iOS]
* [Użyj hello biblioteki uwierzytelniania usługi Active Directory dla systemu Android][ADAL-Android]
* [Użyj hello Active Directory Authentication biblioteki dla systemu Windows i Xamarin][ADAL-dotnet]

Użyj następującego zasobów, jeśli chcesz, aby toouse hello klient skierowany przepływu dla usługi Facebook hello:

* [Użyj hello Facebook zestawu SDK dla systemu iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#facebook-sdk)

Użyj powitania po zasobów, jeśli chcesz, aby toouse hello klient skierowany przepływ Twitter:

* [Użyj usługi Twitter sieci szkieletowej dla systemu iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#twitter-fabric)

Użyj hello następujące zasoby, jeśli chcesz, aby toouse hello klient skierowany przepływu dla usług Google:

* [Użyj hello Google logowania zestawu SDK dla systemu iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#google-sdk)

### <a name="api-applications"></a>Aplikacje interfejsu API
Witaj, jak następujące samouczki Pokaż tooprotect aplikacji interfejsu API:

* [Uwierzytelnianie użytkownika dla aplikacji interfejsu API w usłudze Azure App Service][apia-user]
* [Uwierzytelnianie główną usługi dla aplikacji interfejsu API w usłudze Azure App Service][apia-service]

[apia-user]: ../app-service-api/app-service-api-dotnet-user-principal-auth.md
[apia-service]: ../app-service-api/app-service-api-dotnet-service-principal-auth.md

[web-getstarted]: ../app-service-web/app-service-web-get-started-2.md#authenticate-your-users

[iOS]: ../app-service-mobile/app-service-mobile-ios-get-started-users.md
[Android]: ../app-service-mobile/app-service-mobile-android-get-started-users.md
[Xamarin.iOS]: ../app-service-mobile/app-service-mobile-xamarin-ios-get-started-users.md
[ Xamarin.Android]: ../app-service-mobile/app-service-mobile-xamarin-android-get-started-users.md
[platformy Xamarin.Forms]: ../app-service-mobile/app-service-mobile-xamarin-forms-get-started-users.md
[Windows]: ../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-users.md
[Cordova]: ../app-service-mobile/app-service-mobile-cordova-get-started-users.md

[AAD]: ../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md
[Facebook]: ../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md
[Google]: ../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md
[MSA]: ../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md
[Twitter]: ../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md

[custom-auth]: ../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth

[ADAL-Android]: ../app-service-mobile/app-service-mobile-android-how-to-use-client-library.md#adal
[ADAL-iOS]: ../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#adal
[ADAL-dotnet]: ../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md#adal
