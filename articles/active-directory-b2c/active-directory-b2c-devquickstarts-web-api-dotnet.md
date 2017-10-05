---
title: Azure Active Directory B2C | Dokumentacja firmy Microsoft
description: "Jak utworzyć aplikację sieci Web .NET i wywoływanie sieci web interfejsu api przy użyciu tokenów dostępu do usługi Azure Active Directory B2C i OAuth 2.0."
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
ms.openlocfilehash: 48452eb68f826d1c7aa61d5e5531f941ac1422b0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="166a9-103">Usługa Azure AD B2C: Wywołanie interfejsu API sieci web .NET z aplikacji sieci web .NET</span><span class="sxs-lookup"><span data-stu-id="166a9-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="166a9-104">Za pomocą usługi Azure AD B2C, można dodawać tożsamości zaawansowanych funkcji zarządzania do aplikacji sieci web i interfejsów API sieci web.</span><span class="sxs-lookup"><span data-stu-id="166a9-104">By using Azure AD B2C, you can add powerful identity management features to your web apps and web APIs.</span></span> <span data-ttu-id="166a9-105">W tym artykule omówiono sposób żądań tokenów dostępu i Utwórz wywołania z aplikacji sieci web .NET "Lista zadań do wykonania".NET interfejs api sieci web.</span><span class="sxs-lookup"><span data-stu-id="166a9-105">This article discusses how to request access tokens and make calls from a .NET "to-do list" web app to a .NET web api.</span></span>

<span data-ttu-id="166a9-106">W tym artykule nie opisano sposobu wdrażania logowania, rejestracji i zarządzania profilami w usłudze Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="166a9-106">This article does not cover how to implement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="166a9-107">Uwzględniono w szczególności wywoływania interfejsów API sieci web po użytkownik jest już uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="166a9-107">It focuses on calling web APIs after the user is already authenticated.</span></span> <span data-ttu-id="166a9-108">Jeśli nie jest jeszcze, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="166a9-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="166a9-109">Rozpoczynanie pracy z [aplikacji sieci web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="166a9-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="166a9-110">Rozpoczynanie pracy z [interfejs api sieci web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="166a9-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="166a9-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="166a9-111">Prerequisite</span></span>

<span data-ttu-id="166a9-112">Aby utworzyć aplikację sieci web, która wywołuje sieci web interfejsu api, musisz:</span><span class="sxs-lookup"><span data-stu-id="166a9-112">To build a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="166a9-113">[Tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="166a9-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="166a9-114">[Zarejestruj sieci web interfejsu api](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="166a9-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="166a9-115">[Rejestrowanie aplikacji sieci web](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="166a9-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="166a9-116">[Ustawianie zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="166a9-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="166a9-117">[Przyznać uprawnienia aplikacji sieci web w sieci web interfejsu api](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="166a9-117">[Grant the web app permissions to use the web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="166a9-118">Aplikacja kliencka i interfejs API sieci Web muszą korzystać z tego samego katalogu usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="166a9-118">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="download-the-code"></a><span data-ttu-id="166a9-119">Pobieranie kodu</span><span class="sxs-lookup"><span data-stu-id="166a9-119">Download the code</span></span>

<span data-ttu-id="166a9-120">Kod używany w tym samouczku [jest przechowywany w serwisie GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="166a9-120">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="166a9-121">Przykład można sklonować, uruchamiając polecenie:</span><span class="sxs-lookup"><span data-stu-id="166a9-121">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="166a9-122">Po pobraniu przykładu kodu otwórz plik SLN programu Visual Studio, aby rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="166a9-122">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="166a9-123">Plik rozwiązania zawiera dwa projekty: `TaskWebApp` i `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="166a9-123">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="166a9-124">`TaskWebApp`to aplikacja sieci web MVC, którą użytkownik wchodzi w interakcję z.</span><span class="sxs-lookup"><span data-stu-id="166a9-124">`TaskWebApp` is a MVC web application that the user interacts with.</span></span> <span data-ttu-id="166a9-125">`TaskService` to interfejs API zaplecza aplikacji, który przechowuje listy zadań do wykonania poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="166a9-125">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="166a9-126">W tym artykule opisano tworzenie `TaskWebApp` aplikacji sieci web lub `TaskService` interfejs api sieci web.</span><span class="sxs-lookup"><span data-stu-id="166a9-126">This article does not cover building the `TaskWebApp` web app or the `TaskService` web api.</span></span> <span data-ttu-id="166a9-127">Aby dowiedzieć się, jak utworzyć aplikację sieci web platformy .NET przy użyciu usługi Azure AD B2C, zobacz nasze [samouczek aplikacji sieci web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="166a9-127">To learn how to build the .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="166a9-128">Aby dowiedzieć się, jak tworzyć chronione przy użyciu usługi Azure AD B2C interfejsu API sieci web .NET, zobacz nasze [interfejsu API sieci web platformy .NET — samouczek](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="166a9-128">To learn how to build the .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="166a9-129">Aktualizowanie konfiguracji usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="166a9-129">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="166a9-130">Nasz przykład został skonfigurowany do używania zasad i identyfikatora klienta dzierżawy pokazowej.</span><span class="sxs-lookup"><span data-stu-id="166a9-130">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="166a9-131">Jeśli chcesz korzystać z własnych dzierżawy:</span><span class="sxs-lookup"><span data-stu-id="166a9-131">If you would like to use your own tenant:</span></span>

1. <span data-ttu-id="166a9-132">Otwórz plik `web.config` w projekcie `TaskService` i zastąp wartości</span><span class="sxs-lookup"><span data-stu-id="166a9-132">Open `web.config` in the `TaskService` project and replace the values for</span></span>

    * <span data-ttu-id="166a9-133">`ida:Tenant` nazwą dzierżawy</span><span class="sxs-lookup"><span data-stu-id="166a9-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="166a9-134">`ida:ClientId`za pomocą Identyfikatora aplikacji interfejsu api sieci web</span><span class="sxs-lookup"><span data-stu-id="166a9-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="166a9-135">`ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania</span><span class="sxs-lookup"><span data-stu-id="166a9-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="166a9-136">Otwórz plik `web.config` w projekcie `TaskWebApp` i zastąp wartości</span><span class="sxs-lookup"><span data-stu-id="166a9-136">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>

    * <span data-ttu-id="166a9-137">`ida:Tenant` nazwą dzierżawy</span><span class="sxs-lookup"><span data-stu-id="166a9-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="166a9-138">`ida:ClientId` identyfikatorem aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="166a9-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="166a9-139">`ida:ClientSecret` kluczem tajnym aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="166a9-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="166a9-140">`ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania</span><span class="sxs-lookup"><span data-stu-id="166a9-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="166a9-141">`ida:EditProfilePolicyId` nazwą zasady edycji profilu</span><span class="sxs-lookup"><span data-stu-id="166a9-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="166a9-142">`ida:ResetPasswordPolicyId` nazwą zasady resetowania hasła</span><span class="sxs-lookup"><span data-stu-id="166a9-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="166a9-143">Żądania i zapisywanie token dostępu</span><span class="sxs-lookup"><span data-stu-id="166a9-143">Requesting and saving an access token</span></span>

### <a name="specify-the-permissions"></a><span data-ttu-id="166a9-144">Określ uprawnienia</span><span class="sxs-lookup"><span data-stu-id="166a9-144">Specify the permissions</span></span>

<span data-ttu-id="166a9-145">Aby wprowadzić wywołanie interfejsu API sieci web, należy uwierzytelnić użytkownika (przy użyciu Twojego konta-konta/zasad logowania) i [odbierania token dostępu](active-directory-b2c-access-tokens.md) z usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="166a9-145">In order to make the call to the web API, you need to authenticate the user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="166a9-146">Aby otrzymywać tokenu dostępu, należy najpierw określić chcesz tokenu dostępu, aby udzielić uprawnień.</span><span class="sxs-lookup"><span data-stu-id="166a9-146">In order to receive an access token, you first must specify the permissions you would like the access token to grant.</span></span> <span data-ttu-id="166a9-147">Uprawnienia są określone w `scope` parametru po wprowadzeniu żądania `/authorize` punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="166a9-147">The permissions are specified in the `scope` parameter when you make the request to the `/authorize` endpoint.</span></span> <span data-ttu-id="166a9-148">Na przykład, aby uzyskać token dostępu z uprawnieniami "do odczytu", do aplikacji zasobów, która zawiera identyfikator URI aplikacji z `https://contoso.onmicrosoft.com/tasks`, zakres będzie `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="166a9-148">For example, to acquire an access token with the “read” permission to the resource application that has the App ID URI of `https://contoso.onmicrosoft.com/tasks`, the scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="166a9-149">Aby określić zakres w naszym przykładzie, otwórz plik `App_Start\Startup.Auth.cs` i zdefiniuj `Scope` zmiennej w OpenIdConnectAuthenticationOptions.</span><span class="sxs-lookup"><span data-stu-id="166a9-149">To specify the scope in our sample, open the file `App_Start\Startup.Auth.cs` and define the `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-the-authorization-code-for-an-access-token"></a><span data-ttu-id="166a9-150">Kod autoryzacji dla tokenu dostępu programu Exchange</span><span class="sxs-lookup"><span data-stu-id="166a9-150">Exchange the authorization code for an access token</span></span>

<span data-ttu-id="166a9-151">Po użytkownik kończy proces rejestracji i logowania, aplikacja zostanie wyświetlony kod autoryzacji z usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="166a9-151">After an user completes the sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="166a9-152">Oprogramowanie pośredniczące OWIN OpenID Connect zapisze kod, ale nie będzie exchange dla tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="166a9-152">The OWIN OpenID Connect middleware will store the code, but will not exchange it for an access token.</span></span> <span data-ttu-id="166a9-153">Można użyć [biblioteki MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) dokonanie programu exchange.</span><span class="sxs-lookup"><span data-stu-id="166a9-153">You can use the [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) to make the exchange.</span></span> <span data-ttu-id="166a9-154">W naszym przykładzie został skonfigurowany wywołanie zwrotne powiadomienia w oprogramowaniu pośredniczącym protokołu OpenID Connect przy każdym odebraniu kod autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="166a9-154">In our sample, we configured a notification callback into the OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="166a9-155">Podczas wywołania zwrotnego używamy MSAL wymiany kod tokenu i zapisać token do pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="166a9-155">In the callback, we use MSAL to exchange the code for a token and save the token into the cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract the code from the response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange the code for a token. Make sure to specify the necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-the-web-api"></a><span data-ttu-id="166a9-156">Wywołanie interfejsu API sieci web</span><span class="sxs-lookup"><span data-stu-id="166a9-156">Calling the web API</span></span>

<span data-ttu-id="166a9-157">W tej sekcji omówiono sposób użycia tokenu otrzymał podczas tworzenia-konta/logowania w usłudze Azure AD B2C, aby uzyskać dostęp do interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="166a9-157">This section discusses how to use the token received during sign-up/sign-in with Azure AD B2C in order to access the web API.</span></span>

### <a name="retrieve-the-saved-token-in-the-controllers"></a><span data-ttu-id="166a9-158">Pobierz token zapisany w kontrolerów</span><span class="sxs-lookup"><span data-stu-id="166a9-158">Retrieve the saved token in the controllers</span></span>

<span data-ttu-id="166a9-159">`TasksController` Jest odpowiedzialny za komunikację z interfejsu API sieci web i do wysyłania żądań HTTP do interfejsu API mogą odczytywać, tworzyć i usuwać zadania.</span><span class="sxs-lookup"><span data-stu-id="166a9-159">The `TasksController` is responsible for communicating with the web API and for sending HTTP requests to the API to read, create, and delete tasks.</span></span> <span data-ttu-id="166a9-160">Ponieważ interfejsu API jest zabezpieczony przez usługę Azure AD B2C, należy najpierw pobrać token, który został zapisany w kroku powyżej.</span><span class="sxs-lookup"><span data-stu-id="166a9-160">Because the API is secured by Azure AD B2C, you need to first retrieve the token you saved in the above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL to retrieve the token from the cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve the token using the provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-the-web-api"></a><span data-ttu-id="166a9-161">Odczytywanie zadań z interfejsu API sieci web</span><span class="sxs-lookup"><span data-stu-id="166a9-161">Read tasks from the web API</span></span>

<span data-ttu-id="166a9-162">Jeśli masz token może dołączyć ją do HTTP `GET` zażądać `Authorization` nagłówek, aby bezpiecznie wywoływać `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="166a9-162">When you have a token, you can attach it to the HTTP `GET` request in the `Authorization` header to securely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve the token with the specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token to the Authorization header and make the request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-the-web-api"></a><span data-ttu-id="166a9-163">Tworzenie i usuwanie zadań w interfejsie API sieci web</span><span class="sxs-lookup"><span data-stu-id="166a9-163">Create and delete tasks on the web API</span></span>

<span data-ttu-id="166a9-164">Wykonują te same czynności, po wysłaniu `POST` i `DELETE` żądania sieci Web interfejsu API, przy użyciu MSAL można pobrać token dostępu z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="166a9-164">Follow the same pattern when you send `POST` and `DELETE` requests to the web API, using MSAL to retrieve the access token from the cache.</span></span>

## <a name="run-the-sample-app"></a><span data-ttu-id="166a9-165">Uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="166a9-165">Run the sample app</span></span>

<span data-ttu-id="166a9-166">Na koniec Skompiluj i uruchom obie aplikacje.</span><span class="sxs-lookup"><span data-stu-id="166a9-166">Finally, build and run both the apps.</span></span> <span data-ttu-id="166a9-167">Zarejestruj się i zaloguj się i Utwórz zadania dla zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="166a9-167">Sign up and sign in, and create tasks for the signed-in user.</span></span> <span data-ttu-id="166a9-168">Wyloguj się i zaloguj się jako inny użytkownik.</span><span class="sxs-lookup"><span data-stu-id="166a9-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="166a9-169">Utwórz zadania dla tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="166a9-169">Create tasks for that user.</span></span> <span data-ttu-id="166a9-170">Zwróć uwagę, jak zadania są przechowywane dla poszczególnych użytkowników w interfejsie API, ponieważ wyodrębnia on tożsamość użytkownika z tokenu, który odbiera.</span><span class="sxs-lookup"><span data-stu-id="166a9-170">Notice how the tasks are stored per-user on the API, because the API extracts the user's identity from the token it receives.</span></span> <span data-ttu-id="166a9-171">Spróbuj również gry z zakresów.</span><span class="sxs-lookup"><span data-stu-id="166a9-171">Also try playing with the scopes.</span></span> <span data-ttu-id="166a9-172">Usuń uprawnienie do "write", a następnie spróbuj dodać zadania.</span><span class="sxs-lookup"><span data-stu-id="166a9-172">Remove the permission to "write" and then try adding a task.</span></span> <span data-ttu-id="166a9-173">Po prostu upewnij się, że Wyloguj każdej zmianie zakresu.</span><span class="sxs-lookup"><span data-stu-id="166a9-173">Just make sure to sign out each time you change the scope.</span></span>

