---
title: "aaaAzure AD v2 ASP.NET Web Server wprowadzenie — Instalator | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: eadc59666557e9cd294e6e99391001120579144c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Konfigurowanie projektu

W tej sekcji przedstawiono hello kroki tooinstall i konfiguruje potok uwierzytelniania hello za pomocą oprogramowania pośredniczącego OWIN w projekcie ASP.NET przy użyciu protokołu OpenID Connect. 

> Preferowane projektu Visual Studio tego przykładu toodownload zamiast niego? [Pobieranie projektu](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) i pominąć toohello [kroku konfiguracji](#create-an-application-express) przykładowy kod hello tooconfigure przed wykonaniem.

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a>Tworzenie projektu platformy ASP.NET

> 1. W programie Visual Studio:`File` > `New` > `Project`<br/>
> 2. W obszarze *Visual C# \Web*, wybierz pozycję `ASP.NET Web Application (.NET Framework)`.
> 3. Nazwa aplikacji, a następnie kliknij przycisk *OK*
> 4. Wybierz `Empty` i hello zaznacz pole wyboru tooadd `MVC` odwołania
<!--end-collapse-->

## <a name="add-authentication-components"></a>Dodaj składniki uwierzytelniania

1. W programie Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Dodaj *pakietów NuGet oprogramowanie pośredniczące OWIN* , wpisując następujące hello w oknie konsoli Menedżera pakietów hello:

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a>Te biblioteki — informacje

>Włącz powyższych bibliotek Hello rejestracji jednokrotnej (SSO) przy użyciu protokołu OpenID Connect przy użyciu uwierzytelniania opartego na pliku cookie. Po zakończeniu uwierzytelniania i token hello reprezentujący użytkownika hello jest wysyłany tooyour aplikacji, oprogramowanie pośredniczące OWIN tworzy plik cookie sesji. przeglądarki Hello następnie używa tego pliku cookie dla kolejnych żądań tak hello użytkownik nie musi tooretype swoje hasło i nie jest wymagane nie dodatkowej weryfikacji.
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a>Konfigurowanie procesu uwierzytelniania hello
Poniższe kroki Hello są używane toocreate uwierzytelniania OWIN oprogramowanie pośredniczące Klasa początkowa tooconfigure OpenID Connect. Ta klasa zostanie uruchomiony automatycznie po rozpoczęciu procesu programu IIS.

> Jeśli projekt nie ma `Startup.cs` pliku w folderze głównym hello:<br/>
> 1. Kliknij prawym przyciskiem myszy w folderze głównym projektu hello: >`Add` > `New Item...` > `OWIN Startup class`<br/>
> 2. Nadaj jej nazwę`Startup.cs`

> Upewnij się, wybranej klasy hello jest klasę początkową OWIN i nie C# klasa standardowa. To potwierdzić, sprawdzając występowanie `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` powyżej hello przestrzeni nazw.


1. Dodaj *OWIN* i *Microsoft.IdentityModel* odwołuje się do zbyt`Startup.cs`:

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Zastąp klasy początkowej hello poniższy kod:
</li>
</ol>

```csharp
public class Startup
{        
    // hello Client ID is used by hello application toouniquely identify itself tooAzure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is hello URL where hello user will be redirected tooafter they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is hello tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is hello URL for authority, composed by Azure Active Directory v2 endpoint and hello tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN toouse OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets hello ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is hello page that users will be redirected tooafter sign-out. In this case, it is using hello home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set toorequest hello id_token - which contains basic information about hello signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set toofalse tooallow personal and work accounts from any organization toosign in tooyour application
                // tooonly allow users from a single organizations, set ValidateIssuer tootrue and 'tenant' setting in web.config toohello tenant name
                // tooallow users from only a list of specific organizations, set ValidateIssuer tootrue and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN toosend notification of failed authentications tooOnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting hello user toohello home page with an error in hello query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a>Więcej informacji

> Witaj podane parametry *OpenIDConnectAuthenticationOptions* służyć jako współrzędne toocommunicate aplikacji hello z usługą Azure AD. Ponieważ oprogramowania pośredniczącego hello OpenID Connect używa plików cookie w tle hello, należy również tooset się uwierzytelniania plików cookie jako kod hello powyżej przedstawiono. Witaj *ValidateIssuer* wartość informuje OpenIdConnect toonot Ogranicz dostęp tooone określonej organizacji.
<!--end-collapse-->

