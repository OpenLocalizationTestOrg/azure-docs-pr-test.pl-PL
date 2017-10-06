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
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a>Usługa Azure AD B2C: Wywołanie interfejsu API sieci web .NET z aplikacji sieci web .NET

Za pomocą usługi Azure AD B2C, można dodawać aplikacje sieci web tooyour funkcje zarządzania zaawansowanych tożsamości i interfejsów API sieci web. W tym artykule omówiono sposób toorequest tokenów dostępu i nawiązywać połączenia z "listą zadań".NET tooa aplikacji sieci web .NET interfejs api sieci web.

W tym artykule nie opisano, jak tooimplement logowania, rejestracji i profilu zarządzania za pomocą usługi Azure AD B2C. Uwzględniono w szczególności wywoływania interfejsów API sieci web po hello użytkownik jest już uwierzytelniony. Jeśli nie jest jeszcze, wykonaj następujące czynności:

* Rozpoczynanie pracy z [aplikacji sieci web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)
* Rozpoczynanie pracy z [interfejs api sieci web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)

## <a name="prerequisite"></a>Wymagania wstępne

toobuild aplikacji sieci web, która wywołuje sieci web interfejsu api, musisz:

1. [Tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md).
2. [Zarejestruj sieci web interfejsu api](active-directory-b2c-app-registration.md#register-a-web-api).
3. [Rejestrowanie aplikacji sieci web](active-directory-b2c-app-registration.md#register-a-web-app).
4. [Ustawianie zasad](active-directory-b2c-reference-policies.md).
5. [Udziel hello sieci web aplikacji uprawnienia toouse hello interfejs api sieci web](active-directory-b2c-access-tokens.md#publishing-permissions).

> [!IMPORTANT]
> Aplikacja kliencka Hello i interfejs API sieci web muszą używać katalogu B2C hello tej samej usługi Azure AD.
>

## <a name="download-hello-code"></a>Pobierz kod hello

Witaj kod dla tego samouczka jest przechowywany w [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Przykład Witaj można sklonować, uruchamiając:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Po pobraniu hello przykładowy kod tooget plik SLN programu Visual Studio Otwórz hello jest uruchomiona. Witaj plik rozwiązania zawiera dwa projekty: `TaskWebApp` i `TaskService`. `TaskWebApp`jest aplikacją sieci web MVC, który hello użytkownika współdziała z. `TaskService`to interfejs API sieci web zaplecza aplikacji hello, który przechowuje listy zadań do wykonania poszczególnych użytkowników. W tym artykule nie opisano hello budynku `TaskWebApp` aplikacji sieci web lub hello `TaskService` interfejs api sieci web. toolearn toobuild hello .NET sieci web aplikacji przy użyciu usługi Azure AD B2C, zobacz nasze [samouczek aplikacji sieci web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md). toolearn jak toobuild hello .NET sieci web interfejsu API zabezpieczone przy użyciu usługi Azure AD B2C, zobacz nasze [interfejsu API sieci web platformy .NET — samouczek](active-directory-b2c-devquickstarts-api-dotnet.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Zaktualizuj konfigurację hello Azure AD B2C

Naszej próbki jest skonfigurowany toouse hello zasady i klienta identyfikator dzierżawy naszych pokaz. Jeśli chcesz toouse własne dzierżawy:

1. Otwórz `web.config` w hello `TaskService` projektu i Zastąp wartości hello

    * `ida:Tenant` nazwą dzierżawy
    * `ida:ClientId`za pomocą Identyfikatora aplikacji interfejsu api sieci web
    * `ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania

2. Otwórz `web.config` w hello `TaskWebApp` projektu i Zastąp wartości hello

    * `ida:Tenant` nazwą dzierżawy
    * `ida:ClientId` identyfikatorem aplikacji sieci Web
    * `ida:ClientSecret` kluczem tajnym aplikacji sieci Web
    * `ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania
    * `ida:EditProfilePolicyId` nazwą zasady edycji profilu
    * `ida:ResetPasswordPolicyId` nazwą zasady resetowania hasła



## <a name="requesting-and-saving-an-access-token"></a>Żądania i zapisywanie token dostępu

### <a name="specify-hello-permissions"></a>Określ uprawnienia hello

W kolejności toomake hello wywołania toohello interfejsu API sieci web, należy tooauthenticate hello użytkownika (przy użyciu Twojego konta-konta/zasad logowania) i [odbierania token dostępu](active-directory-b2c-access-tokens.md) z usługi Azure AD B2C. W kolejności tooreceive tokenu dostępu najpierw należy określić uprawnienia hello chcesz toogrant tokenu dostępu hello. uprawnienia Hello są określone w hello `scope` parametru po wprowadzeniu hello żądania toohello `/authorize` punktu końcowego. Na przykład tooacquire uprawnienia toohello zasobów aplikacji, która ma token dostępu z hello "Odczyt" hello identyfikator URI aplikacji z `https://contoso.onmicrosoft.com/tasks`, będzie zakresu hello `https://contoso.onmicrosoft.com/tasks/read`.

zakres hello toospecify w naszym hello przykładowa, otwórz plik `App_Start\Startup.Auth.cs` i zdefiniuj hello `Scope` zmiennej w OpenIdConnectAuthenticationOptions.

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

### <a name="exchange-hello-authorization-code-for-an-access-token"></a>Kod autoryzacji hello Exchange token dostępu

Po zakończeniu hello środowisko tworzenia konta lub logowanie użytkownika aplikacji otrzyma kod autoryzacji z usługi Azure AD B2C. oprogramowanie pośredniczące OWIN OpenID Connect w Hello zapisze hello kodu, ale nie będzie exchange dla tokenu dostępu. Można użyć hello [biblioteki MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange. W naszym przykładzie został skonfigurowany wywołanie zwrotne powiadomienia do oprogramowania pośredniczącego hello OpenID Connect przy każdym odebraniu kod autoryzacji. W hello wywołania zwrotnego możemy użyć MSAL tooexchange hello kodu dla tokenu i Zapisz hello token do pamięci podręcznej hello.

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

## <a name="calling-hello-web-api"></a>Wywołanie interfejsu API sieci web hello

W tej sekcji omówiono sposób toouse hello token otrzymał podczas tworzenia-konta/logowania w usłudze Azure AD B2C w kolejności tooaccess hello interfejsu API sieci web.

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a>Pobrać token hello zapisane w hello kontrolerów

Witaj `TasksController` jest odpowiedzialny za komunikację z interfejsu API sieci web hello wysyłania tooread toohello interfejsu API żądania HTTP, tworzenie i usuwanie zadań. Ponieważ hello interfejsu API jest zabezpieczony przez usługę Azure AD B2C, należy toofirst pobrać hello token, który został zapisany w hello powyżej kroku.

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

### <a name="read-tasks-from-hello-web-api"></a>Odczytywanie zadań z hello interfejsu API sieci web

Jeśli masz tokenu, możesz dołączyć go toohello HTTP `GET` żądania w hello `Authorization` wywołania toosecurely nagłówka `TaskService`:

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

### <a name="create-and-delete-tasks-on-hello-web-api"></a>Tworzenie i usuwanie zadań na powitania interfejsu API sieci web

Wykonaj hello sam wzorca podczas wysyłania `POST` i `DELETE` żądań toohello interfejsu API sieci web, przy użyciu tokenu dostępu hello tooretrieve MSAL z pamięci podręcznej hello.

## <a name="run-hello-sample-app"></a>Uruchom hello przykładowej aplikacji

Na koniec Skompiluj i uruchom oba aplikacji hello. Zarejestruj się i zaloguj się i Utwórz zadania dla hello zalogowanego użytkownika. Wyloguj się i zaloguj się jako inny użytkownik. Utwórz zadania dla tego użytkownika. Zwróć uwagę, jak hello zadania są przechowywane dla poszczególnych użytkowników hello interfejsu API, ponieważ hello interfejsu API wyodrębnia tożsamości użytkownika hello z hello token, który odbiera. Spróbuj również odtwarzanie z zakresami hello. Usuń uprawnienie hello zbyt "write", a następnie spróbuj dodać zadania. Po prostu upewnij się, że toosign limit każdej zmianie zakresu hello.

