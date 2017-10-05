---
title: "Wprowadzenie logowania aplikacji sieci web usługi Azure AD 2.0 .NET | Dokumentacja firmy Microsoft"
description: "Sposób tworzenia aplikacji sieci Web .NET MVC logujący się użytkowników przy użyciu obu Account firmy Microsoft i konta służbowego."
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
ms.openlocfilehash: ba5bdf7daba6086b70aec54ebe25d4445fa708c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-net-mvc-web-app"></a><span data-ttu-id="4d044-103">Dodaj logowanie do aplikacji sieci web platformy .NET MVC</span><span class="sxs-lookup"><span data-stu-id="4d044-103">Add sign-in to an .NET MVC web app</span></span>
<span data-ttu-id="4d044-104">Z punktem końcowym v2.0 można szybko dodać konta służbowego i uwierzytelniania do aplikacji sieci web z obsługą oba osobistego konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4d044-104">With the v2.0 endpoint, you can quickly add authentication to your web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="4d044-105">W aplikacji sieci web ASP.NET można to zrobić za pomocą oprogramowania pośredniczącego OWIN firmy Microsoft włączone w programie .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="4d044-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="4d044-106">Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="4d044-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="4d044-107">Aby ustalić, czy należy używać punktu końcowego v2.0, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="4d044-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="4d044-108">W tym miejscu będzie budujemy aplikacji sieci web, która używa OWIN zalogować użytkownika, wyświetlane informacje o użytkowniku i zalogować użytkownika poza aplikacją.</span><span class="sxs-lookup"><span data-stu-id="4d044-108">Here we'll build an web app that uses OWIN to sign the user in, display some information about the user, and sign the user out of the app.</span></span>

## <a name="download"></a><span data-ttu-id="4d044-109">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="4d044-109">Download</span></span>
<span data-ttu-id="4d044-110">Kod używany w tym samouczku jest przechowywany [ w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="4d044-110">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="4d044-111">Aby z niego skorzystać, można [pobrać szkielet aplikacji w formie .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) lub sklonować szkielet:</span><span class="sxs-lookup"><span data-stu-id="4d044-111">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="4d044-112">Ukończonej aplikacji znajduje się na końcu również w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="4d044-112">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="4d044-113">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="4d044-113">Register an app</span></span>
<span data-ttu-id="4d044-114">Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="4d044-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="4d044-115">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="4d044-115">Make sure to:</span></span>

* <span data-ttu-id="4d044-116">Skopiuj **identyfikator aplikacji** przypisany do aplikacji, będzie on potrzebny wkrótce.</span><span class="sxs-lookup"><span data-stu-id="4d044-116">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="4d044-117">Dodaj **Web** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4d044-117">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="4d044-118">Wprowadź poprawny **identyfikator URI przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="4d044-118">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="4d044-119">Wskazuje identyfikator uri przekierowania do usługi Azure AD, w którym powinny być kierowane odpowiedzi uwierzytelniania — wartością domyślną tego samouczka jest `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="4d044-119">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="4d044-120">Instalowanie i konfigurowanie uwierzytelniania OWIN</span><span class="sxs-lookup"><span data-stu-id="4d044-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="4d044-121">W tym miejscu skonfigurujemy oprogramowania pośredniczącego OWIN do zastosowania protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="4d044-121">Here, we'll configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="4d044-122">OWIN będzie służyć do wysyłania żądań zalogowania się i wylogowania, zarządzania sesji użytkownika i uzyskać informacje o użytkowniku, między innymi.</span><span class="sxs-lookup"><span data-stu-id="4d044-122">OWIN will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

1. <span data-ttu-id="4d044-123">Aby rozpocząć, otwórz `web.config` plików w folderze głównym projektu, a następnie wprowadź wartości konfiguracji aplikacji w `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="4d044-123">To begin, open the `web.config` file in the root of the project, and enter your app's configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="4d044-124">`ida:ClientId` Jest **identyfikator aplikacji** przypisany do aplikacji w portalu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="4d044-124">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="4d044-125">`ida:RedirectUri` Jest **identyfikator Uri przekierowania** wprowadzony w portalu.</span><span class="sxs-lookup"><span data-stu-id="4d044-125">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>

2. <span data-ttu-id="4d044-126">Następnie dodaj pakiety NuGet oprogramowanie pośredniczące OWIN do projektu przy użyciu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="4d044-126">Next, add the OWIN middleware NuGet packages to the project using the Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="4d044-127">Dodaj "Klasę początkową OWIN" do projektu o nazwie `Startup.cs` --> kliknij projekt prawym **Dodaj** --> **nowy element** --> Wyszukaj "OWIN".</span><span class="sxs-lookup"><span data-stu-id="4d044-127">Add an "OWIN Startup Class" to the project called `Startup.cs`  Right click on the project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="4d044-128">Oprogramowanie pośredniczące OWIN wywoła metodę `Configuration(...)` podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4d044-128">The OWIN middleware will invoke the `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="4d044-129">Deklaracja klasy, aby zmienić `public partial class Startup` — już zaimplementowano część tej klasy dla Ciebie w innym pliku.</span><span class="sxs-lookup"><span data-stu-id="4d044-129">Change the class declaration to `public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="4d044-130">W `Configuration(...)` metody, utworzyć ConfigureAuth(...) wywołana w celu ustawienia uwierzytelniania dla aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="4d044-130">In the `Configuration(...)` method, make a call to ConfigureAuth(...) to set up authentication for your web app</span></span>  

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

5. <span data-ttu-id="4d044-131">Otwórz plik `App_Start\Startup.Auth.cs` i wdrożenie `ConfigureAuth(...)` metody.</span><span class="sxs-lookup"><span data-stu-id="4d044-131">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="4d044-132">Parametry podane `OpenIdConnectAuthenticationOptions` będzie służyć jako współrzędnych dla aplikacji w celu komunikowania się z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d044-132">The parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>  <span data-ttu-id="4d044-133">Należy również skonfigurować uwierzytelniania plików Cookie — oprogramowanie pośredniczące OpenID Connect używa plików cookie poniżej obejmuje.</span><span class="sxs-lookup"><span data-stu-id="4d044-133">You'll also need to set up Cookie Authentication - the OpenID Connect middleware uses cookies underneath the covers.</span></span>

        ```C#
        public void ConfigureAuth(IAppBuilder app)
                     {
                             app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);
        
                             app.UseCookieAuthentication(new CookieAuthenticationOptions());
        
                             app.UseOpenIdConnectAuthentication(
                                     new OpenIdConnectAuthenticationOptions
                                     {
                                             // The `Authority` represents the v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                                             // The `Scope` describes the permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                                             // In a real application you could use issuer validation for additional checks, like making sure the user's organization has signed up for your app, for instance.
        
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

## <a name="send-authentication-requests"></a><span data-ttu-id="4d044-134">Wysyłanie żądania uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="4d044-134">Send authentication requests</span></span>
<span data-ttu-id="4d044-135">Aplikacji jest teraz prawidłowo skonfigurowana do komunikowania się z punktem końcowym v2.0 za pomocą protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="4d044-135">Your app is now properly configured to communicate with the v2.0 endpoint using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="4d044-136">Wszystkie szczegóły ugly obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i podtrzymywanie sesji użytkowników ma podjąć obsługę OWIN.</span><span class="sxs-lookup"><span data-stu-id="4d044-136">OWIN has taken care of all of the ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="4d044-137">Wszystko, co jest pozostaje, aby zapewnić użytkownikom możliwość zalogować się i wylogowywania.</span><span class="sxs-lookup"><span data-stu-id="4d044-137">All that remains is to give your users a way to sign in and sign out.</span></span>

- <span data-ttu-id="4d044-138">Można użyć znaczników w kontrolerach wymaganie, że użytkownik loguje się przed uzyskaniem dostępu do konkretnej strony autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="4d044-138">You can use authorize tags in your controllers to require that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="4d044-139">Otwórz `Controllers\HomeController.cs`i Dodaj `[Authorize]` tag do kontrolera informacje.</span><span class="sxs-lookup"><span data-stu-id="4d044-139">Open `Controllers\HomeController.cs`, and add the `[Authorize]` tag to the About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="4d044-140">OWIN umożliwia również wystawić żądania uwierzytelniania od bezpośrednio w kodzie.</span><span class="sxs-lookup"><span data-stu-id="4d044-140">You can also use OWIN to directly issue authentication requests from within your code.</span></span>  <span data-ttu-id="4d044-141">Otwórz `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="4d044-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="4d044-142">W działaniach SignIn() i SignOut() wystawić odpowiednio OpenID Connect żądania i wylogowania żądania.</span><span class="sxs-lookup"><span data-stu-id="4d044-142">In the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with the v2.0 endpoint is not yet supported.  Here, we just end the session with the web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="4d044-143">Teraz Otwórz `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="4d044-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="4d044-144">Jest to, której będzie wyświetlany, gdy użytkownik łączy logowania i wylogowywania aplikacji, a następnie wydrukuj nazwy użytkownika w widoku.</span><span class="sxs-lookup"><span data-stu-id="4d044-144">This is where you'll show the user your app's sign-in and sign-out links, and print out the user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves.*@
        
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

## <a name="display-user-information"></a><span data-ttu-id="4d044-145">Wyświetl informacje o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="4d044-145">Display user information</span></span>
<span data-ttu-id="4d044-146">Podczas uwierzytelniania użytkowników z OpenID Connect, punktu końcowego v2.0 zwraca żądaniu aplikacja, która zawiera oświadczenia lub potwierdzeniami dotyczącymi użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4d044-146">When authenticating users with OpenID Connect, the v2.0 endpoint returns an id_token to the app that contains claims, or assertions about the user.</span></span>  <span data-ttu-id="4d044-147">Może użyć tych oświadczeń spersonalizować aplikacji:</span><span class="sxs-lookup"><span data-stu-id="4d044-147">You can use these claims to personalize your app:</span></span>

- <span data-ttu-id="4d044-148">Otwórz plik `Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="4d044-148">Open the `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="4d044-149">Dostęp do oświadczeń użytkownika w kontrolerach za pośrednictwem `ClaimsPrincipal.Current` obiekt główny zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4d044-149">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // The object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // The subject or nameidentifier claim can be used to uniquely identify the user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="4d044-150">Uruchom polecenie</span><span class="sxs-lookup"><span data-stu-id="4d044-150">Run</span></span>
<span data-ttu-id="4d044-151">Na koniec Skompiluj i uruchom aplikację!</span><span class="sxs-lookup"><span data-stu-id="4d044-151">Finally, build and run your app!</span></span>   <span data-ttu-id="4d044-152">Zaloguj się przy użyciu Account firmy Microsoft lub konta służbowego i zwróć uwagę, jak tożsamość użytkowników jest widoczny w górnym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="4d044-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="4d044-153">Masz teraz zabezpieczone przy użyciu standardowych protokołach branżowych, uwierzytelniających użytkowników przy użyciu ich osobistych i pracy/służbowego konta aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4d044-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="4d044-154">Próbka ukończone (bez wartości konfiguracji) [jest dostarczane jako zip w tym miejscu](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), lub można ją sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="4d044-154">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="4d044-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4d044-155">Next steps</span></span>
<span data-ttu-id="4d044-156">Możesz teraz przejść do bardziej zaawansowanych tematów.</span><span class="sxs-lookup"><span data-stu-id="4d044-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="4d044-157">Można spróbować:</span><span class="sxs-lookup"><span data-stu-id="4d044-157">You may want to try:</span></span>

[<span data-ttu-id="4d044-158">Zabezpieczanie interfejsu API sieci Web, z punktem końcowym v2.0 >></span><span class="sxs-lookup"><span data-stu-id="4d044-158">Secure a Web API with the the v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="4d044-159">Aby uzyskać dodatkowe zasoby Zobacz:</span><span class="sxs-lookup"><span data-stu-id="4d044-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="4d044-160">Przewodnik dewelopera v2.0 >></span><span class="sxs-lookup"><span data-stu-id="4d044-160">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="4d044-161">Tag StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="4d044-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="4d044-162">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="4d044-162">Get security updates for our products</span></span>
<span data-ttu-id="4d044-163">Firma Microsoft zachęca do przekazywania powiadomień o występujących incydentach zabezpieczeń poprzez wizytę na [tej stronie](https://technet.microsoft.com/security/dd252948) i subskrybowanie Doradczych alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4d044-163">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
