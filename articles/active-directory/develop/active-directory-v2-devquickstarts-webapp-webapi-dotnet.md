---
title: "Wywołanie interfejsu API aplikacji wprowadzenie sieci web 2.0 aaaAzure AD .NET | Dokumentacja firmy Microsoft"
description: "Jak toobuild aplikacji sieci Web MVC .NET, która wywołuje sieci web usług przy użyciu Microsoft osobiste konta i służbowe kont logowania."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1a70791418bc2a7d1fdfbafb9b5126a033a32292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a>Wywoływanie interfejsu API sieci web z aplikacji sieci web .NET
Z punktem końcowym v2.0 hello można szybko dodać aplikacje sieci web tooyour uwierzytelniania i interfejsów API sieci web o obsługę zarówno osobistego konta Microsoft i konta służbowego.  W tym miejscu firma Microsoft będzie kompilacji aplikacji sieci web MVC, który zaloguje się użytkowników przy użyciu protokołu OpenID Connect, z niektórych pomoc od firmy Microsoft oprogramowania pośredniczącego OWIN.  Hello aplikacji sieci web pobieranie tokenów dostępu protokołu OAuth 2.0 dla sieci web interfejsu api zabezpieczone przez OAuth 2.0, który pozwala utworzyć, odczytać i delete na określony użytkownik "listą zadań do wykonania".

W tym samouczku zostanie skupić się głównie na przy użyciu MSAL tooacquire i używaj tokenów dostępu w aplikacji sieci web, w pełni opisane [tutaj](active-directory-v2-flows.md#web-apps).  Jako wymagania wstępne, może być toofirst Dowiedz się, jak za[dodać podstawowe tooa logowania w aplikacji sieci web](active-directory-v2-devquickstarts-dotnet-web.md) lub jak zbyt[właściwie zabezpieczyć interfejs API sieci web](active-directory-v2-devquickstarts-dotnet-api.md).

> [!NOTE]
> Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.  toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-sample-code"></a>Pobierz przykładowy kod
Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).  toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) lub klonowania hello szkielet:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

Można też [Pobierz aplikację ukończyć powitalnych jako .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) lub klonowania ukończyć powitalnych aplikacji:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a>Rejestracja aplikacji
Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).  Upewnij się, że:

* Skopiuj hello **identyfikator aplikacji** przypisany tooyour aplikacji, będzie on potrzebny wkrótce.
* Utwórz **klucz tajny aplikacji** z hello **hasło** typu i skopiuj jej wartość na później
* Dodaj hello **Web** platformy aplikacji.
* Wprowadź poprawny hello **identyfikator URI przekierowania**. Witaj identyfikatora uri przekierowania wskazuje tooAzure AD którym powinny być kierowane odpowiedzi uwierzytelniania — Witaj domyślną w tym samouczku jest `https://localhost:44326/`.

## <a name="install-owin"></a>Instalowanie interfejsu OWIN
Dodaj hello OWIN oprogramowanie pośredniczące NuGet pakiety toohello `TodoList-WebApp` projekt za pomocą hello Konsola Menedżera pakietów.  oprogramowanie pośredniczące OWIN Hello jest używane tooissue żądań logowania i wylogowywania, zarządzanie sesji użytkownika hello i uzyskać informacje o użytkowniku hello, między innymi.

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a>Hello logowania użytkownika
Teraz skonfigurować hello OWIN oprogramowanie pośredniczące toouse hello [protokołu uwierzytelniania OpenID Connect](active-directory-v2-protocols.md).  

* Otwórz hello `web.config` pliku w katalogu głównym hello hello `TodoList-WebApp` projektu, a następnie wprowadź wartości konfiguracji aplikacji w hello `<appSettings>` sekcji.
  * Witaj `ida:ClientId` jest hello **identyfikator aplikacji** przypisane tooyour aplikacji w portalu rejestracji hello.
  * Witaj `ida:ClientSecret` jest hello **klucz tajny aplikacji** utworzone w portalu rejestracji hello.
  * Witaj `ida:RedirectUri` jest hello **identyfikator Uri przekierowania** wprowadzony w portalu hello.
* Otwórz hello `web.config` pliku w katalogu głównym hello hello `TodoList-Service` projektu i Zastąp hello `ida:Audience` z hello sam **identyfikator aplikacji** zgodnie z powyższym.
* Witaj Otwórz plik `App_Start\Startup.Auth.cs` i Dodaj `using` instrukcje dla bibliotek powitania od góry.
* W hello tego samego pliku, implementować hello `ConfigureAuth(...)` metody.  Witaj podane parametry `OpenIDConnectAuthenticationOptions` będzie służyć jako współrzędne toocommunicate Twojej aplikacji z usługą Azure AD.

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // hello `Authority` represents hello v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // hello `Scope` describes hello permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure hello user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // hello `AuthorizationCodeReceived` notification is used toocapture and redeem hello authorization_code that hello v2.0 endpoint returns tooyour app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-tooget-access-tokens"></a>Używaj tokenów dostępu tooget MSAL
W hello `AuthorizationCodeReceived` powiadomień, chcemy toouse [OAuth 2.0 w połączeniu z OpenID Connect](active-directory-v2-protocols.md) authorization_code hello tooredeem dla toohello token dostępu usługi listy zadań do wykonania.  MSAL może ułatwić ten proces można:

* Najpierw zainstaluj wersję zapoznawczą hello MSAL:

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* I dodać kolejne `using` toohello instrukcji `App_Start\Startup.Auth.cs` MSAL w pliku.
* Teraz Dodaj nową metodę hello `OnAuthorizationCodeReceived` obsługi zdarzeń.  Ten program obsługi zostanie użyty tooacquire MSAL toohello tokenu dostępu do interfejsu API listy zadań do wykonania i będą przechowywane w pamięci podręcznej tokenu w MSAL hello token na później:

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* W aplikacji sieci web MSAL ma rozszerzonego tokenu pamięci podręcznej, które mogą być używane toostore tokenów.  W tym przykładzie implementuje hello `NaiveSessionCache` , który używa tokenów toocache magazynu sesji http.

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a>Witaj wywołania interfejsu API sieci Web
Teraz nadszedł czas, tooactually Użyj hello ' access_token ', które zostało zakupione w kroku 3.  Aplikacja sieci web Otwórz hello `Controllers\TodoListController.cs` pliku, który sprawia, że wszystkie hello CRUD żądań toohello interfejsu API listy zadań do wykonania.

* Można użyć MSAL ponownie tutaj access_tokens toofetch z hello MSAL pamięci podręcznej.  Najpierw dodaj `using` instrukcji MSAL toothis pliku.
  
    `using Microsoft.Identity.Client;`
* W hello `Index` akcji, użyj MSAL `AcquireTokenSilentAsync` tooget metody ' access_token ', które mogą być używane tooread danych z hello usługi listy zadań do wykonania:

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* Witaj próbki dodaje hello wynikowy token toohello żądanie HTTP GET jako hello `Authorization` nagłówka, które usługa listy zadań do wykonania hello używa tooauthenticate hello żądania.
* Jeśli zwróci hello usługi listy zadań do wykonania `401 Unauthorized` odpowiedzi, access_tokens hello w MSAL stały się nieprawidłowy jakiegoś powodu.  W takim przypadku należy porzucić wszystkie access_tokens z hello MSAL pamięci podręcznej i wyświetla komunikat potrzebnych toosign w ponownie, który zostanie uruchomiony ponownie przepływ tokenu nabycia hello hello użytkownika.

```C#
// ...
// If hello call failed with access denied, then drop hello current access token from hello cache,
// and show hello user an error indicating they might need toosign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need toosign in again.");
}
// ...
```

* Podobnie jeśli MSAL tooreturn ' access_token ' jakiejkolwiek przyczyny, należy poinstruować hello toosign użytkownika w ponownie.  Jest tak proste, jak przechwytywanie dowolnego `MSALException`:

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* Witaj dokładnie takie same `AcquireTokenSilentAsync` wywołanie jest implementd w hello `Create` i `Delete` akcje.  W aplikacji sieci web można użyć tego access_tokens tooget metody MSAL zawsze, gdy są potrzebne w Twojej aplikacji.  MSAL zajmie się pobieranie, buforowanie i odświeżanie tokenów.

Na koniec Skompiluj i uruchom aplikację!  Zaloguj się przy użyciu Account Microsoft lub konta usługi Azure AD i zwróć uwagę, jak tożsamość użytkownika hello jest widoczny w hello górnym pasku nawigacyjnym.  Dodaj i usuń niektóre elementy z listy zadań do wykonania hello użytkownika, powitalne toosee OAuth 2.0 zabezpieczone interfejsu API wywołuje w akcji.  Masz teraz aplikacji sieci web i interfejsu API sieci web, zarówno zabezpieczone przy użyciu standardowych protokołach branżowych, uwierzytelniających użytkowników przy użyciu ich osobistych i pracy/służbowego konta.

Odwołania, hello ukończone próbka (bez wartości konfiguracji) [podano tutaj](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).  

## <a name="next-steps"></a>Następne kroki
Aby uzyskać dodatkowe zasoby Zobacz:

* [Przewodnik dewelopera v2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [Tag StackOverflow "azure-active-directory" >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Pobierz aktualizacje zabezpieczeń naszych produktów
Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez wizytę [tę stronę](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.

