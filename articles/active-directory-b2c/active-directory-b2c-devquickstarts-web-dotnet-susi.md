---
title: aaaAzure Active Directory B2C | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji sieci web, z konta-konta/logowania, profilu edycji, a hasło resetowania przy użyciu usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a>Tworzenie aplikacji sieci web platformy ASP.NET z usługi Azure Active Directory B2C profilu rejestracji, logowania, edycji i resetowania hasła

Ten samouczek przedstawia sposób wykonania następujących czynności:

> [!div class="checklist"]
> * Dodawanie aplikacji sieci web tooyour funkcje tożsamości usługi Azure AD B2C
> * Rejestrowanie aplikacji sieci web w katalogu usługi Azure AD B2C
> * Tworzenie użytkownika konta-konta/logowania, edycji profilu i zasady resetowania hasła dla aplikacji sieci web

## <a name="prerequisites"></a>Wymagania wstępne

- Należy połączyć z tooan dzierżawy B2C konto platformy Azure. Możesz utworzyć bezpłatne konto platformy Azure [tutaj](https://azure.microsoft.com/en-us/).
- Należy [programu Microsoft Visual Studio](https://www.visualstudio.com/) lub podobnych program tooview i zmodyfikuj hello przykładowy kod.

## <a name="create-an-azure-ad-b2c-directory"></a>Tworzenie katalogu usługi Azure AD B2C

Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę. Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i inne. Jeśli nie masz już, tworzenia katalogu B2C, przed kontynuowaniem w tym przewodniku.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> Należy tooconnect hello dzierżawy B2C tooyour subskrypcji platformy Azure. Po wybraniu **Utwórz**, wybierz pozycję hello **toomy dzierżawy łącze istniejącej usługi Azure AD B2C subskrypcji platformy Azure** opcji, a następnie w hello **dzierżawy usługi Azure AD B2C** listy rozwijanej wybierz pozycję Dzierżawca Hello ma tooassociate.

## <a name="create-and-register-an-application"></a>Tworzenie i rejestrowania aplikacji

Następnie należy toocreate i rejestrowanie aplikacji hello w katalogu usługi B2C. Zapewnia to informacji wymaganych przez program Azure AD B2C toosecurely komunikacji z aplikacją. 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

Gdy wszystko będzie gotowe, będzie mieć zarówno interfejs API i aplikacji natywnej w ustawienia aplikacji.

## <a name="create-policies-on-your-b2c-tenant"></a>Tworzenie zasad na dzierżawę B2C

W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md). Ten przykładowy kod obejmuje trzy środowiska tożsamości: **rejestracji i logowania**, **edycji profilu**, i **resetowania hasła**.  Należy jedna zasada toocreate każdego typu zgodnie z opisem w hello [artykule o zasadach](active-directory-b2c-reference-policies.md). Dla każdej zasady można się, że atrybut nazwy wyświetlania hello tooselect lub oświadczeń i toocopy dół hello nazwę tej zasady do późniejszego użycia.

### <a name="add-your-identity-providers"></a>Dodaj użytkownika dostawców tożsamości

Wybierz z ustawień **dostawców tożsamości** i wybierz polecenie zapisywania nazwy użytkownika lub rejestracji poczty E-mail.

### <a name="create-a-sign-up-and-sign-in-policy"></a>Tworzenie zasad rejestracji i logowania

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a>Utwórz profil edytowanie zasad

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a>Utwórz zasady resetowania hasła

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

Po utworzeniu zasad, wszystko jest gotowe toobuild aplikacji.

## <a name="download-hello-sample-code"></a>Pobierz hello przykładowy kod

Witaj kod dla tego samouczka jest przechowywany w [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Przykład Witaj można sklonować, uruchamiając:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Po pobraniu hello przykładowy kod tooget plik SLN programu Visual Studio Otwórz hello jest uruchomiona. Witaj plik rozwiązania zawiera dwa projekty: `TaskWebApp` i `TaskService`. `TaskWebApp`jest hello aplikację sieci web MVC hello użytkownik wchodzi w interakcję z. `TaskService`to interfejs API sieci web zaplecza aplikacji hello, który przechowuje listy zadań do wykonania poszczególnych użytkowników. W tym artykule przedstawimy tylko hello `TaskWebApp` aplikacji. toolearn jak toobuild `TaskService` za pomocą usługi Azure AD B2C, zobacz [naszym samouczkiem interfejsu api sieci web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="update-code-toouse-your-tenant-and-policies"></a>Aktualizowanie kodu toouse dzierżawy i zasady

Naszej próbki jest skonfigurowany toouse hello zasady i klienta identyfikator dzierżawy naszych pokaz. tooconnect on tooyour własne dzierżawy, należy tooopen `web.config` w hello `TaskWebApp` projektu i Zastąp hello następujące wartości:

* `ida:Tenant` nazwą dzierżawy
* `ida:ClientId` identyfikatorem aplikacji sieci Web
* `ida:ClientSecret` kluczem tajnym aplikacji sieci Web
* `ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania
* `ida:EditProfilePolicyId` nazwą zasady edycji profilu
* `ida:ResetPasswordPolicyId` nazwą zasady resetowania hasła

## <a name="launch-hello-app"></a>Uruchamianie aplikacji hello
Z poziomu programu Visual Studio, uruchomienie aplikacji hello. Przejdź toohello kartę Lista zadań do wykonania i adres URl jest hello Uwaga: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...

Załóż aplikacji hello przy użyciu poczty e-mail nazwy adres lub użytkownika. Wyloguj się, a następnie zaloguj się ponownie i edytowanie profilu hello lub zresetować hasła hello. Wyloguj się i zaloguj się jako inny użytkownik. 

## <a name="add-social-idps"></a>Dodaj IDPs społecznościowych

Obecnie obsługuje tylko użytkownik, rejestracji i logowania przy użyciu aplikacji hello **kont lokalnych**; kontom przechowywane w katalogu B2C, użyj nazwy użytkownika i hasła. Za pomocą usługi Azure AD B2C, można dodać obsługę innych **dostawców tożsamości** (IDPs) bez zmieniania żadnego kodu.

tooadd społecznościowych IDPs tooyour aplikacji, Rozpocznij od następujących hello szczegółowe instrukcje w tych artykułach. Dla każdego IDP ma toosupport, należy tooregister aplikacji w tym systemie i Uzyskaj identyfikator klienta.

* [Konfigurowanie usługi Facebook jako dostawca tożsamości](active-directory-b2c-setup-fb-app.md)
* [Konfigurowanie usługi Google jako dostawca tożsamości](active-directory-b2c-setup-goog-app.md)
* [Konfigurowanie usługi Amazon jako dostawca tożsamości](active-directory-b2c-setup-amzn-app.md)
* [Konfigurowanie LinkedIn jako dostawca tożsamości](active-directory-b2c-setup-li-app.md)

Po dodaniu tooyour dostawców tożsamości hello katalogu B2C, edycji każdego z trzech zbiorów zasad tooinclude hello IDPs nowe, zgodnie z opisem w hello [artykule o zasadach](active-directory-b2c-reference-policies.md). Po zapisaniu zasad, należy ponownie uruchomić aplikacji hello.  Powinny pojawić się hello IDPs nowe dodane jako opcje logowania i rejestracji w każdym doświadczeniami tożsamości.

Możesz eksperymentować z zasadami i obserwować wpływ hello w przykładowej aplikacji. Dodaj lub usuń IDPs, manipulować oświadczenia aplikacji lub zmień atrybuty rejestracji. Eksperymentu, aż zostanie wyświetlony, jak zasady, żądania uwierzytelniania i OWIN powiązać razem.

## <a name="sample-code-walkthrough"></a>Przykładowy kod wskazówki
następujące sekcje Hello Pokaż konfiguracji hello przykładowy kod aplikacji. Mogą wykorzystać te informacje jako przewodnika przy projektowaniu aplikacji w przyszłości.

### <a name="add-authentication-support"></a>Dodaj obsługę uwierzytelniania

Można teraz skonfigurować toouse Twojej aplikacji usługi Azure AD B2C. Aplikacja komunikuje się z usługi Azure AD B2C, wysyłając żądania uwierzytelniania OpenID Connect. Witaj żądań jest wymagane przez środowisko użytkownika hello aplikacji chce tooexecute przez określenie hello zasad. Można użyć firmy Microsoft OWIN biblioteki toosend te żądania, wykonania zasady, zarządzania sesjami użytkownika i inne.

#### <a name="install-owin"></a>Instalowanie interfejsu OWIN

toobegin, dodać hello OWIN oprogramowanie pośredniczące NuGet pakiety toohello projektu przy użyciu hello Konsola Menedżera pakietów programu Visual Studio.

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a>Dodawanie klasy początkowej OWIN

Dodaj toohello klasy interfejsu API OWIN uruchamiania o nazwie `Startup.cs`.  Kliknij prawym przyciskiem myszy na powitania projektu, zaznacz **Dodaj** i **nowy element**, a następnie wyszukaj interfejs OWIN. oprogramowanie pośredniczące OWIN Hello wywoła hello `Configuration(…)` metody podczas uruchamiania aplikacji.

W naszym przykładzie możemy zmienić deklaracji klasy hello zbyt`public partial class Startup` i implementowane hello drugiej klasy hello w `App_Start\Startup.Auth.cs`. Witaj wewnątrz `Configuration` metody dodaliśmy wywołanie za`ConfigureAuth`, który jest zdefiniowany w `Startup.Auth.cs`. Po modyfikacji hello `Startup.cs` wygląda jak poniżej hello:

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a>Konfigurowanie oprogramowania pośredniczącego uwierzytelniania hello

Witaj Otwórz plik `App_Start\Startup.Auth.cs` i wdrożenie hello `ConfigureAuth(...)` metody. Witaj podane parametry `OpenIdConnectAuthenticationOptions` służyć jako współrzędne toocommunicate Twojej aplikacji w usłudze Azure AD B2C. Jeśli nie określisz niektóre parametry, zostanie użyty hello wartości domyślnej. Na przykład firma Microsoft nie określaj hello `ResponseType` w próbce hello, więc hello wartości domyślnej `code id_token` będzie używany w każdej tooAzure żądania wychodzącego AD B2C.

Należy również tooset się uwierzytelniania plików cookie. oprogramowanie pośredniczące Hello OpenID Connect używa plików cookie sesji użytkownika toomaintain, między innymi.

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

W `OpenIdConnectAuthenticationOptions` powyżej, definiujemy zestaw funkcji wywołania zwrotnego dla określonych powiadomień, które są odbierane przez oprogramowanie pośredniczące hello OpenID Connect. Te zachowania są definiowane przy użyciu `OpenIdConnectAuthenticationNotifications` obiektu i przechowywane w hello `Notifications` zmiennej. W naszym przykładzie definiujemy trzech różnych wywołań zwrotnych w zależności od hello zdarzeń.

### <a name="using-different-policies"></a>Przy użyciu różnych zasad

Witaj `RedirectToIdentityProvider` powiadomień jest zawsze wyzwalane, gdy żądanie tooAzure AD B2C. W funkcji wywołania zwrotnego hello `OnRedirectToIdentityProvider`, sprawdzamy w hello wychodzące połączenie, jeśli chcemy toouse inne zasady. W kolejności toodo hasła resetowania lub edytowanie profilu należy toouse hello odpowiednie zasady, takie jak zasady, zamiast hello domyślne "Rejestracji i logowania" zasady resetowania hasła hello.

W naszym przykładzie gdy użytkownik chce tooreset hello haseł lub edytowanie profilu hello, dodamy zasad hello toouse możemy użyć w kontekście OWIN hello. Który może odbywać się następujący hello:

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

I można zaimplementować funkcja wywołania zwrotnego hello `OnRedirectToIdentityProvider` hello następujący:

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a>Obsługa kodów autoryzacji

Witaj `AuthorizationCodeReceived` powiadomień jest wyzwalane po odebraniu kod autoryzacji. oprogramowanie pośredniczące Hello OpenID Connect nie obsługuje kodów wymianę tokenów dostępu. Należy ręcznie wymienić kod hello token hello w funkcji wywołania zwrotnego. Aby uzyskać więcej informacji, zapoznaj się hello [dokumentacji](active-directory-b2c-devquickstarts-web-api-dotnet.md) objaśniający sposób.

### <a name="handling-errors"></a>Obsługa błędów

Witaj `AuthenticationFailed` powiadomień jest wyzwalane, gdy uwierzytelnianie nie powiedzie się. Metody wywołania zwrotnego może obsługiwać błędy hello zgodnie z wymaganiami. Należy jednak dodać wyboru dla kodu błędu hello `AADB2C90118`. Podczas wykonywania hello zasad "Rejestracji i logowania" hello, użytkownik hello ma hello możliwości tooselect **nie pamiętasz hasła?** łącza. W takim przypadku usługi Azure AD B2C wysyła aplikacji, ten kod błędu wskazujący, czy aplikacji należy wysłać żądanie, zamiast zasady resetowania hasła hello.

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a>Wyślij tooAzure żądań uwierzytelniania AD

Aplikacja jest teraz toocommunicate poprawnie skonfigurowane w usłudze Azure AD B2C przy użyciu protokołu uwierzytelniania OpenID Connect hello. OWIN zarządza szczegóły hello obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD B2C i podtrzymywanie sesji użytkowników. Wszystkie opcje, które pozostaje jest tooinitiate przepływu każdego użytkownika.

Gdy użytkownik wybierze **up logowania/logowania**, **edytowanie profilu**, lub **resetowania hasła** w aplikacji sieci web hello hello skojarzonych akcji jest wywoływana w `Controllers\AccountController.cs`:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

Umożliwia także toosign OWIN limit hello użytkownika z aplikacji hello. W `Controllers\AccountController.cs` mamy:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

W tooexplicitly dodanie wywoływanie zasad, można użyć `[Authorize]` tag w kontrolerach, który wykonuje zasadę, jeśli użytkownik hello nie jest zalogowany. Otwórz `Controllers\HomeController.cs` i Dodaj hello `[Authorize]` tag toohello oświadczeń kontrolera.  OWIN wybiera hello ostatnio zasady skonfigurowane podczas hello `[Authorize]` tag zostaje trafiony.

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a>Wyświetl informacje o użytkowniku

Podczas uwierzytelniania użytkowników za pomocą protokołu OpenID Connect, usługi Azure AD B2C zwraca identyfikator tokenu toohello aplikacja, która zawiera **oświadczeń**. Te są potwierdzeniami dotyczącymi hello użytkownika. Toopersonalize oświadczeń można użyć w swojej aplikacji.

Otwórz hello `Controllers\HomeController.cs` pliku. Oświadczenia użytkowników są dostępne w kontrolerach za pośrednictwem hello `ClaimsPrincipal.Current` obiekt główny zabezpieczeń.

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

Są dostępne wszelkie oświadczenia, że aplikacja odbiera w hello sam sposób.  Lista wszystkich oświadczeń hello odbiera aplikacji hello jest dostępne na powitania **oświadczeń** strony.
