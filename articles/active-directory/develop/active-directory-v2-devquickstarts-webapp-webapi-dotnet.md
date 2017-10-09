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
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="60f74-103">Wywoływanie interfejsu API sieci web z aplikacji sieci web .NET</span><span class="sxs-lookup"><span data-stu-id="60f74-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="60f74-104">Z punktem końcowym v2.0 hello można szybko dodać aplikacje sieci web tooyour uwierzytelniania i interfejsów API sieci web o obsługę zarówno osobistego konta Microsoft i konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="60f74-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="60f74-105">W tym miejscu firma Microsoft będzie kompilacji aplikacji sieci web MVC, który zaloguje się użytkowników przy użyciu protokołu OpenID Connect, z niektórych pomoc od firmy Microsoft oprogramowania pośredniczącego OWIN.</span><span class="sxs-lookup"><span data-stu-id="60f74-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="60f74-106">Hello aplikacji sieci web pobieranie tokenów dostępu protokołu OAuth 2.0 dla sieci web interfejsu api zabezpieczone przez OAuth 2.0, który pozwala utworzyć, odczytać i delete na określony użytkownik "listą zadań do wykonania".</span><span class="sxs-lookup"><span data-stu-id="60f74-106">hello web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="60f74-107">W tym samouczku zostanie skupić się głównie na przy użyciu MSAL tooacquire i używaj tokenów dostępu w aplikacji sieci web, w pełni opisane [tutaj](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="60f74-107">This tutorial will focus primarily on using MSAL tooacquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="60f74-108">Jako wymagania wstępne, może być toofirst Dowiedz się, jak za[dodać podstawowe tooa logowania w aplikacji sieci web](active-directory-v2-devquickstarts-dotnet-web.md) lub jak zbyt[właściwie zabezpieczyć interfejs API sieci web](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="60f74-108">As prerequisites, you may want toofirst learn how too[add basic sign-in tooa web app](active-directory-v2-devquickstarts-dotnet-web.md) or how too[properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="60f74-109">Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="60f74-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="60f74-110">toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="60f74-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="60f74-111">Pobierz przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="60f74-111">Download sample code</span></span>
<span data-ttu-id="60f74-112">Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="60f74-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="60f74-113">toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) lub klonowania hello szkielet:</span><span class="sxs-lookup"><span data-stu-id="60f74-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="60f74-114">Można też [Pobierz aplikację ukończyć powitalnych jako .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) lub klonowania ukończyć powitalnych aplikacji:</span><span class="sxs-lookup"><span data-stu-id="60f74-114">Alternatively, you can [download hello completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone hello completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="60f74-115">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="60f74-115">Register an app</span></span>
<span data-ttu-id="60f74-116">Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="60f74-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="60f74-117">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="60f74-117">Make sure to:</span></span>

* <span data-ttu-id="60f74-118">Skopiuj hello **identyfikator aplikacji** przypisany tooyour aplikacji, będzie on potrzebny wkrótce.</span><span class="sxs-lookup"><span data-stu-id="60f74-118">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="60f74-119">Utwórz **klucz tajny aplikacji** z hello **hasło** typu i skopiuj jej wartość na później</span><span class="sxs-lookup"><span data-stu-id="60f74-119">Create an **App Secret** of hello **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="60f74-120">Dodaj hello **Web** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="60f74-120">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="60f74-121">Wprowadź poprawny hello **identyfikator URI przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="60f74-121">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="60f74-122">Witaj identyfikatora uri przekierowania wskazuje tooAzure AD którym powinny być kierowane odpowiedzi uwierzytelniania — Witaj domyślną w tym samouczku jest `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="60f74-122">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="60f74-123">Instalowanie interfejsu OWIN</span><span class="sxs-lookup"><span data-stu-id="60f74-123">Install OWIN</span></span>
<span data-ttu-id="60f74-124">Dodaj hello OWIN oprogramowanie pośredniczące NuGet pakiety toohello `TodoList-WebApp` projekt za pomocą hello Konsola Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="60f74-124">Add hello OWIN middleware NuGet packages toohello `TodoList-WebApp` project using hello Package Manager Console.</span></span>  <span data-ttu-id="60f74-125">oprogramowanie pośredniczące OWIN Hello jest używane tooissue żądań logowania i wylogowywania, zarządzanie sesji użytkownika hello i uzyskać informacje o użytkowniku hello, między innymi.</span><span class="sxs-lookup"><span data-stu-id="60f74-125">hello OWIN middleware will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a><span data-ttu-id="60f74-126">Hello logowania użytkownika</span><span class="sxs-lookup"><span data-stu-id="60f74-126">Sign hello user in</span></span>
<span data-ttu-id="60f74-127">Teraz skonfigurować hello OWIN oprogramowanie pośredniczące toouse hello [protokołu uwierzytelniania OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="60f74-127">Now configure hello OWIN middleware toouse hello [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="60f74-128">Otwórz hello `web.config` pliku w katalogu głównym hello hello `TodoList-WebApp` projektu, a następnie wprowadź wartości konfiguracji aplikacji w hello `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="60f74-128">Open hello `web.config` file in hello root of hello `TodoList-WebApp` project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="60f74-129">Witaj `ida:ClientId` jest hello **identyfikator aplikacji** przypisane tooyour aplikacji w portalu rejestracji hello.</span><span class="sxs-lookup"><span data-stu-id="60f74-129">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="60f74-130">Witaj `ida:ClientSecret` jest hello **klucz tajny aplikacji** utworzone w portalu rejestracji hello.</span><span class="sxs-lookup"><span data-stu-id="60f74-130">hello `ida:ClientSecret` is hello **App Secret** you created in hello registration portal.</span></span>
  * <span data-ttu-id="60f74-131">Witaj `ida:RedirectUri` jest hello **identyfikator Uri przekierowania** wprowadzony w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="60f74-131">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>
* <span data-ttu-id="60f74-132">Otwórz hello `web.config` pliku w katalogu głównym hello hello `TodoList-Service` projektu i Zastąp hello `ida:Audience` z hello sam **identyfikator aplikacji** zgodnie z powyższym.</span><span class="sxs-lookup"><span data-stu-id="60f74-132">Open hello `web.config` file in hello root of hello `TodoList-Service` project, and replace hello `ida:Audience` with hello same **Application Id** as above.</span></span>
* <span data-ttu-id="60f74-133">Witaj Otwórz plik `App_Start\Startup.Auth.cs` i Dodaj `using` instrukcje dla bibliotek powitania od góry.</span><span class="sxs-lookup"><span data-stu-id="60f74-133">Open hello file `App_Start\Startup.Auth.cs` and add `using` statements for hello libraries from above.</span></span>
* <span data-ttu-id="60f74-134">W hello tego samego pliku, implementować hello `ConfigureAuth(...)` metody.</span><span class="sxs-lookup"><span data-stu-id="60f74-134">In hello same file, implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="60f74-135">Witaj podane parametry `OpenIDConnectAuthenticationOptions` będzie służyć jako współrzędne toocommunicate Twojej aplikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60f74-135">hello parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

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

## <a name="use-msal-tooget-access-tokens"></a><span data-ttu-id="60f74-136">Używaj tokenów dostępu tooget MSAL</span><span class="sxs-lookup"><span data-stu-id="60f74-136">Use MSAL tooget access tokens</span></span>
<span data-ttu-id="60f74-137">W hello `AuthorizationCodeReceived` powiadomień, chcemy toouse [OAuth 2.0 w połączeniu z OpenID Connect](active-directory-v2-protocols.md) authorization_code hello tooredeem dla toohello token dostępu usługi listy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="60f74-137">In hello `AuthorizationCodeReceived` notification, we want toouse [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code for an access token toohello To-Do List Service.</span></span>  <span data-ttu-id="60f74-138">MSAL może ułatwić ten proces można:</span><span class="sxs-lookup"><span data-stu-id="60f74-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="60f74-139">Najpierw zainstaluj wersję zapoznawczą hello MSAL:</span><span class="sxs-lookup"><span data-stu-id="60f74-139">First, install hello preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="60f74-140">I dodać kolejne `using` toohello instrukcji `App_Start\Startup.Auth.cs` MSAL w pliku.</span><span class="sxs-lookup"><span data-stu-id="60f74-140">And add another `using` statement toohello `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="60f74-141">Teraz Dodaj nową metodę hello `OnAuthorizationCodeReceived` obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="60f74-141">Now add a new method, hello `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="60f74-142">Ten program obsługi zostanie użyty tooacquire MSAL toohello tokenu dostępu do interfejsu API listy zadań do wykonania i będą przechowywane w pamięci podręcznej tokenu w MSAL hello token na później:</span><span class="sxs-lookup"><span data-stu-id="60f74-142">This handler will use MSAL tooacquire an access token toohello To-Do List API, and will store hello token in MSAL's token cache for later:</span></span>

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

* <span data-ttu-id="60f74-143">W aplikacji sieci web MSAL ma rozszerzonego tokenu pamięci podręcznej, które mogą być używane toostore tokenów.</span><span class="sxs-lookup"><span data-stu-id="60f74-143">In web apps, MSAL has an extensible token cache that can be used toostore tokens.</span></span>  <span data-ttu-id="60f74-144">W tym przykładzie implementuje hello `NaiveSessionCache` , który używa tokenów toocache magazynu sesji http.</span><span class="sxs-lookup"><span data-stu-id="60f74-144">This sample implements hello `NaiveSessionCache` which uses http session storage toocache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a><span data-ttu-id="60f74-145">Witaj wywołania interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="60f74-145">Call hello Web API</span></span>
<span data-ttu-id="60f74-146">Teraz nadszedł czas, tooactually Użyj hello ' access_token ', które zostało zakupione w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="60f74-146">Now it's time tooactually use hello access_token you acquired in step 3.</span></span>  <span data-ttu-id="60f74-147">Aplikacja sieci web Otwórz hello `Controllers\TodoListController.cs` pliku, który sprawia, że wszystkie hello CRUD żądań toohello interfejsu API listy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="60f74-147">Open hello web app's `Controllers\TodoListController.cs` file, which makes all hello CRUD requests toohello To-Do List API.</span></span>

* <span data-ttu-id="60f74-148">Można użyć MSAL ponownie tutaj access_tokens toofetch z hello MSAL pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="60f74-148">You can use MSAL again here toofetch access_tokens from hello MSAL cache.</span></span>  <span data-ttu-id="60f74-149">Najpierw dodaj `using` instrukcji MSAL toothis pliku.</span><span class="sxs-lookup"><span data-stu-id="60f74-149">First, add a `using` statement for MSAL toothis file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="60f74-150">W hello `Index` akcji, użyj MSAL `AcquireTokenSilentAsync` tooget metody ' access_token ', które mogą być używane tooread danych z hello usługi listy zadań do wykonania:</span><span class="sxs-lookup"><span data-stu-id="60f74-150">In hello `Index` action, use MSAL's `AcquireTokenSilentAsync` method tooget an access_token that can be used tooread data from hello To-Do List service:</span></span>

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

* <span data-ttu-id="60f74-151">Witaj próbki dodaje hello wynikowy token toohello żądanie HTTP GET jako hello `Authorization` nagłówka, które usługa listy zadań do wykonania hello używa tooauthenticate hello żądania.</span><span class="sxs-lookup"><span data-stu-id="60f74-151">hello sample then adds hello resulting token toohello HTTP GET request as hello `Authorization` header, which hello To-Do List service uses tooauthenticate hello request.</span></span>
* <span data-ttu-id="60f74-152">Jeśli zwróci hello usługi listy zadań do wykonania `401 Unauthorized` odpowiedzi, access_tokens hello w MSAL stały się nieprawidłowy jakiegoś powodu.</span><span class="sxs-lookup"><span data-stu-id="60f74-152">If hello To-Do List service returns a `401 Unauthorized` response, hello access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="60f74-153">W takim przypadku należy porzucić wszystkie access_tokens z hello MSAL pamięci podręcznej i wyświetla komunikat potrzebnych toosign w ponownie, który zostanie uruchomiony ponownie przepływ tokenu nabycia hello hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="60f74-153">In this case, you should drop any access_tokens from hello MSAL cache and show hello user a message that they may need toosign in again, which will restart hello token acquisition flow.</span></span>

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

* <span data-ttu-id="60f74-154">Podobnie jeśli MSAL tooreturn ' access_token ' jakiejkolwiek przyczyny, należy poinstruować hello toosign użytkownika w ponownie.</span><span class="sxs-lookup"><span data-stu-id="60f74-154">Similarly, if MSAL is unable tooreturn an access_token for any reason, you should instruct hello user toosign in again.</span></span>  <span data-ttu-id="60f74-155">Jest tak proste, jak przechwytywanie dowolnego `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="60f74-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* <span data-ttu-id="60f74-156">Witaj dokładnie takie same `AcquireTokenSilentAsync` wywołanie jest implementd w hello `Create` i `Delete` akcje.</span><span class="sxs-lookup"><span data-stu-id="60f74-156">hello exact same `AcquireTokenSilentAsync` call is implementd in hello `Create` and `Delete` actions.</span></span>  <span data-ttu-id="60f74-157">W aplikacji sieci web można użyć tego access_tokens tooget metody MSAL zawsze, gdy są potrzebne w Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="60f74-157">In web apps, you can use this MSAL method tooget access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="60f74-158">MSAL zajmie się pobieranie, buforowanie i odświeżanie tokenów.</span><span class="sxs-lookup"><span data-stu-id="60f74-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="60f74-159">Na koniec Skompiluj i uruchom aplikację!</span><span class="sxs-lookup"><span data-stu-id="60f74-159">Finally, build and run your app!</span></span>  <span data-ttu-id="60f74-160">Zaloguj się przy użyciu Account Microsoft lub konta usługi Azure AD i zwróć uwagę, jak tożsamość użytkownika hello jest widoczny w hello górnym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="60f74-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="60f74-161">Dodaj i usuń niektóre elementy z listy zadań do wykonania hello użytkownika, powitalne toosee OAuth 2.0 zabezpieczone interfejsu API wywołuje w akcji.</span><span class="sxs-lookup"><span data-stu-id="60f74-161">Add and delete some items from hello user's To-Do List toosee hello OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="60f74-162">Masz teraz aplikacji sieci web i interfejsu API sieci web, zarówno zabezpieczone przy użyciu standardowych protokołach branżowych, uwierzytelniających użytkowników przy użyciu ich osobistych i pracy/służbowego konta.</span><span class="sxs-lookup"><span data-stu-id="60f74-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="60f74-163">Odwołania, hello ukończone próbka (bez wartości konfiguracji) [podano tutaj](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="60f74-163">For reference, hello completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="60f74-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="60f74-164">Next Steps</span></span>
<span data-ttu-id="60f74-165">Aby uzyskać dodatkowe zasoby Zobacz:</span><span class="sxs-lookup"><span data-stu-id="60f74-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="60f74-166">Przewodnik dewelopera v2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="60f74-166">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="60f74-167">Tag StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="60f74-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="60f74-168">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="60f74-168">Get security updates for our products</span></span>
<span data-ttu-id="60f74-169">Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez wizytę [tę stronę](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.</span><span class="sxs-lookup"><span data-stu-id="60f74-169">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

