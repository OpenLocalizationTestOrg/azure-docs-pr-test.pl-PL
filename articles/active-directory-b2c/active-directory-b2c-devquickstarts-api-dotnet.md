---
title: "Usługa Azure AD B2C | Microsoft Docs"
description: "Jak utworzyć interfejs API sieci Web programu .NET przy użyciu usługi Azure Active Directory B2C zabezpieczonej przy użyciu tokenów dostępu protokołu OAuth 2.0 na potrzeby uwierzytelniania."
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
ms.openlocfilehash: 48749bfa2ab54a0e766a4aad4f39073cc4e90818
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="94052-103">Azure Active Directory B2C: tworzenie interfejsu API sieci Web platformy .NET</span><span class="sxs-lookup"><span data-stu-id="94052-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="94052-104">Usługa Azure Active Directory (Azure AD) B2C umożliwia zabezpieczanie interfejsu API sieci Web za pomocą tokenów dostępu protokołu OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="94052-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="94052-105">Tokeny te służą aplikacjom klienckim do uwierzytelniania w obrębie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="94052-105">These tokens allow your client apps to authenticate to the API.</span></span> <span data-ttu-id="94052-106">W tym artykule pokazano, jak utworzyć interfejs API „lista zadań do wykonania” kontrolera MVC platformy .NET umożliwiający użytkownikom aplikacji klienckiej wykonywanie zadań CRUD.</span><span class="sxs-lookup"><span data-stu-id="94052-106">This article shows you how to create a .NET MVC "to-do list" API that allows users of your client application to CRUD tasks.</span></span> <span data-ttu-id="94052-107">Interfejs API sieci Web jest zabezpieczony za pomocą usługi Azure AD B2C i zezwala na zarządzanie listami zadań do wykonania tylko uwierzytelnionym użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="94052-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="94052-108">Tworzenie katalogu usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="94052-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="94052-109">Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.</span><span class="sxs-lookup"><span data-stu-id="94052-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="94052-110">Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów.</span><span class="sxs-lookup"><span data-stu-id="94052-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="94052-111">Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.</span><span class="sxs-lookup"><span data-stu-id="94052-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="94052-112">Aplikacja kliencka i interfejs API sieci Web muszą korzystać z tego samego katalogu usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="94052-112">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="94052-113">Tworzenie interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="94052-113">Create a web API</span></span>

<span data-ttu-id="94052-114">Następnie musisz utworzyć aplikację interfejsu API sieci Web w katalogu usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="94052-114">Next, you need to create a web API app in your B2C directory.</span></span> <span data-ttu-id="94052-115">Dzięki temu informacje wymagane do bezpiecznego komunikowania się z aplikacją będą przekazywane do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="94052-115">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="94052-116">Aby utworzyć aplikację, postępuj zgodnie z [tymi instrukcjami](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="94052-116">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="94052-117">Należy pamiętać o wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="94052-117">Be sure to:</span></span>

* <span data-ttu-id="94052-118">Uwzględnij **aplikację sieci Web** lub **interfejs API sieci Web** w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94052-118">Include a **web app** or **web API** in the application.</span></span>
* <span data-ttu-id="94052-119">Użyj **identyfikatora URI przekierowania** `https://localhost:44332/` dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="94052-119">Use the **Redirect URI** `https://localhost:44332/` for the web app.</span></span> <span data-ttu-id="94052-120">Jest to domyślna lokalizacja klienta aplikacji sieci Web dla tego przykładu kodu.</span><span class="sxs-lookup"><span data-stu-id="94052-120">This is the default location of the web app client for this code sample.</span></span>
* <span data-ttu-id="94052-121">Skopiuj **Identyfikator aplikacji** przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94052-121">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="94052-122">Będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="94052-122">You'll need it later.</span></span>
* <span data-ttu-id="94052-123">Wprowadź identyfikator aplikacji do **identyfikatora URI aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="94052-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="94052-124">Dodaj uprawnienia za pomocą menu **Opublikowane zakresy**.</span><span class="sxs-lookup"><span data-stu-id="94052-124">Add permissions through the **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="94052-125">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="94052-125">Create your policies</span></span>

<span data-ttu-id="94052-126">W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="94052-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="94052-127">Należy utworzyć zasady komunikacji z usługą Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="94052-127">You will need to create a policy to communicate with Azure AD B2C.</span></span> <span data-ttu-id="94052-128">Zaleca się używanie połączonych zasad tworzenia/logowania, zgodnie z opisem w [artykule Informacje ogólne o zasadach](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="94052-128">We recommend using the combined sign-up/sign-in policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="94052-129">Podczas tworzenia zasad należy pamiętać, aby:</span><span class="sxs-lookup"><span data-stu-id="94052-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="94052-130">Wybrać wartość **Nazwa wyświetlana** i inne atrybuty tworzenia konta w zasadach.</span><span class="sxs-lookup"><span data-stu-id="94052-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="94052-131">Wybrać oświadczenia **Nazwa wyświetlana** i **Identyfikator obiektu** jako oświadczenia aplikacji dla wszystkich zasad.</span><span class="sxs-lookup"><span data-stu-id="94052-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="94052-132">Można również wybrać inne oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="94052-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="94052-133">Skopiować każdą utworzoną wartość **Nazwa** zasad.</span><span class="sxs-lookup"><span data-stu-id="94052-133">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="94052-134">Nazwa zasad będzie potrzebna później.</span><span class="sxs-lookup"><span data-stu-id="94052-134">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="94052-135">Po pomyślnym utworzeniu zasad możesz rozpocząć tworzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94052-135">After you have successfully created the policy, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="94052-136">Pobieranie kodu</span><span class="sxs-lookup"><span data-stu-id="94052-136">Download the code</span></span>

<span data-ttu-id="94052-137">Kod używany w tym samouczku [jest przechowywany w serwisie GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="94052-137">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="94052-138">Przykład można sklonować, uruchamiając polecenie:</span><span class="sxs-lookup"><span data-stu-id="94052-138">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="94052-139">Po pobraniu przykładu kodu otwórz plik SLN programu Visual Studio, aby rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="94052-139">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="94052-140">Plik rozwiązania zawiera dwa projekty: `TaskWebApp` i `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="94052-140">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="94052-141">`TaskWebApp` to aplikacja sieci Web z architekturą MVC, z której korzysta użytkownik.</span><span class="sxs-lookup"><span data-stu-id="94052-141">`TaskWebApp` is an MVC web application that the user interacts with.</span></span> <span data-ttu-id="94052-142">`TaskService` to interfejs API zaplecza aplikacji, który przechowuje listy zadań do wykonania poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="94052-142">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="94052-143">Ten artykuł zawiera jedynie omówienie aplikacji `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="94052-143">This article will only discuss the `TaskService` application.</span></span> <span data-ttu-id="94052-144">Aby dowiedzieć się, jak utworzyć `TaskWebApp`, używając usługi Azure AD B2C, zobacz nasz [samouczek dotyczący aplikacji sieci Web platformy .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="94052-144">To learn how to build `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="94052-145">Aktualizowanie konfiguracji usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="94052-145">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="94052-146">Nasz przykład został skonfigurowany do używania zasad i identyfikatora klienta dzierżawy pokazowej.</span><span class="sxs-lookup"><span data-stu-id="94052-146">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="94052-147">Jeśli chcesz użyć własnej dzierżawy, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="94052-147">If you would like to use your own tenant, you will need to do the following:</span></span>

1. <span data-ttu-id="94052-148">Otwórz plik `web.config` w projekcie `TaskService` i zastąp wartości</span><span class="sxs-lookup"><span data-stu-id="94052-148">Open `web.config` in the `TaskService` project and replace the values for</span></span>
    * <span data-ttu-id="94052-149">`ida:Tenant` nazwą dzierżawy</span><span class="sxs-lookup"><span data-stu-id="94052-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="94052-150">`ida:ClientId` identyfikatorem aplikacji interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="94052-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="94052-151">`ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania</span><span class="sxs-lookup"><span data-stu-id="94052-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="94052-152">Otwórz plik `web.config` w projekcie `TaskWebApp` i zastąp wartości</span><span class="sxs-lookup"><span data-stu-id="94052-152">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>
    * <span data-ttu-id="94052-153">`ida:Tenant` nazwą dzierżawy</span><span class="sxs-lookup"><span data-stu-id="94052-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="94052-154">`ida:ClientId` identyfikatorem aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="94052-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="94052-155">`ida:ClientSecret` kluczem tajnym aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="94052-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="94052-156">`ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania</span><span class="sxs-lookup"><span data-stu-id="94052-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="94052-157">`ida:EditProfilePolicyId` nazwą zasady edycji profilu</span><span class="sxs-lookup"><span data-stu-id="94052-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="94052-158">`ida:ResetPasswordPolicyId` nazwą zasady resetowania hasła</span><span class="sxs-lookup"><span data-stu-id="94052-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-the-api"></a><span data-ttu-id="94052-159">Zabezpieczanie interfejsu API</span><span class="sxs-lookup"><span data-stu-id="94052-159">Secure the API</span></span>

<span data-ttu-id="94052-160">Jeśli klient wywołuje interfejs API, należy zabezpieczyć interfejs API (np. `TaskService`) za pomocą tokenów elementu nośnego OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="94052-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="94052-161">Dzięki temu każde żądanie dotyczące interfejsu API będzie poprawne, tylko jeśli zawiera token elementu nośnego.</span><span class="sxs-lookup"><span data-stu-id="94052-161">This ensures that each request to your API will only be valid if the request has a bearer token.</span></span> <span data-ttu-id="94052-162">Interfejs API może akceptować i weryfikować tokeny elementu nośnego przy użyciu biblioteki interfejsu OWIN (Open Web Interface for .NET) firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="94052-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="94052-163">Instalowanie interfejsu OWIN</span><span class="sxs-lookup"><span data-stu-id="94052-163">Install OWIN</span></span>

<span data-ttu-id="94052-164">Rozpocznij od zainstalowania potoku uwierzytelniania OWIN OAuth przy użyciu konsoli Menedżera pakietów Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="94052-164">Begin by installing the OWIN OAuth authentication pipeline by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="94052-165">Spowoduje to zainstalowanie oprogramowania pośredniczącego OWIN, które będzie akceptować i sprawdzać poprawność tokenów elementu nośnego.</span><span class="sxs-lookup"><span data-stu-id="94052-165">This will install the OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="94052-166">Dodawanie klasy początkowej OWIN</span><span class="sxs-lookup"><span data-stu-id="94052-166">Add an OWIN startup class</span></span>

<span data-ttu-id="94052-167">Dodaj klasę początkową OWIN do interfejsu API o nazwie `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="94052-167">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="94052-168">Kliknij projekt prawym przyciskiem myszy, wybierz kolejno pozycje **Dodaj** i **Nowy element**, a następnie wyszukaj interfejs OWIN.</span><span class="sxs-lookup"><span data-stu-id="94052-168">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="94052-169">Oprogramowanie pośredniczące OWIN wywoła metodę `Configuration(…)` podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94052-169">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="94052-170">W naszym przykładzie zmieniliśmy deklarację klasy na `public partial class Startup` i wdrożyliśmy drugą część klasy w `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="94052-170">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="94052-171">Wewnątrz metody `Configuration` dodaliśmy wywołanie `ConfigureAuth`, które jest zdefiniowane w `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="94052-171">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="94052-172">Po modyfikacji `Startup.cs` wygląda podobnie do następujących:</span><span class="sxs-lookup"><span data-stu-id="94052-172">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="94052-173">Konfigurowanie uwierzytelniania OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="94052-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="94052-174">Otwórz plik `App_Start\Startup.Auth.cs` i zaimplementuj metodę `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="94052-174">Open the file `App_Start\Startup.Auth.cs`, and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="94052-175">Na przykład może ona wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="94052-175">For example, it could look like the following:</span></span>

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
         * Configure the authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where the audience of the token is equal to the client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches the Azure AD B2C metadata & signing keys from the OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-the-task-controller"></a><span data-ttu-id="94052-176">Zabezpieczanie kontrolera zadań</span><span class="sxs-lookup"><span data-stu-id="94052-176">Secure the task controller</span></span>

<span data-ttu-id="94052-177">Po skonfigurowaniu aplikacji do używania uwierzytelniania OAuth 2.0 możesz zabezpieczyć interfejs API sieci Web, dodając tag `[Authorize]` do kontrolera zadań.</span><span class="sxs-lookup"><span data-stu-id="94052-177">After the app is configured to use OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag to the task controller.</span></span> <span data-ttu-id="94052-178">Jest to kontroler, w obrębie którego odbywają się wszystkie operacje edytowania listy zadań do wykonania, dlatego należy zabezpieczyć cały kontroler na poziomie klasy.</span><span class="sxs-lookup"><span data-stu-id="94052-178">This is the controller where all to-do list manipulation takes place, so you should secure the entire controller at the class level.</span></span> <span data-ttu-id="94052-179">Można również dodać tag `[Authorize]` do poszczególnych czynności w celu uzyskania ściślejszej kontroli.</span><span class="sxs-lookup"><span data-stu-id="94052-179">You can also add the `[Authorize]` tag to individual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-the-token"></a><span data-ttu-id="94052-180">Uzyskiwanie informacji o użytkowniku z tokenu</span><span class="sxs-lookup"><span data-stu-id="94052-180">Get user information from the token</span></span>

<span data-ttu-id="94052-181">`TasksController` przechowuje zadania w bazie danych. Z każdym zadaniem jest skojarzony użytkownik będący jego „właścicielem”.</span><span class="sxs-lookup"><span data-stu-id="94052-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" the task.</span></span> <span data-ttu-id="94052-182">Właściciel jest identyfikowany za pomocą **identyfikatora obiektu** użytkownika.</span><span class="sxs-lookup"><span data-stu-id="94052-182">The owner is identified by the user's **object ID**.</span></span> <span data-ttu-id="94052-183">(Dlatego trzeba było dodać identyfikator obiektu jako oświadczenie aplikacji we wszystkich zasadach).</span><span class="sxs-lookup"><span data-stu-id="94052-183">(This is why you needed to add the object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-the-permissions-in-the-token"></a><span data-ttu-id="94052-184">Weryfikowanie uprawnień w tokenie</span><span class="sxs-lookup"><span data-stu-id="94052-184">Validate the permissions in the token</span></span>

<span data-ttu-id="94052-185">Typowym wymogiem dla interfejsów API sieci Web jest weryfikacja „zakresów” występujących w tokenie.</span><span class="sxs-lookup"><span data-stu-id="94052-185">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="94052-186">Daje to gwarancję, że użytkownik wyraził zgodę na uprawnienia wymagane do uzyskania dostępu do usługi listy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="94052-186">This ensures that the user has consented to the permissions required to access the to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "The Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="94052-187">Uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="94052-187">Run the sample app</span></span>

<span data-ttu-id="94052-188">Na koniec skompiluj i uruchom oba projekty: `TaskWebApp` i `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="94052-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="94052-189">Utwórz kilka zadań na liście użytkownika i zwróć uwagę na to, że zostają one zachowane w interfejsie API nawet po zatrzymaniu i ponownym uruchomieniu klienta.</span><span class="sxs-lookup"><span data-stu-id="94052-189">Create some tasks on the user's to-do list and notice how they are persisted in the API even after you stop and restart the client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="94052-190">Edytowanie zasad</span><span class="sxs-lookup"><span data-stu-id="94052-190">Edit your policies</span></span>

<span data-ttu-id="94052-191">Po zabezpieczeniu interfejsu API za pomocą usługi Azure AD B2C możesz eksperymentować z zasadą tworzenia konta/logowania i sprawdzać skutki (lub ich brak) powiązane z interfejsem API.</span><span class="sxs-lookup"><span data-stu-id="94052-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view the effects (or lack thereof) on the API.</span></span> <span data-ttu-id="94052-192">Możesz manipulować oświadczeniami aplikacji w zasadach i zmieniać informacje o użytkowniku dostępne w interfejsie API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="94052-192">You can manipulate the application claims in the policies and change the user information that is available in the web API.</span></span> <span data-ttu-id="94052-193">Wszystkie dodane oświadczenia będą dostępne dla interfejsu API sieci Web w architekturze MVC programu .NET w obiekcie `ClaimsPrincipal`, zgodnie z opisem we wcześniejszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="94052-193">Any claims that you add will be available to your .NET MVC web API in the `ClaimsPrincipal` object, as described earlier in this article.</span></span>
