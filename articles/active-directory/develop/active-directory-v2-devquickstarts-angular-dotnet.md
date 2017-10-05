---
title: "Aplikację usługi Azure AD w wersji 2.0 .NET AngularJS jednej strony wprowadzenie | Dokumentacja firmy Microsoft"
description: "Sposób tworzenia aplikacji jednostronicowej kątowego JS logujący się użytkowników z obu osobistego konta Microsoft i konta firmowego lub szkolnego."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 6a341781-278f-461b-92ca-7572a06e6852
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c68180c0ecabf5c0732f0db77ef1f3cc93be965b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---net"></a><span data-ttu-id="76a8c-103">Dodawanie logowania do aplikacji jednej strony AngularJS - .NET</span><span class="sxs-lookup"><span data-stu-id="76a8c-103">Add sign-in to an AngularJS single page app - .NET</span></span>
<span data-ttu-id="76a8c-104">W tym artykule dodamy Zaloguj się przy użyciu konta Microsoft, jej do AngularJS aplikacji za pomocą punktu końcowego v2.0 usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="76a8c-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span>  <span data-ttu-id="76a8c-105">Punktu końcowego v2.0 umożliwia wykonywanie jednego integracji w aplikacji i uwierzytelnianie użytkowników przy użyciu kont osobistych i pracy/służbowe.</span><span class="sxs-lookup"><span data-stu-id="76a8c-105">The v2.0 endpoint enables you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="76a8c-106">Ten przykład jest prostej aplikacji jednej strony listy zadań do wykonania, która przechowuje zadania w wewnętrznej bazie danych interfejsu API REST, napisane przy użyciu platformy .NET 4.5 MVC i chronione za pomocą tokenów elementu nośnego OAuth z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76a8c-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using the .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="76a8c-107">AngularJS aplikacja będzie używać nasza Biblioteka uwierzytelniania JavaScript typu open source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) do obsługi całego logowania procesu i uzyskać tokeny wywołania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="76a8c-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="76a8c-108">Do uwierzytelniania innych interfejsów API REST, tak samo, jak można zastosować tego samego wzorca [Microsoft Graph](https://graph.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="76a8c-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="76a8c-109">Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="76a8c-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="76a8c-110">Aby ustalić, czy należy używać punktu końcowego v2.0, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="76a8c-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="76a8c-111">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="76a8c-111">Download</span></span>
<span data-ttu-id="76a8c-112">Aby rozpocząć pracę, musisz pobrać i zainstalować program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="76a8c-112">To get started, you'll need to download & install Visual Studio.</span></span>  <span data-ttu-id="76a8c-113">Następnie można sklonować lub [Pobierz](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) szkielet aplikacji:</span><span class="sxs-lookup"><span data-stu-id="76a8c-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

<span data-ttu-id="76a8c-114">Szkielet aplikacji obejmuje całego kodu umożliwiającego prostej aplikacji AngularJS, ale brakuje wszystkie elementy związane z tożsamości.</span><span class="sxs-lookup"><span data-stu-id="76a8c-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="76a8c-115">Jeśli nie chcesz z niego skorzystać, zamiast tego można sklonować lub [Pobierz](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) próbki ukończone.</span><span class="sxs-lookup"><span data-stu-id="76a8c-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="76a8c-116">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="76a8c-116">Register an app</span></span>
<span data-ttu-id="76a8c-117">Najpierw utwórz aplikację w [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="76a8c-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="76a8c-118">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="76a8c-118">Make sure to:</span></span>

* <span data-ttu-id="76a8c-119">Dodaj **Web** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="76a8c-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="76a8c-120">Wprowadź poprawny **identyfikator URI przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="76a8c-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="76a8c-121">Wartością domyślną w tym przykładzie jest `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="76a8c-121">The default for this sample is `https://localhost:44326/`.</span></span>
* <span data-ttu-id="76a8c-122">Pozostaw **Zezwalaj przepływu niejawnego** pole wyboru jest włączone.</span><span class="sxs-lookup"><span data-stu-id="76a8c-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="76a8c-123">Skopiuj **identyfikator aplikacji** przypisany do aplikacji, będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="76a8c-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="76a8c-124">Zainstaluj adal.js</span><span class="sxs-lookup"><span data-stu-id="76a8c-124">Install adal.js</span></span>
<span data-ttu-id="76a8c-125">Aby rozpocząć, przejdź do projektu, należy pobrać i zainstalować adal.js.</span><span class="sxs-lookup"><span data-stu-id="76a8c-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="76a8c-126">Jeśli masz [bower](http://bower.io/) zainstalowany, możesz po prostu uruchomić to polecenie.</span><span class="sxs-lookup"><span data-stu-id="76a8c-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="76a8c-127">W przypadku niezgodności wersji zależności wystarczy wybrać nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="76a8c-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="76a8c-128">Alternatywnie możesz ręcznie pobrać [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) i [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="76a8c-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="76a8c-129">Dodaj oba pliki do `app/lib/adal-angular-experimental/dist` katalog `TodoSPA` projektu.</span><span class="sxs-lookup"><span data-stu-id="76a8c-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory of the `TodoSPA` project.</span></span>

<span data-ttu-id="76a8c-130">Teraz Otwórz projekt w programie Visual Studio i załadować adal.js na końcu treści strony głównej:</span><span class="sxs-lookup"><span data-stu-id="76a8c-130">Now open the project in Visual Studio, and load adal.js at the end of the main page's body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="76a8c-131">Ustawianie interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="76a8c-131">Set up the REST API</span></span>
<span data-ttu-id="76a8c-132">Gdy konfigurujemy rzeczy, możemy rozpocząć pracę interfejsu API REST wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="76a8c-132">While we're setting things up, let's get the backend REST API working.</span></span>  <span data-ttu-id="76a8c-133">W katalogu głównym projektu, otwórz `web.config` i Zastąp `audience` wartość.</span><span class="sxs-lookup"><span data-stu-id="76a8c-133">In the root of the project, open `web.config` and replace the `audience` value.</span></span>  <span data-ttu-id="76a8c-134">Ta wartość zostanie użyta do sprawdzania poprawności tokenów otrzymywanych z poziomu aplikacji kątową AJAX żądania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="76a8c-134">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

<span data-ttu-id="76a8c-135">Nadszedł czas, którą spróbujemy poświęcić dyskutować działanie interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="76a8c-135">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="76a8c-136">Możesz także umieszczania przy w kodzie, ale jeśli chcesz dowiedzieć się więcej na temat zabezpieczania sieci web API z usługi Azure AD, zapoznaj się [w tym artykule](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="76a8c-136">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="76a8c-137">Loguj użytkowników</span><span class="sxs-lookup"><span data-stu-id="76a8c-137">Sign users in</span></span>
<span data-ttu-id="76a8c-138">Czas do pisania kodu tożsamości.</span><span class="sxs-lookup"><span data-stu-id="76a8c-138">Time to write some identity code.</span></span>  <span data-ttu-id="76a8c-139">Zwróć uwagę na to już tego adal.js zawiera dostawcy AngularJS, który dobrze odgrywa kątowego mechanizmów routingu.</span><span class="sxs-lookup"><span data-stu-id="76a8c-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="76a8c-140">Rozpocznij od dodania modułu adal w aplikacji:</span><span class="sxs-lookup"><span data-stu-id="76a8c-140">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="76a8c-141">Można teraz zainicjować `adalProvider` za pomocą Identyfikatora aplikacji:</span><span class="sxs-lookup"><span data-stu-id="76a8c-141">You can now initialize the `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for the public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // The 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from the registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - the default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="76a8c-142">Duża, adal.js ma teraz wszystkie informacje potrzebne do zabezpieczania aplikacji i zaloguj się użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="76a8c-142">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="76a8c-143">Aby wymusić logowania dla określonej trasy w aplikacji, potrzebny jest jeden wiersz kodu:</span><span class="sxs-lookup"><span data-stu-id="76a8c-143">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that the user must be logged in to access the route
})

...
```

<span data-ttu-id="76a8c-144">Teraz, gdy użytkownik kliknie `TodoList` łącza, adal.js spowoduje automatyczne przekierowanie do usługi Azure AD dla logowania w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="76a8c-144">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="76a8c-145">Można również jawnie wysyłać żądania logowania i wylogowywania, wywołując adal.js w kontrolerach:</span><span class="sxs-lookup"><span data-stu-id="76a8c-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js the same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect the user to sign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect the user to log out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="76a8c-146">Wyświetl informacje o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="76a8c-146">Display user info</span></span>
<span data-ttu-id="76a8c-147">Teraz, gdy użytkownik jest zalogowany, prawdopodobnie musisz uzyskać dostęp do danych uwierzytelniania zalogowanego użytkownika w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="76a8c-147">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="76a8c-148">Adal.js przedstawia tych informacji w `userInfo` obiektu.</span><span class="sxs-lookup"><span data-stu-id="76a8c-148">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="76a8c-149">Aby uzyskać dostęp do tego obiektu w widoku, należy najpierw dodać adal.js do zakresie głównym odpowiedniego kontrolera:</span><span class="sxs-lookup"><span data-stu-id="76a8c-149">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="76a8c-150">Następnie można bezpośrednio usunąć `userInfo` obiektu w tym widoku:</span><span class="sxs-lookup"><span data-stu-id="76a8c-150">Then you can directly address the `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get the user's profile information from the ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="76a8c-151">Można również użyć `userInfo` obiektem, aby określić, czy użytkownik jest zalogowany lub nie.</span><span class="sxs-lookup"><span data-stu-id="76a8c-151">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use the ADAL userInfo object to show the right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-the-rest-api"></a><span data-ttu-id="76a8c-152">Wywołanie interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="76a8c-152">Call the REST API</span></span>
<span data-ttu-id="76a8c-153">Na koniec nadszedł czas do uzyskania niektórych tokenów i wywołania interfejsu API REST do tworzenia, odczytu, aktualizacji i usuwania zadań.</span><span class="sxs-lookup"><span data-stu-id="76a8c-153">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="76a8c-154">Dobrze wieści.</span><span class="sxs-lookup"><span data-stu-id="76a8c-154">Well guess what?</span></span>  <span data-ttu-id="76a8c-155">Musisz wykonać *przedmiotu*.</span><span class="sxs-lookup"><span data-stu-id="76a8c-155">You don't have to do *a thing*.</span></span>  <span data-ttu-id="76a8c-156">Adal.js automatycznie zajmie się pobieranie, buforowanie i odświeżanie tokenów.</span><span class="sxs-lookup"><span data-stu-id="76a8c-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="76a8c-157">On również zajmie się dołączanie tych tokenów do wychodzących żądania AJAX, które wysyłają do interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="76a8c-157">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="76a8c-158">Dokładnie jak to działa?</span><span class="sxs-lookup"><span data-stu-id="76a8c-158">How exactly does this work?</span></span> <span data-ttu-id="76a8c-159">To wszystko dzięki użyciu magic z [interceptory AngularJS](https://docs.angularjs.org/api/ng/service/$http), co pozwala adal.js do przekształcania wychodzące i przychodzące komunikaty http.</span><span class="sxs-lookup"><span data-stu-id="76a8c-159">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="76a8c-160">Ponadto adal.js przyjęto założenie, że wszystkie żądania wysyłania do tej samej domeny jako okno należy używać tokeny przeznaczonych dla tego samego Identyfikatora aplikacji jako aplikacji AngularJS.</span><span class="sxs-lookup"><span data-stu-id="76a8c-160">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="76a8c-161">Jest to, dlaczego użyliśmy ten sam identyfikator aplikacji w aplikacji kątowego i interfejsu API REST NodeJS.</span><span class="sxs-lookup"><span data-stu-id="76a8c-161">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="76a8c-162">Oczywiście można zmienić to zachowanie i poinformuj adal.js uzyskać tokenów dla innych interfejsów API REST w razie potrzeby — ale dla tego prostego scenariusza wykona wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="76a8c-162">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="76a8c-163">Oto fragment kodu, który pokazuje, jak łatwo jest wysłać żądania za pomocą tokenów elementu nośnego z usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="76a8c-163">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="76a8c-164">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="76a8c-164">Congratulations!</span></span>  <span data-ttu-id="76a8c-165">Zintegrowane jednej strony aplikacji usługi Azure AD jest teraz ukończona.</span><span class="sxs-lookup"><span data-stu-id="76a8c-165">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="76a8c-166">Teraz, podjąć łuku.</span><span class="sxs-lookup"><span data-stu-id="76a8c-166">Go ahead, take a bow.</span></span>  <span data-ttu-id="76a8c-167">Go może uwierzytelniać użytkowników, bezpiecznie wywołać jej zaplecza interfejsu API REST przy użyciu protokołu OpenID Connect i uzyskać podstawowe informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="76a8c-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="76a8c-168">Fabrycznej obsługuje on każdy użytkownik, osobiste Account Microsoft lub konta pracy/służbowych z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76a8c-168">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="76a8c-169">Uruchom aplikację, a w przeglądarce przejdź do `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="76a8c-169">Run the app, and in a browser navigate to `https://localhost:44326/`.</span></span>  <span data-ttu-id="76a8c-170">Zaloguj się przy użyciu konto robocze/służbowe lub osobiste konto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="76a8c-170">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="76a8c-171">Dodawanie zadań do listy zadań do wykonania użytkownika, a Wyloguj.</span><span class="sxs-lookup"><span data-stu-id="76a8c-171">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="76a8c-172">Spróbuj zalogować się za innego typu konta.</span><span class="sxs-lookup"><span data-stu-id="76a8c-172">Try signing in with the other type of account.</span></span> <span data-ttu-id="76a8c-173">Jeśli potrzebujesz dzierżawa usługi Azure AD do tworzenia użytkowników pracy/służbowe [Dowiedz się, jak uzyskać, w tym miejscu](active-directory-howto-tenant.md) (jest bezpłatna).</span><span class="sxs-lookup"><span data-stu-id="76a8c-173">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="76a8c-174">Aby kontynuować zapoznawanie punktu końcowego v2.0, head z powrotem do naszej [przewodnik dewelopera v2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76a8c-174">To continue learning about the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="76a8c-175">Aby uzyskać dodatkowe zasoby Zobacz:</span><span class="sxs-lookup"><span data-stu-id="76a8c-175">For additional resources, check out:</span></span>

* [<span data-ttu-id="76a8c-176">Przykłady Azure z witryny GitHub >></span><span class="sxs-lookup"><span data-stu-id="76a8c-176">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="76a8c-177">Azure AD na przepełnienie stosu >></span><span class="sxs-lookup"><span data-stu-id="76a8c-177">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="76a8c-178">Dokumentacja usługi Azure AD [witryny Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="76a8c-178">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="76a8c-179">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="76a8c-179">Get security updates for our products</span></span>
<span data-ttu-id="76a8c-180">Firma Microsoft zachęca do przekazywania powiadomień o występujących incydentach zabezpieczeń poprzez wizytę na [tej stronie](https://technet.microsoft.com/security/dd252948) i subskrybowanie Doradczych alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="76a8c-180">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

