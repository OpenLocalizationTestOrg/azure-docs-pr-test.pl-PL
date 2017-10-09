---
title: "aaaAzure usługi Active Directory ograniczenia punktu końcowego v2.0 | Dokumentacja firmy Microsoft"
description: "Lista ograniczenia dla punktu końcowego v2.0 hello Azure AD."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a99289c0-e6ce-410c-94f6-c279387b4f66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: bcbb7239f1d117002d16ac23dca8f1feb13a9161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-use-hello-v20-endpoint"></a>Należy użyć punktu końcowego v2.0 hello?
Podczas tworzenia aplikacji, które integrują się z usługą Azure Active Directory, należy toodecide, czy protokołów uwierzytelniania i punktu końcowego v2.0 hello odpowiadają Twoim potrzebom. Oryginalny punktu końcowego usługi Azure Active Directory firmy jest nadal w pełni obsługiwane i pod pewnymi względami jest więcej zaawansowanej funkcji niż wersja 2.0. Jednak hello punktu końcowego v2.0 [wprowadzono znaczące korzyści](active-directory-v2-compare.md) dla deweloperów.

Oto nasze uproszczony zalecenia dla deweloperów w tym momencie:

* Jeśli zachodzi potrzeba obsługi osobistego konta Microsoft w aplikacji, użyj punktu końcowego v2.0 hello. Jednak zanim to zrobisz, należy się upewnić, że rozumiesz hello ograniczenia, które omówiono w tym artykule.
* Jeśli aplikacja wymaga tylko toosupport pracy firmy Microsoft i konta służbowego, nie używaj hello punktu końcowego v2.0. Zamiast tego należy odwoływać się tooour [przewodnik dewelopera usługi Azure AD](active-directory-developers-guide.md).

Wraz z upływem czasu punktu końcowego v2.0 hello wzrośnie tooeliminate hello ograniczenia wymienione w tym miejscu, dzięki czemu będą tylko trzeba punktu końcowego v2.0 hello toouse. W hello czasu, w tym artykule jest toohelp zamierzone, możesz określić, czy punktu końcowego v2.0 hello jest odpowiednie dla Ciebie. Będziemy nadal tooupdate tego artykułu tooreflect hello bieżący stan punktu końcowego v2.0 hello. Sprawdzać, czy tooreevaluate wymagań możliwościami w wersji 2.0.

Jeśli masz istniejącą aplikację usługi Azure AD, która nie korzysta z punktu końcowego v2.0 hello nie ma toostart nie konieczności od początku. W przyszłości hello firma Microsoft zapewnia łatwy sposób dla toouse możesz istniejących aplikacji usługi Azure AD z punktem końcowym v2.0 hello.

## <a name="restrictions-on-app-types"></a>Ograniczenia dotyczące typów aplikacji
Obecnie hello następujące typy aplikacji nie są obsługiwane przez hello punktu końcowego v2.0. Opis typów obsługiwanych aplikacji, zobacz [typy aplikacji dla punktu końcowego v2.0 usługi Azure Active Directory hello](active-directory-v2-flows.md).

### <a name="standalone-web-apis"></a>Interfejsy API sieci Web autonomiczny
Można użyć punktu końcowego v2.0 hello zbyt[kompilacji API sieci Web chronionej OAuth 2.0](active-directory-v2-flows.md#web-apis). Jednak tego interfejsu API sieci Web może odbierać tokeny tylko z aplikacji, która ma hello sam identyfikator aplikacji. Nie masz dostępu do interfejsu API sieci Web z klienta, który ma inną nazwę aplikacji. powitania klienta nie będzie można toorequest stanie lub uzyskać tooyour uprawnienia interfejsu API sieci Web.

toosee toobuild interfejsu API sieci Web, który akceptuje tokeny od klienta, który ma hello tego samego Identyfikatora aplikacji, zobacz temat hello przykłady interfejsu API sieci Web punktu końcowego v2.0 w naszym [wprowadzenie](active-directory-appmodel-v2-overview.md#getting-started) sekcji.

## <a name="restrictions-on-app-registrations"></a>Ograniczenia dotyczące rejestracji aplikacji
Obecnie dla każdej aplikacji, które mają toointegrate z punktem końcowym v2.0 hello, musisz utworzyć rejestracji aplikacji w hello nowe [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList). Istniejące usługi Azure AD lub nie są zgodne z punktu końcowego v2.0 hello aplikacji konta Microsoft. Aplikacje, które są zarejestrowane w żadnym portalem niż hello portalu rejestracji aplikacji nie są zgodne z punktem końcowym v2.0 hello. W przyszłości hello planujemy tooprovide toouse sposób istniejącej aplikacji jako aplikacji w wersji 2.0. Jednak nie istnieje aktualnie nie ma ścieżki migracji dla istniejących toowork aplikacji z punktem końcowym v2.0 hello.

Ponadto rejestracji aplikacji, które możesz utworzyć w hello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ma hello następujące ostrzeżenia:

* Tylko dwa klucze tajne aplikacji są dozwolone na identyfikator aplikacji.
* Można wyświetlać i zarządzać tylko konto dewelopera pojedynczego rejestracji aplikacji zarejestrowanych przez użytkownika z osobistego konta Microsoft. Nie można współużytkować między wielu deweloperów.  Jeśli chcesz tooshare rejestracji aplikacji wśród wielu deweloperów, można utworzyć aplikacji hello po zalogowaniu się do portalu rejestracji hello przy użyciu konta usługi Azure AD.
* Istnieje kilka ograniczeń na hello format hello przekierowania URI, który jest dozwolony. Aby uzyskać więcej informacji na temat identyfikatorów URI przekierowania zobacz hello następnej sekcji.

## <a name="restrictions-on-redirect-uris"></a>Ograniczenia dotyczące przekierowania URI
Aplikacje, które są zarejestrowane w portalu rejestracji aplikacji hello są obecnie ograniczone tooa ograniczony zestaw wartości identyfikatora URI przekierowania. Witaj przekierowania URI dla usług i aplikacji sieci web musi rozpoczynać się od schematu hello `https`, a wszystkie wartości identyfikatora URI przekierowania musi współdzielenie jednej domeny DNS. Na przykład nie można zarejestrować aplikacji sieci web o jednym z tych identyfikatorów URI przekierowania:

`https://login-east.contoso.com`  
`https://login-west.contoso.com`

system rejestracji Hello porównuje hello całego nazwę DNS hello istniejących przekierowania URI toohello nazwy DNS hello przekierowania URI, który dodajesz. Nazwa DNS hello Hello żądania tooadd zakończy się niepowodzeniem, jeśli jest spełniony dowolny z hello następujące warunki:  

* Hello całą nazwę DNS identyfikator URI przekierowania nowe hello jest niezgodny z nazwy DNS hello identyfikator URI przekierowania istniejących hello.
* Hello całą nazwę DNS identyfikator URI przekierowania nowe hello nie jest poddomeną identyfikatora URI przekierowania istniejących hello.

Na przykład, jeśli aplikacja hello ma ten identyfikator URI przekierowania:

`https://login.contoso.com`

Można dodać tooit w następujący sposób:

`https://login.contoso.com/new`

W takim przypadku nazwa DNS hello są dokładnie. Można też zrobić tak:

`https://new.login.contoso.com`

W takim przypadku odwołujesz poddomenie DNS tooa login.contoso.com. Jeśli chcesz toohave logowania east.contoso.com i west.contoso.com logowania jako identyfikator URI przekierowania aplikacji, należy dodać te przekierowania URI w następującej kolejności:

`https://contoso.com`  
`https://login-east.contoso.com`  
`https://login-west.contoso.com`  

Witaj ostatnie dwa ponieważ są one poddomen hello najpierw identyfikator URI przekierowania, można dodać contoso.com. To ograniczenie zostanie usunięta w przyszłych wersji.

toolearn tooregister jako aplikacja w hello portalu rejestracji aplikacji, zobacz temat [jak tooregister aplikacji z punktem końcowym v2.0 hello](active-directory-v2-app-registration.md).

## <a name="restrictions-on-services-and-apis"></a>Ograniczenia dotyczące usług i interfejsów API
Obecnie obsługuje punktu końcowego v2.0 hello logowania dla wszystkich aplikacji, która jest zarejestrowana w portalu rejestracji aplikacji hello i znajduje się lista hello [obsługiwane przepływów uwierzytelniania](active-directory-v2-flows.md). Jednak te aplikacje mogą uzyskać tokenów dostępu protokołu OAuth 2.0 dla bardzo ograniczony zestaw zasobów. problemy dotyczące punktu końcowego v2.0 Hello dostępu tokeny tylko dla:

* Aplikacja Hello żądanym hello tokenu. Aplikacji można uzyskać tokenu dostępu dla siebie, jeśli aplikację logiczną hello składa się z kilku różnych składników lub warstwy. toosee w tym scenariuszu akcji, zobacz nasze [wprowadzenie](active-directory-appmodel-v2-overview.md#getting-started) samouczki.
* Hello poczty programu Outlook, kalendarza i kontaktów interfejsów API REST, które znajdują się w https://outlook.office.com. toolearn toowrite aplikację, która uzyskuje dostęp do tych interfejsów API, zobacz temat hello [wprowadzenie Office](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2) samouczki.
* Interfejsy API programu Microsoft Graph. Użytkownik może dowiedzieć się więcej o [Microsoft Graph](https://graph.microsoft.io) i hello dane, które są dostępne tooyou.

Żadne inne usługi są obsługiwane w tej chwili. Więcej usług Microsoft Online Services zostaną dodane w przyszłości, hello dodatkowo toosupport własne niestandardowej interfejsów API sieci Web i usług.

## <a name="restrictions-on-libraries-and-sdks"></a>Ograniczenia dotyczące biblioteki i zestawy SDK
Obecnie Obsługa bibliotek dla punktu końcowego v2.0 hello jest ograniczona. Jeśli chcesz toouse punktu końcowego v2.0 hello w aplikacji produkcyjnej, masz tych opcji:

* Jeśli tworzysz aplikację sieci web, można bezpiecznie użyć Microsoft ogólnie dostępna po stronie serwera oprogramowanie pośredniczące tooperform logowania i tokenu weryfikacji. Obejmują one oprogramowanie pośredniczące OWIN Open ID Connect w hello ASP.NET i hello Node.js Passport wtyczki. Aby uzyskać przykłady kodu, korzystających z oprogramowania pośredniczącego firmy Microsoft, zobacz nasze [wprowadzenie](active-directory-appmodel-v2-overview.md#getting-started) sekcji.
* Jeśli tworzysz aplikację desktop lub mobile można użyć jednej z naszym podglądzie biblioteki uwierzytelniania firmy Microsoft (MSAL).  Te biblioteki są w podglądzie obsługiwane w środowisku produkcyjnym, więc jest bezpieczne toouse ich w aplikacji produkcyjnych. Możesz przeczytać więcej informacji na temat warunków hello hello Podgląd i hello dostępnych bibliotek w naszym [dokumentacja bibliotek uwierzytelniania](active-directory-v2-libraries.md).
* W przypadku platform nie pasuje do żadnego biblioteki Microsoft można zintegrować z punktu końcowego v2.0 hello przez bezpośrednie wysyłanie i odbieranie wiadomości protokołu w kodzie aplikacji. Witaj protokoły OpenID Connect i OAuth 2.0 [są udokumentowane](active-directory-v2-protocols.md) toohelp wykonywać takie integracji.
* Na koniec można open source Otwórz ID Connect i OAuth bibliotek toointegrate z punktem końcowym v2.0 hello. Protokół v2.0 Hello powinna być zgodna z wielu bibliotek protokołu open source bez istotne zmiany. dostępność Hello tego rodzaju biblioteki jest zależna od języka i platformy. Witaj [Open ID Connect](http://openid.net/connect/) i [OAuth 2.0](http://oauth.net/2/) listę popularnych implementacje Obsługa witryn sieci Web. Aby uzyskać więcej informacji, zobacz [biblioteki Azure Active Directory w wersji 2.0 i uwierzytelniania](active-directory-v2-libraries.md)i listę powitania klienta open source biblioteki i przykłady, które zostały przetestowane z punktem końcowym v2.0 hello.

## <a name="restrictions-on-protocols"></a>Ograniczenia protokołów
punktu końcowego v2.0 Hello nie obsługuje SAML lub WS-Federation; obsługuje tylko Open ID Connect i OAuth 2.0.  Nie wszystkie funkcje i możliwości protokołów OAuth zostały włączone do punktu końcowego v2.0 hello. Te funkcje protokołu i możliwości są obecnie *nie jest dostępny* w punktu końcowego v2.0 hello:

* Nie zawierają tokeny Identyfikatora, które są wydawane przez punktu końcowego v2.0 hello `email` oświadczenia dla użytkownika hello, nawet jeśli w przypadku uzyskania zgody tooview użytkownika hello poczty e-mail.
* punkt końcowy protokołu OpenID Connect UserInfo Hello nie został zaimplementowany dla punktu końcowego v2.0 hello. Jednak wszystkie dane profilu użytkownika, które potencjalnie będą pojawi się w tym punkcie końcowym jest dostępna z hello Microsoft Graph `/me` punktu końcowego.
* punktu końcowego v2.0 Hello nie obsługuje wystawiającego oświadczeń roli lub grupy w tokenach identyfikator.
* Witaj [2.0 właściciela zasobów hasło poświadczeń OAuth](https://tools.ietf.org/html/rfc6749#section-4.3) nie jest obsługiwany przez hello punktu końcowego v2.0.

W addtion punktu końcowego v2.0 hello nie obsługuje żadnych formularza hello SAML lub protokołów WS-Federation.

toobetter zrozumieć zakres hello protokołu funkcje obsługiwane w hello punktu końcowego v2.0, zapoznaj się z artykułem naszych [referencyjne protokołu OpenID Connect i OAuth 2.0](active-directory-v2-protocols.md).

## <a name="restrictions-for-work-and-school-accounts"></a>Ograniczenia dotyczące kont służbowych
Jeśli Active Directory Authentication Library (ADAL) była używana w aplikacjach systemu Windows, mogą miały zaletą zintegrowanego uwierzytelniania systemu Windows, które używa hello Security (Assertion Markup Language SAML) potwierdzenia grant. Z tym grant użytkowników federacyjnych usługi Azure AD dzierżaw dyskretnie mogą uwierzytelniać się w ich lokalnym wystąpieniem usługi Active Directory bez konieczności wprowadzania poświadczeń. Obecnie grant potwierdzenia SAML hello jest nieobsługiwana w punkcie końcowym v2.0 hello.
