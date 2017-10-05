---
title: Azure AD .NET sieci web interfejsu API wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak utworzyć .NET MVC składnika web API, która integruje się z usługą Azure AD do uwierzytelniania i autoryzacji."
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
ms.openlocfilehash: f44d75f45073a5d9aa9b1863ed227aba4efcf785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="43d28-103">Zabezpieczanie interfejsu API sieci web za pomocą tokenów elementu nośnego z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="43d28-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="43d28-104">Jeśli tworzysz aplikację, która zapewnia dostęp do chronionych zasobów, musisz wiedzieć, jak uniemożliwić nieuzasadnione dostęp do tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="43d28-104">If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.</span></span>
<span data-ttu-id="43d28-105">Azure Active Directory (Azure AD) powoduje, że jej proste i bezpośrednie zabezpieczyć interfejs API sieci web przy użyciu dostępu elementu nośnego OAuth 2.0 tokeny przy tylko kilku wierszy kodu.</span><span class="sxs-lookup"><span data-stu-id="43d28-105">Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="43d28-106">W aplikacji sieci web ASP.NET można wykonywać tę ochronę za pomocą przez firmę Microsoft implementacją społeczność oprogramowania pośredniczącego OWIN uwzględnione w programie .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="43d28-106">In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="43d28-107">W tym miejscu użyjemy OWIN do kompilacji "Lista zadań do wykonania" składnika web API, które:</span><span class="sxs-lookup"><span data-stu-id="43d28-107">Here we’ll use OWIN to build a "To Do List" web API that:</span></span>

* <span data-ttu-id="43d28-108">Określa, które interfejsy API są chronione.</span><span class="sxs-lookup"><span data-stu-id="43d28-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="43d28-109">Sprawdza, czy wywołania interfejsu API sieci web zawiera tokenu dostępu prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="43d28-109">Validates that the web API calls contain a valid access token.</span></span>

<span data-ttu-id="43d28-110">Aby utworzyć do czy listy interfejsu API, należy najpierw:</span><span class="sxs-lookup"><span data-stu-id="43d28-110">To build the To Do List API, you first need to:</span></span>

1. <span data-ttu-id="43d28-111">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43d28-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="43d28-112">Skonfigurować aplikację do używania uwierzytelniania potoku OWIN.</span><span class="sxs-lookup"><span data-stu-id="43d28-112">Set up the app to use the OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="43d28-113">Skonfigurować aplikację klienta do wywołania interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="43d28-113">Configure a client application to call the web API.</span></span>

<span data-ttu-id="43d28-114">Aby rozpocząć, [pobrać szkielet aplikacji](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) lub [Pobieranie ukończone próbki](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="43d28-114">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="43d28-115">Każdy jest rozwiązanie Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="43d28-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="43d28-116">Należy również dzierżawa usługi Azure AD, w którym można zarejestrować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="43d28-116">You also need an Azure AD tenant in which to register your application.</span></span> <span data-ttu-id="43d28-117">Jeśli nie masz już, [Dowiedz się, jak kupić](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="43d28-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="43d28-118">Krok 1: Rejestrowanie aplikacji w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="43d28-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="43d28-119">Aby ułatwić zabezpieczanie aplikacji, należy najpierw utworzyć aplikację w dzierżawie i udostępnia usługi Azure AD z kilka kluczowych informacji.</span><span class="sxs-lookup"><span data-stu-id="43d28-119">To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="43d28-120">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43d28-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="43d28-121">Na górnym pasku kliknij konto.</span><span class="sxs-lookup"><span data-stu-id="43d28-121">On the top bar, click your account.</span></span> <span data-ttu-id="43d28-122">W **katalogu** wybierz dzierżawy usługi Azure AD, które chcesz zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="43d28-122">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>

3. <span data-ttu-id="43d28-123">Kliknij przycisk **więcej usług** w okienku po lewej stronie, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="43d28-123">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="43d28-124">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="43d28-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="43d28-125">Postępuj zgodnie z monitami i utworzyć nową **aplikacji sieci Web i/lub interfejs API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="43d28-125">Follow the prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="43d28-126">**Nazwa** opisuje aplikacji dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="43d28-126">**Name** describes your application to users.</span></span> <span data-ttu-id="43d28-127">Wprowadź **Lista zadań do wykonania usługi**.</span><span class="sxs-lookup"><span data-stu-id="43d28-127">Enter **To Do List Service**.</span></span>
  * <span data-ttu-id="43d28-128">**Identyfikator Uri przekierowania** jest kombinacją schemat i ciąg, korzystającą z usługi Azure AD w celu zwracać wszystkie tokeny, których aplikacja zażądała.</span><span class="sxs-lookup"><span data-stu-id="43d28-128">**Redirect Uri** is a scheme and string combination that Azure AD uses to return any tokens that your app has requested.</span></span> <span data-ttu-id="43d28-129">Wprowadź `https://localhost:44321/` dla tej wartości.</span><span class="sxs-lookup"><span data-stu-id="43d28-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="43d28-130">Z **ustawienia** -> **właściwości** strony dla aplikacji, zaktualizuj identyfikator URI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="43d28-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="43d28-131">Wprowadź identyfikator specyficznego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="43d28-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="43d28-132">Na przykład wprowadź wartość `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="43d28-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="43d28-133">Zapisz konfigurację.</span><span class="sxs-lookup"><span data-stu-id="43d28-133">Save the configuration.</span></span> <span data-ttu-id="43d28-134">Pozostaw portalu otwarty, ponieważ należy również zarejestrować aplikację klienta wkrótce.</span><span class="sxs-lookup"><span data-stu-id="43d28-134">Leave the portal open, because you'll also need to register your client application shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="43d28-135">Krok 2: Konfigurowanie aplikacji do używania uwierzytelniania potoku OWIN</span><span class="sxs-lookup"><span data-stu-id="43d28-135">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="43d28-136">Można sprawdzić poprawności przychodzących żądań i tokenów, należy skonfigurować aplikację do komunikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43d28-136">To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.</span></span>

1. <span data-ttu-id="43d28-137">Aby rozpocząć, otwórz rozwiązanie i dodawanie pakietów NuGet oprogramowanie pośredniczące OWIN do projektu TodoListService przy użyciu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="43d28-137">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="43d28-138">Dodawanie klasy początkowej OWIN do projektu TodoListService o nazwie `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="43d28-138">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="43d28-139">Kliknij prawym przyciskiem myszy projekt, wybierz **Dodaj** > **nowy element**, a następnie wyszukaj **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="43d28-139">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="43d28-140">Oprogramowanie pośredniczące OWIN wywoła metodę `Configuration(…)` podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="43d28-140">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="43d28-141">Deklaracja klasy, aby zmienić `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="43d28-141">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="43d28-142">Już zaimplementowano część tej klasy dla Ciebie w innym pliku.</span><span class="sxs-lookup"><span data-stu-id="43d28-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="43d28-143">W `Configuration(…)` utworzyć wywołanie metody `ConfgureAuth(…)` Aby skonfigurować uwierzytelnianie dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="43d28-143">In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="43d28-144">Otwórz plik `App_Start\Startup.Auth.cs` i wdrożenie `ConfigureAuth(…)` metody.</span><span class="sxs-lookup"><span data-stu-id="43d28-144">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="43d28-145">Parametry, które należy podać w `WindowsAzureActiveDirectoryBearerAuthenticationOptions` będzie służyć jako współrzędnych dla aplikacji w celu komunikowania się z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43d28-145">The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

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

5. <span data-ttu-id="43d28-146">Teraz można używać `[Authorize]` atrybutów, aby lepiej chronić Twoje kontrolerów i akcji przy użyciu uwierzytelniania elementu nośnego tokenu Web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="43d28-146">Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="43d28-147">Dekoracji `Controllers\TodoListController.cs` klasy z tagiem autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="43d28-147">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="43d28-148">Spowoduje to wymuszenie użytkownika do logowania przed uzyskaniem dostępu do tej strony.</span><span class="sxs-lookup"><span data-stu-id="43d28-148">This will force the user to sign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="43d28-149">Gdy Autoryzowany rozmówca pomyślnie wywołuje jeden z `TodoListController` interfejsów API, działania mogą wymagać dostępu do informacji o elemencie wywołującym.</span><span class="sxs-lookup"><span data-stu-id="43d28-149">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span> <span data-ttu-id="43d28-150">OWIN zapewnia dostęp do oświadczeń wewnątrz tokenu elementu nośnego za pośrednictwem `ClaimsPrincpal` obiektu.</span><span class="sxs-lookup"><span data-stu-id="43d28-150">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="43d28-151">Typowym wymogiem dla interfejsów API sieci Web jest weryfikacja „zakresów” występujących w tokenie.</span><span class="sxs-lookup"><span data-stu-id="43d28-151">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="43d28-152">Dzięki temu, że użytkownik zgodził się na uprawnienia wymagane do uzyskania dostępu do czy listy usługi.</span><span class="sxs-lookup"><span data-stu-id="43d28-152">This ensures that the user has consented to the permissions required to access the To Do List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="43d28-153">Otwórz `web.config` plików w folderze głównym projektu TodoListService, a następnie wprowadź wartości konfiguracji w `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="43d28-153">Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="43d28-154">`ida:Tenant`to nazwa dzierżawy usługi Azure AD — na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="43d28-154">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="43d28-155">`ida:Audience`to identyfikator URI aplikacji w aplikacji, którą wprowadzono w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="43d28-155">`ida:Audience` is the App ID URI of the application that you entered in the Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-the-service"></a><span data-ttu-id="43d28-156">Krok 3: Konfigurowanie aplikacji klienta i uruchamiania usługi</span><span class="sxs-lookup"><span data-stu-id="43d28-156">Step 3: Configure a client application and run the service</span></span>
<span data-ttu-id="43d28-157">Zanim zobaczysz do czy listy działanie usługi, należy skonfigurować klienta listy zadań do wykonania, może uzyskać tokenów z usługi Azure AD i wykonywania wywołań do usługi.</span><span class="sxs-lookup"><span data-stu-id="43d28-157">Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.</span></span>

1. <span data-ttu-id="43d28-158">Wróć do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43d28-158">Go back to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="43d28-159">Utwórz nową aplikację w dzierżawie usługi Azure AD, a następnie wybierz **natywną aplikację kliencką** wynikowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="43d28-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.</span></span>
  * <span data-ttu-id="43d28-160">**Nazwa** opisuje aplikacji dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="43d28-160">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="43d28-161">Wprowadź `http://TodoListClient/` dla **identyfikator Uri przekierowania** wartość.</span><span class="sxs-lookup"><span data-stu-id="43d28-161">Enter `http://TodoListClient/` for the **Redirect Uri** value.</span></span>

3. <span data-ttu-id="43d28-162">Po zakończeniu rejestracji usługi Azure AD przypisuje unikatowy identyfikator aplikacji do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="43d28-162">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="43d28-163">Ta wartość jest potrzebny w następnych krokach, dlatego skopiuj go ze strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="43d28-163">You’ll need this value in the next steps, so copy it from the application page.</span></span>

4. <span data-ttu-id="43d28-164">Z **ustawienia** wybierz pozycję **wymagane uprawnienia**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="43d28-164">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="43d28-165">Zlokalizuj i wybierz do czy listy usługi, dodać **TodoListService dostępu** uprawnienie w obszarze **delegowane uprawnienia**, a następnie kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="43d28-165">Locate and select the To Do List Service, add the **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="43d28-166">W programie Visual Studio Otwórz `App.config` w TodoListClient projektu, a następnie wprowadź wartości konfiguracji w `<appSettings>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="43d28-166">In Visual Studio, open `App.config` in the TodoListClient project, and then enter your configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="43d28-167">`ida:Tenant`to nazwa dzierżawy usługi Azure AD — na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="43d28-167">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="43d28-168">`ida:ClientId`jest to identyfikator aplikacji skopiowany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="43d28-168">`ida:ClientId` is the app ID that you copied from the Azure portal.</span></span>
  * <span data-ttu-id="43d28-169">`todo:TodoListResourceId`to identyfikator URI aplikacji w aplikacji do usługi listy czy wprowadzony w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="43d28-169">`todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43d28-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43d28-170">Next steps</span></span>
<span data-ttu-id="43d28-171">Ponadto wyczyścić, skompilować i uruchomić każdy projekt.</span><span class="sxs-lookup"><span data-stu-id="43d28-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="43d28-172">Jeśli nie jest jeszcze nadszedł czas, aby utworzyć nowy użytkownik w dzierżawie z *. onmicrosoft.com domeny.</span><span class="sxs-lookup"><span data-stu-id="43d28-172">If you haven’t already, now is the time to create a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="43d28-173">Zaloguj się do klienta listy zadań do wykonania z użytkownikiem, a następnie dodać niektóre zadania do listy zadań do wykonania przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="43d28-173">Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.</span></span>

<span data-ttu-id="43d28-174">Odwołanie, ukończonych próbka (bez wartości konfiguracji) są dostępne w [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="43d28-174">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="43d28-175">Możesz teraz przejść do scenariuszy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="43d28-175">You can now move on to more identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
