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
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="e1305-103">Aplikacja sieci web ASP.NET, logowania i wylogowywania z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1305-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="e1305-104">Podając jednego logowania i wylogowywania tylko kilka wierszy kodu, Azure Active Directory (Azure AD) prościej możesz toooutsource aplikacji sieci web zarządzania tożsamościami.</span><span class="sxs-lookup"><span data-stu-id="e1305-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you toooutsource web-app identity management.</span></span> <span data-ttu-id="e1305-105">Może się zarejestrować użytkowników i aplikacji sieci web ASP.NET przy użyciu hello firmę Microsoft implementacją interfejsu Open Web dla platformy .NET (OWIN) oprogramowania pośredniczącego.</span><span class="sxs-lookup"><span data-stu-id="e1305-105">You can sign users in and out of ASP.NET web apps by using hello Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="e1305-106">Społeczność oprogramowania pośredniczącego OWIN znajduje się w programie .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e1305-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="e1305-107">W tym artykule przedstawiono sposób toouse OWIN do:</span><span class="sxs-lookup"><span data-stu-id="e1305-107">This article shows how toouse OWIN to:</span></span>

* <span data-ttu-id="e1305-108">Loguj użytkowników w aplikacjach tooweb za pomocą usługi Azure AD jako dostawcy tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-108">Sign users in tooweb apps by using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="e1305-109">Wyświetlane informacje użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e1305-109">Display some user information.</span></span>
* <span data-ttu-id="e1305-110">Loguj użytkowników spoza aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-110">Sign users out of hello apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="e1305-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="e1305-111">Before you get started</span></span>
* <span data-ttu-id="e1305-112">Pobierz hello [szkielet aplikacji](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) lub pobrać hello [ukończone próbki](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="e1305-112">Download hello [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download hello [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="e1305-113">Należy również dzierżawa usługi Azure AD, w których aplikacja hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="e1305-113">You also need an Azure AD tenant in which tooregister hello app.</span></span> <span data-ttu-id="e1305-114">Jeśli nie masz już dzierżawę usługi Azure AD [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="e1305-114">If you don't already have an Azure AD tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="e1305-115">Gdy wszystko będzie gotowe, wykonaj procedury hello hello obok cztery sekcje.</span><span class="sxs-lookup"><span data-stu-id="e1305-115">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-register-hello-new-app-with-azure-ad"></a><span data-ttu-id="e1305-116">Krok 1: Zarejestruj hello nowej aplikacji z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1305-116">Step 1: Register hello new app with Azure AD</span></span>
<span data-ttu-id="e1305-117">tooset użytkowników tooauthenticate aplikacji hello, najpierw zarejestrować go w dzierżawie powitalnych następujący:</span><span class="sxs-lookup"><span data-stu-id="e1305-117">tooset up hello app tooauthenticate users, first register it in your tenant by doing hello following:</span></span>

1. <span data-ttu-id="e1305-118">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1305-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e1305-119">Na górnym pasku hello kliknij nazwę konta.</span><span class="sxs-lookup"><span data-stu-id="e1305-119">On hello top bar, click your account name.</span></span> <span data-ttu-id="e1305-120">W obszarze hello **katalogu** listy, wybierz hello dzierżawy usługi Active Directory, w którym ma tooregister aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-120">Under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="e1305-121">Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e1305-121">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="e1305-122">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="e1305-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="e1305-123">Wykonaj hello monituje toocreate nowy **aplikacji sieci Web i/lub WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="e1305-123">Follow hello prompts toocreate a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="e1305-124">**Nazwa** opisuje toousers aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-124">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="e1305-125">**Adres URL logowania** jest hello podstawowy adres URL aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-125">**Sign-On URL** is hello base URL of hello app.</span></span> <span data-ttu-id="e1305-126">szkielet Hello domyślny adres URL jest https://localhost:44320 /.</span><span class="sxs-lookup"><span data-stu-id="e1305-126">hello skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="e1305-127">Po zakończeniu rejestracji hello Azure AD przypisuje aplikacji hello identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="e1305-127">After you've completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="e1305-128">Skopiuj wartość hello z toouse strony aplikacji hello w kolejnych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-128">Copy hello value from hello app page toouse in hello next sections.</span></span>
7. <span data-ttu-id="e1305-129">Z hello **ustawienia** -> **właściwości** strony dla aplikacji, aktualizacji hello identyfikator URI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e1305-129">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="e1305-130">Witaj **identyfikator URI aplikacji** to unikatowy identyfikator dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-130">hello **App ID URI** is a unique identifier for hello app.</span></span> <span data-ttu-id="e1305-131">Witaj konwencją nazewnictwa jest `https://<tenant-domain>/<app-name>` (na przykład `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="e1305-131">hello naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="e1305-132">Krok 2: Konfigurowanie potoku uwierzytelniania OWIN toouse hello hello aplikacji</span><span class="sxs-lookup"><span data-stu-id="e1305-132">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="e1305-133">W tym kroku skonfigurujesz hello OWIN oprogramowanie pośredniczące toouse hello protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="e1305-133">In this step, you configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="e1305-134">Użyj żądania logowania i wylogowywania tooissue OWIN, zarządzania sesjami użytkownika, uzyskiwanie informacji o użytkowniku i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="e1305-134">You use OWIN tooissue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="e1305-135">toobegin, dodać hello OWIN oprogramowanie pośredniczące NuGet pakiety toohello projektu przy użyciu konsoli Menedżera pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-135">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="e1305-136">tooadd o nazwie Projekt startowy OWIN klasy toohello `Startup.cs`, kliknij prawym przyciskiem myszy projekt hello, wybierz **Dodaj**, wybierz pozycję **nowy element**, a następnie wyszukaj **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="e1305-136">tooadd an OWIN Startup class toohello project called `Startup.cs`, right-click hello project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="e1305-137">oprogramowanie pośredniczące OWIN Hello wywołuje hello **Configuration(...)**  metoda po uruchomieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-137">hello OWIN middleware invokes hello **Configuration(...)** method when hello app starts.</span></span>
3. <span data-ttu-id="e1305-138">Zmiana deklaracji klasy hello zbyt`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="e1305-138">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="e1305-139">Już zaimplementowano część tej klasy dla Ciebie w innym pliku.</span><span class="sxs-lookup"><span data-stu-id="e1305-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="e1305-140">W hello **Configuration(...)**  metody wywoływania zbyt**ConfgureAuth(...)**  tooset się uwierzytelniania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-140">In hello **Configuration(...)** method, make a call too**ConfgureAuth(...)** tooset up authentication for hello app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="e1305-141">Otwórz plik App_Start\Startup.Auth.cs hello, a następnie wdrożyć hello **ConfigureAuth(...)**  metody.</span><span class="sxs-lookup"><span data-stu-id="e1305-141">Open hello App_Start\Startup.Auth.cs file, and then implement hello **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="e1305-142">Witaj podane parametry *OpenIDConnectAuthenticationOptions* służyć jako współrzędne toocommunicate aplikacji hello z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1305-142">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello app toocommunicate with Azure AD.</span></span> <span data-ttu-id="e1305-143">Należy również tooset się uwierzytelniania plików cookie, ponieważ oprogramowanie pośredniczące hello OpenID Connect używa plików cookie w tle hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-143">You also need tooset up cookie authentication, because hello OpenID Connect middleware uses cookies in hello background.</span></span>

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

5. <span data-ttu-id="e1305-144">Otwórz plik web.config hello w katalogu głównym hello hello projektu, a następnie wprowadź wartości konfiguracji hello w hello `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="e1305-144">Open hello web.config file in hello root of hello project, and then enter hello configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="e1305-145">`ida:ClientId`: hello GUID skopiowany z hello portalu Azure w "krok 1: hello zarejestrować nową aplikację z usługą Azure AD."</span><span class="sxs-lookup"><span data-stu-id="e1305-145">`ida:ClientId`: hello GUID you copied from hello Azure portal in "Step 1: Register hello new app with Azure AD."</span></span>
  * <span data-ttu-id="e1305-146">`ida:Tenant`: hello nazwa dzierżawy usługi Azure AD (np. contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="e1305-146">`ida:Tenant`: hello name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="e1305-147">`ida:PostLogoutRedirectUri`: hello wskaźnika, który informuje usługi Azure AD, w którym użytkownik powinien być przekierowany po pomyślnym zakończeniu wylogowania żądania.</span><span class="sxs-lookup"><span data-stu-id="e1305-147">`ida:PostLogoutRedirectUri`: hello indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="e1305-148">Krok 3: Użycie tooAzure AD żądań OWIN tooissue logowania się i wylogowania</span><span class="sxs-lookup"><span data-stu-id="e1305-148">Step 3: Use OWIN tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="e1305-149">Aplikacja Hello jest teraz toocommunicate poprawnie skonfigurowane w usłudze Azure AD przy użyciu protokołu uwierzytelniania OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-149">hello app is now properly configured toocommunicate with Azure AD by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="e1305-150">OWIN obsłużyła wszystkie szczegóły hello obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i utrzymywanie sesji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e1305-150">OWIN has handled all of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="e1305-151">Wszystkie opcje, które pozostaje jest toogive użytkownikom toosign sposób w i wylogowywania.</span><span class="sxs-lookup"><span data-stu-id="e1305-151">All that remains is toogive your users a way toosign in and sign out.</span></span>

1. <span data-ttu-id="e1305-152">Można autoryzować tagów w Twojej kontrolerów toorequire użytkowników toosign w, aby dostęp do określonych stron.</span><span class="sxs-lookup"><span data-stu-id="e1305-152">You can use authorize tags in your controllers toorequire users toosign in before they access certain pages.</span></span> <span data-ttu-id="e1305-153">toodo tak, otwórz Controllers\HomeController.cs, a następnie dodaj hello `[Authorize]` tagu toohello dotyczące kontrolera.</span><span class="sxs-lookup"><span data-stu-id="e1305-153">toodo so, open Controllers\HomeController.cs, and then add hello `[Authorize]` tag toohello About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="e1305-154">Umożliwia także żądania uwierzytelniania OWIN toodirectly problem z w kodzie.</span><span class="sxs-lookup"><span data-stu-id="e1305-154">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span> <span data-ttu-id="e1305-155">toodo, otwórz Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="e1305-155">toodo so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="e1305-156">Następnie w akcji SignIn() i SignOut() hello wystawiania żądań wylogowania i żądania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="e1305-156">Then, in hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

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

3. <span data-ttu-id="e1305-157">Otwórz Views\Shared\_LoginPartial.cshtml tooshow hello hello aplikacji logowania i wylogowywania łącza użytkownika i tooprint się nazwa użytkownika hello w widoku.</span><span class="sxs-lookup"><span data-stu-id="e1305-157">Open Views\Shared\_LoginPartial.cshtml tooshow hello user hello app sign-in and sign-out links, and tooprint out hello user's name in a view.</span></span>

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

## <a name="step-4-display-user-information"></a><span data-ttu-id="e1305-158">Krok 4: Wyświetlane informacje o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="e1305-158">Step 4: Display user information</span></span>
<span data-ttu-id="e1305-159">Podczas uwierzytelniania użytkowników z OpenID Connect, usługi Azure AD zwraca aplikację toohello żądaniu, która zawiera "oświadczenia" lub potwierdzeniami dotyczącymi hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e1305-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token toohello app that contains "claims," or assertions about hello user.</span></span> <span data-ttu-id="e1305-160">Możesz użyć tych aplikacji hello toopersonalize oświadczeń hello następujący:</span><span class="sxs-lookup"><span data-stu-id="e1305-160">You can use these claims toopersonalize hello app by doing hello following:</span></span>

1. <span data-ttu-id="e1305-161">Otwórz plik Controllers\HomeController.cs hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-161">Open hello Controllers\HomeController.cs file.</span></span> <span data-ttu-id="e1305-162">Dostęp do oświadczeń użytkowników hello w kontrolerach za pośrednictwem hello `ClaimsPrincipal.Current` obiekt główny zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e1305-162">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

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

2. <span data-ttu-id="e1305-163">Tworzenie i uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-163">Build and run hello app.</span></span> <span data-ttu-id="e1305-164">Jeśli nie zostało utworzone nowy użytkownik w dzierżawie z domeny onmicrosoft.com, teraz jest toodo czas hello tak.</span><span class="sxs-lookup"><span data-stu-id="e1305-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is hello time toodo so.</span></span> <span data-ttu-id="e1305-165">Oto kroki tej procedury:</span><span class="sxs-lookup"><span data-stu-id="e1305-165">Here's how:</span></span>

  <span data-ttu-id="e1305-166">a.</span><span class="sxs-lookup"><span data-stu-id="e1305-166">a.</span></span> <span data-ttu-id="e1305-167">Zaloguj się przy użyciu tego użytkownika, zwracając uwagę, jak tożsamość użytkownika hello jest odzwierciedlone na górnym pasku hello.</span><span class="sxs-lookup"><span data-stu-id="e1305-167">Sign in with that user, and note how hello user's identity is reflected on hello top bar.</span></span>

  <span data-ttu-id="e1305-168">b.</span><span class="sxs-lookup"><span data-stu-id="e1305-168">b.</span></span> <span data-ttu-id="e1305-169">Wyloguj się, a następnie zalogować się jako inny użytkownik w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="e1305-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="e1305-170">c.</span><span class="sxs-lookup"><span data-stu-id="e1305-170">c.</span></span> <span data-ttu-id="e1305-171">Jeśli czujesz szczególnie ambitne, Zarejestruj i uruchomić inne wystąpienie tej aplikacji (z jego własnej clientId), a Obejrzyj jednej operacji logowania w akcji.</span><span class="sxs-lookup"><span data-stu-id="e1305-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1305-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e1305-172">Next steps</span></span>
<span data-ttu-id="e1305-173">Aby informacje, zobacz [próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (bez wartości konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="e1305-173">For reference, see [hello completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="e1305-174">Możesz teraz przejść toomore Tematy zaawansowane.</span><span class="sxs-lookup"><span data-stu-id="e1305-174">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="e1305-175">Na przykład, spróbuj [zabezpieczyć interfejs API sieci Web z usługą Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e1305-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
