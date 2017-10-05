---
title: "Dodaj logowania do sieci web .NET MVC interfejsu API przy użyciu punktu końcowego v2.0 usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Jak utworzyć interfejs Api sieci Web .NET MVC, który akceptuje tokeny od obu Account firmy Microsoft i konta firmowego lub szkolnego."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: b2d7bbfcd9218698f71e9dfdb1ad5d9ff8740f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="afb29-103">Zabezpiecz interfejs API web MVC</span><span class="sxs-lookup"><span data-stu-id="afb29-103">Secure an MVC web API</span></span>
<span data-ttu-id="afb29-104">Z usługą Azure Active Directory punktu końcowego v2.0, można chronić przy użyciu interfejsu API sieci Web [OAuth 2.0](active-directory-v2-protocols.md) dostęp do tokenów, umożliwiając użytkownikom z obu osobistego konta Microsoft i służbowego konta do bezpiecznego dostępu do interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="afb29-104">With Azure Active Directory the v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts to securely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="afb29-105">Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="afb29-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="afb29-106">Aby ustalić, czy należy używać punktu końcowego v2.0, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="afb29-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="afb29-107">W sieci web ASP.NET interfejsów API można to zrobić za pomocą oprogramowania pośredniczącego OWIN firmy Microsoft włączone w programie .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="afb29-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="afb29-108">W tym miejscu użyjemy OWIN do tworzenia interfejs API sieci Web MVC "Lista zadań do wykonania", który pozwala na tworzenie i odczytywanie zadań z listy zadań do wykonania przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="afb29-108">Here we’ll use OWIN to build a "To Do List" MVC Web API that allows clients to create and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="afb29-109">Interfejs API sieci web zostanie przeprowadzona Weryfikacja, czy żądania przychodzące zawiera prawidłowy dostęp do tokenu i Odrzuć wszelkie żądania nie przeszedł pomyślnie weryfikacji w trasie chronionych.</span><span class="sxs-lookup"><span data-stu-id="afb29-109">The web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="afb29-110">W tym przykładzie został utworzony przy użyciu programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="afb29-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="afb29-111">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="afb29-111">Download</span></span>
<span data-ttu-id="afb29-112">Kod używany w tym samouczku jest przechowywany [ w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="afb29-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="afb29-113">Aby z niego skorzystać, można [pobrać szkielet aplikacji w formie .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) lub sklonować szkielet:</span><span class="sxs-lookup"><span data-stu-id="afb29-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="afb29-114">Szkielet aplikacji obejmuje całego kodu umożliwiającego prosty interfejs API, ale brakuje wszystkie elementy związane z tożsamości.</span><span class="sxs-lookup"><span data-stu-id="afb29-114">The skeleton app includes all the boilerplate code for a simple API, but is missing all of the identity-related pieces.</span></span> <span data-ttu-id="afb29-115">Jeśli nie chcesz z niego skorzystać, zamiast tego można sklonować lub [Pobieranie ukończone próbki](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="afb29-115">If you don't want to follow along, you can instead clone or [download the completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="afb29-116">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="afb29-116">Register an app</span></span>
<span data-ttu-id="afb29-117">Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="afb29-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="afb29-118">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="afb29-118">Make sure to:</span></span>

* <span data-ttu-id="afb29-119">Skopiuj **identyfikator aplikacji** przypisany do aplikacji, będzie on potrzebny wkrótce.</span><span class="sxs-lookup"><span data-stu-id="afb29-119">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>

<span data-ttu-id="afb29-120">To rozwiązanie visual studio zawiera także "TodoListClient", która jest prosta aplikacja WPF.</span><span class="sxs-lookup"><span data-stu-id="afb29-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="afb29-121">TodoListClient służy do pokazują, jak użytkownika logowania i jak klient może wysyłać żądania do interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="afb29-121">The TodoListClient is used to demonstrate how a user signs-in and how a client can issue requests to your Web API.</span></span>  <span data-ttu-id="afb29-122">W takim przypadku zarówno TodoListClient i TodoListService są reprezentowane przez tej samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="afb29-122">In this case, both the TodoListClient and the TodoListService are represented by the same app.</span></span>  <span data-ttu-id="afb29-123">Aby skonfigurować TodoListClient, należy również:</span><span class="sxs-lookup"><span data-stu-id="afb29-123">To configure the TodoListClient, you should also:</span></span>

* <span data-ttu-id="afb29-124">Dodaj **Mobile** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="afb29-124">Add the **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="afb29-125">Instalowanie interfejsu OWIN</span><span class="sxs-lookup"><span data-stu-id="afb29-125">Install OWIN</span></span>
<span data-ttu-id="afb29-126">Teraz, gdy został zarejestrowany aplikację, musisz skonfigurować aplikację do komunikacji z punktem końcowym v2.0 do weryfikacji przychodzących żądań i tokenów.</span><span class="sxs-lookup"><span data-stu-id="afb29-126">Now that you’ve registered an app, you need to set up your app to communicate with the v2.0 endpoint in order to validate incoming requests & tokens.</span></span>

* <span data-ttu-id="afb29-127">Aby rozpocząć, otwórz rozwiązanie i dodawanie pakietów NuGet oprogramowanie pośredniczące OWIN do projektu TodoListService przy użyciu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="afb29-127">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="afb29-128">Konfigurowanie uwierzytelniania OAuth</span><span class="sxs-lookup"><span data-stu-id="afb29-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="afb29-129">Dodawanie klasy początkowej OWIN do projektu TodoListService o nazwie `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="afb29-129">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="afb29-130">Kliknij prawym przyciskiem projekt myszy--> **Dodaj** --> **nowy element** --> Wyszukaj "OWIN".</span><span class="sxs-lookup"><span data-stu-id="afb29-130">Right click on the project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="afb29-131">Oprogramowanie pośredniczące OWIN wywoła metodę `Configuration(…)` podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="afb29-131">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="afb29-132">Deklaracja klasy, aby zmienić `public partial class Startup` — już zaimplementowano część tej klasy dla Ciebie w innym pliku.</span><span class="sxs-lookup"><span data-stu-id="afb29-132">Change the class declaration to `public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="afb29-133">W `Configuration(…)` metody, utworzyć ConfgureAuth(...) wywołana w celu ustawienia uwierzytelniania dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="afb29-133">In the `Configuration(…)` method, make a call to ConfgureAuth(…) to set up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="afb29-134">Otwórz plik `App_Start\Startup.Auth.cs` i wdrożenie `ConfigureAuth(…)` metodę, która zostanie skonfigurowany w interfejsie API sieci Web akceptuje tokeny od punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="afb29-134">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method, which will set up the Web API to accept tokens from the v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, the TodoListClient and TodoListService
                // are represented using the same Application Id - we use
                // the Application Id to represent the audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that the user's organization (if applicable) has
                // signed up for the app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up the OWIN pipeline to use OAuth 2.0 Bearer authentication.
        // The options provided here tell the middleware about the type of tokens
        // that will be recieved, which are JWTs for the v2.0 endpoint.

        // NOTE: The usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by the v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used to fetch & use the OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="afb29-135">Teraz można używać `[Authorize]` atrybutów ochrony kontrolerów i akcji z uwierzytelniania elementu nośnego OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="afb29-135">Now you can use `[Authorize]` attributes to protect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="afb29-136">Dekoracji `Controllers\TodoListController.cs` klasy z tagiem autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="afb29-136">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="afb29-137">Spowoduje to wymuszenie użytkownika do logowania przed uzyskaniem dostępu do tej strony.</span><span class="sxs-lookup"><span data-stu-id="afb29-137">This will force the user to sign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="afb29-138">Gdy Autoryzowany rozmówca pomyślnie wywołuje jeden z `TodoListController` interfejsów API, działania mogą wymagać dostępu do informacji o elemencie wywołującym.</span><span class="sxs-lookup"><span data-stu-id="afb29-138">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span>  <span data-ttu-id="afb29-139">OWIN zapewnia dostęp do oświadczeń wewnątrz tokenu elementu nośnego za pośrednictwem `ClaimsPrincpal` obiektu.</span><span class="sxs-lookup"><span data-stu-id="afb29-139">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use the ClaimsPrincipal to access information about the
    // user making the call.  In this case, we use the 'sub' or
    // NameIdentifier claim to serve as a key for the tasks in the data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="afb29-140">Na koniec Otwórz `web.config` plików w folderze głównym projektu TodoListService, a następnie wprowadź wartości konfiguracji w `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="afb29-140">Finally, open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="afb29-141">Twoje `ida:Audience` jest **identyfikator aplikacji** aplikacji, którą wprowadzono w portalu.</span><span class="sxs-lookup"><span data-stu-id="afb29-141">Your `ida:Audience` is the **Application Id** of the app that you entered in the portal.</span></span>

## <a name="configure-the-client-app"></a><span data-ttu-id="afb29-142">Konfigurowanie aplikacji klienta</span><span class="sxs-lookup"><span data-stu-id="afb29-142">Configure the client app</span></span>
<span data-ttu-id="afb29-143">Zanim zobaczysz usługi listy Todo w akcji, należy skonfigurować klienta listy Todo, więc mogą uzyskać tokeny z punktem końcowym v2.0 ani nawiązywania połączeń z usługą.</span><span class="sxs-lookup"><span data-stu-id="afb29-143">Before you can see the Todo List Service in action, you need to configure the Todo List Client so it can get tokens from the v2.0 endpoint and make calls to the service.</span></span>

* <span data-ttu-id="afb29-144">W projekcie TodoListClient Otwórz `App.config` , a następnie wprowadź wartości konfiguracji w `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="afb29-144">In the TodoListClient project, open `App.config` and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="afb29-145">Twoje `ida:ClientId` identyfikator aplikacji został skopiowany z portalu.</span><span class="sxs-lookup"><span data-stu-id="afb29-145">Your `ida:ClientId` Application Id you copied from the portal.</span></span>

<span data-ttu-id="afb29-146">Ponadto wyczyścić, skompilować i uruchomić każdy projekt!</span><span class="sxs-lookup"><span data-stu-id="afb29-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="afb29-147">Masz teraz interfejs API sieci Web .NET MVC, który akceptuje tokeny od oba osobistego konta Microsoft i konta firmowego lub szkolnego.</span><span class="sxs-lookup"><span data-stu-id="afb29-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="afb29-148">Zaloguj się do TodoListClient i wywoływania składnika web api, aby dodać zadania do listy zadań do wykonania przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="afb29-148">Sign into the TodoListClient, and call your web api to add tasks to the user's To-Do list.</span></span>

<span data-ttu-id="afb29-149">Próbka ukończone (bez wartości konfiguracji) [jest dostarczane jako zip w tym miejscu](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), lub można ją sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="afb29-149">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="afb29-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="afb29-150">Next steps</span></span>
<span data-ttu-id="afb29-151">Możesz teraz przejść do dodatkowe tematy.</span><span class="sxs-lookup"><span data-stu-id="afb29-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="afb29-152">Można spróbować:</span><span class="sxs-lookup"><span data-stu-id="afb29-152">You may want to try:</span></span>

[<span data-ttu-id="afb29-153">Wywoływanie interfejsu API sieci Web z aplikacji sieci Web >></span><span class="sxs-lookup"><span data-stu-id="afb29-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="afb29-154">Aby uzyskać dodatkowe zasoby Zobacz:</span><span class="sxs-lookup"><span data-stu-id="afb29-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="afb29-155">Przewodnik dewelopera v2.0 >></span><span class="sxs-lookup"><span data-stu-id="afb29-155">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="afb29-156">Tag StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="afb29-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="afb29-157">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="afb29-157">Get security updates for our products</span></span>
<span data-ttu-id="afb29-158">Firma Microsoft zachęca do przekazywania powiadomień o występujących incydentach zabezpieczeń poprzez wizytę na [tej stronie](https://technet.microsoft.com/security/dd252948) i subskrybowanie Doradczych alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="afb29-158">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
