---
title: aaaAzure AD AngularJS wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji jednostronicowej AngularJS integruje się z usługą Azure AD, logowania i wywołuje Azure interfejsów API, które są chronione przez usługi AD za pomocą uwierzytelniania OAuth."
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
ms.openlocfilehash: eca5e1c9662186dfae4f96ca3041f9350583cf79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="a6fa8-103">Zabezpieczanie aplikacji jednostronicowej AngularJS za pomocą usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6fa8-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="a6fa8-104">Azure Active Directory (Azure AD) powoduje proste i bezpośrednie dla możesz tooadd logowania, wylogowania i tooyour wywołania bezpiecznego uwierzytelniania OAuth interfejsu API, aplikacji jednej strony.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you tooadd sign-in, sign-out, and secure OAuth API calls tooyour single-page apps.</span></span>  <span data-ttu-id="a6fa8-105">Umożliwia użytkownikom tooauthenticate aplikacji przy użyciu ich kont usługi Active Directory systemu Windows Server, a korzystanie z dowolnej sieci web interfejsu API usługi Azure AD pozwala to chronić, takich jak hello interfejsami API usługi Office 365 lub hello interfejsu API Azure.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-105">It enables your apps tooauthenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="a6fa8-106">W przypadku aplikacji JavaScript działającego w przeglądarce, usługa Azure AD zapewnia hello Active Directory Authentication Library (ADAL) lub adal.js.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-106">For JavaScript applications running in a browser, Azure AD provides hello Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="a6fa8-107">jedynym celem adal.js Hello jest toomake go łatwo tooget tokenów dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-107">hello sole purpose of adal.js is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="a6fa8-108">toodemonstrate Ci, jak łatwo jest, w tym miejscu będzie budujemy tooDo AngularJS listy aplikacji który:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-108">toodemonstrate just how easy it is, here we'll build an AngularJS tooDo List application that:</span></span>

* <span data-ttu-id="a6fa8-109">Loguje użytkownika hello w toohello aplikację za pomocą usługi Azure AD jako dostawcy tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-109">Signs hello user in toohello app by using Azure AD as hello identity provider.</span></span>

* <span data-ttu-id="a6fa8-110">Przedstawia niektóre informacje na temat hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-110">Displays some information about hello user.</span></span>
* <span data-ttu-id="a6fa8-111">Bezpieczne wywołania hello tooDo aplikacji interfejsu API listy za pomocą tokenów elementu nośnego z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-111">Securely calls hello app's tooDo List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="a6fa8-112">Znaki hello użytkownika poza aplikacją hello.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-112">Signs hello user out of hello app.</span></span>

<span data-ttu-id="a6fa8-113">toobuild hello zakończeniu działającą aplikację, musisz:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-113">toobuild hello complete, working application, you need to:</span></span>

1. <span data-ttu-id="a6fa8-114">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="a6fa8-115">Zainstaluj biblioteki ADAL i skonfiguruj hello jednostronicowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-115">Install ADAL and configure hello single-page app.</span></span>
3. <span data-ttu-id="a6fa8-116">Użyj strony bezpiecznego ADAL toohelp w hello jednostronicowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-116">Use ADAL toohelp secure pages in hello single-page app.</span></span>

<span data-ttu-id="a6fa8-117">Rozpoczęto, tooget [pobrać szkielet aplikacji hello](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) lub [pobieranie próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a6fa8-117">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="a6fa8-118">Należy również dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="a6fa8-119">Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="a6fa8-119">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-hello-directorysearcher-application"></a><span data-ttu-id="a6fa8-120">Krok 1: Zarejestruj hello DirectorySearcher aplikacji</span><span class="sxs-lookup"><span data-stu-id="a6fa8-120">Step 1: Register hello DirectorySearcher application</span></span>
<span data-ttu-id="a6fa8-121">tooenable użytkownicy tooauthenticate aplikacji i tokeny get, należy najpierw tooregister dzierżawy w usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-121">tooenable your app tooauthenticate users and get tokens, you first need tooregister it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="a6fa8-122">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6fa8-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a6fa8-123">Jeśli użytkownik jest zarejestrowany w katalogach toomultiple, może być konieczne tooensure wyświetlasz hello poprawnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-123">If you are signed in toomultiple directories, you may need tooensure you are viewing hello correct directory.</span></span> <span data-ttu-id="a6fa8-124">toodo tak, na górnym pasku powitania kliknij swoje konto.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-124">toodo so, on hello top bar, click your account.</span></span> <span data-ttu-id="a6fa8-125">W obszarze hello **katalogu** wybierz dzierżawy usługi Azure AD hello miejscu tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-125">Under hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="a6fa8-126">Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="a6fa8-127">Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="a6fa8-128">Postępuj zgodnie z monitami hello i utworzyć nową aplikację sieci web i/lub interfejs API sieci web:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-128">Follow hello prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="a6fa8-129">**Nazwa** opisuje toousers Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-129">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="a6fa8-130">**Identyfikator Uri przekierowania** jest toowhich lokalizacji hello Azure AD zwróci tokenów.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-130">**Redirect Uri** is hello location toowhich Azure AD will return tokens.</span></span> <span data-ttu-id="a6fa8-131">Witaj domyślna lokalizacja dla tego przykładu `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-131">hello default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="a6fa8-132">Po zakończeniu rejestracji usługi Azure AD przypisuje aplikacji Unikatowy identyfikator tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-132">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span>  <span data-ttu-id="a6fa8-133">Ta wartość jest potrzebny w kolejnych sekcjach hello, dlatego skopiuj go na karcie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-133">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="a6fa8-134">Adal.js używa toocommunicate niejawnego przepływu OAuth hello z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-134">Adal.js uses hello OAuth implicit flow toocommunicate with Azure AD.</span></span> <span data-ttu-id="a6fa8-135">Należy włączyć hello niejawnego przepływu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-135">You must enable hello implicit flow for your application:</span></span>
  1. <span data-ttu-id="a6fa8-136">Kliknij aplikację hello i wybierz **manifestu** tooopen hello wbudowanego manifestu edytora.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-136">Click hello application and select **Manifest** tooopen hello inline manifest editor.</span></span>
  2. <span data-ttu-id="a6fa8-137">Zlokalizuj hello `oauth2AllowImplicitFlow` właściwości.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-137">Locate hello `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="a6fa8-138">Ustaw dla niego wartość zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-138">Set its value too`true`.</span></span>
  3. <span data-ttu-id="a6fa8-139">Kliknij przycisk **zapisać** toosave hello manifestu.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-139">Click **Save** toosave hello manifest.</span></span>
8. <span data-ttu-id="a6fa8-140">Przyznaj uprawnienia w dzierżawie dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="a6fa8-141">Przejdź za**ustawienia** > **właściwości** > **wymagane uprawnienia**i kliknij przycisk hello **udzielanie uprawnień**przycisk na górnym pasku hello.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-141">Go too**Settings** > **Properties** > **Required Permissions**, and click hello **Grant Permissions** button on hello top bar.</span></span> <span data-ttu-id="a6fa8-142">Kliknij przycisk **tak** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-142">Click **Yes** tooconfirm.</span></span>

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a><span data-ttu-id="a6fa8-143">Krok 2: Install ADAL i skonfigurować hello jednostronicowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="a6fa8-143">Step 2: Install ADAL and configure hello single-page app</span></span>
<span data-ttu-id="a6fa8-144">Teraz, gdy masz aplikacji w usłudze Azure AD, można zainstalować adal.js i wpisz swój kod dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-hello-javascript-client"></a><span data-ttu-id="a6fa8-145">Konfigurowanie powitania klienta JavaScript</span><span class="sxs-lookup"><span data-stu-id="a6fa8-145">Configure hello JavaScript client</span></span>
<span data-ttu-id="a6fa8-146">Rozpocznij, dodając adal.js toohello TodoSPA projektu przy użyciu konsoli Menedżera pakietów hello:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-146">Begin by adding adal.js toohello TodoSPA project by using hello Package Manager Console:</span></span>
  1. <span data-ttu-id="a6fa8-147">Pobierz [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) i dodaj go toohello `App/Scripts/` katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it toohello `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="a6fa8-148">Pobierz [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) i dodaj go toohello `App/Scripts/` katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it toohello `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="a6fa8-149">Ładowanie każdego skryptu przed końcem hello hello `</body>` w `index.html`:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-149">Load each script before hello end of hello `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a><span data-ttu-id="a6fa8-150">Konfigurowanie serwera zaplecza hello</span><span class="sxs-lookup"><span data-stu-id="a6fa8-150">Configure hello back end server</span></span>
<span data-ttu-id="a6fa8-151">Tooaccept interfejsu API listy tokenów aplikacji jednej strony hello tooDo zaplecza przy użyciu przeglądarki hello zaplecza hello musi informacji konfiguracyjnych dotyczących rejestracji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-151">For hello single-page app's back-end tooDo List API tooaccept tokens from hello browser, hello back end needs configuration information about hello app registration.</span></span> <span data-ttu-id="a6fa8-152">W projekcie TodoSPA hello Otwórz `web.config`.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-152">In hello TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="a6fa8-153">Zastąp wartości hello elementów hello na powitania `<appSettings>` sekcji tooreflect hello wartości, używane w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-153">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="a6fa8-154">Kod będzie odwoływać tych wartości, przy każdym użyciu biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="a6fa8-155">`ida:Tenant`jest hello domeny dzierżawy usługi Azure AD — na przykład contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-155">`ida:Tenant` is hello domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="a6fa8-156">`ida:Audience`jest hello identyfikator klienta aplikacji, który został skopiowany z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-156">`ida:Audience` is hello client ID of your application that you copied from hello portal.</span></span>

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a><span data-ttu-id="a6fa8-157">Krok 3: Użyj ADAL toohelp bezpiecznego stron w aplikacji jednej strony hello</span><span class="sxs-lookup"><span data-stu-id="a6fa8-157">Step 3: Use ADAL toohelp secure pages in hello single-page app</span></span>
<span data-ttu-id="a6fa8-158">Adal.js integruje się z AngularJS trasy i dostawców HTTP, więc bezpiecznego poszczególnych widoków może pomóc w aplikacji jednej strony.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="a6fa8-159">W `App/Scripts/app.js`, Przełącz w hello adal.js module:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-159">In `App/Scripts/app.js`, bring in hello adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="a6fa8-160">Inicjowanie `adalProvider` przy użyciu wartości konfiguracji hello Twojej rejestracji aplikacji, również w `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-160">Initialize `adalProvider` by using hello configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="a6fa8-161">Pomoc bezpiecznego hello `TodoList` widoku w aplikacji hello przy użyciu tylko jeden wiersz kodu: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-161">Help secure hello `TodoList` view in hello app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="a6fa8-162">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a6fa8-162">Summary</span></span>
<span data-ttu-id="a6fa8-163">Masz teraz bezpiecznych aplikacji jednej strony, zaloguj się użytkowników i wystawić interfejs API zaplecza tooits żądań chronionego tokenu elementu nośnego.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests tooits back-end API.</span></span> <span data-ttu-id="a6fa8-164">Gdy użytkownik kliknie hello **TodoList** łącza, adal.js spowoduje automatyczne przekierowanie tooAzure AD do logowania w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-164">When a user clicks hello **TodoList** link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span> <span data-ttu-id="a6fa8-165">Ponadto adal.js automatycznie dołączać dostępu tokenu tooany Ajax żądań wysłania toohello aplikacji zaplecza.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-165">In addition, adal.js will automatically attach an access token tooany Ajax requests that are sent toohello app's back end.</span></span>  

<span data-ttu-id="a6fa8-166">Witaj powyższych kroków są hello systemu od zera minimalne wymagane toobuild jednostronicowej aplikacji przy użyciu adal.js.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-166">hello preceding steps are hello bare minimum necessary toobuild a single-page app by using adal.js.</span></span> <span data-ttu-id="a6fa8-167">Jednak kilka innych funkcji są przydatne w aplikacji jednej strony:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="a6fa8-168">tooexplicitly wysyłania żądań zalogowania się i wylogowania, funkcji można zdefiniować w kontrolerach, które wywołują adal.js.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-168">tooexplicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="a6fa8-169">W `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="a6fa8-170">Możesz toopresent informacje o użytkowniku w Interfejsie użytkownika aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-170">You might want toopresent user information in hello app's UI.</span></span> <span data-ttu-id="a6fa8-171">Witaj usługi ADAL został już dodany toohello `userDataCtrl` kontrolera, umożliwi dostęp hello `userInfo` skojarzony obiekt w hello widoku `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-171">hello ADAL service has already been added toohello `userDataCtrl` controller, so you can access hello `userInfo` object in hello associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="a6fa8-172">Istnieje wiele scenariuszy, w których należy tooknow Jeśli hello użytkownik jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-172">There are many scenarios in which you'll want tooknow if hello user is signed in or not.</span></span> <span data-ttu-id="a6fa8-173">Można również użyć hello `userInfo` obiekt toogather te informacje.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-173">You can also use hello `userInfo` object toogather this information.</span></span>  <span data-ttu-id="a6fa8-174">Na przykład w `index.html`, można wyświetlić albo hello **logowania** lub **wylogowania** przycisk na podstawie uwierzytelniania stanu:</span><span class="sxs-lookup"><span data-stu-id="a6fa8-174">For instance, in `index.html`, you can show either hello **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="a6fa8-175">Azure aplikacji jednostronicowej zintegrowanej z usługą AD może uwierzytelniać użytkowników, bezpiecznie wywołać jej zaplecza przy użyciu protokołu OAuth 2.0 i uzyskać podstawowe informacje o użytkowniku hello.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about hello user.</span></span> <span data-ttu-id="a6fa8-176">Jeśli nie jest jeszcze teraz jest hello toopopulate czas dzierżawy z niektórych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-176">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span> <span data-ttu-id="a6fa8-177">Uruchamianie aplikacji jednostronicowej tooDo listy, a następnie zaloguj się przy użyciu jednej z tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-177">Run your tooDo List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="a6fa8-178">Dodawanie listy zadań do wykonania zadania toohello użytkownika, wyloguj się i zaloguj się ponownie.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-178">Add tasks toohello user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="a6fa8-179">Adal.js umożliwia łatwe tooincorporate wspólne funkcje tożsamości w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-179">Adal.js makes it easy tooincorporate common identity features into your application.</span></span> <span data-ttu-id="a6fa8-180">Zapewnia obsługę wszystkich prac dirty hello, dla Ciebie: Zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika z logowaniem interfejsu użytkownika, odświeżanie wygaśnięcia tokenów i inne.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-180">It takes care of all hello dirty work for you: cache management, OAuth protocol support, presenting hello user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="a6fa8-181">Odwołania, jest dostępna w ukończyć powitalnych próbka (bez wartości konfiguracji) [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a6fa8-181">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6fa8-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6fa8-182">Next steps</span></span>
<span data-ttu-id="a6fa8-183">Możesz teraz przejść na tooadditional scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="a6fa8-183">You can now move on tooadditional scenarios.</span></span> <span data-ttu-id="a6fa8-184">Może być tootry: [wywołać mechanizmu CORS interfejsu API sieci web z aplikacji jednej strony](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="a6fa8-184">You might want tootry: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
