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
## <a name="set-up-your-project"></a><span data-ttu-id="91d80-103">Konfigurowanie projektu</span><span class="sxs-lookup"><span data-stu-id="91d80-103">Set up your project</span></span>

<span data-ttu-id="91d80-104">W tej sekcji przedstawiono hello kroki tooinstall i konfiguruje potok uwierzytelniania hello za pomocą oprogramowania pośredniczącego OWIN w projekcie ASP.NET przy użyciu protokołu OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="91d80-104">This section shows hello steps tooinstall and configure hello authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span></span> 

> <span data-ttu-id="91d80-105">Preferowane projektu Visual Studio tego przykładu toodownload zamiast niego?</span><span class="sxs-lookup"><span data-stu-id="91d80-105">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="91d80-106">[Pobieranie projektu](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) i pominąć toohello [kroku konfiguracji](#create-an-application-express) przykładowy kod hello tooconfigure przed wykonaniem.</span><span class="sxs-lookup"><span data-stu-id="91d80-106">[Download a project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a><span data-ttu-id="91d80-107">Tworzenie projektu platformy ASP.NET</span><span class="sxs-lookup"><span data-stu-id="91d80-107">Create your ASP.NET project</span></span>

> 1. <span data-ttu-id="91d80-108">W programie Visual Studio:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="91d80-108">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
> 2. <span data-ttu-id="91d80-109">W obszarze *Visual C# \Web*, wybierz pozycję `ASP.NET Web Application (.NET Framework)`.</span><span class="sxs-lookup"><span data-stu-id="91d80-109">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span></span>
> 3. <span data-ttu-id="91d80-110">Nazwa aplikacji, a następnie kliknij przycisk *OK*</span><span class="sxs-lookup"><span data-stu-id="91d80-110">Name your application and click *OK*</span></span>
> 4. <span data-ttu-id="91d80-111">Wybierz `Empty` i hello zaznacz pole wyboru tooadd `MVC` odwołania</span><span class="sxs-lookup"><span data-stu-id="91d80-111">Select `Empty` and select hello checkbox tooadd `MVC` references</span></span>
<!--end-collapse-->

## <a name="add-authentication-components"></a><span data-ttu-id="91d80-112">Dodaj składniki uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="91d80-112">Add authentication components</span></span>

1. <span data-ttu-id="91d80-113">W programie Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="91d80-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="91d80-114">Dodaj *pakietów NuGet oprogramowanie pośredniczące OWIN* , wpisując następujące hello w oknie konsoli Menedżera pakietów hello:</span><span class="sxs-lookup"><span data-stu-id="91d80-114">Add *OWIN middleware NuGet packages* by typing hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a><span data-ttu-id="91d80-115">Te biblioteki — informacje</span><span class="sxs-lookup"><span data-stu-id="91d80-115">About these libraries</span></span>

><span data-ttu-id="91d80-116">Włącz powyższych bibliotek Hello rejestracji jednokrotnej (SSO) przy użyciu protokołu OpenID Connect przy użyciu uwierzytelniania opartego na pliku cookie.</span><span class="sxs-lookup"><span data-stu-id="91d80-116">hello libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span></span> <span data-ttu-id="91d80-117">Po zakończeniu uwierzytelniania i token hello reprezentujący użytkownika hello jest wysyłany tooyour aplikacji, oprogramowanie pośredniczące OWIN tworzy plik cookie sesji.</span><span class="sxs-lookup"><span data-stu-id="91d80-117">After authentication is completed and hello token representing hello user is sent tooyour application, OWIN middleware creates a session cookie.</span></span> <span data-ttu-id="91d80-118">przeglądarki Hello następnie używa tego pliku cookie dla kolejnych żądań tak hello użytkownik nie musi tooretype swoje hasło i nie jest wymagane nie dodatkowej weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="91d80-118">hello browser then uses this cookie on subsequent requests so hello user doesn't need tooretype their password, and no additional verification is needed.</span></span>
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a><span data-ttu-id="91d80-119">Konfigurowanie procesu uwierzytelniania hello</span><span class="sxs-lookup"><span data-stu-id="91d80-119">Configure hello authentication pipeline</span></span>
<span data-ttu-id="91d80-120">Poniższe kroki Hello są używane toocreate uwierzytelniania OWIN oprogramowanie pośredniczące Klasa początkowa tooconfigure OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="91d80-120">hello steps below are used toocreate an OWIN middleware Startup Class tooconfigure OpenID Connect authentication.</span></span> <span data-ttu-id="91d80-121">Ta klasa zostanie uruchomiony automatycznie po rozpoczęciu procesu programu IIS.</span><span class="sxs-lookup"><span data-stu-id="91d80-121">This class will be executed automatically when your IIS process starts.</span></span>

> <span data-ttu-id="91d80-122">Jeśli projekt nie ma `Startup.cs` pliku w folderze głównym hello:</span><span class="sxs-lookup"><span data-stu-id="91d80-122">If your project doesn't have a `Startup.cs` file in hello root folder:</span></span><br/>
> 1. <span data-ttu-id="91d80-123">Kliknij prawym przyciskiem myszy w folderze głównym projektu hello: >`Add` > `New Item...` > `OWIN Startup class`</span><span class="sxs-lookup"><span data-stu-id="91d80-123">Right click on hello project's root folder: >  `Add` > `New Item...` > `OWIN Startup class`</span></span><br/>
> 2. <span data-ttu-id="91d80-124">Nadaj jej nazwę`Startup.cs`</span><span class="sxs-lookup"><span data-stu-id="91d80-124">Name it `Startup.cs`</span></span>

> <span data-ttu-id="91d80-125">Upewnij się, wybranej klasy hello jest klasę początkową OWIN i nie C# klasa standardowa.</span><span class="sxs-lookup"><span data-stu-id="91d80-125">Make sure hello class selected is an OWIN Startup Class and not a standard C# class.</span></span> <span data-ttu-id="91d80-126">To potwierdzić, sprawdzając występowanie `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` powyżej hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="91d80-126">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above hello namespace.</span></span>


1. <span data-ttu-id="91d80-127">Dodaj *OWIN* i *Microsoft.IdentityModel* odwołuje się do zbyt`Startup.cs`:</span><span class="sxs-lookup"><span data-stu-id="91d80-127">Add *OWIN* and *Microsoft.IdentityModel* references too`Startup.cs`:</span></span>

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
<span data-ttu-id="91d80-128">Zastąp klasy początkowej hello poniższy kod:</span><span class="sxs-lookup"><span data-stu-id="91d80-128">Replace Startup class with hello code below:</span></span>
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
> ### <a name="more-information"></a><span data-ttu-id="91d80-129">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="91d80-129">More Information</span></span>

> <span data-ttu-id="91d80-130">Witaj podane parametry *OpenIDConnectAuthenticationOptions* służyć jako współrzędne toocommunicate aplikacji hello z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91d80-130">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello application toocommunicate with Azure AD.</span></span> <span data-ttu-id="91d80-131">Ponieważ oprogramowania pośredniczącego hello OpenID Connect używa plików cookie w tle hello, należy również tooset się uwierzytelniania plików cookie jako kod hello powyżej przedstawiono.</span><span class="sxs-lookup"><span data-stu-id="91d80-131">Because hello OpenID Connect middleware uses cookies in hello background, you also need tooset up cookie authentication as hello code above shows.</span></span> <span data-ttu-id="91d80-132">Witaj *ValidateIssuer* wartość informuje OpenIdConnect toonot Ogranicz dostęp tooone określonej organizacji.</span><span class="sxs-lookup"><span data-stu-id="91d80-132">hello *ValidateIssuer* value tells OpenIdConnect toonot restrict access tooone specific organization.</span></span>
<!--end-collapse-->

