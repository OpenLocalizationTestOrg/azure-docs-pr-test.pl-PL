---
title: wprowadzenie aaaAzure AD w wersji 2.0 .NET AngularJS jednostronicowej aplikacji | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji jednostronicowej kątowego JS logujący się użytkowników z obu osobistych Microsoft kont i pracy lub konta służbowego."
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
ms.openlocfilehash: bd3fc8dce91eb0bedcbfed47a9b3ef52c5568c6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---net"></a><span data-ttu-id="a6dde-103">Dodawanie aplikacji jednej strony AngularJS logowania tooan - .NET</span><span class="sxs-lookup"><span data-stu-id="a6dde-103">Add sign-in tooan AngularJS single page app - .NET</span></span>
<span data-ttu-id="a6dde-104">W tym artykule dodamy Zaloguj się przy użyciu Microsoft zasilane kont tooan AngularJS aplikacji przy użyciu punktu końcowego v2.0 usługi Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="a6dde-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span>  <span data-ttu-id="a6dde-105">punktu końcowego v2.0 Hello pozwala tooperform pojedynczego integracji w aplikacji oraz uwierzytelnianie użytkowników przy użyciu kont osobistych i pracy/służbowe.</span><span class="sxs-lookup"><span data-stu-id="a6dde-105">hello v2.0 endpoint enables you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="a6dde-106">Ten przykład jest prostej aplikacji jednej strony listy zadań do wykonania, która przechowuje zadania w wewnętrznej bazie danych interfejsu API REST, napisane przy użyciu platformy .NET 4.5 MVC hello i chronione za pomocą tokenów elementu nośnego OAuth z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6dde-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using hello .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="a6dde-107">Witaj AngularJS aplikacja będzie używać nasza Biblioteka uwierzytelniania JavaScript typu open source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello znak całego procesu i uzyskać tokeny dla hello wywołania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="a6dde-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="a6dde-108">Witaj tego samego wzorca może być zastosowane tooauthenticate tooother interfejsów API REST, takich jak hello [Microsoft Graph](https://graph.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a6dde-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="a6dde-109">Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="a6dde-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="a6dde-110">toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a6dde-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="a6dde-111">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="a6dde-111">Download</span></span>
<span data-ttu-id="a6dde-112">tooget uruchomiona, będzie konieczne toodownload & Zainstaluj program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6dde-112">tooget started, you'll need toodownload & install Visual Studio.</span></span>  <span data-ttu-id="a6dde-113">Następnie można sklonować lub [Pobierz](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) szkielet aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a6dde-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

<span data-ttu-id="a6dde-114">szkielet aplikacji Hello obejmuje wszystkie hello schematyczny kod służący do prostej aplikacji AngularJS, ale brakuje wszystkie części hello dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="a6dde-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="a6dde-115">Jeśli nie chcesz toofollow wzdłuż, zamiast tego można sklonować lub [Pobierz](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) próbki hello ukończone.</span><span class="sxs-lookup"><span data-stu-id="a6dde-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="a6dde-116">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="a6dde-116">Register an app</span></span>
<span data-ttu-id="a6dde-117">Najpierw utwórz aplikację w hello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a6dde-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="a6dde-118">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="a6dde-118">Make sure to:</span></span>

* <span data-ttu-id="a6dde-119">Dodaj hello **Web** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6dde-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="a6dde-120">Wprowadź poprawny hello **identyfikator URI przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="a6dde-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="a6dde-121">Witaj domyślną w tym przykładzie jest `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="a6dde-121">hello default for this sample is `https://localhost:44326/`.</span></span>
* <span data-ttu-id="a6dde-122">Pozostaw hello **Zezwalaj przepływu niejawnego** pole wyboru jest włączone.</span><span class="sxs-lookup"><span data-stu-id="a6dde-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="a6dde-123">Skopiuj hello **identyfikator aplikacji** tooyour przypisanej aplikacji, będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="a6dde-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="a6dde-124">Zainstaluj adal.js</span><span class="sxs-lookup"><span data-stu-id="a6dde-124">Install adal.js</span></span>
<span data-ttu-id="a6dde-125">toostart, przejdź tooproject, który można pobrać i zainstalować adal.js.</span><span class="sxs-lookup"><span data-stu-id="a6dde-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="a6dde-126">Jeśli masz [bower](http://bower.io/) zainstalowany, możesz po prostu uruchomić to polecenie.</span><span class="sxs-lookup"><span data-stu-id="a6dde-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="a6dde-127">W przypadku niezgodności wersji zależności wystarczy wybrać hello nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="a6dde-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="a6dde-128">Alternatywnie możesz ręcznie pobrać [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) i [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="a6dde-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="a6dde-129">Dodaj oba pliki toohello `app/lib/adal-angular-experimental/dist` katalog hello `TodoSPA` projektu.</span><span class="sxs-lookup"><span data-stu-id="a6dde-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory of hello `TodoSPA` project.</span></span>

<span data-ttu-id="a6dde-130">Teraz Otwórz projekt hello w programie Visual Studio i załadować adal.js na końcu hello treści hello strony głównej:</span><span class="sxs-lookup"><span data-stu-id="a6dde-130">Now open hello project in Visual Studio, and load adal.js at hello end of hello main page's body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="a6dde-131">Konfigurowanie hello interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="a6dde-131">Set up hello REST API</span></span>
<span data-ttu-id="a6dde-132">Gdy konfigurujemy rzeczy, umożliwia działało hello zaplecza interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="a6dde-132">While we're setting things up, let's get hello backend REST API working.</span></span>  <span data-ttu-id="a6dde-133">Witaj katalog główny projektu hello, otwórz `web.config` i Zastąp hello `audience` wartość.</span><span class="sxs-lookup"><span data-stu-id="a6dde-133">In hello root of hello project, open `web.config` and replace hello `audience` value.</span></span>  <span data-ttu-id="a6dde-134">Witaj interfejsu API REST użyje tokenów toovalidate tej wartości, otrzymywanych z aplikacji kątowego hello żądania AJAX.</span><span class="sxs-lookup"><span data-stu-id="a6dde-134">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

<span data-ttu-id="a6dde-135">To wszystko, czas hello zamierzamy toospend omówieniem działania hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="a6dde-135">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="a6dde-136">Możesz wolnego toopoke w kodzie hello, ale jeśli chcesz toolearn więcej informacji na temat zabezpieczania sieci web API z usługi Azure AD, zapoznaj się [w tym artykule](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="a6dde-136">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="a6dde-137">Loguj użytkowników</span><span class="sxs-lookup"><span data-stu-id="a6dde-137">Sign users in</span></span>
<span data-ttu-id="a6dde-138">Czas toowrite kodu tożsamości.</span><span class="sxs-lookup"><span data-stu-id="a6dde-138">Time toowrite some identity code.</span></span>  <span data-ttu-id="a6dde-139">Zwróć uwagę na to już tego adal.js zawiera dostawcy AngularJS, który dobrze odgrywa kątowego mechanizmów routingu.</span><span class="sxs-lookup"><span data-stu-id="a6dde-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="a6dde-140">Rozpocznij od dodania aplikacji toohello adal modułu hello:</span><span class="sxs-lookup"><span data-stu-id="a6dde-140">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="a6dde-141">Teraz można zainicjować hello `adalProvider` za pomocą Identyfikatora aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a6dde-141">You can now initialize hello `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for hello public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // hello 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from hello registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - hello default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="a6dde-142">Doskonałe teraz adal.js ma wszystkie informacje hello musi toosecure użytkownikom aplikację i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="a6dde-142">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="a6dde-143">tooforce logowania dla określonej trasy w aplikacji hello, wszystkie, potrzebny jest jeden wiersz kodu:</span><span class="sxs-lookup"><span data-stu-id="a6dde-143">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that hello user must be logged in tooaccess hello route
})

...
```

<span data-ttu-id="a6dde-144">Teraz, gdy użytkownik kliknie hello `TodoList` łącza, adal.js spowoduje automatyczne przekierowanie tooAzure AD do logowania w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="a6dde-144">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="a6dde-145">Można również jawnie wysyłać żądania logowania i wylogowywania, wywołując adal.js w kontrolerach:</span><span class="sxs-lookup"><span data-stu-id="a6dde-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js hello same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect hello user toosign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect hello user toolog out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="a6dde-146">Wyświetl informacje o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="a6dde-146">Display user info</span></span>
<span data-ttu-id="a6dde-147">Teraz, gdy hello użytkownik jest zalogowany, prawdopodobnie musisz tooaccess hello zalogowanego użytkownika dane uwierzytelniania w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6dde-147">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="a6dde-148">Adal.js udostępnia te informacje dla Ciebie w hello `userInfo` obiektu.</span><span class="sxs-lookup"><span data-stu-id="a6dde-148">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="a6dde-149">tooaccess ten obiekt w widoku, najpierw dodać zakresie głównym toohello adal.js hello odpowiedniego kontrolera:</span><span class="sxs-lookup"><span data-stu-id="a6dde-149">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="a6dde-150">Następnie można bezpośrednio usunąć hello `userInfo` obiektu w tym widoku:</span><span class="sxs-lookup"><span data-stu-id="a6dde-150">Then you can directly address hello `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get hello user's profile information from hello ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="a6dde-151">Można również użyć hello `userInfo` obiektu toodetermine, jeśli hello użytkownik jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="a6dde-151">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use hello ADAL userInfo object tooshow hello right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-hello-rest-api"></a><span data-ttu-id="a6dde-152">Witaj wywołania interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="a6dde-152">Call hello REST API</span></span>
<span data-ttu-id="a6dde-153">Na koniec jest czas tooget niektórych tokeny i wywołanie hello toocreate interfejsu API REST, odczytu, aktualizowania i usuwania zadań.</span><span class="sxs-lookup"><span data-stu-id="a6dde-153">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="a6dde-154">Dobrze wieści.</span><span class="sxs-lookup"><span data-stu-id="a6dde-154">Well guess what?</span></span>  <span data-ttu-id="a6dde-155">Nie masz toodo *przedmiotu*.</span><span class="sxs-lookup"><span data-stu-id="a6dde-155">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="a6dde-156">Adal.js automatycznie zajmie się pobieranie, buforowanie i odświeżanie tokenów.</span><span class="sxs-lookup"><span data-stu-id="a6dde-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="a6dde-157">On również zajmie się dołączanie tych tokenów żądania toooutgoing AJAX wysłanie toohello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="a6dde-157">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="a6dde-158">Dokładnie jak to działa?</span><span class="sxs-lookup"><span data-stu-id="a6dde-158">How exactly does this work?</span></span> <span data-ttu-id="a6dde-159">Jest wszystkich magic toohello Dziękujemy z [interceptory AngularJS](https://docs.angularjs.org/api/ng/service/$http), co pozwala adal.js tootransform wychodzące i przychodzące komunikaty http.</span><span class="sxs-lookup"><span data-stu-id="a6dde-159">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="a6dde-160">Ponadto adal.js przyjęto założenie, że wszystkie żądania, Wyślij toohello tej samej domenie jako okno hello należy używać tokeny przeznaczonych do hello takim samym identyfikatorze jak hello AngularJS aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6dde-160">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="a6dde-161">Dlatego użyliśmy hello tego samego Identyfikatora aplikacji w obu kątowego aplikacji hello i hello NodeJS interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="a6dde-161">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="a6dde-162">Oczywiście możesz zmienić to zachowanie i poinformuj adal.js tooget tokeny dla innych interfejsów API REST w razie potrzeby — ale dla tego prostego scenariusza hello wykona wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="a6dde-162">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="a6dde-163">Oto fragment kodu, który pokazuje, jak łatwo jest toosend żądania za pomocą tokenów elementu nośnego z usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a6dde-163">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="a6dde-164">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="a6dde-164">Congratulations!</span></span>  <span data-ttu-id="a6dde-165">Zintegrowane jednej strony aplikacji usługi Azure AD jest teraz ukończona.</span><span class="sxs-lookup"><span data-stu-id="a6dde-165">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="a6dde-166">Teraz, podjąć łuku.</span><span class="sxs-lookup"><span data-stu-id="a6dde-166">Go ahead, take a bow.</span></span>  <span data-ttu-id="a6dde-167">Go może uwierzytelniać użytkowników, bezpiecznie wywołać jej zaplecza interfejsu API REST przy użyciu protokołu OpenID Connect i uzyskać podstawowe informacje o użytkowniku hello.</span><span class="sxs-lookup"><span data-stu-id="a6dde-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="a6dde-168">Fabrycznej hello obsługuje on każdy użytkownik, osobiste Account Microsoft lub konta pracy/służbowych z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6dde-168">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="a6dde-169">Uruchamianie aplikacji hello, a następnie w przeglądarce Przejdź zbyt`https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="a6dde-169">Run hello app, and in a browser navigate too`https://localhost:44326/`.</span></span>  <span data-ttu-id="a6dde-170">Zaloguj się przy użyciu konto robocze/służbowe lub osobiste konto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a6dde-170">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="a6dde-171">Dodaj do listy zadań do wykonania zadania toohello użytkownika, a Wyloguj.  Spróbuj podpisywania przy użyciu hello innego typu konta.</span><span class="sxs-lookup"><span data-stu-id="a6dde-171">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="a6dde-172">Jeśli potrzebujesz użytkowników usługi Azure AD dzierżawy toocreate pracy/służbowe, [Dowiedz się, jak jeden tutaj tooget](active-directory-howto-tenant.md) (jest bezpłatna).</span><span class="sxs-lookup"><span data-stu-id="a6dde-172">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="a6dde-173">toocontinue poznawania hello końcowym v2.0, head tooour Wstecz [przewodnik dewelopera v2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6dde-173">toocontinue learning about hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="a6dde-174">Aby uzyskać dodatkowe zasoby Zobacz:</span><span class="sxs-lookup"><span data-stu-id="a6dde-174">For additional resources, check out:</span></span>

* [<span data-ttu-id="a6dde-175">Przykłady Azure z witryny GitHub >></span><span class="sxs-lookup"><span data-stu-id="a6dde-175">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="a6dde-176">Azure AD na przepełnienie stosu >></span><span class="sxs-lookup"><span data-stu-id="a6dde-176">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="a6dde-177">Dokumentacja usługi Azure AD [witryny Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="a6dde-177">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="a6dde-178">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="a6dde-178">Get security updates for our products</span></span>
<span data-ttu-id="a6dde-179">Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez wizytę [tę stronę](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.</span><span class="sxs-lookup"><span data-stu-id="a6dde-179">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

