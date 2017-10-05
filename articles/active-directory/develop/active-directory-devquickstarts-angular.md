---
title: Azure AD AngularJS, wprowadzenie | Dokumentacja firmy Microsoft
description: "Sposób tworzenia aplikacji jednostronicowej AngularJS, która integruje się z usługą Azure AD, logowania i wywołuje Azure interfejsów API, które są chronione przez usługi AD za pomocą uwierzytelniania OAuth."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 4153910bc03f112f84c26cda6f9c78f11028b934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="a6d69-103">Zabezpieczanie aplikacji jednostronicowej AngularJS za pomocą usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6d69-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="a6d69-104">Azure Active Directory (Azure AD) powoduje, że proste i bezpośrednie dodanie logowania, wylogowywania i bezpieczny OAuth interfejs API wywołuje do aplikacji jednej strony.</span><span class="sxs-lookup"><span data-stu-id="a6d69-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.</span></span>  <span data-ttu-id="a6d69-105">Umożliwia aplikacji do uwierzytelniania użytkowników przy użyciu ich kont usługi Active Directory systemu Windows Server i korzystać z dowolnej sieci web interfejsu API usługi Azure AD pozwala to chronić, takich jak interfejsami API usługi Office 365 lub interfejsu API platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a6d69-105">It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="a6d69-106">W przypadku aplikacji JavaScript działającego w przeglądarce usługa Azure AD zapewnia Active Directory Authentication Library (ADAL) lub adal.js.</span><span class="sxs-lookup"><span data-stu-id="a6d69-106">For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="a6d69-107">Jest wyłącznie w celu adal.js umożliwia łatwe uzyskanie tokenów dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6d69-107">The sole purpose of adal.js is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="a6d69-108">Aby zademonstrować, jak łatwo jest, w tym miejscu będzie budujemy aplikacji AngularJS listy zadań do wykonania który:</span><span class="sxs-lookup"><span data-stu-id="a6d69-108">To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:</span></span>

* <span data-ttu-id="a6d69-109">Loguje użytkownika do aplikacji przy użyciu usługi Azure AD jako dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="a6d69-109">Signs the user in to the app by using Azure AD as the identity provider.</span></span>

* <span data-ttu-id="a6d69-110">Przedstawia niektóre informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="a6d69-110">Displays some information about the user.</span></span>
* <span data-ttu-id="a6d69-111">Bezpieczne wywołania aplikacji do czy listy interfejsu API za pomocą tokenów elementu nośnego z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6d69-111">Securely calls the app's To Do List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="a6d69-112">Loguje użytkownika poza aplikacją.</span><span class="sxs-lookup"><span data-stu-id="a6d69-112">Signs the user out of the app.</span></span>

<span data-ttu-id="a6d69-113">Aby utworzyć pełną, działającą aplikację, musisz:</span><span class="sxs-lookup"><span data-stu-id="a6d69-113">To build the complete, working application, you need to:</span></span>

1. <span data-ttu-id="a6d69-114">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6d69-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="a6d69-115">Instalowanie ADAL i konfigurowanie aplikacji jednej strony.</span><span class="sxs-lookup"><span data-stu-id="a6d69-115">Install ADAL and configure the single-page app.</span></span>
3. <span data-ttu-id="a6d69-116">Umożliwia bezpieczne strony w aplikacji jednej strony pomocy biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="a6d69-116">Use ADAL to help secure pages in the single-page app.</span></span>

<span data-ttu-id="a6d69-117">Aby rozpocząć, [pobrać szkielet aplikacji](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) lub [Pobieranie ukończone próbki](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a6d69-117">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="a6d69-118">Należy również dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6d69-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="a6d69-119">Jeśli nie masz już dzierżawę, [Dowiedz się, jak kupić](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="a6d69-119">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-the-directorysearcher-application"></a><span data-ttu-id="a6d69-120">Krok 1: Zarejestrować aplikację DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="a6d69-120">Step 1: Register the DirectorySearcher application</span></span>
<span data-ttu-id="a6d69-121">Aby umożliwić aplikacji w celu uwierzytelniania użytkowników i uzyskać tokeny, należy najpierw zarejestrować ją w dzierżawie usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a6d69-121">To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="a6d69-122">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6d69-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a6d69-123">Jeśli użytkownik jest zalogowany do wielu katalogów, konieczne może być upewnij się, że wyświetlany jest poprawnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="a6d69-123">If you are signed in to multiple directories, you may need to ensure you are viewing the correct directory.</span></span> <span data-ttu-id="a6d69-124">Aby to zrobić, na górnym pasku kliknij swoje konto.</span><span class="sxs-lookup"><span data-stu-id="a6d69-124">To do so, on the top bar, click your account.</span></span> <span data-ttu-id="a6d69-125">W obszarze **katalogu** wybierz dzierżawy usługi Azure AD, które chcesz zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="a6d69-125">Under the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="a6d69-126">Kliknij przycisk **więcej usług** w okienku po lewej stronie, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a6d69-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="a6d69-127">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a6d69-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="a6d69-128">Postępuj zgodnie z monitami i utworzyć nową aplikację sieci web i/lub interfejs API sieci web:</span><span class="sxs-lookup"><span data-stu-id="a6d69-128">Follow the prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="a6d69-129">**Nazwa** opisuje aplikacji dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a6d69-129">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="a6d69-130">**Identyfikator Uri przekierowania** to lokalizacja, do której usługi Azure AD zwróci tokenów.</span><span class="sxs-lookup"><span data-stu-id="a6d69-130">**Redirect Uri** is the location to which Azure AD will return tokens.</span></span> <span data-ttu-id="a6d69-131">Domyślna lokalizacja dla tego przykładu `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="a6d69-131">The default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="a6d69-132">Po zakończeniu rejestracji usługi Azure AD przypisuje unikatowy identyfikator aplikacji do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6d69-132">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span>  <span data-ttu-id="a6d69-133">Ta wartość jest potrzebny w kolejnych sekcjach, dlatego skopiuj go na karcie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6d69-133">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="a6d69-134">Adal.js używa niejawnego przepływu OAuth do komunikowania się z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6d69-134">Adal.js uses the OAuth implicit flow to communicate with Azure AD.</span></span> <span data-ttu-id="a6d69-135">Należy włączyć niejawnego przepływu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a6d69-135">You must enable the implicit flow for your application:</span></span>
  1. <span data-ttu-id="a6d69-136">Kliknij aplikację, a następnie wybierz **manifestu** aby otworzyć Edytor manifestu w tekście.</span><span class="sxs-lookup"><span data-stu-id="a6d69-136">Click the application and select **Manifest** to open the inline manifest editor.</span></span>
  2. <span data-ttu-id="a6d69-137">Zlokalizuj `oauth2AllowImplicitFlow` właściwości.</span><span class="sxs-lookup"><span data-stu-id="a6d69-137">Locate the `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="a6d69-138">Ustaw dla niego wartość `true`.</span><span class="sxs-lookup"><span data-stu-id="a6d69-138">Set its value to `true`.</span></span>
  3. <span data-ttu-id="a6d69-139">Kliknij przycisk **zapisać** można zapisać manifestu.</span><span class="sxs-lookup"><span data-stu-id="a6d69-139">Click **Save** to save the manifest.</span></span>
8. <span data-ttu-id="a6d69-140">Przyznaj uprawnienia w dzierżawie dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6d69-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="a6d69-141">Przejdź do **ustawienia** > **właściwości** > **wymagane uprawnienia**i kliknij przycisk **udzielanie uprawnień** przycisk na górnym pasku.</span><span class="sxs-lookup"><span data-stu-id="a6d69-141">Go to **Settings** > **Properties** > **Required Permissions**, and click the **Grant Permissions** button on the top bar.</span></span> <span data-ttu-id="a6d69-142">Kliknij przycisk **Tak**, aby potwierdzić.</span><span class="sxs-lookup"><span data-stu-id="a6d69-142">Click **Yes** to confirm.</span></span>

## <a name="step-2-install-adal-and-configure-the-single-page-app"></a><span data-ttu-id="a6d69-143">Krok 2: Install ADAL i konfigurowanie aplikacji jednostronicowej</span><span class="sxs-lookup"><span data-stu-id="a6d69-143">Step 2: Install ADAL and configure the single-page app</span></span>
<span data-ttu-id="a6d69-144">Teraz, gdy masz aplikacji w usłudze Azure AD, można zainstalować adal.js i wpisz swój kod dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="a6d69-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-the-javascript-client"></a><span data-ttu-id="a6d69-145">Konfigurowanie klienta JavaScript</span><span class="sxs-lookup"><span data-stu-id="a6d69-145">Configure the JavaScript client</span></span>
<span data-ttu-id="a6d69-146">Rozpocznij, dodając adal.js do projektu TodoSPA przy użyciu konsoli Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="a6d69-146">Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:</span></span>
  1. <span data-ttu-id="a6d69-147">Pobierz [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) i dodaj go do `App/Scripts/` katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="a6d69-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="a6d69-148">Pobierz [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) i dodaj go do `App/Scripts/` katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="a6d69-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="a6d69-149">Ładowanie każdego skryptu przed końcem `</body>` w `index.html`:</span><span class="sxs-lookup"><span data-stu-id="a6d69-149">Load each script before the end of the `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-the-back-end-server"></a><span data-ttu-id="a6d69-150">Konfigurowanie serwera zaplecza</span><span class="sxs-lookup"><span data-stu-id="a6d69-150">Configure the back end server</span></span>
<span data-ttu-id="a6d69-151">Dla aplikacji jednej strony zaplecza do czy listy interfejsu API zaakceptować tokeny z przeglądarki wewnętrznej musi informacji konfiguracyjnych dotyczących rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6d69-151">For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration.</span></span> <span data-ttu-id="a6d69-152">W projekcie TodoSPA Otwórz `web.config`.</span><span class="sxs-lookup"><span data-stu-id="a6d69-152">In the TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="a6d69-153">Zastąp wartości elementów w `<appSettings>` sekcji do wartości, które były używane w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a6d69-153">Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="a6d69-154">Kod będzie odwoływać tych wartości, przy każdym użyciu biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="a6d69-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="a6d69-155">`ida:Tenant`jest to domena dzierżawy usługi Azure AD — na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="a6d69-155">`ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="a6d69-156">`ida:Audience`jest to identyfikator klienta aplikacji, który został skopiowany z portalu.</span><span class="sxs-lookup"><span data-stu-id="a6d69-156">`ida:Audience` is the client ID of your application that you copied from the portal.</span></span>

## <a name="step-3-use-adal-to-help-secure-pages-in-the-single-page-app"></a><span data-ttu-id="a6d69-157">Krok 3: Użyj biblioteki ADAL w celu bezpiecznego stron w aplikacji jednej strony</span><span class="sxs-lookup"><span data-stu-id="a6d69-157">Step 3: Use ADAL to help secure pages in the single-page app</span></span>
<span data-ttu-id="a6d69-158">Adal.js integruje się z AngularJS trasy i dostawców HTTP, więc bezpiecznego poszczególnych widoków może pomóc w aplikacji jednej strony.</span><span class="sxs-lookup"><span data-stu-id="a6d69-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="a6d69-159">W `App/Scripts/app.js`, umieść w adal.js module:</span><span class="sxs-lookup"><span data-stu-id="a6d69-159">In `App/Scripts/app.js`, bring in the adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="a6d69-160">Inicjowanie `adalProvider` przy użyciu wartości konfiguracji aplikacji rejestrację, również w `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="a6d69-160">Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

    ```js
    adalProvider.init(
      {
          instance: 'https://login.microsoftonline.com/',
          tenant: 'Enter your tenant name here e.g. contoso.onmicrosoft.com',
          clientId: 'Enter your client ID here e.g. e9a5a8b6-8af7-4719-9821-0deef255f68e',
          extraQueryParameter: 'nux=1',
          //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
      },
      $httpProvider
    );
    ```
3. <span data-ttu-id="a6d69-161">Zabezpieczanie `TodoList` widoku w aplikacji przy użyciu tylko jeden wiersz kodu: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="a6d69-161">Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="a6d69-162">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a6d69-162">Summary</span></span>
<span data-ttu-id="a6d69-163">Masz teraz bezpiecznego aplikacji jednej strony, który można zarejestrować użytkowników i wysyłania żądań chronionego tokenu elementu nośnego do jego interfejs API zaplecza.</span><span class="sxs-lookup"><span data-stu-id="a6d69-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API.</span></span> <span data-ttu-id="a6d69-164">Gdy użytkownik kliknie **TodoList** łącza, adal.js spowoduje automatyczne przekierowanie do usługi Azure AD dla logowania w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="a6d69-164">When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span> <span data-ttu-id="a6d69-165">Ponadto adal.js automatycznie dołączą token dostępu do żadnych żądania Ajax, które są wysyłane do zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6d69-165">In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.</span></span>  

<span data-ttu-id="a6d69-166">Te czynności są systemu od zera minimalna niezbędnych do tworzenia aplikacji jednej strony przy użyciu adal.js.</span><span class="sxs-lookup"><span data-stu-id="a6d69-166">The preceding steps are the bare minimum necessary to build a single-page app by using adal.js.</span></span> <span data-ttu-id="a6d69-167">Jednak kilka innych funkcji są przydatne w aplikacji jednej strony:</span><span class="sxs-lookup"><span data-stu-id="a6d69-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="a6d69-168">Aby jawnie wysyłania żądań zalogowania się i wylogowania, można zdefiniować funkcje w kontrolerach, które wywołują adal.js.</span><span class="sxs-lookup"><span data-stu-id="a6d69-168">To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="a6d69-169">W `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="a6d69-169">In `App/Scripts/homeCtrl.js`:</span></span>

    ```js
    ...
    $scope.login = function () {
        adalService.login();
    };
    $scope.logout = function () {
        adalService.logOut();
    };
    ...
    ```
* <span data-ttu-id="a6d69-170">Można prezentować informacje o użytkowniku w Interfejsie użytkownika aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6d69-170">You might want to present user information in the app's UI.</span></span> <span data-ttu-id="a6d69-171">Usługa ADAL został już dodany do `userDataCtrl` kontrolera, więc można uzyskać dostęp do `userInfo` obiektu w widoku skojarzonego `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="a6d69-171">The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="a6d69-172">Istnieje wiele scenariuszy, w których należy sprawdzić, czy użytkownik jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="a6d69-172">There are many scenarios in which you'll want to know if the user is signed in or not.</span></span> <span data-ttu-id="a6d69-173">Można również użyć `userInfo` obiektu zebranie tych informacji.</span><span class="sxs-lookup"><span data-stu-id="a6d69-173">You can also use the `userInfo` object to gather this information.</span></span>  <span data-ttu-id="a6d69-174">Na przykład w `index.html`, można wyświetlić **logowania** lub **wylogowania** przycisk na podstawie uwierzytelniania stanu:</span><span class="sxs-lookup"><span data-stu-id="a6d69-174">For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="a6d69-175">Azure aplikacji jednostronicowej zintegrowanej z usługą AD może uwierzytelniać użytkowników, bezpiecznie wywołać jej zaplecza przy użyciu protokołu OAuth 2.0 i uzyskać podstawowe informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="a6d69-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user.</span></span> <span data-ttu-id="a6d69-176">Jeśli nie jest jeszcze nadszedł czas do wypełnienia dzierżawy z niektórych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a6d69-176">If you haven't already, now is the time to populate your tenant with some users.</span></span> <span data-ttu-id="a6d69-177">Uruchamianie aplikacji jednostronicowej listy zadań do wykonania, a następnie zaloguj się przy użyciu jednej z tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a6d69-177">Run your To Do List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="a6d69-178">Dodać zadania do listy zadań do wykonania użytkownika, wyloguj się i zaloguj się ponownie.</span><span class="sxs-lookup"><span data-stu-id="a6d69-178">Add tasks to the user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="a6d69-179">Adal.js można łatwo zastosować wspólne funkcje tożsamości w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6d69-179">Adal.js makes it easy to incorporate common identity features into your application.</span></span> <span data-ttu-id="a6d69-180">Zapewnia obsługę pracy dirty, można: Zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający użytkownika z logowaniem interfejsu użytkownika, odświeżanie wygaśnięcia tokenów i inne.</span><span class="sxs-lookup"><span data-stu-id="a6d69-180">It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="a6d69-181">Odwołanie, ukończonych próbka (bez wartości konfiguracji) są dostępne w [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a6d69-181">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6d69-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6d69-182">Next steps</span></span>
<span data-ttu-id="a6d69-183">Możesz teraz przejść do dodatkowe scenariusze.</span><span class="sxs-lookup"><span data-stu-id="a6d69-183">You can now move on to additional scenarios.</span></span> <span data-ttu-id="a6d69-184">Możesz spróbować: [wywołać mechanizmu CORS interfejsu API sieci web z aplikacji jednej strony](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="a6d69-184">You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
