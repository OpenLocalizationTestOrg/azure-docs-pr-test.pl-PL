---
title: "przy użyciu logowania tooa interfejsu API sieci web .NET MVC aaaAdd hello punktu końcowego v2.0 usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Jak toobuild interfejs Api sieci Web .NET MVC, który akceptuje tokeny od obu Account firmy Microsoft i konta firmowego lub szkolnego."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a>Zabezpiecz interfejs API web MVC
Z punktem końcowym v2.0 hello Azure Active Directory, można chronić przy użyciu interfejsu API sieci Web [OAuth 2.0](active-directory-v2-protocols.md) tokenów dostępu, włączenie użytkowników z obu osobistego konta Microsoft i konta służbowe toosecurely dostęp do interfejsu API sieci Web.

> [!NOTE]
> Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.  toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
>
>

W sieci web ASP.NET interfejsów API można to zrobić za pomocą oprogramowania pośredniczącego OWIN firmy Microsoft włączone w programie .NET Framework 4.5.  W tym miejscu użyjemy toobuild OWIN interfejs API sieci Web MVC "tooDo listy" umożliwia klientom toocreate i Odczyt zadań z listy zadań do wykonania przez użytkownika.  Hello interfejsu API sieci web zostanie przeprowadzona Weryfikacja, czy żądania przychodzące zawiera prawidłowy dostęp do tokenu i Odrzuć wszelkie żądania nie przeszedł pomyślnie weryfikacji w trasie chronionych.  W tym przykładzie został utworzony przy użyciu programu Visual Studio 2015.

## <a name="download"></a>Do pobrania
Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).  toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) lub klonowania hello szkielet:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

szkielet aplikacji Hello obejmuje wszystkie hello schematyczny kod prosty interfejs API, ale brakuje wszystkie części hello dotyczące tożsamości. Jeśli nie chcesz toofollow wzdłuż, zamiast tego można sklonować lub [pobieranie próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a>Rejestracja aplikacji
Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).  Upewnij się, że:

* Skopiuj hello **identyfikator aplikacji** przypisany tooyour aplikacji, będzie on potrzebny wkrótce.

To rozwiązanie visual studio zawiera także "TodoListClient", która jest prosta aplikacja WPF.  Hello TodoListClient jest używany toodemonstrate sposób logowania użytkownika i jak wystawiać klient żąda tooyour interfejsu API sieci Web.  W takim przypadku zarówno hello TodoListClient i hello TodoListService są reprezentowane przez hello tej samej aplikacji.  tooconfigure hello TodoListClient, należy również:

* Dodaj hello **Mobile** platformy aplikacji.

## <a name="install-owin"></a>Instalowanie interfejsu OWIN
Został zarejestrowany aplikację, trzeba tooset się toocommunicate Twojej aplikacji z punktem końcowym v2.0 hello w kolejności toovalidate przychodzących żądań & tokenów.

* toobegin, otwórz rozwiązanie hello i Dodaj hello OWIN oprogramowanie pośredniczące NuGet pakiety toohello TodoListService projektu przy użyciu konsoli Menedżera pakietów hello.

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a>Konfigurowanie uwierzytelniania OAuth
* Dodaj OWIN klasy toohello TodoListService projekt startowy o nazwie `Startup.cs`.  Kliknij prawym przyciskiem projekt hello myszy--> **Dodaj** --> **nowy element** --> Wyszukaj "OWIN".  oprogramowanie pośredniczące OWIN Hello wywoła hello `Configuration(…)` metody podczas uruchamiania aplikacji.
* Zmiana deklaracji klasy hello zbyt`public partial class Startup` — już zaimplementowano część tej klasy dla Ciebie w innym pliku.  W hello `Configuration(…)` metody, należy tooset tooConfgureAuth(...) wywołania zapasowej uwierzytelniania dla aplikacji sieci web.

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* Otwórz hello pliku `App_Start\Startup.Auth.cs` i wdrożenie hello `ConfigureAuth(…)` metodę, która zostanie skonfigurowana hello interfejsu API sieci Web tooaccept tokenów z punktu końcowego v2.0 hello.

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* Teraz można używać `[Authorize]` atrybutów tooprotect Twojego kontrolerów i akcji przy użyciu uwierzytelniania elementu nośnego OAuth 2.0.  Dekoracji hello `Controllers\TodoListController.cs` klasy z tagiem autoryzacji.  Spowoduje to wymuszenie hello toosign użytkownika w przed uzyskaniem dostępu do tej strony.

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* Gdy Autoryzowany rozmówca pomyślnie wywołuje jeden hello `TodoListController` interfejsów API, akcja hello mogą muszą uzyskiwać dostęp do tooinformation o hello wywołującego.  OWIN zapewnia dostęp toohello oświadczenia w tokenie hello elementu nośnego za pośrednictwem hello `ClaimsPrincpal` obiektu.  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* Na koniec Otwórz hello `web.config` plików w katalogu głównym hello hello TodoListService projektu, a następnie wprowadź wartości konfiguracji w hello `<appSettings>` sekcji.
  * Twoje `ida:Audience` jest hello **identyfikator aplikacji** aplikacji hello, którą wprowadzono w portalu hello.

## <a name="configure-hello-client-app"></a>Konfigurowanie aplikacji klienta hello
Zanim zobaczysz hello usługi listy Todo w akcji, należy tooconfigure powitania klienta listy Todo, mogą uzyskać tokeny z punktu końcowego v2.0 hello i wprowadzić wywołania toohello usługi.

* W projekcie TodoListClient hello Otwórz `App.config` , a następnie wprowadź wartości konfiguracji w hello `<appSettings>` sekcji.
  * Twoje `ida:ClientId` skopiowany z portalu hello identyfikator aplikacji.

Ponadto wyczyścić, skompilować i uruchomić każdy projekt!  Masz teraz interfejs API sieci Web .NET MVC, który akceptuje tokeny od oba osobistego konta Microsoft i konta firmowego lub szkolnego.  Zaloguj się do hello TodoListClient i Wywołaj listy zadań do wykonania w sieci web interfejsu api tooadd zadania toohello użytkownika.

Odwołania, hello ukończone próbka (bez wartości konfiguracji) [jest dostarczane jako zip w tym miejscu](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), lub można ją sklonować z serwisu GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a>Następne kroki
Możesz teraz przejść do dodatkowe tematy.  Można tootry:

[Wywoływanie interfejsu API sieci Web z aplikacji sieci Web >>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

Aby uzyskać dodatkowe zasoby Zobacz:

* [Przewodnik dewelopera v2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [Tag StackOverflow "azure-active-directory" >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Pobierz aktualizacje zabezpieczeń naszych produktów
Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez wizytę [tę stronę](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.
