---
title: aaaAzure AD .NET sieci web interfejsu API wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild interfejs API sieci web .NET MVC która integruje się z usługą Azure AD do uwierzytelniania i autoryzacji."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="d7114-103">Zabezpieczanie interfejsu API sieci web za pomocą tokenów elementu nośnego z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7114-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="d7114-104">Jeśli tworzysz aplikację, która zapewnia dostęp do zasobów tooprotected należy tooknow jak tooprevent nieuzasadnione uzyskiwać dostęp do zasobów toothose.</span><span class="sxs-lookup"><span data-stu-id="d7114-104">If you’re building an application that provides access tooprotected resources, you need tooknow how tooprevent unwarranted access toothose resources.</span></span>
<span data-ttu-id="d7114-105">Azure Active Directory (Azure AD) umożliwia proste i bezpośrednie toohelp chronić interfejsu API sieci web przy użyciu tokenów dostępu do elementu nośnego OAuth 2.0 tylko kilka wierszy kodu.</span><span class="sxs-lookup"><span data-stu-id="d7114-105">Azure Active Directory (Azure AD) makes it simple and straightforward toohelp protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="d7114-106">W aplikacji sieci web ASP.NET można osiągnąć tę ochronę za pomocą implementacja firmy Microsoft hello hello społeczność oprogramowania pośredniczącego OWIN uwzględnione w programie .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="d7114-106">In ASP.NET web apps, you can accomplish this protection by using hello Microsoft implementation of hello community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="d7114-107">W tym miejscu użyjemy toobuild OWIN interfejs API sieci web "tooDo listy" który:</span><span class="sxs-lookup"><span data-stu-id="d7114-107">Here we’ll use OWIN toobuild a "tooDo List" web API that:</span></span>

* <span data-ttu-id="d7114-108">Określa, które interfejsy API są chronione.</span><span class="sxs-lookup"><span data-stu-id="d7114-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="d7114-109">Sprawdza, czy hello wywołania interfejsu API sieci web zawiera tokenu dostępu prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="d7114-109">Validates that hello web API calls contain a valid access token.</span></span>

<span data-ttu-id="d7114-110">tooDo hello toobuild listy interfejsu API, musisz najpierw:</span><span class="sxs-lookup"><span data-stu-id="d7114-110">toobuild hello tooDo List API, you first need to:</span></span>

1. <span data-ttu-id="d7114-111">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7114-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="d7114-112">Konfigurowanie potoku uwierzytelniania OWIN toouse hello hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7114-112">Set up hello app toouse hello OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="d7114-113">Konfigurowanie klienta aplikacji toocall hello interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="d7114-113">Configure a client application toocall hello web API.</span></span>

<span data-ttu-id="d7114-114">Rozpoczęto, tooget [pobrać szkielet aplikacji hello](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) lub [pobieranie próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d7114-114">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="d7114-115">Każdy jest rozwiązanie Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="d7114-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="d7114-116">Należy również dzierżawa usługi Azure AD, w których tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7114-116">You also need an Azure AD tenant in which tooregister your application.</span></span> <span data-ttu-id="d7114-117">Jeśli nie masz już, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="d7114-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="d7114-118">Krok 1: Rejestrowanie aplikacji w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7114-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="d7114-119">toohelp zabezpieczyć aplikację, należy najpierw toocreate aplikację w dzierżawie i dostarczają usługi Azure AD kilka kluczowych informacji.</span><span class="sxs-lookup"><span data-stu-id="d7114-119">toohelp secure your application, you first need toocreate an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="d7114-120">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d7114-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d7114-121">Na górnym pasku powitania kliknij swoje konto.</span><span class="sxs-lookup"><span data-stu-id="d7114-121">On hello top bar, click your account.</span></span> <span data-ttu-id="d7114-122">W hello **katalogu** wybierz dzierżawy usługi Azure AD hello miejscu tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7114-122">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="d7114-123">Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7114-123">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="d7114-124">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d7114-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="d7114-125">Postępuj zgodnie z monitami hello i utworzyć nową **aplikacji sieci Web i/lub interfejs API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="d7114-125">Follow hello prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="d7114-126">**Nazwa** opisuje toousers Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7114-126">**Name** describes your application toousers.</span></span> <span data-ttu-id="d7114-127">Wprowadź **tooDo usługi listy**.</span><span class="sxs-lookup"><span data-stu-id="d7114-127">Enter **tooDo List Service**.</span></span>
  * <span data-ttu-id="d7114-128">**Identyfikator Uri przekierowania** inną schemat i ciąg tooreturn dowolne tokeny zażądał aplikacja korzysta z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7114-128">**Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn any tokens that your app has requested.</span></span> <span data-ttu-id="d7114-129">Wprowadź `https://localhost:44321/` dla tej wartości.</span><span class="sxs-lookup"><span data-stu-id="d7114-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="d7114-130">Z hello **ustawienia** -> **właściwości** strony dla aplikacji, aktualizacji hello identyfikator URI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7114-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="d7114-131">Wprowadź identyfikator specyficznego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="d7114-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="d7114-132">Na przykład wprowadź wartość `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="d7114-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="d7114-133">Zapisz konfigurację hello.</span><span class="sxs-lookup"><span data-stu-id="d7114-133">Save hello configuration.</span></span> <span data-ttu-id="d7114-134">Pozostaw portalu hello otwarty, ponieważ potrzebna będzie również tooregister aplikacja kliencka wkrótce.</span><span class="sxs-lookup"><span data-stu-id="d7114-134">Leave hello portal open, because you'll also need tooregister your client application shortly.</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="d7114-135">Krok 2: Konfigurowanie potoku uwierzytelniania OWIN toouse hello hello aplikacji</span><span class="sxs-lookup"><span data-stu-id="d7114-135">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="d7114-136">przychodzące żądania toovalidate i tokeny należy tooset się toocommunicate Twojej aplikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7114-136">toovalidate incoming requests and tokens, you need tooset up your application toocommunicate with Azure AD.</span></span>

1. <span data-ttu-id="d7114-137">toobegin, otwórz rozwiązanie hello i Dodaj projekt TodoListService toohello pakiety NuGet hello OWIN oprogramowanie pośredniczące przy użyciu konsoli Menedżera pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="d7114-137">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="d7114-138">Dodaj OWIN klasy toohello TodoListService projekt startowy o nazwie `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="d7114-138">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="d7114-139">Projekt powitania kliknij prawym przyciskiem myszy, wybierz opcję **Dodaj** > **nowy element**, a następnie wyszukaj **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="d7114-139">Right-click hello project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="d7114-140">oprogramowanie pośredniczące OWIN Hello wywoła hello `Configuration(…)` metody podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7114-140">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="d7114-141">Zmiana deklaracji klasy hello zbyt`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="d7114-141">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="d7114-142">Już zaimplementowano część tej klasy dla Ciebie w innym pliku.</span><span class="sxs-lookup"><span data-stu-id="d7114-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="d7114-143">W hello `Configuration(…)` metody wywoływania zbyt`ConfgureAuth(…)` tooset się uwierzytelniania dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d7114-143">In hello `Configuration(…)` method, make a call too`ConfgureAuth(…)` tooset up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="d7114-144">Witaj Otwórz plik `App_Start\Startup.Auth.cs` i wdrożenie hello `ConfigureAuth(…)` metody.</span><span class="sxs-lookup"><span data-stu-id="d7114-144">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="d7114-145">Witaj parametrów, które należy podać w `WindowsAzureActiveDirectoryBearerAuthenticationOptions` będzie służyć jako współrzędne toocommunicate Twojej aplikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7114-145">hello parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. <span data-ttu-id="d7114-146">Teraz można używać `[Authorize]` toohelp atrybutów ochrony kontrolerów i akcji z uwierzytelniania elementu nośnego tokenu Web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="d7114-146">Now you can use `[Authorize]` attributes toohelp protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="d7114-147">Dekoracji hello `Controllers\TodoListController.cs` klasy z tagiem autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="d7114-147">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="d7114-148">Spowoduje to wymuszenie hello toosign użytkownika w przed uzyskaniem dostępu do tej strony.</span><span class="sxs-lookup"><span data-stu-id="d7114-148">This will force hello user toosign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="d7114-149">Gdy Autoryzowany rozmówca pomyślnie wywołuje jeden hello `TodoListController` interfejsów API, akcja hello mogą muszą uzyskiwać dostęp do tooinformation o hello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="d7114-149">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span> <span data-ttu-id="d7114-150">OWIN zapewnia dostęp toohello oświadczenia w tokenie hello elementu nośnego za pośrednictwem hello `ClaimsPrincpal` obiektu.</span><span class="sxs-lookup"><span data-stu-id="d7114-150">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="d7114-151">Typowe wymagania dotyczące interfejsów API sieci web jest hello toovalidate "zakresy" występuje w tokenie hello.</span><span class="sxs-lookup"><span data-stu-id="d7114-151">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="d7114-152">Dzięki temu użytkownik hello zgodził toohello uprawnienia wymagane tooaccess hello tooDo usługi listy.</span><span class="sxs-lookup"><span data-stu-id="d7114-152">This ensures that hello user has consented toohello permissions required tooaccess hello tooDo List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="d7114-153">Otwórz hello `web.config` plików w katalogu głównym hello hello TodoListService projektu, a następnie wprowadź wartości konfiguracji w hello `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="d7114-153">Open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="d7114-154">`ida:Tenant`to nazwa hello dzierżawy usługi Azure AD — na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d7114-154">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="d7114-155">`ida:Audience`jest hello identyfikator URI aplikacji hello, wprowadzony w portalu Azure hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7114-155">`ida:Audience` is hello App ID URI of hello application that you entered in hello Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a><span data-ttu-id="d7114-156">Krok 3: Konfigurowanie aplikacji klienta i uruchamianie usługi hello</span><span class="sxs-lookup"><span data-stu-id="d7114-156">Step 3: Configure a client application and run hello service</span></span>
<span data-ttu-id="d7114-157">Zanim zobaczysz hello tooDo usługi listy w akcji, potrzebujesz tooconfigure hello tooDo listy klienta, można uzyskać tokenów z usługi Azure AD i wprowadzić wywołania toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="d7114-157">Before you can see hello tooDo List Service in action, you need tooconfigure hello tooDo List client so it can get tokens from Azure AD and make calls toohello service.</span></span>

1. <span data-ttu-id="d7114-158">Przejdź wstecz toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d7114-158">Go back toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d7114-159">Utwórz nową aplikację w dzierżawie usługi Azure AD, a następnie wybierz **natywną aplikację kliencką** hello wynikowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d7114-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in hello resulting prompt.</span></span>
  * <span data-ttu-id="d7114-160">**Nazwa** opisuje toousers Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7114-160">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="d7114-161">Wprowadź `http://TodoListClient/` dla hello **identyfikator Uri przekierowania** wartość.</span><span class="sxs-lookup"><span data-stu-id="d7114-161">Enter `http://TodoListClient/` for hello **Redirect Uri** value.</span></span>

3. <span data-ttu-id="d7114-162">Po zakończeniu rejestracji usługi Azure AD przypisuje aplikacji Unikatowy identyfikator tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7114-162">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="d7114-163">Ta wartość jest potrzebny w następnych krokach hello, dlatego skopiuj go ze strony aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d7114-163">You’ll need this value in hello next steps, so copy it from hello application page.</span></span>

4. <span data-ttu-id="d7114-164">Z hello **ustawienia** wybierz pozycję **wymagane uprawnienia**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d7114-164">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="d7114-165">Zlokalizuj i wybierz tooDo hello usługi listy i Dodaj hello **TodoListService dostępu** uprawnienie w obszarze **delegowane uprawnienia**, a następnie kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="d7114-165">Locate and select hello tooDo List Service, add hello **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="d7114-166">W programie Visual Studio Otwórz `App.config` w hello TodoListClient projektu, a następnie wprowadź wartości konfiguracji w hello `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="d7114-166">In Visual Studio, open `App.config` in hello TodoListClient project, and then enter your configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="d7114-167">`ida:Tenant`to nazwa hello dzierżawy usługi Azure AD — na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d7114-167">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="d7114-168">`ida:ClientId`jest identyfikator aplikacji hello skopiowany z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d7114-168">`ida:ClientId` is hello app ID that you copied from hello Azure portal.</span></span>
  * <span data-ttu-id="d7114-169">`todo:TodoListResourceId`Identyfikator URI aplikacji hello tooDo aplikacji z listy, wprowadzony w portalu Azure hello hello jest.</span><span class="sxs-lookup"><span data-stu-id="d7114-169">`todo:TodoListResourceId` is hello App ID URI of hello tooDo List Service application that you entered in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7114-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d7114-170">Next steps</span></span>
<span data-ttu-id="d7114-171">Ponadto wyczyścić, skompilować i uruchomić każdy projekt.</span><span class="sxs-lookup"><span data-stu-id="d7114-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="d7114-172">Jeśli nie jest jeszcze teraz jest toocreate czas hello nowego użytkownika w dzierżawie z *. onmicrosoft.com domeny.</span><span class="sxs-lookup"><span data-stu-id="d7114-172">If you haven’t already, now is hello time toocreate a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="d7114-173">Zaloguj się toohello tooDo listy klienta z użytkownikiem, a następnie dodaj listy zadań do wykonania niektórych zadań toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d7114-173">Sign in toohello tooDo List client with that user, and add some tasks toohello user's to-do list.</span></span>

<span data-ttu-id="d7114-174">Odwołania, jest dostępna w ukończyć powitalnych próbka (bez wartości konfiguracji) [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d7114-174">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="d7114-175">Możesz teraz przejść na toomore tożsamości scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="d7114-175">You can now move on toomore identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
