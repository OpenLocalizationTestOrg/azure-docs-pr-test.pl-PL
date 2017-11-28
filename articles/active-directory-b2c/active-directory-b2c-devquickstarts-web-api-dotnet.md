---
title: aaaAzure Active Directory B2C | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji sieci .NET Web i wywoływanie sieci web interfejsu api przy użyciu tokenów dostępu do usługi Azure Active Directory B2C i OAuth 2.0."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 9b248e3bf18968e12aae73c07083fa8278befb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="dbc81-103">Usługa Azure AD B2C: Wywołanie interfejsu API sieci web .NET z aplikacji sieci web .NET</span><span class="sxs-lookup"><span data-stu-id="dbc81-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="dbc81-104">Za pomocą usługi Azure AD B2C, można dodawać aplikacje sieci web tooyour funkcje zarządzania zaawansowanych tożsamości i interfejsów API sieci web.</span><span class="sxs-lookup"><span data-stu-id="dbc81-104">By using Azure AD B2C, you can add powerful identity management features tooyour web apps and web APIs.</span></span> <span data-ttu-id="dbc81-105">W tym artykule omówiono sposób toorequest tokenów dostępu i nawiązywać połączenia z "listą zadań".NET tooa aplikacji sieci web .NET interfejs api sieci web.</span><span class="sxs-lookup"><span data-stu-id="dbc81-105">This article discusses how toorequest access tokens and make calls from a .NET "to-do list" web app tooa .NET web api.</span></span>

<span data-ttu-id="dbc81-106">W tym artykule nie opisano, jak tooimplement logowania, rejestracji i profilu zarządzania za pomocą usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="dbc81-106">This article does not cover how tooimplement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="dbc81-107">Uwzględniono w szczególności wywoływania interfejsów API sieci web po hello użytkownik jest już uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="dbc81-107">It focuses on calling web APIs after hello user is already authenticated.</span></span> <span data-ttu-id="dbc81-108">Jeśli nie jest jeszcze, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dbc81-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="dbc81-109">Rozpoczynanie pracy z [aplikacji sieci web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="dbc81-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="dbc81-110">Rozpoczynanie pracy z [interfejs api sieci web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="dbc81-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="dbc81-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dbc81-111">Prerequisite</span></span>

<span data-ttu-id="dbc81-112">toobuild aplikacji sieci web, która wywołuje sieci web interfejsu api, musisz:</span><span class="sxs-lookup"><span data-stu-id="dbc81-112">toobuild a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="dbc81-113">[Tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dbc81-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="dbc81-114">[Zarejestruj sieci web interfejsu api](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="dbc81-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="dbc81-115">[Rejestrowanie aplikacji sieci web](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="dbc81-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="dbc81-116">[Ustawianie zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="dbc81-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="dbc81-117">[Udziel hello sieci web aplikacji uprawnienia toouse hello interfejs api sieci web](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="dbc81-117">[Grant hello web app permissions toouse hello web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbc81-118">Aplikacja kliencka Hello i interfejs API sieci web muszą używać katalogu B2C hello tej samej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dbc81-118">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="download-hello-code"></a><span data-ttu-id="dbc81-119">Pobierz kod hello</span><span class="sxs-lookup"><span data-stu-id="dbc81-119">Download hello code</span></span>

<span data-ttu-id="dbc81-120">Witaj kod dla tego samouczka jest przechowywany w [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="dbc81-120">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="dbc81-121">Przykład Witaj można sklonować, uruchamiając:</span><span class="sxs-lookup"><span data-stu-id="dbc81-121">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="dbc81-122">Po pobraniu hello przykładowy kod tooget plik SLN programu Visual Studio Otwórz hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="dbc81-122">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="dbc81-123">Witaj plik rozwiązania zawiera dwa projekty: `TaskWebApp` i `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="dbc81-123">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="dbc81-124">`TaskWebApp`jest aplikacją sieci web MVC, który hello użytkownika współdziała z.</span><span class="sxs-lookup"><span data-stu-id="dbc81-124">`TaskWebApp` is a MVC web application that hello user interacts with.</span></span> <span data-ttu-id="dbc81-125">`TaskService`to interfejs API sieci web zaplecza aplikacji hello, który przechowuje listy zadań do wykonania poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="dbc81-125">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="dbc81-126">W tym artykule nie opisano hello budynku `TaskWebApp` aplikacji sieci web lub hello `TaskService` interfejs api sieci web.</span><span class="sxs-lookup"><span data-stu-id="dbc81-126">This article does not cover building hello `TaskWebApp` web app or hello `TaskService` web api.</span></span> <span data-ttu-id="dbc81-127">toolearn toobuild hello .NET sieci web aplikacji przy użyciu usługi Azure AD B2C, zobacz nasze [samouczek aplikacji sieci web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="dbc81-127">toolearn how toobuild hello .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="dbc81-128">toolearn jak toobuild hello .NET sieci web interfejsu API zabezpieczone przy użyciu usługi Azure AD B2C, zobacz nasze [interfejsu API sieci web platformy .NET — samouczek](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="dbc81-128">toolearn how toobuild hello .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="dbc81-129">Zaktualizuj konfigurację hello Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="dbc81-129">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="dbc81-130">Naszej próbki jest skonfigurowany toouse hello zasady i klienta identyfikator dzierżawy naszych pokaz.</span><span class="sxs-lookup"><span data-stu-id="dbc81-130">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="dbc81-131">Jeśli chcesz toouse własne dzierżawy:</span><span class="sxs-lookup"><span data-stu-id="dbc81-131">If you would like toouse your own tenant:</span></span>

1. <span data-ttu-id="dbc81-132">Otwórz `web.config` w hello `TaskService` projektu i Zastąp wartości hello</span><span class="sxs-lookup"><span data-stu-id="dbc81-132">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>

    * <span data-ttu-id="dbc81-133">`ida:Tenant` nazwą dzierżawy</span><span class="sxs-lookup"><span data-stu-id="dbc81-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="dbc81-134">`ida:ClientId`za pomocą Identyfikatora aplikacji interfejsu api sieci web</span><span class="sxs-lookup"><span data-stu-id="dbc81-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="dbc81-135">`ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania</span><span class="sxs-lookup"><span data-stu-id="dbc81-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="dbc81-136">Otwórz `web.config` w hello `TaskWebApp` projektu i Zastąp wartości hello</span><span class="sxs-lookup"><span data-stu-id="dbc81-136">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>

    * <span data-ttu-id="dbc81-137">`ida:Tenant` nazwą dzierżawy</span><span class="sxs-lookup"><span data-stu-id="dbc81-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="dbc81-138">`ida:ClientId` identyfikatorem aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="dbc81-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="dbc81-139">`ida:ClientSecret` kluczem tajnym aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="dbc81-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="dbc81-140">`ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania</span><span class="sxs-lookup"><span data-stu-id="dbc81-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="dbc81-141">`ida:EditProfilePolicyId` nazwą zasady edycji profilu</span><span class="sxs-lookup"><span data-stu-id="dbc81-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="dbc81-142">`ida:ResetPasswordPolicyId` nazwą zasady resetowania hasła</span><span class="sxs-lookup"><span data-stu-id="dbc81-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="dbc81-143">Żądania i zapisywanie token dostępu</span><span class="sxs-lookup"><span data-stu-id="dbc81-143">Requesting and saving an access token</span></span>

### <a name="specify-hello-permissions"></a><span data-ttu-id="dbc81-144">Określ uprawnienia hello</span><span class="sxs-lookup"><span data-stu-id="dbc81-144">Specify hello permissions</span></span>

<span data-ttu-id="dbc81-145">W kolejności toomake hello wywołania toohello interfejsu API sieci web, należy tooauthenticate hello użytkownika (przy użyciu Twojego konta-konta/zasad logowania) i [odbierania token dostępu](active-directory-b2c-access-tokens.md) z usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="dbc81-145">In order toomake hello call toohello web API, you need tooauthenticate hello user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="dbc81-146">W kolejności tooreceive tokenu dostępu najpierw należy określić uprawnienia hello chcesz toogrant tokenu dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="dbc81-146">In order tooreceive an access token, you first must specify hello permissions you would like hello access token toogrant.</span></span> <span data-ttu-id="dbc81-147">uprawnienia Hello są określone w hello `scope` parametru po wprowadzeniu hello żądania toohello `/authorize` punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="dbc81-147">hello permissions are specified in hello `scope` parameter when you make hello request toohello `/authorize` endpoint.</span></span> <span data-ttu-id="dbc81-148">Na przykład tooacquire uprawnienia toohello zasobów aplikacji, która ma token dostępu z hello "Odczyt" hello identyfikator URI aplikacji z `https://contoso.onmicrosoft.com/tasks`, będzie zakresu hello `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="dbc81-148">For example, tooacquire an access token with hello “read” permission toohello resource application that has hello App ID URI of `https://contoso.onmicrosoft.com/tasks`, hello scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="dbc81-149">zakres hello toospecify w naszym hello przykładowa, otwórz plik `App_Start\Startup.Auth.cs` i zdefiniuj hello `Scope` zmiennej w OpenIdConnectAuthenticationOptions.</span><span class="sxs-lookup"><span data-stu-id="dbc81-149">toospecify hello scope in our sample, open hello file `App_Start\Startup.Auth.cs` and define hello `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-hello-authorization-code-for-an-access-token"></a><span data-ttu-id="dbc81-150">Kod autoryzacji hello Exchange token dostępu</span><span class="sxs-lookup"><span data-stu-id="dbc81-150">Exchange hello authorization code for an access token</span></span>

<span data-ttu-id="dbc81-151">Po zakończeniu hello środowisko tworzenia konta lub logowanie użytkownika aplikacji otrzyma kod autoryzacji z usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="dbc81-151">After an user completes hello sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="dbc81-152">oprogramowanie pośredniczące OWIN OpenID Connect w Hello zapisze hello kodu, ale nie będzie exchange dla tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="dbc81-152">hello OWIN OpenID Connect middleware will store hello code, but will not exchange it for an access token.</span></span> <span data-ttu-id="dbc81-153">Można użyć hello [biblioteki MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange.</span><span class="sxs-lookup"><span data-stu-id="dbc81-153">You can use hello [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange.</span></span> <span data-ttu-id="dbc81-154">W naszym przykładzie został skonfigurowany wywołanie zwrotne powiadomienia do oprogramowania pośredniczącego hello OpenID Connect przy każdym odebraniu kod autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="dbc81-154">In our sample, we configured a notification callback into hello OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="dbc81-155">W hello wywołania zwrotnego możemy użyć MSAL tooexchange hello kodu dla tokenu i Zapisz hello token do pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="dbc81-155">In hello callback, we use MSAL tooexchange hello code for a token and save hello token into hello cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract hello code from hello response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange hello code for a token. Make sure toospecify hello necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-hello-web-api"></a><span data-ttu-id="dbc81-156">Wywołanie interfejsu API sieci web hello</span><span class="sxs-lookup"><span data-stu-id="dbc81-156">Calling hello web API</span></span>

<span data-ttu-id="dbc81-157">W tej sekcji omówiono sposób toouse hello token otrzymał podczas tworzenia-konta/logowania w usłudze Azure AD B2C w kolejności tooaccess hello interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="dbc81-157">This section discusses how toouse hello token received during sign-up/sign-in with Azure AD B2C in order tooaccess hello web API.</span></span>

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a><span data-ttu-id="dbc81-158">Pobrać token hello zapisane w hello kontrolerów</span><span class="sxs-lookup"><span data-stu-id="dbc81-158">Retrieve hello saved token in hello controllers</span></span>

<span data-ttu-id="dbc81-159">Witaj `TasksController` jest odpowiedzialny za komunikację z interfejsu API sieci web hello wysyłania tooread toohello interfejsu API żądania HTTP, tworzenie i usuwanie zadań.</span><span class="sxs-lookup"><span data-stu-id="dbc81-159">hello `TasksController` is responsible for communicating with hello web API and for sending HTTP requests toohello API tooread, create, and delete tasks.</span></span> <span data-ttu-id="dbc81-160">Ponieważ hello interfejsu API jest zabezpieczony przez usługę Azure AD B2C, należy toofirst pobrać hello token, który został zapisany w hello powyżej kroku.</span><span class="sxs-lookup"><span data-stu-id="dbc81-160">Because hello API is secured by Azure AD B2C, you need toofirst retrieve hello token you saved in hello above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL tooretrieve hello token from hello cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve hello token using hello provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-hello-web-api"></a><span data-ttu-id="dbc81-161">Odczytywanie zadań z hello interfejsu API sieci web</span><span class="sxs-lookup"><span data-stu-id="dbc81-161">Read tasks from hello web API</span></span>

<span data-ttu-id="dbc81-162">Jeśli masz tokenu, możesz dołączyć go toohello HTTP `GET` żądania w hello `Authorization` wywołania toosecurely nagłówka `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="dbc81-162">When you have a token, you can attach it toohello HTTP `GET` request in hello `Authorization` header toosecurely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve hello token with hello specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token toohello Authorization header and make hello request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-hello-web-api"></a><span data-ttu-id="dbc81-163">Tworzenie i usuwanie zadań na powitania interfejsu API sieci web</span><span class="sxs-lookup"><span data-stu-id="dbc81-163">Create and delete tasks on hello web API</span></span>

<span data-ttu-id="dbc81-164">Wykonaj hello sam wzorca podczas wysyłania `POST` i `DELETE` żądań toohello interfejsu API sieci web, przy użyciu tokenu dostępu hello tooretrieve MSAL z pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="dbc81-164">Follow hello same pattern when you send `POST` and `DELETE` requests toohello web API, using MSAL tooretrieve hello access token from hello cache.</span></span>

## <a name="run-hello-sample-app"></a><span data-ttu-id="dbc81-165">Uruchom hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="dbc81-165">Run hello sample app</span></span>

<span data-ttu-id="dbc81-166">Na koniec Skompiluj i uruchom oba aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="dbc81-166">Finally, build and run both hello apps.</span></span> <span data-ttu-id="dbc81-167">Zarejestruj się i zaloguj się i Utwórz zadania dla hello zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dbc81-167">Sign up and sign in, and create tasks for hello signed-in user.</span></span> <span data-ttu-id="dbc81-168">Wyloguj się i zaloguj się jako inny użytkownik.</span><span class="sxs-lookup"><span data-stu-id="dbc81-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="dbc81-169">Utwórz zadania dla tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dbc81-169">Create tasks for that user.</span></span> <span data-ttu-id="dbc81-170">Zwróć uwagę, jak hello zadania są przechowywane dla poszczególnych użytkowników hello interfejsu API, ponieważ hello interfejsu API wyodrębnia tożsamości użytkownika hello z hello token, który odbiera.</span><span class="sxs-lookup"><span data-stu-id="dbc81-170">Notice how hello tasks are stored per-user on hello API, because hello API extracts hello user's identity from hello token it receives.</span></span> <span data-ttu-id="dbc81-171">Spróbuj również odtwarzanie z zakresami hello.</span><span class="sxs-lookup"><span data-stu-id="dbc81-171">Also try playing with hello scopes.</span></span> <span data-ttu-id="dbc81-172">Usuń uprawnienie hello zbyt "write", a następnie spróbuj dodać zadania.</span><span class="sxs-lookup"><span data-stu-id="dbc81-172">Remove hello permission too"write" and then try adding a task.</span></span> <span data-ttu-id="dbc81-173">Po prostu upewnij się, że toosign limit każdej zmianie zakresu hello.</span><span class="sxs-lookup"><span data-stu-id="dbc81-173">Just make sure toosign out each time you change hello scope.</span></span>

