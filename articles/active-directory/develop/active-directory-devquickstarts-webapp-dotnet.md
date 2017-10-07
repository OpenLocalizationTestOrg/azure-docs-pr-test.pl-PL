---
title: Aplikacja sieci web .NET aaaAzure AD wprowadzenie | Dokumentacja firmy Microsoft
description: "Tworzenie aplikacji sieci web .NET MVC, która integruje się z usługą Azure AD dla logowania."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a>Aplikacja sieci web ASP.NET, logowania i wylogowywania z usługą Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Podając jednego logowania i wylogowywania tylko kilka wierszy kodu, Azure Active Directory (Azure AD) prościej możesz toooutsource aplikacji sieci web zarządzania tożsamościami. Może się zarejestrować użytkowników i aplikacji sieci web ASP.NET przy użyciu hello firmę Microsoft implementacją interfejsu Open Web dla platformy .NET (OWIN) oprogramowania pośredniczącego. Społeczność oprogramowania pośredniczącego OWIN znajduje się w programie .NET Framework 4.5. W tym artykule przedstawiono sposób toouse OWIN do:

* Loguj użytkowników w aplikacjach tooweb za pomocą usługi Azure AD jako dostawcy tożsamości hello.
* Wyświetlane informacje użytkownika.
* Loguj użytkowników spoza aplikacji hello.

## <a name="before-you-get-started"></a>Przed rozpoczęciem
* Pobierz hello [szkielet aplikacji](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) lub pobrać hello [ukończone próbki](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).
* Należy również dzierżawa usługi Azure AD, w których aplikacja hello tooregister. Jeśli nie masz już dzierżawę usługi Azure AD [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).

Gdy wszystko będzie gotowe, wykonaj procedury hello hello obok cztery sekcje.

## <a name="step-1-register-hello-new-app-with-azure-ad"></a>Krok 1: Zarejestruj hello nowej aplikacji z usługą Azure AD
tooset użytkowników tooauthenticate aplikacji hello, najpierw zarejestrować go w dzierżawie powitalnych następujący:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na górnym pasku hello kliknij nazwę konta. W obszarze hello **katalogu** listy, wybierz hello dzierżawy usługi Active Directory, w którym ma tooregister aplikacji hello.
3. Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.
4. Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.
5. Wykonaj hello monituje toocreate nowy **aplikacji sieci Web i/lub WebAPI**.
  * **Nazwa** opisuje toousers aplikacji hello.
  * **Adres URL logowania** jest hello podstawowy adres URL aplikacji hello. szkielet Hello domyślny adres URL jest https://localhost:44320 /.
6. Po zakończeniu rejestracji hello Azure AD przypisuje aplikacji hello identyfikatora aplikacji Skopiuj wartość hello z toouse strony aplikacji hello w kolejnych sekcjach hello.
7. Z hello **ustawienia** -> **właściwości** strony dla aplikacji, aktualizacji hello identyfikator URI aplikacji. Witaj **identyfikator URI aplikacji** to unikatowy identyfikator dla aplikacji hello. Witaj konwencją nazewnictwa jest `https://<tenant-domain>/<app-name>` (na przykład `https://contoso.onmicrosoft.com/my-first-aad-app`).

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Krok 2: Konfigurowanie potoku uwierzytelniania OWIN toouse hello hello aplikacji
W tym kroku skonfigurujesz hello OWIN oprogramowanie pośredniczące toouse hello protokołu uwierzytelniania OpenID Connect. Użyj żądania logowania i wylogowywania tooissue OWIN, zarządzania sesjami użytkownika, uzyskiwanie informacji o użytkowniku i tak dalej.

1. toobegin, dodać hello OWIN oprogramowanie pośredniczące NuGet pakiety toohello projektu przy użyciu konsoli Menedżera pakietów hello.

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. tooadd o nazwie Projekt startowy OWIN klasy toohello `Startup.cs`, kliknij prawym przyciskiem myszy projekt hello, wybierz **Dodaj**, wybierz pozycję **nowy element**, a następnie wyszukaj **OWIN**. oprogramowanie pośredniczące OWIN Hello wywołuje hello **Configuration(...)**  metoda po uruchomieniu aplikacji hello.
3. Zmiana deklaracji klasy hello zbyt`public partial class Startup`. Już zaimplementowano część tej klasy dla Ciebie w innym pliku. W hello **Configuration(...)**  metody wywoływania zbyt**ConfgureAuth(...)**  tooset się uwierzytelniania aplikacji hello.  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. Otwórz plik App_Start\Startup.Auth.cs hello, a następnie wdrożyć hello **ConfigureAuth(...)**  metody. Witaj podane parametry *OpenIDConnectAuthenticationOptions* służyć jako współrzędne toocommunicate aplikacji hello z usługą Azure AD. Należy również tooset się uwierzytelniania plików cookie, ponieważ oprogramowanie pośredniczące hello OpenID Connect używa plików cookie w tle hello.

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. Otwórz plik web.config hello w katalogu głównym hello hello projektu, a następnie wprowadź wartości konfiguracji hello w hello `<appSettings>` sekcji.
  * `ida:ClientId`: hello GUID skopiowany z hello portalu Azure w "krok 1: hello zarejestrować nową aplikację z usługą Azure AD."
  * `ida:Tenant`: hello nazwa dzierżawy usługi Azure AD (np. contoso.onmicrosoft.com).
  * `ida:PostLogoutRedirectUri`: hello wskaźnika, który informuje usługi Azure AD, w którym użytkownik powinien być przekierowany po pomyślnym zakończeniu wylogowania żądania.

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Krok 3: Użycie tooAzure AD żądań OWIN tooissue logowania się i wylogowania
Aplikacja Hello jest teraz toocommunicate poprawnie skonfigurowane w usłudze Azure AD przy użyciu protokołu uwierzytelniania OpenID Connect hello. OWIN obsłużyła wszystkie szczegóły hello obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i utrzymywanie sesji użytkownika. Wszystkie opcje, które pozostaje jest toogive użytkownikom toosign sposób w i wylogowywania.

1. Można autoryzować tagów w Twojej kontrolerów toorequire użytkowników toosign w, aby dostęp do określonych stron. toodo tak, otwórz Controllers\HomeController.cs, a następnie dodaj hello `[Authorize]` tagu toohello dotyczące kontrolera.

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. Umożliwia także żądania uwierzytelniania OWIN toodirectly problem z w kodzie. toodo, otwórz Controllers\AccountController.cs. Następnie w akcji SignIn() i SignOut() hello wystawiania żądań wylogowania i żądania OpenID Connect.

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. Otwórz Views\Shared\_LoginPartial.cshtml tooshow hello hello aplikacji logowania i wylogowywania łącza użytkownika i tooprint się nazwa użytkownika hello w widoku.

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
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

## <a name="step-4-display-user-information"></a>Krok 4: Wyświetlane informacje o użytkowniku
Podczas uwierzytelniania użytkowników z OpenID Connect, usługi Azure AD zwraca aplikację toohello żądaniu, która zawiera "oświadczenia" lub potwierdzeniami dotyczącymi hello użytkownika. Możesz użyć tych aplikacji hello toopersonalize oświadczeń hello następujący:

1. Otwórz plik Controllers\HomeController.cs hello. Dostęp do oświadczeń użytkowników hello w kontrolerach za pośrednictwem hello `ClaimsPrincipal.Current` obiekt główny zabezpieczeń.

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. Tworzenie i uruchamianie aplikacji hello. Jeśli nie zostało utworzone nowy użytkownik w dzierżawie z domeny onmicrosoft.com, teraz jest toodo czas hello tak. Oto kroki tej procedury:

  a. Zaloguj się przy użyciu tego użytkownika, zwracając uwagę, jak tożsamość użytkownika hello jest odzwierciedlone na górnym pasku hello.

  b. Wyloguj się, a następnie zalogować się jako inny użytkownik w dzierżawie.

  c. Jeśli czujesz szczególnie ambitne, Zarejestruj i uruchomić inne wystąpienie tej aplikacji (z jego własnej clientId), a Obejrzyj jednej operacji logowania w akcji.

## <a name="next-steps"></a>Następne kroki
Aby informacje, zobacz [próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (bez wartości konfiguracji).

Możesz teraz przejść toomore Tematy zaawansowane. Na przykład, spróbuj [zabezpieczyć interfejs API sieci Web z usługą Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
