---
title: aaaAzure AD B2C | Dokumentacja firmy Microsoft
description: "Jak toobuild interfejsu API sieci Web platformy .NET przy użyciu usługi Azure Active Directory B2C zabezpieczonej przy użyciu tokenów dostępu protokołu OAuth 2.0 do uwierzytelniania."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="d6df7-103">Azure Active Directory B2C: tworzenie interfejsu API sieci Web platformy .NET</span><span class="sxs-lookup"><span data-stu-id="d6df7-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="d6df7-104">Usługa Azure Active Directory (Azure AD) B2C umożliwia zabezpieczanie interfejsu API sieci Web za pomocą tokenów dostępu protokołu OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d6df7-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="d6df7-105">Tokeny te Zezwalaj klienta toohello tooauthenticate aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d6df7-105">These tokens allow your client apps tooauthenticate toohello API.</span></span> <span data-ttu-id="d6df7-106">W tym artykule opisano, jak toocreate interfejs API programu .NET MVC "Lista zadań do wykonania" umożliwiająca użytkownikom klienta zadań tooCRUD aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d6df7-106">This article shows you how toocreate a .NET MVC "to-do list" API that allows users of your client application tooCRUD tasks.</span></span> <span data-ttu-id="d6df7-107">Interfejs API sieci web Hello jest zabezpieczone przy użyciu usługi Azure AD B2C i tylko umożliwia toomanage uwierzytelnionym użytkownikom ich listy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="d6df7-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="d6df7-108">Tworzenie katalogu usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d6df7-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="d6df7-109">Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.</span><span class="sxs-lookup"><span data-stu-id="d6df7-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="d6df7-110">Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów.</span><span class="sxs-lookup"><span data-stu-id="d6df7-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="d6df7-111">Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.</span><span class="sxs-lookup"><span data-stu-id="d6df7-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="d6df7-112">Aplikacja kliencka Hello i interfejs API sieci web muszą używać katalogu B2C hello tej samej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6df7-112">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="d6df7-113">Tworzenie interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="d6df7-113">Create a web API</span></span>

<span data-ttu-id="d6df7-114">Następnie należy toocreate aplikacji interfejsu API sieci web w katalogu usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="d6df7-114">Next, you need toocreate a web API app in your B2C directory.</span></span> <span data-ttu-id="d6df7-115">Dzięki temu informacje usługi Azure AD, czy go wymaga toosecurely komunikować się z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="d6df7-115">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="d6df7-116">toocreate usługi aplikacji, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="d6df7-116">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="d6df7-117">Należy pamiętać o wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="d6df7-117">Be sure to:</span></span>

* <span data-ttu-id="d6df7-118">Obejmują **aplikacji sieci web** lub **interfejs API sieci web** w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d6df7-118">Include a **web app** or **web API** in hello application.</span></span>
* <span data-ttu-id="d6df7-119">Użyj hello **identyfikator URI przekierowania** `https://localhost:44332/` hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d6df7-119">Use hello **Redirect URI** `https://localhost:44332/` for hello web app.</span></span> <span data-ttu-id="d6df7-120">To jest domyślna lokalizacja hello powitania klienta aplikacji sieci web dla tego przykładu kodu.</span><span class="sxs-lookup"><span data-stu-id="d6df7-120">This is hello default location of hello web app client for this code sample.</span></span>
* <span data-ttu-id="d6df7-121">Kopiuj hello **identyfikator aplikacji** czyli przypisanej tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d6df7-121">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="d6df7-122">Będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="d6df7-122">You'll need it later.</span></span>
* <span data-ttu-id="d6df7-123">Wprowadź identyfikator aplikacji do **identyfikatora URI aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="d6df7-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="d6df7-124">Należy dodać uprawnienia za pomocą hello **opublikowane zakresy** menu.</span><span class="sxs-lookup"><span data-stu-id="d6df7-124">Add permissions through hello **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="d6df7-125">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="d6df7-125">Create your policies</span></span>

<span data-ttu-id="d6df7-126">W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d6df7-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d6df7-127">Konieczne będzie toocreate toocommunicate zasad w usłudze Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d6df7-127">You will need toocreate a policy toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="d6df7-128">Zaleca się przy użyciu hello połączone konta-konta/zasad logowania, zgodnie z opisem w hello [artykule o zasadach](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d6df7-128">We recommend using hello combined sign-up/sign-in policy, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d6df7-129">Podczas tworzenia zasad należy pamiętać, aby:</span><span class="sxs-lookup"><span data-stu-id="d6df7-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="d6df7-130">Wybrać wartość **Nazwa wyświetlana** i inne atrybuty tworzenia konta w zasadach.</span><span class="sxs-lookup"><span data-stu-id="d6df7-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="d6df7-131">Wybrać oświadczenia **Nazwa wyświetlana** i **Identyfikator obiektu** jako oświadczenia aplikacji dla wszystkich zasad.</span><span class="sxs-lookup"><span data-stu-id="d6df7-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="d6df7-132">Można również wybrać inne oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="d6df7-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="d6df7-133">Kopiuj hello **nazwa** poszczególnych zasad po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="d6df7-133">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="d6df7-134">Nazwa zasad hello będą potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="d6df7-134">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="d6df7-135">Po pomyślnym utworzeniu zasad hello wszystko jest gotowe toobuild aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d6df7-135">After you have successfully created hello policy, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="d6df7-136">Pobierz kod hello</span><span class="sxs-lookup"><span data-stu-id="d6df7-136">Download hello code</span></span>

<span data-ttu-id="d6df7-137">Witaj kod dla tego samouczka jest przechowywany w [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="d6df7-137">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="d6df7-138">Przykład Witaj można sklonować, uruchamiając:</span><span class="sxs-lookup"><span data-stu-id="d6df7-138">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="d6df7-139">Po pobraniu hello przykładowy kod tooget plik SLN programu Visual Studio Otwórz hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="d6df7-139">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="d6df7-140">Witaj plik rozwiązania zawiera dwa projekty: `TaskWebApp` i `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="d6df7-140">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="d6df7-141">`TaskWebApp`to aplikacja sieci web MVC, która hello użytkownika współdziała z.</span><span class="sxs-lookup"><span data-stu-id="d6df7-141">`TaskWebApp` is an MVC web application that hello user interacts with.</span></span> <span data-ttu-id="d6df7-142">`TaskService`to interfejs API sieci web zaplecza aplikacji hello, który przechowuje listy zadań do wykonania poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d6df7-142">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="d6df7-143">W tym artykule przedstawimy tylko hello `TaskService` aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d6df7-143">This article will only discuss hello `TaskService` application.</span></span> <span data-ttu-id="d6df7-144">toolearn jak toobuild `TaskWebApp` za pomocą usługi Azure AD B2C, zobacz [naszym samouczku aplikacji sieci web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="d6df7-144">toolearn how toobuild `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="d6df7-145">Zaktualizuj konfigurację hello Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d6df7-145">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="d6df7-146">Naszej próbki jest skonfigurowany toouse hello zasady i klienta identyfikator dzierżawy naszych pokaz.</span><span class="sxs-lookup"><span data-stu-id="d6df7-146">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="d6df7-147">Jeśli chcesz toouse własną dzierżawę, konieczne będzie hello toodo następujące:</span><span class="sxs-lookup"><span data-stu-id="d6df7-147">If you would like toouse your own tenant, you will need toodo hello following:</span></span>

1. <span data-ttu-id="d6df7-148">Otwórz `web.config` w hello `TaskService` projektu i Zastąp wartości hello</span><span class="sxs-lookup"><span data-stu-id="d6df7-148">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>
    * <span data-ttu-id="d6df7-149">`ida:Tenant` nazwą dzierżawy</span><span class="sxs-lookup"><span data-stu-id="d6df7-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="d6df7-150">`ida:ClientId` identyfikatorem aplikacji interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="d6df7-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="d6df7-151">`ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania</span><span class="sxs-lookup"><span data-stu-id="d6df7-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="d6df7-152">Otwórz `web.config` w hello `TaskWebApp` projektu i Zastąp wartości hello</span><span class="sxs-lookup"><span data-stu-id="d6df7-152">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>
    * <span data-ttu-id="d6df7-153">`ida:Tenant` nazwą dzierżawy</span><span class="sxs-lookup"><span data-stu-id="d6df7-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="d6df7-154">`ida:ClientId` identyfikatorem aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="d6df7-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="d6df7-155">`ida:ClientSecret` kluczem tajnym aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="d6df7-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="d6df7-156">`ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania</span><span class="sxs-lookup"><span data-stu-id="d6df7-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="d6df7-157">`ida:EditProfilePolicyId` nazwą zasady edycji profilu</span><span class="sxs-lookup"><span data-stu-id="d6df7-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="d6df7-158">`ida:ResetPasswordPolicyId` nazwą zasady resetowania hasła</span><span class="sxs-lookup"><span data-stu-id="d6df7-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-hello-api"></a><span data-ttu-id="d6df7-159">Zabezpiecz interfejs API hello</span><span class="sxs-lookup"><span data-stu-id="d6df7-159">Secure hello API</span></span>

<span data-ttu-id="d6df7-160">Jeśli klient wywołuje interfejs API, należy zabezpieczyć interfejs API (np. `TaskService`) za pomocą tokenów elementu nośnego OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d6df7-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="d6df7-161">Dzięki temu API tooyour każdego żądania będą tylko ważne, jeśli Żądanie hello ma token elementu nośnego.</span><span class="sxs-lookup"><span data-stu-id="d6df7-161">This ensures that each request tooyour API will only be valid if hello request has a bearer token.</span></span> <span data-ttu-id="d6df7-162">Interfejs API może akceptować i weryfikować tokeny elementu nośnego przy użyciu biblioteki interfejsu OWIN (Open Web Interface for .NET) firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d6df7-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="d6df7-163">Instalowanie interfejsu OWIN</span><span class="sxs-lookup"><span data-stu-id="d6df7-163">Install OWIN</span></span>

<span data-ttu-id="d6df7-164">Rozpocznij od zainstalowania potoku uwierzytelniania OAuth interfejsu OWIN hello przy użyciu hello Konsola Menedżera pakietów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6df7-164">Begin by installing hello OWIN OAuth authentication pipeline by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="d6df7-165">Spowoduje to zainstalowanie oprogramowania pośredniczącego OWIN hello, który będzie akceptować i sprawdzania poprawności tokenów elementu nośnego.</span><span class="sxs-lookup"><span data-stu-id="d6df7-165">This will install hello OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="d6df7-166">Dodawanie klasy początkowej OWIN</span><span class="sxs-lookup"><span data-stu-id="d6df7-166">Add an OWIN startup class</span></span>

<span data-ttu-id="d6df7-167">Dodaj toohello klasy interfejsu API OWIN uruchamiania o nazwie `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="d6df7-167">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="d6df7-168">Kliknij prawym przyciskiem myszy na powitania projektu, zaznacz **Dodaj** i **nowy element**, a następnie wyszukaj interfejs OWIN.</span><span class="sxs-lookup"><span data-stu-id="d6df7-168">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="d6df7-169">oprogramowanie pośredniczące OWIN Hello wywoła hello `Configuration(…)` metody podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d6df7-169">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="d6df7-170">W naszym przykładzie możemy zmienić deklaracji klasy hello zbyt`public partial class Startup` i implementowane hello drugiej klasy hello w `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="d6df7-170">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="d6df7-171">Witaj wewnątrz `Configuration` metody dodaliśmy wywołanie za`ConfigureAuth`, który jest zdefiniowany w `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="d6df7-171">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="d6df7-172">Po modyfikacji hello `Startup.cs` wygląda jak poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="d6df7-172">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="d6df7-173">Konfigurowanie uwierzytelniania OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="d6df7-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="d6df7-174">Witaj Otwórz plik `App_Start\Startup.Auth.cs`i wdrożenie hello `ConfigureAuth(...)` metody.</span><span class="sxs-lookup"><span data-stu-id="d6df7-174">Open hello file `App_Start\Startup.Auth.cs`, and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="d6df7-175">Na przykład może wyglądać podobnie jak poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="d6df7-175">For example, it could look like hello following:</span></span>

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a><span data-ttu-id="d6df7-176">Zabezpieczanie kontrolera zadań hello</span><span class="sxs-lookup"><span data-stu-id="d6df7-176">Secure hello task controller</span></span>

<span data-ttu-id="d6df7-177">Po aplikacji hello jest uwierzytelnianie skonfigurowanego toouse OAuth 2.0, można zabezpieczyć interfejs API sieci web, dodając `[Authorize]` kontrolera zadań toohello tagu.</span><span class="sxs-lookup"><span data-stu-id="d6df7-177">After hello app is configured toouse OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag toohello task controller.</span></span> <span data-ttu-id="d6df7-178">Jest to kontroler hello, jeśli wszystkie operacje edytowania listy zadań do wykonania ma miejsce, dlatego należy zabezpieczyć cały kontroler hello na poziomie klasy hello.</span><span class="sxs-lookup"><span data-stu-id="d6df7-178">This is hello controller where all to-do list manipulation takes place, so you should secure hello entire controller at hello class level.</span></span> <span data-ttu-id="d6df7-179">Możesz także dodać hello `[Authorize]` tagu tooindividual akcji dla bardziej szczegółową kontrolę.</span><span class="sxs-lookup"><span data-stu-id="d6df7-179">You can also add hello `[Authorize]` tag tooindividual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a><span data-ttu-id="d6df7-180">Uzyskiwanie informacji o użytkowniku z hello tokenu</span><span class="sxs-lookup"><span data-stu-id="d6df7-180">Get user information from hello token</span></span>

<span data-ttu-id="d6df7-181">`TasksController`przechowuje zadania w bazie danych, gdzie każde zadanie ma skojarzony użytkownik będący jego "właścicielem" hello zadań.</span><span class="sxs-lookup"><span data-stu-id="d6df7-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" hello task.</span></span> <span data-ttu-id="d6df7-182">Witaj właściciel jest identyfikowany przez użytkownika hello **obiekt o identyfikatorze**.</span><span class="sxs-lookup"><span data-stu-id="d6df7-182">hello owner is identified by hello user's **object ID**.</span></span> <span data-ttu-id="d6df7-183">(Dlatego potrzebne identyfikator obiektu hello tooadd jako aplikacji we wszystkich zasadach.)</span><span class="sxs-lookup"><span data-stu-id="d6df7-183">(This is why you needed tooadd hello object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a><span data-ttu-id="d6df7-184">Sprawdź poprawność uprawnień hello w tokenie hello</span><span class="sxs-lookup"><span data-stu-id="d6df7-184">Validate hello permissions in hello token</span></span>

<span data-ttu-id="d6df7-185">Typowe wymagania dotyczące interfejsów API sieci web jest hello toovalidate "zakresy" występuje w tokenie hello.</span><span class="sxs-lookup"><span data-stu-id="d6df7-185">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="d6df7-186">Dzięki temu użytkownik hello zgodził usługi listy zadań do wykonania hello toohello uprawnienia wymagane tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d6df7-186">This ensures that hello user has consented toohello permissions required tooaccess hello to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="d6df7-187">Uruchom hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="d6df7-187">Run hello sample app</span></span>

<span data-ttu-id="d6df7-188">Na koniec skompiluj i uruchom oba projekty: `TaskWebApp` i `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="d6df7-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="d6df7-189">Utwórz kilka zadań na liście zadań do wykonania hello użytkownika i zwróć uwagę, jak są zachowywane w hello interfejsu API nawet po Zatrzymaj i uruchom ponownie powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="d6df7-189">Create some tasks on hello user's to-do list and notice how they are persisted in hello API even after you stop and restart hello client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="d6df7-190">Edytowanie zasad</span><span class="sxs-lookup"><span data-stu-id="d6df7-190">Edit your policies</span></span>

<span data-ttu-id="d6df7-191">Po zabezpieczeniu interfejsu API za pomocą usługi Azure AD B2C możesz eksperymentować z zasad logowania — w/tworzenia konta i widoku hello skutki (lub ich brak) na powitania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d6df7-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view hello effects (or lack thereof) on hello API.</span></span> <span data-ttu-id="d6df7-192">Można manipulować oświadczeniami aplikacji hello w hello zasad i zmienić informacje o użytkowniku hello dostępnym w hello interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="d6df7-192">You can manipulate hello application claims in hello policies and change hello user information that is available in hello web API.</span></span> <span data-ttu-id="d6df7-193">Wszelkie oświadczenia, które można dodać będą dostępne tooyour interfejsu API sieci web .NET MVC w hello `ClaimsPrincipal` obiektu, zgodnie z opisem we wcześniejszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6df7-193">Any claims that you add will be available tooyour .NET MVC web API in hello `ClaimsPrincipal` object, as described earlier in this article.</span></span>
