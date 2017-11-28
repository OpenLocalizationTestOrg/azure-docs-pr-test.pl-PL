---
title: aaaAzure AD w wersji 2.0 wprowadzenie aplikacji jednej strony NodeJS AngularJS | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji jednostronicowej kątowego JS logujący się użytkowników z obu osobistych Microsoft kont i pracy lub konta służbowego."
services: active-directory
documentationcenter: 
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: d286aa33-8a94-452f-beb7-ddc6c6daa5c8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 1ab450caf08ab05fba140b94b1b8de652e99cbc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a><span data-ttu-id="3d69c-103">Dodawanie aplikacji jednej strony AngularJS logowania tooan - NodeJS</span><span class="sxs-lookup"><span data-stu-id="3d69c-103">Add sign-in tooan AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="3d69c-104">W tym artykule dodamy Zaloguj się przy użyciu Microsoft zasilane kont tooan AngularJS aplikacji przy użyciu punktu końcowego v2.0 usługi Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="3d69c-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="3d69c-105">punktu końcowego v2.0 Hello pozwalają tooperform pojedynczego integracji w aplikacji i uwierzytelnianie użytkowników przy użyciu kont osobistych i pracy/służbowe.</span><span class="sxs-lookup"><span data-stu-id="3d69c-105">hello v2.0 endpoint enable you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="3d69c-106">Ten przykład jest prostej aplikacji jednej strony listy zadań do wykonania, która przechowuje zadania w wewnętrznej bazie danych interfejsu API REST, napisana w środowisku NodeJS i chronione za pomocą tokenów elementu nośnego OAuth z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d69c-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="3d69c-107">Witaj AngularJS aplikacja będzie używać nasza Biblioteka uwierzytelniania JavaScript typu open source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello znak całego procesu i uzyskać tokeny dla hello wywołania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="3d69c-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="3d69c-108">Witaj tego samego wzorca może być zastosowane tooauthenticate tooother interfejsów API REST, takich jak hello [Microsoft Graph](https://graph.microsoft.com) lub hello interfejsów API usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3d69c-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com) or hello Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="3d69c-109">Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="3d69c-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="3d69c-110">toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="3d69c-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="3d69c-111">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="3d69c-111">Download</span></span>
<span data-ttu-id="3d69c-112">należy uruchomić tooget, toodownload & instalacji [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="3d69c-112">tooget started, you'll need toodownload & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="3d69c-113">Następnie można sklonować lub [Pobierz](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) szkielet aplikacji:</span><span class="sxs-lookup"><span data-stu-id="3d69c-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="3d69c-114">szkielet aplikacji Hello obejmuje wszystkie hello schematyczny kod służący do prostej aplikacji AngularJS, ale brakuje wszystkie części hello dotyczące tożsamości.</span><span class="sxs-lookup"><span data-stu-id="3d69c-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="3d69c-115">Jeśli nie chcesz toofollow wzdłuż, zamiast tego można sklonować lub [Pobierz](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) próbki hello ukończone.</span><span class="sxs-lookup"><span data-stu-id="3d69c-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="3d69c-116">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="3d69c-116">Register an app</span></span>
<span data-ttu-id="3d69c-117">Najpierw utwórz aplikację w hello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="3d69c-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="3d69c-118">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="3d69c-118">Make sure to:</span></span>

* <span data-ttu-id="3d69c-119">Dodaj hello **Web** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3d69c-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="3d69c-120">Wprowadź poprawny hello **identyfikator URI przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="3d69c-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="3d69c-121">Witaj domyślną w tym przykładzie jest `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="3d69c-121">hello default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="3d69c-122">Pozostaw hello **Zezwalaj przepływu niejawnego** pole wyboru jest włączone.</span><span class="sxs-lookup"><span data-stu-id="3d69c-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="3d69c-123">Skopiuj hello **identyfikator aplikacji** tooyour przypisanej aplikacji, będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="3d69c-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="3d69c-124">Zainstaluj adal.js</span><span class="sxs-lookup"><span data-stu-id="3d69c-124">Install adal.js</span></span>
<span data-ttu-id="3d69c-125">toostart, przejdź tooproject, który można pobrać i zainstalować adal.js.</span><span class="sxs-lookup"><span data-stu-id="3d69c-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="3d69c-126">Jeśli masz [bower](http://bower.io/) zainstalowany, możesz po prostu uruchomić to polecenie.</span><span class="sxs-lookup"><span data-stu-id="3d69c-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="3d69c-127">W przypadku niezgodności wersji zależności wystarczy wybrać hello nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="3d69c-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="3d69c-128">Alternatywnie możesz ręcznie pobrać [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) i [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="3d69c-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="3d69c-129">Dodaj oba pliki toohello `app/lib/adal-angular-experimental/dist` katalogu.</span><span class="sxs-lookup"><span data-stu-id="3d69c-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="3d69c-130">Teraz Otwórz projekt hello w w ulubionym edytorze tekstów i załadować adal.js na końcu hello hello treści strony:</span><span class="sxs-lookup"><span data-stu-id="3d69c-130">Now open hello project in your favorite text editor, and load adal.js at hello end of hello page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="3d69c-131">Konfigurowanie hello interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="3d69c-131">Set up hello REST API</span></span>
<span data-ttu-id="3d69c-132">Gdy konfigurujemy rzeczy, umożliwia get hello zaplecza interfejsu API REST pracy.</span><span class="sxs-lookup"><span data-stu-id="3d69c-132">While we're setting things up, lets get hello backend REST API working.</span></span>  <span data-ttu-id="3d69c-133">W wierszu polecenia, instalowanie wszystkich wymaganych pakietów hello uruchamiając (Upewnij się, znajdujesz się w katalogu najwyższego poziomu hello hello projektu):</span><span class="sxs-lookup"><span data-stu-id="3d69c-133">In a command prompt, install all hello necessary packages by running (make sure you're in hello top-level directory of hello project):</span></span>

```
npm install
```

<span data-ttu-id="3d69c-134">Teraz otworzyć `config.js` i Zastąp hello `audience` wartość:</span><span class="sxs-lookup"><span data-stu-id="3d69c-134">Now open `config.js` and replace hello `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="3d69c-135">Witaj interfejsu API REST użyje tokenów toovalidate tej wartości, otrzymywanych z aplikacji kątowego hello żądania AJAX.</span><span class="sxs-lookup"><span data-stu-id="3d69c-135">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>  <span data-ttu-id="3d69c-136">Należy pamiętać, że to prosty interfejs API REST przechowuje dane w pamięci — dzięki czas toostop hello server spowoduje utratę wszystkich zadań utworzonej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="3d69c-136">Note that this simple REST API stores data in-memory - so each time toostop hello server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="3d69c-137">To wszystko, czas hello zamierzamy toospend omówieniem działania hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="3d69c-137">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="3d69c-138">Możesz wolnego toopoke w kodzie hello, ale jeśli chcesz toolearn więcej informacji na temat zabezpieczania sieci web API z usługi Azure AD, zapoznaj się [w tym artykule](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="3d69c-138">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="3d69c-139">Loguj użytkowników</span><span class="sxs-lookup"><span data-stu-id="3d69c-139">Sign users in</span></span>
<span data-ttu-id="3d69c-140">Czas toowrite kodu tożsamości.</span><span class="sxs-lookup"><span data-stu-id="3d69c-140">Time toowrite some identity code.</span></span>  <span data-ttu-id="3d69c-141">Zwróć uwagę na to już tego adal.js zawiera dostawcy AngularJS, który dobrze odgrywa kątowego mechanizmów routingu.</span><span class="sxs-lookup"><span data-stu-id="3d69c-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="3d69c-142">Rozpocznij od dodania aplikacji toohello adal modułu hello:</span><span class="sxs-lookup"><span data-stu-id="3d69c-142">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="3d69c-143">Teraz można zainicjować hello `adalProvider` za pomocą Identyfikatora aplikacji:</span><span class="sxs-lookup"><span data-stu-id="3d69c-143">You can now initialize hello `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="3d69c-144">Doskonałe teraz adal.js ma wszystkie informacje hello musi toosecure użytkownikom aplikację i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="3d69c-144">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="3d69c-145">tooforce logowania dla określonej trasy w aplikacji hello, wszystkie, potrzebny jest jeden wiersz kodu:</span><span class="sxs-lookup"><span data-stu-id="3d69c-145">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="3d69c-146">Teraz, gdy użytkownik kliknie hello `TodoList` łącza, adal.js spowoduje automatyczne przekierowanie tooAzure AD do logowania w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="3d69c-146">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="3d69c-147">Można również jawnie wysyłać żądania logowania i wylogowywania, wywołując adal.js w kontrolerach:</span><span class="sxs-lookup"><span data-stu-id="3d69c-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="3d69c-148">Wyświetl informacje o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="3d69c-148">Display user info</span></span>
<span data-ttu-id="3d69c-149">Teraz, gdy hello użytkownik jest zalogowany, prawdopodobnie musisz tooaccess hello zalogowanego użytkownika dane uwierzytelniania w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3d69c-149">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="3d69c-150">Adal.js udostępnia te informacje dla Ciebie w hello `userInfo` obiektu.</span><span class="sxs-lookup"><span data-stu-id="3d69c-150">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="3d69c-151">tooaccess ten obiekt w widoku, najpierw dodać zakresie głównym toohello adal.js hello odpowiedniego kontrolera:</span><span class="sxs-lookup"><span data-stu-id="3d69c-151">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="3d69c-152">Następnie można bezpośrednio usunąć hello `userInfo` obiektu w tym widoku:</span><span class="sxs-lookup"><span data-stu-id="3d69c-152">Then you can directly address hello `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="3d69c-153">Można również użyć hello `userInfo` obiektu toodetermine, jeśli hello użytkownik jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="3d69c-153">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

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

## <a name="call-hello-rest-api"></a><span data-ttu-id="3d69c-154">Witaj wywołania interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="3d69c-154">Call hello REST API</span></span>
<span data-ttu-id="3d69c-155">Na koniec jest czas tooget niektórych tokeny i wywołanie hello toocreate interfejsu API REST, odczytu, aktualizowania i usuwania zadań.</span><span class="sxs-lookup"><span data-stu-id="3d69c-155">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="3d69c-156">Dobrze wieści.</span><span class="sxs-lookup"><span data-stu-id="3d69c-156">Well guess what?</span></span>  <span data-ttu-id="3d69c-157">Nie masz toodo *przedmiotu*.</span><span class="sxs-lookup"><span data-stu-id="3d69c-157">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="3d69c-158">Adal.js automatycznie zajmie się pobieranie, buforowanie i odświeżanie tokenów.</span><span class="sxs-lookup"><span data-stu-id="3d69c-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="3d69c-159">On również zajmie się dołączanie tych tokenów żądania toooutgoing AJAX wysłanie toohello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="3d69c-159">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="3d69c-160">Dokładnie jak to działa?</span><span class="sxs-lookup"><span data-stu-id="3d69c-160">How exactly does this work?</span></span> <span data-ttu-id="3d69c-161">Jest wszystkich magic toohello Dziękujemy z [interceptory AngularJS](https://docs.angularjs.org/api/ng/service/$http), co pozwala adal.js tootransform wychodzące i przychodzące komunikaty http.</span><span class="sxs-lookup"><span data-stu-id="3d69c-161">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="3d69c-162">Ponadto adal.js przyjęto założenie, że wszystkie żądania, Wyślij toohello tej samej domenie jako okno hello należy używać tokeny przeznaczonych do hello takim samym identyfikatorze jak hello AngularJS aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3d69c-162">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="3d69c-163">Dlatego użyliśmy hello tego samego Identyfikatora aplikacji w obu kątowego aplikacji hello i hello NodeJS interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="3d69c-163">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="3d69c-164">Oczywiście możesz zmienić to zachowanie i poinformuj adal.js tooget tokeny dla innych interfejsów API REST w razie potrzeby — ale dla tego prostego scenariusza hello wykona wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="3d69c-164">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="3d69c-165">Oto fragment kodu, który pokazuje, jak łatwo jest toosend żądania za pomocą tokenów elementu nośnego z usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="3d69c-165">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="3d69c-166">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="3d69c-166">Congratulations!</span></span>  <span data-ttu-id="3d69c-167">Zintegrowane jednej strony aplikacji usługi Azure AD jest teraz ukończona.</span><span class="sxs-lookup"><span data-stu-id="3d69c-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="3d69c-168">Teraz, podjąć łuku.</span><span class="sxs-lookup"><span data-stu-id="3d69c-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="3d69c-169">Go może uwierzytelniać użytkowników, bezpiecznie wywołać jej zaplecza interfejsu API REST przy użyciu protokołu OpenID Connect i uzyskać podstawowe informacje o użytkowniku hello.</span><span class="sxs-lookup"><span data-stu-id="3d69c-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="3d69c-170">Fabrycznej hello obsługuje on każdy użytkownik, osobiste Account Microsoft lub konta pracy/służbowych z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d69c-170">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="3d69c-171">Wypróbuj aplikacji hello uruchamiając:</span><span class="sxs-lookup"><span data-stu-id="3d69c-171">Give hello app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="3d69c-172">W przeglądarce Przejdź zbyt`http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="3d69c-172">In a browser navigate too`http://localhost:8080`.</span></span>  <span data-ttu-id="3d69c-173">Zaloguj się przy użyciu konto robocze/służbowe lub osobiste konto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3d69c-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="3d69c-174">Dodaj do listy zadań do wykonania zadania toohello użytkownika, a Wyloguj.  Spróbuj podpisywania przy użyciu hello innego typu konta.</span><span class="sxs-lookup"><span data-stu-id="3d69c-174">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="3d69c-175">Jeśli potrzebujesz użytkowników usługi Azure AD dzierżawy toocreate pracy/służbowe, [Dowiedz się, jak jeden tutaj tooget](active-directory-howto-tenant.md) (jest bezpłatna).</span><span class="sxs-lookup"><span data-stu-id="3d69c-175">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="3d69c-176">toocontinue poznawania hello hello punktu końcowego v2.0, przejdź wstecz tooour [przewodnik dewelopera v2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3d69c-176">toocontinue learning about hello hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="3d69c-177">Aby uzyskać dodatkowe zasoby Zobacz:</span><span class="sxs-lookup"><span data-stu-id="3d69c-177">For additional resources, check out:</span></span>

* [<span data-ttu-id="3d69c-178">Przykłady Azure z witryny GitHub >></span><span class="sxs-lookup"><span data-stu-id="3d69c-178">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="3d69c-179">Azure AD na przepełnienie stosu >></span><span class="sxs-lookup"><span data-stu-id="3d69c-179">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="3d69c-180">Dokumentacja usługi Azure AD [witryny Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="3d69c-180">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="3d69c-181">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="3d69c-181">Get security updates for our products</span></span>
<span data-ttu-id="3d69c-182">Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez wizytę [tę stronę](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.</span><span class="sxs-lookup"><span data-stu-id="3d69c-182">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

