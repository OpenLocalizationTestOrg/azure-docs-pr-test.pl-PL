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
# <a name="add-sign-in-tooan-angularjs-single-page-app---net"></a>Dodawanie aplikacji jednej strony AngularJS logowania tooan - .NET
W tym artykule dodamy Zaloguj się przy użyciu Microsoft zasilane kont tooan AngularJS aplikacji przy użyciu punktu końcowego v2.0 usługi Azure Active Directory hello.  punktu końcowego v2.0 Hello pozwala tooperform pojedynczego integracji w aplikacji oraz uwierzytelnianie użytkowników przy użyciu kont osobistych i pracy/służbowe.

Ten przykład jest prostej aplikacji jednej strony listy zadań do wykonania, która przechowuje zadania w wewnętrznej bazie danych interfejsu API REST, napisane przy użyciu platformy .NET 4.5 MVC hello i chronione za pomocą tokenów elementu nośnego OAuth z usługi Azure AD.  Witaj AngularJS aplikacja będzie używać nasza Biblioteka uwierzytelniania JavaScript typu open source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello znak całego procesu i uzyskać tokeny dla hello wywołania interfejsu API REST.  Witaj tego samego wzorca może być zastosowane tooauthenticate tooother interfejsów API REST, takich jak hello [Microsoft Graph](https://graph.microsoft.com).

> [!NOTE]
> Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.  toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download"></a>Do pobrania
tooget uruchomiona, będzie konieczne toodownload & Zainstaluj program Visual Studio.  Następnie można sklonować lub [Pobierz](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) szkielet aplikacji:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

szkielet aplikacji Hello obejmuje wszystkie hello schematyczny kod służący do prostej aplikacji AngularJS, ale brakuje wszystkie części hello dotyczące tożsamości.  Jeśli nie chcesz toofollow wzdłuż, zamiast tego można sklonować lub [Pobierz](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) próbki hello ukończone.

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a>Rejestracja aplikacji
Najpierw utwórz aplikację w hello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj następujące [szczegółowe kroki](active-directory-v2-app-registration.md).  Upewnij się, że:

* Dodaj hello **Web** platformy aplikacji.
* Wprowadź poprawny hello **identyfikator URI przekierowania**. Witaj domyślną w tym przykładzie jest `https://localhost:44326/`.
* Pozostaw hello **Zezwalaj przepływu niejawnego** pole wyboru jest włączone. 

Skopiuj hello **identyfikator aplikacji** tooyour przypisanej aplikacji, będzie on potrzebny później. 

## <a name="install-adaljs"></a>Zainstaluj adal.js
toostart, przejdź tooproject, który można pobrać i zainstalować adal.js.  Jeśli masz [bower](http://bower.io/) zainstalowany, możesz po prostu uruchomić to polecenie.  W przypadku niezgodności wersji zależności wystarczy wybrać hello nowszej wersji.

```
bower install adal-angular#experimental
```

Alternatywnie możesz ręcznie pobrać [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) i [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).  Dodaj oba pliki toohello `app/lib/adal-angular-experimental/dist` katalog hello `TodoSPA` projektu.

Teraz Otwórz projekt hello w programie Visual Studio i załadować adal.js na końcu hello treści hello strony głównej:

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a>Konfigurowanie hello interfejsu API REST
Gdy konfigurujemy rzeczy, umożliwia działało hello zaplecza interfejsu API REST.  Witaj katalog główny projektu hello, otwórz `web.config` i Zastąp hello `audience` wartość.  Witaj interfejsu API REST użyje tokenów toovalidate tej wartości, otrzymywanych z aplikacji kątowego hello żądania AJAX.

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

To wszystko, czas hello zamierzamy toospend omówieniem działania hello interfejsu API REST.  Możesz wolnego toopoke w kodzie hello, ale jeśli chcesz toolearn więcej informacji na temat zabezpieczania sieci web API z usługi Azure AD, zapoznaj się [w tym artykule](active-directory-v2-devquickstarts-dotnet-api.md). 

## <a name="sign-users-in"></a>Loguj użytkowników
Czas toowrite kodu tożsamości.  Zwróć uwagę na to już tego adal.js zawiera dostawcy AngularJS, który dobrze odgrywa kątowego mechanizmów routingu.  Rozpocznij od dodania aplikacji toohello adal modułu hello:

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

Teraz można zainicjować hello `adalProvider` za pomocą Identyfikatora aplikacji:

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

Doskonałe teraz adal.js ma wszystkie informacje hello musi toosecure użytkownikom aplikację i zaloguj się.  tooforce logowania dla określonej trasy w aplikacji hello, wszystkie, potrzebny jest jeden wiersz kodu:

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

Teraz, gdy użytkownik kliknie hello `TodoList` łącza, adal.js spowoduje automatyczne przekierowanie tooAzure AD do logowania w razie potrzeby.  Można również jawnie wysyłać żądania logowania i wylogowywania, wywołując adal.js w kontrolerach:

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

## <a name="display-user-info"></a>Wyświetl informacje o użytkowniku
Teraz, gdy hello użytkownik jest zalogowany, prawdopodobnie musisz tooaccess hello zalogowanego użytkownika dane uwierzytelniania w aplikacji.  Adal.js udostępnia te informacje dla Ciebie w hello `userInfo` obiektu.  tooaccess ten obiekt w widoku, najpierw dodać zakresie głównym toohello adal.js hello odpowiedniego kontrolera:

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

Następnie można bezpośrednio usunąć hello `userInfo` obiektu w tym widoku: 

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

Można również użyć hello `userInfo` obiektu toodetermine, jeśli hello użytkownik jest zalogowany.

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

## <a name="call-hello-rest-api"></a>Witaj wywołania interfejsu API REST
Na koniec jest czas tooget niektórych tokeny i wywołanie hello toocreate interfejsu API REST, odczytu, aktualizowania i usuwania zadań.  Dobrze wieści.  Nie masz toodo *przedmiotu*.  Adal.js automatycznie zajmie się pobieranie, buforowanie i odświeżanie tokenów.  On również zajmie się dołączanie tych tokenów żądania toooutgoing AJAX wysłanie toohello interfejsu API REST.  

Dokładnie jak to działa? Jest wszystkich magic toohello Dziękujemy z [interceptory AngularJS](https://docs.angularjs.org/api/ng/service/$http), co pozwala adal.js tootransform wychodzące i przychodzące komunikaty http.  Ponadto adal.js przyjęto założenie, że wszystkie żądania, Wyślij toohello tej samej domenie jako okno hello należy używać tokeny przeznaczonych do hello takim samym identyfikatorze jak hello AngularJS aplikacji.  Dlatego użyliśmy hello tego samego Identyfikatora aplikacji w obu kątowego aplikacji hello i hello NodeJS interfejsu API REST.  Oczywiście możesz zmienić to zachowanie i poinformuj adal.js tooget tokeny dla innych interfejsów API REST w razie potrzeby — ale dla tego prostego scenariusza hello wykona wartości domyślnych.

Oto fragment kodu, który pokazuje, jak łatwo jest toosend żądania za pomocą tokenów elementu nośnego z usługi Azure AD:

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

Gratulacje!  Zintegrowane jednej strony aplikacji usługi Azure AD jest teraz ukończona.  Teraz, podjąć łuku.  Go może uwierzytelniać użytkowników, bezpiecznie wywołać jej zaplecza interfejsu API REST przy użyciu protokołu OpenID Connect i uzyskać podstawowe informacje o użytkowniku hello.  Fabrycznej hello obsługuje on każdy użytkownik, osobiste Account Microsoft lub konta pracy/służbowych z usługi Azure AD.  Uruchamianie aplikacji hello, a następnie w przeglądarce Przejdź zbyt`https://localhost:44326/`.  Zaloguj się przy użyciu konto robocze/służbowe lub osobiste konto Microsoft.  Dodaj do listy zadań do wykonania zadania toohello użytkownika, a Wyloguj.  Spróbuj podpisywania przy użyciu hello innego typu konta. Jeśli potrzebujesz użytkowników usługi Azure AD dzierżawy toocreate pracy/służbowe, [Dowiedz się, jak jeden tutaj tooget](active-directory-howto-tenant.md) (jest bezpłatna).

toocontinue poznawania hello końcowym v2.0, head tooour Wstecz [przewodnik dewelopera v2.0](active-directory-appmodel-v2-overview.md).  Aby uzyskać dodatkowe zasoby Zobacz:

* [Przykłady Azure z witryny GitHub >>](https://github.com/Azure-Samples)
* [Azure AD na przepełnienie stosu >>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* Dokumentacja usługi Azure AD [witryny Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)

## <a name="get-security-updates-for-our-products"></a>Pobierz aktualizacje zabezpieczeń naszych produktów
Firma Microsoft zachęca tooget powiadomień o występujących incydentach zabezpieczeń poprzez wizytę [tę stronę](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.

