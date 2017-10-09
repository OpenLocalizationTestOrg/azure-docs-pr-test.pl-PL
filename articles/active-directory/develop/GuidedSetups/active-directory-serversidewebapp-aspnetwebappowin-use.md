---
title: "aaaAzure AD v2 ASP.NET Web Server wprowadzenie - Użyj | Dokumentacja firmy Microsoft"
description: "Implementowanie logowania firmy Microsoft dla rozwiązania ASP.NET z aplikacji opartych na przeglądarce sieci web tradycyjnych przy użyciu standardowego protokołu OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 03afce6fa6598215e8c4af841c00762c143a0cd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a>Dodaj żądania kontrolera toohandle logowania się i wylogowania

Ten krok pokazuje, jak toocreate nowe tooexpose kontrolera logowania i wylogowywania metody.

1.  Kliknij prawym przyciskiem myszy hello `Controllers` i wybierz polecenie`Add` > `Controller`
2.  Wybierz pozycję `MVC (.NET version) Controller – Empty`.
3.  Kliknij przycisk *Dodaj*
4.  Nadaj mu nazwę `HomeController` i kliknij przycisk *Dodaj*
5.  Dodaj *OWIN* odwołuje się do klasy toohello:

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Dodaj dwie metody hello poniżej toohandle logowanie się i wylogowania tooyour kontrolera inicjując żądania uwierzytelnienia za pomocą kodu:
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate hello SignIn method with hello [Authorize] attribute
/// </summary>
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}

/// <summary>
/// Send an OpenID Connect sign-out request.
/// </summary>
public void SignOut()
{
    HttpContext.GetOwinContext().Authentication.SignOut(
            OpenIdConnectAuthenticationDefaults.AuthenticationType,
            CookieAuthenticationDefaults.AuthenticationType);
}
```

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a>Utwórz toosign strony głównej aplikacji hello wśród użytkowników za pośrednictwem przycisku logowania

W programie Visual Studio Utwórz nowy widok tooadd hello logowania przycisk i Wyświetl informacje o użytkowniku po uwierzytelnieniu:

1.  Kliknij prawym przyciskiem myszy hello `Views\Home` i wybierz polecenie`Add View`
2.  Nadaj jej nazwę `Index`.
3.  Dodaj hello następującego kodu HTML, który zawiera hello logowania przycisk, toohello pliku:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If hello user is not authenticated, display hello sign-in button -->
    <a href="@Url.Action("SignIn", "Home")" style="text-decoration: none;">
        <svg xmlns="http://www.w3.org/2000/svg" xml:space="preserve" width="300px" height="50px" viewBox="0 0 3278 522" class="SignInButton">
        <style type="text/css">.fil0:hover {fill: #4B4B4B;} .fnt0 {font-size: 260px;font-family: 'Segoe UI Semibold', 'Segoe UI'; text-decoration: none;}</style>
        <rect class="fil0" x="2" y="2" width="3174" height="517" fill="black" />
        <rect x="150" y="129" width="122" height="122" fill="#F35325" />
        <rect x="284" y="129" width="122" height="122" fill="#81BC06" />
        <rect x="150" y="263" width="122" height="122" fill="#05A6F0" />
        <rect x="284" y="263" width="122" height="122" fill="#FFBA08" />
        <text x="470" y="357" fill="white" class="fnt0">Sign in with Microsoft</text>
        </svg>
    </a>
}
else
{
    <span><br/>Hello @System.Security.Claims.ClaimsPrincipal.Current.FindFirst("name").Value;</span>
    <br /><br />
    @Html.ActionLink("See Your Claims", "Index", "Claims")
    <br /><br />
    @Html.ActionLink("Sign out", "SignOut", "Home")
}
@if (!string.IsNullOrWhiteSpace(Request.QueryString["errormessage"]))
{
    <div style="background-color:red;color:white;font-weight: bold;">Error: @Request.QueryString["errormessage"]</div>
}
</body>
</html>
```
<!--start-collapse-->
### <a name="more-information"></a>Więcej informacji
> Ta strona dodaje przycisk Zarejestruj się w formacie SVG z czarnym tle:<br/>![Logowania z firmą Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)<br/> Więcej logowania przycisków, przejdź toohello [tej strony](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "znakowanie wytyczne").
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a>Dodaj oświadczenia użytkownika toodisplay kontrolera
Ten kontroler pokazuje hello korzysta z hello `[Authorize]` atrybutu tooprotect kontrolera. Ten atrybut ogranicza dostęp toohello kontrolera zezwalając tylko użytkownicy uwierzytelnieni. Witaj poniższy kod korzysta z oświadczeń użytkowników toodisplay atrybutu hello, które zostały pobrane w ramach logowania hello.

1.  Kliknij prawym przyciskiem myszy hello `Controllers` folderu:`Add` > `Controller`
2.  Wybierz pozycję `MVC {version} Controller – Empty`.
3.  Kliknij przycisk *Dodaj*
4.  Nadaj jej nazwę`ClaimsController`
5.  Zastąp kod hello klasy kontrolera z kodem hello poniżej — spowoduje to dodanie hello `[Authorize]` toohello klasy atrybutu:

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims tooviewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get hello user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // hello 'preferred_username' claim can be used for showing hello username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // hello subject claim can be used toouniquely identify hello user across hello web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is hello unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Więcej informacji
> Ze względu na użycie hello hello `[Authorize]` atrybutu, wszystkie metody tego kontrolera można wykonać tylko, jeśli hello użytkownik jest uwierzytelniony. Jeśli hello użytkownika nie jest uwierzytelniony, próbuje tooaccess hello kontrolera OWIN inicjują żądania uwierzytelnienia i wymusić hello tooauthenticate użytkownika. Kod Hello powyżej wygląda na powitania oświadczeń kolekcji hello `ClaimsPrincipal.Current` wystąpienia dla określonego użytkownika atrybuty uwzględnione w tokenie hello użytkownika. Te atrybuty obejmować imię i nazwisko użytkownika hello i nazwę użytkownika, a także hello użytkownika globalny identyfikator podmiotu. Zawiera także hello *identyfikator dzierżawcy*, reprezentuje hello identyfikator organizacji hello użytkownika. 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a>Tworzenie widoku toodisplay hello oświadczeń użytkownika

W programie Visual Studio Utwórz nowy widok toodisplay hello oświadczeń użytkownika na stronie sieci web:

1.  Kliknij prawym przyciskiem myszy hello `Views\Claims` folderu oraz:`Add View`
2.  Nadaj jej nazwę `Index`.
3.  Dodaj następującego pliku HTML toohello hello:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Sample</title>
    <link href="@Url.Content("~/Content/bootstrap.min.css")" rel="stylesheet" type="text/css" />
</head>
<body style="padding:50px">
    <h3>Main Claims:</h3>
    <table class="table table-striped table-bordered table-hover">
        <tr><td>Name</td><td>@ViewBag.Name</td></tr>
        <tr><td>Username</td><td>@ViewBag.Username</td></tr>
        <tr><td>Subject</td><td>@ViewBag.Subject</td></tr>
        <tr><td>TenantId</td><td>@ViewBag.TenantId</td></tr>
    </table>
    <br />
    <h3>All Claims:</h3>
    <table class="table table-striped table-bordered table-hover table-condensed">
    @foreach (var claim in System.Security.Claims.ClaimsPrincipal.Current.Claims)
    {
        <tr><td>@claim.Type</td><td>@claim.Value</td></tr>
    }
</table>
    <br />
    <br />
    @Html.ActionLink("Sign out", "SignOut", "Home", null, new { @class = "btn btn-primary" })
</body>
</html>
```
