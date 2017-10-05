---
title: Azure AD .NET aplikacji sieci web wprowadzenie | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 7ac5d3e5cc28ead993e159d003244e6451acb0cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="85dc5-103">Aplikacja sieci web ASP.NET, logowania i wylogowywania z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="85dc5-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="85dc5-104">Podając jednego logowania i wylogowywania tylko kilka wierszy kodu, Azure Active Directory (Azure AD) upraszcza umożliwiające zewnętrzny Zarządzanie tożsamościami aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="85dc5-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="85dc5-105">Może się zarejestrować użytkowników i aplikacji sieci web ASP.NET przy użyciu przez firmę Microsoft implementacją interfejsu Open Web dla platformy .NET (OWIN) oprogramowania pośredniczącego.</span><span class="sxs-lookup"><span data-stu-id="85dc5-105">You can sign users in and out of ASP.NET web apps by using the Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="85dc5-106">Społeczność oprogramowania pośredniczącego OWIN znajduje się w programie .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="85dc5-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="85dc5-107">W tym artykule przedstawiono sposób użycia OWIN do:</span><span class="sxs-lookup"><span data-stu-id="85dc5-107">This article shows how to use OWIN to:</span></span>

* <span data-ttu-id="85dc5-108">Logowania użytkowników do aplikacji sieci web przy użyciu usługi Azure AD jako dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="85dc5-108">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="85dc5-109">Wyświetlane informacje użytkownika.</span><span class="sxs-lookup"><span data-stu-id="85dc5-109">Display some user information.</span></span>
* <span data-ttu-id="85dc5-110">Loguj użytkowników spoza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85dc5-110">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="85dc5-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="85dc5-111">Before you get started</span></span>
* <span data-ttu-id="85dc5-112">Pobierz [szkielet aplikacji](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) lub pobrać [ukończone próbki](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="85dc5-112">Download the [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download the [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="85dc5-113">Należy również dzierżawa usługi Azure AD, w którym można zarejestrować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85dc5-113">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="85dc5-114">Jeśli nie masz już dzierżawę usługi Azure AD [Dowiedz się, jak kupić](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="85dc5-114">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="85dc5-115">Gdy wszystko będzie gotowe, wykonaj procedury opisane w obok cztery sekcje.</span><span class="sxs-lookup"><span data-stu-id="85dc5-115">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="85dc5-116">Krok 1: Zarejestrować nową aplikację z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="85dc5-116">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="85dc5-117">Aby skonfigurować aplikację do uwierzytelniania użytkowników, najpierw zarejestrować ją w dzierżawie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="85dc5-117">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="85dc5-118">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="85dc5-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="85dc5-119">Na górnym pasku kliknij nazwę konta.</span><span class="sxs-lookup"><span data-stu-id="85dc5-119">On the top bar, click your account name.</span></span> <span data-ttu-id="85dc5-120">W obszarze **katalogu** wybierz dzierżawy usługi Active Directory, które chcesz zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="85dc5-120">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="85dc5-121">Kliknij przycisk **więcej usług** w okienku po lewej stronie, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="85dc5-121">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="85dc5-122">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="85dc5-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="85dc5-123">Postępuj zgodnie z monitami, aby utworzyć nową **aplikacji sieci Web i/lub WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="85dc5-123">Follow the prompts to create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="85dc5-124">**Nazwa** opisuje aplikacji dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="85dc5-124">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="85dc5-125">**Adres URL logowania** jest podstawowy adres URL aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85dc5-125">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="85dc5-126">Szkielet domyślny adres URL jest https://localhost:44320 /.</span><span class="sxs-lookup"><span data-stu-id="85dc5-126">The skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="85dc5-127">Po zakończeniu rejestracji usługi Azure AD przypisuje aplikacji identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="85dc5-127">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="85dc5-128">Skopiuj wartość ze strony aplikacji do użycia w kolejnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="85dc5-128">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="85dc5-129">Z **ustawienia** -> **właściwości** strony dla aplikacji, zaktualizuj identyfikator URI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85dc5-129">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="85dc5-130">**Identyfikator URI aplikacji** to unikatowy identyfikator dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85dc5-130">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="85dc5-131">Konwencja nazewnictwa jest `https://<tenant-domain>/<app-name>` (na przykład `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="85dc5-131">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="85dc5-132">Krok 2: Konfigurowanie aplikacji do używania uwierzytelniania potoku OWIN</span><span class="sxs-lookup"><span data-stu-id="85dc5-132">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="85dc5-133">W tym kroku skonfigurujesz oprogramowanie pośredniczące OWIN do używania protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="85dc5-133">In this step, you configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="85dc5-134">OWIN służy do wysyłania żądań zalogowania się i wylogowania, zarządzania sesjami użytkownika uzyskiwanie informacji o użytkowniku i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="85dc5-134">You use OWIN to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="85dc5-135">Aby rozpocząć, Dodaj pakiety NuGet oprogramowanie pośredniczące OWIN do projektu przy użyciu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="85dc5-135">To begin, add the OWIN middleware NuGet packages to the project by using the Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="85dc5-136">Aby dodać klasy początkowej OWIN do projektu o nazwie `Startup.cs`, kliknij prawym przyciskiem myszy projekt, wybierz **Dodaj**, wybierz pozycję **nowy element**, a następnie wyszukaj **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="85dc5-136">To add an OWIN Startup class to the project called `Startup.cs`, right-click the project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="85dc5-137">Wywołuje oprogramowanie pośredniczące OWIN **Configuration(...)**  metoda po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85dc5-137">The OWIN middleware invokes the **Configuration(...)** method when the app starts.</span></span>
3. <span data-ttu-id="85dc5-138">Deklaracja klasy, aby zmienić `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="85dc5-138">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="85dc5-139">Już zaimplementowano część tej klasy dla Ciebie w innym pliku.</span><span class="sxs-lookup"><span data-stu-id="85dc5-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="85dc5-140">W **Configuration(...)**  utworzyć wywołanie metody **ConfgureAuth(...)**  Aby skonfigurować uwierzytelnianie dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85dc5-140">In the **Configuration(...)** method, make a call to **ConfgureAuth(...)** to set up authentication for the app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="85dc5-141">Otwórz plik App_Start\Startup.Auth.cs, a następnie wdrożyć to rozwiązanie **ConfigureAuth(...)**  metody.</span><span class="sxs-lookup"><span data-stu-id="85dc5-141">Open the App_Start\Startup.Auth.cs file, and then implement the **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="85dc5-142">Parametry podane *OpenIDConnectAuthenticationOptions* służyć jako współrzędnych dla aplikacji w celu komunikowania się z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85dc5-142">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the app to communicate with Azure AD.</span></span> <span data-ttu-id="85dc5-143">Należy również skonfigurować uwierzytelniania plików cookie, ponieważ oprogramowanie pośredniczące OpenID Connect używa plików cookie w tle.</span><span class="sxs-lookup"><span data-stu-id="85dc5-143">You also need to set up cookie authentication, because the OpenID Connect middleware uses cookies in the background.</span></span>

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

5. <span data-ttu-id="85dc5-144">Otwórz plik web.config w katalogu głównym projektu, a następnie wprowadź wartości konfiguracji w `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="85dc5-144">Open the web.config file in the root of the project, and then enter the configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="85dc5-145">`ida:ClientId`: Identyfikator GUID został skopiowany z portalu Azure w "krok 1: zarejestrować nową aplikację z usługą Azure AD."</span><span class="sxs-lookup"><span data-stu-id="85dc5-145">`ida:ClientId`: The GUID you copied from the Azure portal in "Step 1: Register the new app with Azure AD."</span></span>
  * <span data-ttu-id="85dc5-146">`ida:Tenant`: Nazwa dzierżawy usługi Azure AD (np. contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="85dc5-146">`ida:Tenant`: The name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="85dc5-147">`ida:PostLogoutRedirectUri`Wskaźnik, który informuje usługi Azure AD, w którym użytkownik powinien być przekierowany po pomyślnym zakończeniu wylogowania żądania.</span><span class="sxs-lookup"><span data-stu-id="85dc5-147">`ida:PostLogoutRedirectUri`: The indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="85dc5-148">Krok 3: Użyj OWIN do wysyłania żądań zalogowania się i wylogowania do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="85dc5-148">Step 3: Use OWIN to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="85dc5-149">Aplikacji jest teraz prawidłowo skonfigurowana do komunikowania się z usługą Azure AD przy użyciu protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="85dc5-149">The app is now properly configured to communicate with Azure AD by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="85dc5-150">OWIN obsłużyła wszystkie szczegóły obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i utrzymywanie sesji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="85dc5-150">OWIN has handled all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="85dc5-151">Wszystko, co jest pozostaje, aby zapewnić użytkownikom możliwość zalogować się i wylogowywania.</span><span class="sxs-lookup"><span data-stu-id="85dc5-151">All that remains is to give your users a way to sign in and sign out.</span></span>

1. <span data-ttu-id="85dc5-152">Można autoryzować tagów w kontrolerach, aby wymagać od użytkowników do logowania, aby dostęp do określonych stron.</span><span class="sxs-lookup"><span data-stu-id="85dc5-152">You can use authorize tags in your controllers to require users to sign in before they access certain pages.</span></span> <span data-ttu-id="85dc5-153">Aby to zrobić, otwórz Controllers\HomeController.cs, a następnie dodaj `[Authorize]` tag do kontrolera informacje.</span><span class="sxs-lookup"><span data-stu-id="85dc5-153">To do so, open Controllers\HomeController.cs, and then add the `[Authorize]` tag to the About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="85dc5-154">OWIN umożliwia również wystawić żądania uwierzytelniania od bezpośrednio w kodzie.</span><span class="sxs-lookup"><span data-stu-id="85dc5-154">You can also use OWIN to directly issue authentication requests from within your code.</span></span> <span data-ttu-id="85dc5-155">Aby to zrobić, otwórz Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="85dc5-155">To do so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="85dc5-156">Następnie w SignIn() i SignOut() akcje wystawiania żądań wylogowania i żądania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="85dc5-156">Then, in the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

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

3. <span data-ttu-id="85dc5-157">Otwórz Views\Shared\_LoginPartial.cshtml wyświetlany, gdy użytkownik łączy logowania i wylogowywania aplikacji i wydrukuj nazwy użytkownika w widoku.</span><span class="sxs-lookup"><span data-stu-id="85dc5-157">Open Views\Shared\_LoginPartial.cshtml to show the user the app sign-in and sign-out links, and to print out the user's name in a view.</span></span>

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

## <a name="step-4-display-user-information"></a><span data-ttu-id="85dc5-158">Krok 4: Wyświetlane informacje o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="85dc5-158">Step 4: Display user information</span></span>
<span data-ttu-id="85dc5-159">Podczas uwierzytelniania użytkowników z OpenID Connect, usługi Azure AD zwraca żądaniu aplikacja, która zawiera "oświadczenia" lub potwierdzeniami dotyczącymi użytkownika.</span><span class="sxs-lookup"><span data-stu-id="85dc5-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token to the app that contains "claims," or assertions about the user.</span></span> <span data-ttu-id="85dc5-160">Może użyć tych oświadczeń spersonalizować aplikacji, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="85dc5-160">You can use these claims to personalize the app by doing the following:</span></span>

1. <span data-ttu-id="85dc5-161">Otwórz plik Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="85dc5-161">Open the Controllers\HomeController.cs file.</span></span> <span data-ttu-id="85dc5-162">Dostęp do oświadczeń użytkownika w kontrolerach za pośrednictwem `ClaimsPrincipal.Current` obiekt główny zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="85dc5-162">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

2. <span data-ttu-id="85dc5-163">Skompiluj i uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="85dc5-163">Build and run the app.</span></span> <span data-ttu-id="85dc5-164">Jeśli nie zostało utworzone nowy użytkownik w dzierżawie z domeny onmicrosoft.com, należy teraz Aby to zrobić.</span><span class="sxs-lookup"><span data-stu-id="85dc5-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is the time to do so.</span></span> <span data-ttu-id="85dc5-165">Oto kroki tej procedury:</span><span class="sxs-lookup"><span data-stu-id="85dc5-165">Here's how:</span></span>

  <span data-ttu-id="85dc5-166">a.</span><span class="sxs-lookup"><span data-stu-id="85dc5-166">a.</span></span> <span data-ttu-id="85dc5-167">Zaloguj się przy użyciu tego użytkownika, zwracając uwagę, jak tożsamość użytkowników jest odzwierciedlone na górnym pasku.</span><span class="sxs-lookup"><span data-stu-id="85dc5-167">Sign in with that user, and note how the user's identity is reflected on the top bar.</span></span>

  <span data-ttu-id="85dc5-168">b.</span><span class="sxs-lookup"><span data-stu-id="85dc5-168">b.</span></span> <span data-ttu-id="85dc5-169">Wyloguj się, a następnie zalogować się jako inny użytkownik w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="85dc5-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="85dc5-170">c.</span><span class="sxs-lookup"><span data-stu-id="85dc5-170">c.</span></span> <span data-ttu-id="85dc5-171">Jeśli czujesz szczególnie ambitne, Zarejestruj i uruchomić inne wystąpienie tej aplikacji (z jego własnej clientId), a Obejrzyj jednej operacji logowania w akcji.</span><span class="sxs-lookup"><span data-stu-id="85dc5-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85dc5-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="85dc5-172">Next steps</span></span>
<span data-ttu-id="85dc5-173">Aby informacje, zobacz [ukończone próbki](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (bez wartości konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="85dc5-173">For reference, see [the completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="85dc5-174">Możesz teraz przejść do bardziej zaawansowanych tematów.</span><span class="sxs-lookup"><span data-stu-id="85dc5-174">You can now move on to more advanced topics.</span></span> <span data-ttu-id="85dc5-175">Na przykład, spróbuj [zabezpieczyć interfejs API sieci Web z usługą Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="85dc5-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
