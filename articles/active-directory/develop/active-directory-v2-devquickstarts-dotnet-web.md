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
# <a name="add-sign-in-tooan-net-mvc-web-app"></a><span data-ttu-id="7dcdb-103">Dodawanie aplikacji sieci web .NET MVC tooan logowania</span><span class="sxs-lookup"><span data-stu-id="7dcdb-103">Add sign-in tooan .NET MVC web app</span></span>
<span data-ttu-id="7dcdb-104">Z punktem końcowym v2.0 hello można szybko dodać uwierzytelniania aplikacji sieci web tooyour o obsługę zarówno osobistego konta Microsoft i konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="7dcdb-105">W aplikacji sieci web ASP.NET można to zrobić za pomocą oprogramowania pośredniczącego OWIN firmy Microsoft włączone w programie .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="7dcdb-106">Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="7dcdb-107">toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="7dcdb-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="7dcdb-108">W tym miejscu będzie budujemy aplikacji sieci web, która używa OWIN toosign hello użytkownika w wyświetlania niektóre informacje o użytkowniku hello, a znak hello użytkownika poza aplikacją hello.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-108">Here we'll build an web app that uses OWIN toosign hello user in, display some information about hello user, and sign hello user out of hello app.</span></span>

## <a name="download"></a><span data-ttu-id="7dcdb-109">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="7dcdb-109">Download</span></span>
<span data-ttu-id="7dcdb-110">Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="7dcdb-110">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="7dcdb-111">toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) lub klonowania hello szkielet:</span><span class="sxs-lookup"><span data-stu-id="7dcdb-111">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="7dcdb-112">ukończyć powitalnych aplikacji znajduje się na końcu hello również w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-112">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="7dcdb-113">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="7dcdb-113">Register an app</span></span>
<span data-ttu-id="7dcdb-114">Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="7dcdb-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="7dcdb-115">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="7dcdb-115">Make sure to:</span></span>

* <span data-ttu-id="7dcdb-116">Skopiuj hello **identyfikator aplikacji** przypisany tooyour aplikacji, będzie on potrzebny wkrótce.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-116">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="7dcdb-117">Dodaj hello **Web** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-117">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="7dcdb-118">Wprowadź poprawny hello **identyfikator URI przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-118">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="7dcdb-119">Witaj identyfikatora uri przekierowania wskazuje tooAzure AD którym powinny być kierowane odpowiedzi uwierzytelniania — Witaj domyślną w tym samouczku jest `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-119">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="7dcdb-120">Instalowanie i konfigurowanie uwierzytelniania OWIN</span><span class="sxs-lookup"><span data-stu-id="7dcdb-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="7dcdb-121">W tym miejscu skonfigurujemy hello OWIN oprogramowanie pośredniczące toouse hello protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-121">Here, we'll configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="7dcdb-122">OWIN być używane tooissue żądań logowania i wylogowywania, zarządzanie sesji użytkownika hello i uzyskać informacje o użytkowniku hello, między innymi.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-122">OWIN will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

1. <span data-ttu-id="7dcdb-123">toobegin, otwórz hello `web.config` plików w katalogu głównym hello hello projektu, a następnie wprowadź wartości konfiguracji aplikacji w hello `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-123">toobegin, open hello `web.config` file in hello root of hello project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="7dcdb-124">Witaj `ida:ClientId` jest hello **identyfikator aplikacji** przypisane tooyour aplikacji w portalu rejestracji hello.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-124">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="7dcdb-125">Witaj `ida:RedirectUri` jest hello **identyfikator Uri przekierowania** wprowadzony w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-125">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>

2. <span data-ttu-id="7dcdb-126">Następnie dodaj przy użyciu konsoli Menedżera pakietów hello hello OWIN oprogramowanie pośredniczące NuGet pakiety toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-126">Next, add hello OWIN middleware NuGet packages toohello project using hello Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="7dcdb-127">Dodaj projekt toohello "Klasy początkowej OWIN" nazywany `Startup.cs` prawej, kliknij na powitania projektu--> **Dodaj** --> **nowy element** --> Wyszukaj "OWIN".</span><span class="sxs-lookup"><span data-stu-id="7dcdb-127">Add an "OWIN Startup Class" toohello project called `Startup.cs`  Right click on hello project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="7dcdb-128">oprogramowanie pośredniczące OWIN Hello wywoła hello `Configuration(...)` metody podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-128">hello OWIN middleware will invoke hello `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="7dcdb-129">Zmiana deklaracji klasy hello zbyt`public partial class Startup` — już zaimplementowano część tej klasy dla Ciebie w innym pliku.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-129">Change hello class declaration too`public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="7dcdb-130">W hello `Configuration(...)` metody, należy tooset tooConfigureAuth(...) wywołania zapasowej uwierzytelniania dla aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="7dcdb-130">In hello `Configuration(...)` method, make a call tooConfigureAuth(...) tooset up authentication for your web app</span></span>  

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

5. <span data-ttu-id="7dcdb-131">Witaj Otwórz plik `App_Start\Startup.Auth.cs` i wdrożenie hello `ConfigureAuth(...)` metody.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-131">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="7dcdb-132">Witaj podane parametry `OpenIdConnectAuthenticationOptions` będzie służyć jako współrzędne toocommunicate Twojej aplikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-132">hello parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>  <span data-ttu-id="7dcdb-133">Należy również tooset się uwierzytelniania plików Cookie — oprogramowanie pośredniczące hello OpenID Connect używa plików cookie poniżej obejmuje hello.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-133">You'll also need tooset up Cookie Authentication - hello OpenID Connect middleware uses cookies underneath hello covers.</span></span>

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

## <a name="send-authentication-requests"></a><span data-ttu-id="7dcdb-134">Wysyłanie żądania uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="7dcdb-134">Send authentication requests</span></span>
<span data-ttu-id="7dcdb-135">Aplikacja jest teraz prawidłowo skonfigurowana toocommunicate z punktem końcowym v2.0 hello przy użyciu protokołu uwierzytelniania OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-135">Your app is now properly configured toocommunicate with hello v2.0 endpoint using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="7dcdb-136">Wszystkie szczegóły ugly hello obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i podtrzymywanie sesji użytkowników ma podjąć obsługę OWIN.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-136">OWIN has taken care of all of hello ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="7dcdb-137">Wszystkie opcje, które pozostaje jest toogive użytkownikom toosign sposób w i wylogowywania.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-137">All that remains is toogive your users a way toosign in and sign out.</span></span>

- <span data-ttu-id="7dcdb-138">Można autoryzować tagów w Twojej toorequire kontrolerów użytkownik loguje się przed uzyskaniem dostępu do konkretnej strony.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-138">You can use authorize tags in your controllers toorequire that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="7dcdb-139">Otwórz `Controllers\HomeController.cs`i Dodaj hello `[Authorize]` tagu toohello dotyczące kontrolera.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-139">Open `Controllers\HomeController.cs`, and add hello `[Authorize]` tag toohello About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="7dcdb-140">Umożliwia także żądania uwierzytelniania OWIN toodirectly problem z w kodzie.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-140">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span>  <span data-ttu-id="7dcdb-141">Otwórz `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="7dcdb-142">Hello SignIn() i akcje SignOut() wystawić odpowiednio OpenID Connect żądania i żądań wylogowania.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-142">In hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

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

- <span data-ttu-id="7dcdb-143">Teraz Otwórz `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="7dcdb-144">Jest to, której będzie Pokaż linki logowania i wylogowywania aplikacji hello użytkownika, a następnie wydrukuj nazwy użytkownika hello w widoku.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-144">This is where you'll show hello user your app's sign-in and sign-out links, and print out hello user's name in a view.</span></span>

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

## <a name="display-user-information"></a><span data-ttu-id="7dcdb-145">Wyświetl informacje o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="7dcdb-145">Display user information</span></span>
<span data-ttu-id="7dcdb-146">Podczas uwierzytelniania użytkowników z OpenID Connect, punktu końcowego v2.0 hello zwraca aplikację toohello żądaniu, która zawiera oświadczenia lub potwierdzeniami dotyczącymi hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-146">When authenticating users with OpenID Connect, hello v2.0 endpoint returns an id_token toohello app that contains claims, or assertions about hello user.</span></span>  <span data-ttu-id="7dcdb-147">Można użyć tych toopersonalize oświadczenia aplikacji:</span><span class="sxs-lookup"><span data-stu-id="7dcdb-147">You can use these claims toopersonalize your app:</span></span>

- <span data-ttu-id="7dcdb-148">Otwórz hello `Controllers\HomeController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-148">Open hello `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="7dcdb-149">Dostęp do oświadczeń użytkowników hello w kontrolerach za pośrednictwem hello `ClaimsPrincipal.Current` obiekt główny zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-149">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

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

## <a name="run"></a><span data-ttu-id="7dcdb-150">Uruchom polecenie</span><span class="sxs-lookup"><span data-stu-id="7dcdb-150">Run</span></span>
<span data-ttu-id="7dcdb-151">Na koniec Skompiluj i uruchom aplikację!</span><span class="sxs-lookup"><span data-stu-id="7dcdb-151">Finally, build and run your app!</span></span>   <span data-ttu-id="7dcdb-152">Zaloguj się przy użyciu Account firmy Microsoft lub konta służbowego i zwróć uwagę, jak tożsamość użytkownika hello jest widoczny w hello górnym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="7dcdb-153">Masz teraz zabezpieczone przy użyciu standardowych protokołach branżowych, uwierzytelniających użytkowników przy użyciu ich osobistych i pracy/służbowego konta aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="7dcdb-154">Odwołania, hello ukończone próbka (bez wartości konfiguracji) [jest dostarczane jako zip w tym miejscu](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), lub można ją sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="7dcdb-154">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="7dcdb-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7dcdb-155">Next steps</span></span>
<span data-ttu-id="7dcdb-156">Możesz teraz przejść do bardziej zaawansowanych tematów.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="7dcdb-157">Można tootry:</span><span class="sxs-lookup"><span data-stu-id="7dcdb-157">You may want tootry:</span></span>

[<span data-ttu-id="7dcdb-158">Zabezpieczanie interfejsu API sieci Web, z punktem końcowym v2.0 hello hello >></span><span class="sxs-lookup"><span data-stu-id="7dcdb-158">Secure a Web API with hello hello v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="7dcdb-159">Aby uzyskać dodatkowe zasoby Zobacz:</span><span class="sxs-lookup"><span data-stu-id="7dcdb-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="7dcdb-160">Przewodnik dewelopera v2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="7dcdb-160">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="7dcdb-161">Tag StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="7dcdb-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="7dcdb-162">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="7dcdb-162">Get security updates for our products</span></span>
<span data-ttu-id="7dcdb-163">Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez wizytę [tę stronę](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.</span><span class="sxs-lookup"><span data-stu-id="7dcdb-163">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
