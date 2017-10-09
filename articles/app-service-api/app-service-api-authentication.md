---
title: "aaaAuthentication i autoryzacji dla aplikacji interfejsu API w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat usług uwierzytelniania i autoryzacji hello dostępnych w usłudze Azure App Service dla aplikacji interfejsu API."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: d620b53a-5a6f-41c9-84c7-f7ef5ff02ae7
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: alkarche
ms.openlocfilehash: 6d26754b8b606ec232a74768787922ea80577c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a>Uwierzytelnianie i autoryzacja aplikacji interfejsu API w usłudze Azure App Service
## <a name="overview"></a>Omówienie
> [!NOTE]
> W tym temacie zostaną zmigrowane tooa skonsolidowane [aplikacji usługi uwierzytelniania / autoryzacji](../app-service/app-service-authentication-overview.md) temat, który obejmuje aplikacje interfejsu API, mobilne i sieci Web.
> 
> 

Usługa aplikacji Azure oferuje wbudowane uwierzytelnianie i autoryzacja usługi, które implementują [OAuth 2.0](#oauth) i [OpenID Connect](#oauth). W tym artykule opisano hello usług i opcje, które są dostępne dla aplikacji interfejsu API w usłudze Azure App Service.

powitania po diagram przedstawia niektóre właściwości klucza uwierzytelniania usługi aplikacji:

* Go przetwarza wstępnie przychodzące żądania interfejsu API, co oznacza, że działa on z dowolnego języka lub platformy obsługiwanej przez usługę App Service.
* Udostępnia interesujące kilka opcji ile uwierzytelnianie działa, możesz toodo w swoim własnym kodem.
* Działa ona zarówno użytkowników końcowych, jak i uwierzytelnianie konta usługi. 
* Obsługuje ona pięć dostawców tożsamości: Azure Active Directory, Facebook, Google, Twitter i Account firmy Microsoft.
* Jego działania hello takie same dla aplikacji interfejsu API, aplikacji sieci Web i aplikacje mobilne.

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a>Niezależny od języka
Przetwarzanie uwierzytelniania usługi aplikacji znajduje się przed żądań osiągnąć aplikacji interfejsu API, co oznacza, że działanie funkcji uwierzytelniania hello dla aplikacji interfejsu API w dowolnego języka lub struktury.  Interfejs API może bazować na ASP.NET, Java, Node.js lub dowolnej architektury obsługującej usługi aplikacji.

Usługi aplikacji przekazuje tokenu web JSON hello (JWT) w nagłówku autoryzacji hello żądania HTTP, a kod napisany w dowolnego języka lub struktury mogą pobrać hello informacji wymaganych z hello tokenu. Ponadto usługi aplikacji umożliwia łatwiejsze dostęp oświadczeń toohello najczęściej używane przez ustawienie niektórych specjalnych nagłówków, takie jak następujące hello:

* X-MS-KLIENTA-— NAZWA GŁÓWNA
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

W interfejs API programu .NET, można użyć hello `Authorize` atrybutu, a dla szczegółowych autoryzacji można łatwo zapisu kodu na podstawie oświadczenia, ponieważ informacje o oświadczeniach jest wypełniana automatycznie klas .NET.

## <a name="multiple-protection-options"></a>Wiele opcji ochrony
Usługi aplikacji można zapobiec osiągnięciu aplikacji interfejsu API anonimowe żądania HTTP, można przekazać we wszystkich żądaniach i sprawdzania poprawności tokenów dla żądania zawierające je lub jego pozwolić za pośrednictwem wszystkich żądań bez podejmowania żadnych działań na nich:

1. Zezwalaj tylko tooreach uwierzytelnianych żądań aplikacji interfejsu API.
   
    Odebranie żądania od użytkowników anonimowych z przeglądarki, usługa aplikacji przekieruje tooa strony logowania dla dostawcy uwierzytelniania hello (Azure AD, Google, Twitter, itp.) wybrane. 
   
    Po wybraniu tej opcji nie należy toowrite żadnego kodu uwierzytelniania na wszystkich w aplikacji, a kod autoryzacji jest uproszczone, ponieważ oświadczeń najważniejszych hello są udostępniane w nagłówkach hello HTTP.
2. Zezwalaj na wszystkie żądania tooreach aplikacja interfejsu API, ale poprawności żądań uwierzytelnionych i przekazują informacje o uwierzytelnianiu w nagłówkach hello HTTP.
   
    Opcja ta zapewnia większą elastyczność podczas obsługi żądań anonimowych, ale masz kod toowrite, jeśli chcesz, aby użytkownicy anonimowi tooprevent z przy użyciu interfejsu API. Ponieważ hello najpopularniejszych oświadczenia są przekazywane w hello nagłówków żądań HTTP, Kod autoryzacji jest stosunkowo proste.
3. Zezwalaj na wszystkie tooreach żądania interfejsu API, na informacje dotyczące uwierzytelniania w żądaniach hello Nie podejmuj żadnej akcji.
   
    Ta opcja pozostawia zadania hello uwierzytelniania i autoryzacji całkowicie się tooyour kodu aplikacji.

W hello [portalu Azure](https://portal.azure.com/), wybierz opcję hello na powitania **uwierzytelniania / autoryzacji** bloku.

![](./media/app-service-api-authentication/authblade.png)

Dla opcji 1 i 2, Włącz **aplikacji uwierzytelniania usługi**w hello **tootake akcji w przypadku nieuwierzytelnionego żądania** listy rozwijanej wybierz **Zaloguj** lub **Zezwalaj na żądanie (żadnej akcji)**.  Jeśli wybierzesz **Zaloguj**, ma toochoose dostawcy uwierzytelniania i konfigurowania tego dostawcy.

![](./media/app-service-api-authentication/actiontotake.png)

Aby uzyskać szczegółowe informacje na temat uwierzytelniania tooconfigure, zobacz [jak tooconfigure Logowanie usługi Azure Active Directory toouse aplikacji usługi App Service](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Hello artykuł dotyczy tooAPI aplikacji, a także aplikacje mobilne i łączy tooother artykułów dla hello innych dostawców uwierzytelniania.

## <a id="internal"></a>Uwierzytelnianie konta usługi
Usługi aplikacji — uwierzytelnianie działa w przypadku wewnętrznego scenariuszy takich jak telefonicznej z jednej aplikacji interfejsu API tooanother aplikacji interfejsu API. W tym scenariuszu należy uzyskać token przy użyciu poświadczeń dla konta usługi zamiast poświadczeń użytkownika końcowego. Konto usługi jest także znana jako *nazwy głównej usługi* w usłudze Azure Active Directory, a uwierzytelnianie przy użyciu tego konta jest także znana jako scenariusza service-to-service. 

W przypadku scenariuszy usług — ochrona powitalnych wywołuje aplikację interfejsu API za pomocą usługi Azure Active Directory i podaj token autoryzacji głównej usługi AAD po wywołaniu aplikacji hello interfejsu API. Należy uzyskać token przez podanie Identyfikatora klienta hello i klienta w hello usługi AAD aplikacji. Nie specjalne kod tylko do platformy Azure jest wymagane, na przykład true toobe używanych do obsługi hello token Zumo usług Mobile. Ten scenariusz przy użyciu aplikacji interfejsu API platformy ASP.NET przykładem jest objęta samouczek hello [uwierzytelnianie główną usługi dla aplikacji interfejsu API](app-service-api-dotnet-service-principal-auth.md).

Jeśli chcesz toohandle scenariusza service-to-service bez korzystania z usługi aplikacji uwierzytelniania, można użyć uwierzytelniania podstawowego lub certyfikatów klienta. Aby uzyskać informacje o certyfikatach klientów na platformie Azure, zobacz [jak tooConfigure TLS wzajemnego uwierzytelniania dla aplikacji sieci Web](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Aby dowiedzieć się, uwierzytelnianie podstawowe w programie ASP.NET, zobacz [filtry uwierzytelniania w ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters).

Uwierzytelnianie konta usługi z usługi aplikacji — logika aplikację tooan interfejsu API aplikacji jest szczególnych przypadkach, który znajduje się w [przy użyciu niestandardowego interfejsu API hostowanych w usłudze aplikacji z usługą Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="mobile-client-authentication"></a>Uwierzytelnianie klientów urządzeń przenośnych
Aby uzyskać informacje na temat toohandle uwierzytelnianie klientów mobilnych, zobacz hello [dokumentacji dotyczące uwierzytelniania dla aplikacji mobilnych](../app-service-mobile/app-service-mobile-ios-get-started-users.md). Działania uwierzytelniania usługi aplikacji hello taki sam sposób dla aplikacji mobilnych i aplikacji API apps.

## <a name="more-information"></a>Więcej informacji
Aby uzyskać więcej informacji o uwierzytelnianiu i autoryzacji w usłudze Azure App Service zobacz następujące zasoby hello:

* [Powiększające uwierzytelniania usługi aplikacji / autoryzacji](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* [Jak tooconfigure Logowanie usługi Azure Active Directory toouse aplikacji usługi App Service](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (zawiera łącza do innych dostawców uwierzytelniania na początku hello hello strony). 

Aby uzyskać więcej informacji na temat protokołu OAuth 2.0, OpenID Connect i tokenów sieci Web JSON (JWT) zobacz następujące zasoby hello.

* [Wprowadzenie do korzystania z protokołu OAuth 2.0](http://shop.oreilly.com/product/0636920021810.do "wprowadzenie do korzystania z protokołu OAuth 2.0") 
* [TooOAuth2 wprowadzenie OpenID Connect i sieci Web JSON tokeny (JWT) - kursu Pluralsight](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [Tworzenie i zabezpieczanie interfejsu API RESTful dla wielu klientów w programie ASP.NET - kursu Pluralsight](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

Aby uzyskać więcej informacji na temat usługi Azure Active Directory zobacz następujące zasoby hello.

* [Scenariusze usługi Azure AD](http://aka.ms/aadscenarios)
* [Przewodnik Azure deweloperzy AD](http://aka.ms/aaddev)
* [Przykłady Azure AD](http://aka.ms/aadsamples)

## <a name="next-steps"></a>Następne kroki
Ten artykuł zawiera wyjaśniono funkcji uwierzytelnianie i autoryzacja usługi App Service można użyć dla aplikacji interfejsu API. Następny samouczek Hello uzyskiwania hello uruchomiona serii przedstawiono sposób tooimplement [uwierzytelniania użytkowników w aplikacjach interfejsu API usługi aplikacji](app-service-api-dotnet-user-principal-auth.md).

