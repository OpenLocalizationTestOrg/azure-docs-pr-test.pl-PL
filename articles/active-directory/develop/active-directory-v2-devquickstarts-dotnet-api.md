---
title: "przy użyciu logowania tooa interfejsu API sieci web .NET MVC aaaAdd hello punktu końcowego v2.0 usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Jak toobuild interfejs Api sieci Web .NET MVC, który akceptuje tokeny od obu Account firmy Microsoft i konta firmowego lub szkolnego."
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
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="cb1a3-103">Zabezpiecz interfejs API web MVC</span><span class="sxs-lookup"><span data-stu-id="cb1a3-103">Secure an MVC web API</span></span>
<span data-ttu-id="cb1a3-104">Z punktem końcowym v2.0 hello Azure Active Directory, można chronić przy użyciu interfejsu API sieci Web [OAuth 2.0](active-directory-v2-protocols.md) tokenów dostępu, włączenie użytkowników z obu osobistego konta Microsoft i konta służbowe toosecurely dostęp do interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-104">With Azure Active Directory hello v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts toosecurely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="cb1a3-105">Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="cb1a3-106">toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="cb1a3-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="cb1a3-107">W sieci web ASP.NET interfejsów API można to zrobić za pomocą oprogramowania pośredniczącego OWIN firmy Microsoft włączone w programie .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="cb1a3-108">W tym miejscu użyjemy toobuild OWIN interfejs API sieci Web MVC "tooDo listy" umożliwia klientom toocreate i Odczyt zadań z listy zadań do wykonania przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-108">Here we’ll use OWIN toobuild a "tooDo List" MVC Web API that allows clients toocreate and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="cb1a3-109">Hello interfejsu API sieci web zostanie przeprowadzona Weryfikacja, czy żądania przychodzące zawiera prawidłowy dostęp do tokenu i Odrzuć wszelkie żądania nie przeszedł pomyślnie weryfikacji w trasie chronionych.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-109">hello web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="cb1a3-110">W tym przykładzie został utworzony przy użyciu programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="cb1a3-111">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="cb1a3-111">Download</span></span>
<span data-ttu-id="cb1a3-112">Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="cb1a3-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="cb1a3-113">toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) lub klonowania hello szkielet:</span><span class="sxs-lookup"><span data-stu-id="cb1a3-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="cb1a3-114">szkielet aplikacji Hello obejmuje wszystkie hello schematyczny kod prosty interfejs API, ale brakuje wszystkie części hello dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-114">hello skeleton app includes all hello boilerplate code for a simple API, but is missing all of hello identity-related pieces.</span></span> <span data-ttu-id="cb1a3-115">Jeśli nie chcesz toofollow wzdłuż, zamiast tego można sklonować lub [pobieranie próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="cb1a3-115">If you don't want toofollow along, you can instead clone or [download hello completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="cb1a3-116">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="cb1a3-116">Register an app</span></span>
<span data-ttu-id="cb1a3-117">Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="cb1a3-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="cb1a3-118">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="cb1a3-118">Make sure to:</span></span>

* <span data-ttu-id="cb1a3-119">Skopiuj hello **identyfikator aplikacji** przypisany tooyour aplikacji, będzie on potrzebny wkrótce.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-119">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>

<span data-ttu-id="cb1a3-120">To rozwiązanie visual studio zawiera także "TodoListClient", która jest prosta aplikacja WPF.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="cb1a3-121">Hello TodoListClient jest używany toodemonstrate sposób logowania użytkownika i jak wystawiać klient żąda tooyour interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-121">hello TodoListClient is used toodemonstrate how a user signs-in and how a client can issue requests tooyour Web API.</span></span>  <span data-ttu-id="cb1a3-122">W takim przypadku zarówno hello TodoListClient i hello TodoListService są reprezentowane przez hello tej samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-122">In this case, both hello TodoListClient and hello TodoListService are represented by hello same app.</span></span>  <span data-ttu-id="cb1a3-123">tooconfigure hello TodoListClient, należy również:</span><span class="sxs-lookup"><span data-stu-id="cb1a3-123">tooconfigure hello TodoListClient, you should also:</span></span>

* <span data-ttu-id="cb1a3-124">Dodaj hello **Mobile** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-124">Add hello **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="cb1a3-125">Instalowanie interfejsu OWIN</span><span class="sxs-lookup"><span data-stu-id="cb1a3-125">Install OWIN</span></span>
<span data-ttu-id="cb1a3-126">Został zarejestrowany aplikację, trzeba tooset się toocommunicate Twojej aplikacji z punktem końcowym v2.0 hello w kolejności toovalidate przychodzących żądań & tokenów.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-126">Now that you’ve registered an app, you need tooset up your app toocommunicate with hello v2.0 endpoint in order toovalidate incoming requests & tokens.</span></span>

* <span data-ttu-id="cb1a3-127">toobegin, otwórz rozwiązanie hello i Dodaj hello OWIN oprogramowanie pośredniczące NuGet pakiety toohello TodoListService projektu przy użyciu konsoli Menedżera pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-127">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="cb1a3-128">Konfigurowanie uwierzytelniania OAuth</span><span class="sxs-lookup"><span data-stu-id="cb1a3-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="cb1a3-129">Dodaj OWIN klasy toohello TodoListService projekt startowy o nazwie `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-129">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="cb1a3-130">Kliknij prawym przyciskiem projekt hello myszy--> **Dodaj** --> **nowy element** --> Wyszukaj "OWIN".</span><span class="sxs-lookup"><span data-stu-id="cb1a3-130">Right click on hello project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="cb1a3-131">oprogramowanie pośredniczące OWIN Hello wywoła hello `Configuration(…)` metody podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-131">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="cb1a3-132">Zmiana deklaracji klasy hello zbyt`public partial class Startup` — już zaimplementowano część tej klasy dla Ciebie w innym pliku.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-132">Change hello class declaration too`public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="cb1a3-133">W hello `Configuration(…)` metody, należy tooset tooConfgureAuth(...) wywołania zapasowej uwierzytelniania dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-133">In hello `Configuration(…)` method, make a call tooConfgureAuth(…) tooset up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="cb1a3-134">Otwórz hello pliku `App_Start\Startup.Auth.cs` i wdrożenie hello `ConfigureAuth(…)` metodę, która zostanie skonfigurowana hello interfejsu API sieci Web tooaccept tokenów z punktu końcowego v2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-134">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method, which will set up hello Web API tooaccept tokens from hello v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="cb1a3-135">Teraz można używać `[Authorize]` atrybutów tooprotect Twojego kontrolerów i akcji przy użyciu uwierzytelniania elementu nośnego OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-135">Now you can use `[Authorize]` attributes tooprotect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="cb1a3-136">Dekoracji hello `Controllers\TodoListController.cs` klasy z tagiem autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-136">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="cb1a3-137">Spowoduje to wymuszenie hello toosign użytkownika w przed uzyskaniem dostępu do tej strony.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-137">This will force hello user toosign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="cb1a3-138">Gdy Autoryzowany rozmówca pomyślnie wywołuje jeden hello `TodoListController` interfejsów API, akcja hello mogą muszą uzyskiwać dostęp do tooinformation o hello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-138">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span>  <span data-ttu-id="cb1a3-139">OWIN zapewnia dostęp toohello oświadczenia w tokenie hello elementu nośnego za pośrednictwem hello `ClaimsPrincpal` obiektu.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-139">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="cb1a3-140">Na koniec Otwórz hello `web.config` plików w katalogu głównym hello hello TodoListService projektu, a następnie wprowadź wartości konfiguracji w hello `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-140">Finally, open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="cb1a3-141">Twoje `ida:Audience` jest hello **identyfikator aplikacji** aplikacji hello, którą wprowadzono w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-141">Your `ida:Audience` is hello **Application Id** of hello app that you entered in hello portal.</span></span>

## <a name="configure-hello-client-app"></a><span data-ttu-id="cb1a3-142">Konfigurowanie aplikacji klienta hello</span><span class="sxs-lookup"><span data-stu-id="cb1a3-142">Configure hello client app</span></span>
<span data-ttu-id="cb1a3-143">Zanim zobaczysz hello usługi listy Todo w akcji, należy tooconfigure powitania klienta listy Todo, mogą uzyskać tokeny z punktu końcowego v2.0 hello i wprowadzić wywołania toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-143">Before you can see hello Todo List Service in action, you need tooconfigure hello Todo List Client so it can get tokens from hello v2.0 endpoint and make calls toohello service.</span></span>

* <span data-ttu-id="cb1a3-144">W projekcie TodoListClient hello Otwórz `App.config` , a następnie wprowadź wartości konfiguracji w hello `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-144">In hello TodoListClient project, open `App.config` and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="cb1a3-145">Twoje `ida:ClientId` skopiowany z portalu hello identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-145">Your `ida:ClientId` Application Id you copied from hello portal.</span></span>

<span data-ttu-id="cb1a3-146">Ponadto wyczyścić, skompilować i uruchomić każdy projekt!</span><span class="sxs-lookup"><span data-stu-id="cb1a3-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="cb1a3-147">Masz teraz interfejs API sieci Web .NET MVC, który akceptuje tokeny od oba osobistego konta Microsoft i konta firmowego lub szkolnego.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="cb1a3-148">Zaloguj się do hello TodoListClient i Wywołaj listy zadań do wykonania w sieci web interfejsu api tooadd zadania toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-148">Sign into hello TodoListClient, and call your web api tooadd tasks toohello user's To-Do list.</span></span>

<span data-ttu-id="cb1a3-149">Odwołania, hello ukończone próbka (bez wartości konfiguracji) [jest dostarczane jako zip w tym miejscu](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), lub można ją sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="cb1a3-149">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="cb1a3-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cb1a3-150">Next steps</span></span>
<span data-ttu-id="cb1a3-151">Możesz teraz przejść do dodatkowe tematy.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="cb1a3-152">Można tootry:</span><span class="sxs-lookup"><span data-stu-id="cb1a3-152">You may want tootry:</span></span>

[<span data-ttu-id="cb1a3-153">Wywoływanie interfejsu API sieci Web z aplikacji sieci Web >></span><span class="sxs-lookup"><span data-stu-id="cb1a3-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="cb1a3-154">Aby uzyskać dodatkowe zasoby Zobacz:</span><span class="sxs-lookup"><span data-stu-id="cb1a3-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="cb1a3-155">Przewodnik dewelopera v2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="cb1a3-155">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="cb1a3-156">Tag StackOverflow "azure-active-directory" >></span><span class="sxs-lookup"><span data-stu-id="cb1a3-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="cb1a3-157">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="cb1a3-157">Get security updates for our products</span></span>
<span data-ttu-id="cb1a3-158">Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez wizytę [tę stronę](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.</span><span class="sxs-lookup"><span data-stu-id="cb1a3-158">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
