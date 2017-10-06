---
title: aaaAzure AD w wersji 2.0 .NET sieci web logowania aplikacji wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji sieci Web .NET MVC który loguje się użytkowników z obu Account firmy Microsoft i konta służbowego."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c8b97ac6-0a06-4367-81b6-7d1d98152b14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 241e9c90bd752fbecc3696ce4f1bed3f9772189d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-net-mvc-web-app"></a>Dodawanie aplikacji sieci web .NET MVC tooan logowania
Z punktem końcowym v2.0 hello można szybko dodać uwierzytelniania aplikacji sieci web tooyour o obsługę zarówno osobistego konta Microsoft i konta służbowego.  W aplikacji sieci web ASP.NET można to zrobić za pomocą oprogramowania pośredniczącego OWIN firmy Microsoft włączone w programie .NET Framework 4.5.

> [!NOTE]
> Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.  toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
>
>

 W tym miejscu będzie budujemy aplikacji sieci web, która używa OWIN toosign hello użytkownika w wyświetlania niektóre informacje o użytkowniku hello, a znak hello użytkownika poza aplikacją hello.

## <a name="download"></a>Do pobrania
Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).  toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) lub klonowania hello szkielet:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

ukończyć powitalnych aplikacji znajduje się na końcu hello również w tym samouczku.

## <a name="register-an-app"></a>Rejestracja aplikacji
Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).  Upewnij się, że:

* Skopiuj hello **identyfikator aplikacji** przypisany tooyour aplikacji, będzie on potrzebny wkrótce.
* Dodaj hello **Web** platformy aplikacji.
* Wprowadź poprawny hello **identyfikator URI przekierowania**. Witaj identyfikatora uri przekierowania wskazuje tooAzure AD którym powinny być kierowane odpowiedzi uwierzytelniania — Witaj domyślną w tym samouczku jest `https://localhost:44326/`.

## <a name="install--configure-owin-authentication"></a>Instalowanie i konfigurowanie uwierzytelniania OWIN
W tym miejscu skonfigurujemy hello OWIN oprogramowanie pośredniczące toouse hello protokołu uwierzytelniania OpenID Connect.  OWIN być używane tooissue żądań logowania i wylogowywania, zarządzanie sesji użytkownika hello i uzyskać informacje o użytkowniku hello, między innymi.

1. toobegin, otwórz hello `web.config` plików w katalogu głównym hello hello projektu, a następnie wprowadź wartości konfiguracji aplikacji w hello `<appSettings>` sekcji.

  * Witaj `ida:ClientId` jest hello **identyfikator aplikacji** przypisane tooyour aplikacji w portalu rejestracji hello.
  * Witaj `ida:RedirectUri` jest hello **identyfikator Uri przekierowania** wprowadzony w portalu hello.

2. Następnie dodaj przy użyciu konsoli Menedżera pakietów hello hello OWIN oprogramowanie pośredniczące NuGet pakiety toohello projektu.

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. Dodaj projekt toohello "Klasy początkowej OWIN" nazywany `Startup.cs` prawej, kliknij na powitania projektu--> **Dodaj** --> **nowy element** --> Wyszukaj "OWIN".  oprogramowanie pośredniczące OWIN Hello wywoła hello `Configuration(...)` metody podczas uruchamiania aplikacji.
4. Zmiana deklaracji klasy hello zbyt`public partial class Startup` — już zaimplementowano część tej klasy dla Ciebie w innym pliku.  W hello `Configuration(...)` metody, należy tooset tooConfigureAuth(...) wywołania zapasowej uwierzytelniania dla aplikacji sieci web  

        ```C#
        [assembly: OwinStartup(typeof(Startup))]
        
        namespace TodoList_WebApp
        {
            public partial class Startup
            {
                public void Configuration(IAppBuilder app)
                {
                    ConfigureAuth(app);
                }
            }
        }
        ```

5. Witaj Otwórz plik `App_Start\Startup.Auth.cs` i wdrożenie hello `ConfigureAuth(...)` metody.  Witaj podane parametry `OpenIdConnectAuthenticationOptions` będzie służyć jako współrzędne toocommunicate Twojej aplikacji z usługą Azure AD.  Należy również tooset się uwierzytelniania plików Cookie — oprogramowanie pośredniczące hello OpenID Connect używa plików cookie poniżej obejmuje hello.

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
                                             Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0"),
                                             RedirectUri = redirectUri,
                                             Scope = "openid email profile",
                                             ResponseType = "id_token",
                                             PostLogoutRedirectUri = redirectUri,
                                             TokenValidationParameters = new TokenValidationParameters
                                             {
                                                     ValidateIssuer = false,
                                             },
                                             Notifications = new OpenIdConnectAuthenticationNotifications
                                             {
                                                     AuthenticationFailed = OnAuthenticationFailed,
                                             }
                                     });
                     }
        ```

## <a name="send-authentication-requests"></a>Wysyłanie żądania uwierzytelniania
Aplikacja jest teraz prawidłowo skonfigurowana toocommunicate z punktem końcowym v2.0 hello przy użyciu protokołu uwierzytelniania OpenID Connect hello.  Wszystkie szczegóły ugly hello obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i podtrzymywanie sesji użytkowników ma podjąć obsługę OWIN.  Wszystkie opcje, które pozostaje jest toogive użytkownikom toosign sposób w i wylogowywania.

- Można autoryzować tagów w Twojej toorequire kontrolerów użytkownik loguje się przed uzyskaniem dostępu do konkretnej strony.  Otwórz `Controllers\HomeController.cs`i Dodaj hello `[Authorize]` tagu toohello dotyczące kontrolera.
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- Umożliwia także żądania uwierzytelniania OWIN toodirectly problem z w kodzie.  Otwórz `Controllers\AccountController.cs`.  Hello SignIn() i akcje SignOut() wystawić odpowiednio OpenID Connect żądania i żądań wylogowania.

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with hello v2.0 endpoint is not yet supported.  Here, we just end hello session with hello web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- Teraz Otwórz `Views\Shared\_LoginPartial.cshtml`.  Jest to, której będzie Pokaż linki logowania i wylogowywania aplikacji hello użytkownika, a następnie wydrukuj nazwy użytkownika hello w widoku.

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves.*@
        
                        Hello, @(System.Security.Claims.ClaimsPrincipal.Current.FindFirst("preferred_username").Value)!
                    </li>
                    <li>
                        @Html.ActionLink("Sign out", "SignOut", "Account")
                    </li>
                </ul>
            </text>
        }
        else
        {
            <ul class="nav navbar-nav navbar-right">
                <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
            </ul>
        }
        ```

## <a name="display-user-information"></a>Wyświetl informacje o użytkowniku
Podczas uwierzytelniania użytkowników z OpenID Connect, punktu końcowego v2.0 hello zwraca aplikację toohello żądaniu, która zawiera oświadczenia lub potwierdzeniami dotyczącymi hello użytkownika.  Można użyć tych toopersonalize oświadczenia aplikacji:

- Otwórz hello `Controllers\HomeController.cs` pliku.  Dostęp do oświadczeń użytkowników hello w kontrolerach za pośrednictwem hello `ClaimsPrincipal.Current` obiekt główny zabezpieczeń.

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // hello object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // hello subject or nameidentifier claim can be used toouniquely identify hello user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a>Uruchom polecenie
Na koniec Skompiluj i uruchom aplikację!   Zaloguj się przy użyciu Account firmy Microsoft lub konta służbowego i zwróć uwagę, jak tożsamość użytkownika hello jest widoczny w hello górnym pasku nawigacyjnym.  Masz teraz zabezpieczone przy użyciu standardowych protokołach branżowych, uwierzytelniających użytkowników przy użyciu ich osobistych i pracy/służbowego konta aplikacji sieci web.

Odwołania, hello ukończone próbka (bez wartości konfiguracji) [jest dostarczane jako zip w tym miejscu](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), lub można ją sklonować z serwisu GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a>Następne kroki
Możesz teraz przejść do bardziej zaawansowanych tematów.  Można tootry:

[Zabezpieczanie interfejsu API sieci Web, z punktem końcowym v2.0 hello hello >>](active-directory-devquickstarts-webapi-dotnet.md)

Aby uzyskać dodatkowe zasoby Zobacz:

* [Przewodnik dewelopera v2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [Tag StackOverflow "azure-active-directory" >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Pobierz aktualizacje zabezpieczeń naszych produktów
Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez wizytę [tę stronę](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.
