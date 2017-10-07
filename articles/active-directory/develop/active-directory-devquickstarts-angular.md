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
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a>Zabezpieczanie aplikacji jednostronicowej AngularJS za pomocą usługi Azure AD

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory (Azure AD) powoduje proste i bezpośrednie dla możesz tooadd logowania, wylogowania i tooyour wywołania bezpiecznego uwierzytelniania OAuth interfejsu API, aplikacji jednej strony.  Umożliwia użytkownikom tooauthenticate aplikacji przy użyciu ich kont usługi Active Directory systemu Windows Server, a korzystanie z dowolnej sieci web interfejsu API usługi Azure AD pozwala to chronić, takich jak hello interfejsami API usługi Office 365 lub hello interfejsu API Azure.

W przypadku aplikacji JavaScript działającego w przeglądarce, usługa Azure AD zapewnia hello Active Directory Authentication Library (ADAL) lub adal.js. jedynym celem adal.js Hello jest toomake go łatwo tooget tokenów dostępu do aplikacji. toodemonstrate Ci, jak łatwo jest, w tym miejscu będzie budujemy tooDo AngularJS listy aplikacji który:

* Loguje użytkownika hello w toohello aplikację za pomocą usługi Azure AD jako dostawcy tożsamości hello.

* Przedstawia niektóre informacje na temat hello użytkownika.
* Bezpieczne wywołania hello tooDo aplikacji interfejsu API listy za pomocą tokenów elementu nośnego z usługi Azure AD.
* Znaki hello użytkownika poza aplikacją hello.

toobuild hello zakończeniu działającą aplikację, musisz:

1. Zarejestrować aplikację w usłudze Azure AD.
2. Zainstaluj biblioteki ADAL i skonfiguruj hello jednostronicowej aplikacji.
3. Użyj strony bezpiecznego ADAL toohelp w hello jednostronicowej aplikacji.

Rozpoczęto, tooget [pobrać szkielet aplikacji hello](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) lub [pobieranie próbki ukończyć powitalnych](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip). Należy również dzierżawa usługi Azure AD można tworzyć użytkowników i zarejestrowanie aplikacji. Jeśli nie masz już dzierżawę, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).

## <a name="step-1-register-hello-directorysearcher-application"></a>Krok 1: Zarejestruj hello DirectorySearcher aplikacji
tooenable użytkownicy tooauthenticate aplikacji i tokeny get, należy najpierw tooregister dzierżawy w usługi Azure AD:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Jeśli użytkownik jest zarejestrowany w katalogach toomultiple, może być konieczne tooensure wyświetlasz hello poprawnym katalogu. toodo tak, na górnym pasku powitania kliknij swoje konto. W obszarze hello **katalogu** wybierz dzierżawy usługi Azure AD hello miejscu tooregister aplikacji.
3. Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.
4. Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.
5. Postępuj zgodnie z monitami hello i utworzyć nową aplikację sieci web i/lub interfejs API sieci web:
  * **Nazwa** opisuje toousers Twojej aplikacji.
  * **Identyfikator Uri przekierowania** jest toowhich lokalizacji hello Azure AD zwróci tokenów. Witaj domyślna lokalizacja dla tego przykładu `https://localhost:44326/`.
6. Po zakończeniu rejestracji usługi Azure AD przypisuje aplikacji Unikatowy identyfikator tooyour aplikacji.  Ta wartość jest potrzebny w kolejnych sekcjach hello, dlatego skopiuj go na karcie aplikacji hello.
7. Adal.js używa toocommunicate niejawnego przepływu OAuth hello z usługą Azure AD. Należy włączyć hello niejawnego przepływu aplikacji:
  1. Kliknij aplikację hello i wybierz **manifestu** tooopen hello wbudowanego manifestu edytora.
  2. Zlokalizuj hello `oauth2AllowImplicitFlow` właściwości. Ustaw dla niego wartość zbyt`true`.
  3. Kliknij przycisk **zapisać** toosave hello manifestu.
8. Przyznaj uprawnienia w dzierżawie dla aplikacji. Przejdź za**ustawienia** > **właściwości** > **wymagane uprawnienia**i kliknij przycisk hello **udzielanie uprawnień**przycisk na górnym pasku hello. Kliknij przycisk **tak** tooconfirm.

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a>Krok 2: Install ADAL i skonfigurować hello jednostronicowej aplikacji
Teraz, gdy masz aplikacji w usłudze Azure AD, można zainstalować adal.js i wpisz swój kod dotyczące tożsamości.

### <a name="configure-hello-javascript-client"></a>Konfigurowanie powitania klienta JavaScript
Rozpocznij, dodając adal.js toohello TodoSPA projektu przy użyciu konsoli Menedżera pakietów hello:
  1. Pobierz [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) i dodaj go toohello `App/Scripts/` katalogu projektu.
  2. Pobierz [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) i dodaj go toohello `App/Scripts/` katalogu projektu.
  3. Ładowanie każdego skryptu przed końcem hello hello `</body>` w `index.html`:

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a>Konfigurowanie serwera zaplecza hello
Tooaccept interfejsu API listy tokenów aplikacji jednej strony hello tooDo zaplecza przy użyciu przeglądarki hello zaplecza hello musi informacji konfiguracyjnych dotyczących rejestracji aplikacji hello. W projekcie TodoSPA hello Otwórz `web.config`. Zastąp wartości hello elementów hello na powitania `<appSettings>` sekcji tooreflect hello wartości, używane w hello portalu Azure. Kod będzie odwoływać tych wartości, przy każdym użyciu biblioteki ADAL.
  * `ida:Tenant`jest hello domeny dzierżawy usługi Azure AD — na przykład contoso.onmicrosoft.com.
  * `ida:Audience`jest hello identyfikator klienta aplikacji, który został skopiowany z portalu hello.

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a>Krok 3: Użyj ADAL toohelp bezpiecznego stron w aplikacji jednej strony hello
Adal.js integruje się z AngularJS trasy i dostawców HTTP, więc bezpiecznego poszczególnych widoków może pomóc w aplikacji jednej strony.

1. W `App/Scripts/app.js`, Przełącz w hello adal.js module:

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. Inicjowanie `adalProvider` przy użyciu wartości konfiguracji hello Twojej rejestracji aplikacji, również w `App/Scripts/app.js`:

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
3. Pomoc bezpiecznego hello `TodoList` widoku w aplikacji hello przy użyciu tylko jeden wiersz kodu: `requireADLogin`.

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a>Podsumowanie
Masz teraz bezpiecznych aplikacji jednej strony, zaloguj się użytkowników i wystawić interfejs API zaplecza tooits żądań chronionego tokenu elementu nośnego. Gdy użytkownik kliknie hello **TodoList** łącza, adal.js spowoduje automatyczne przekierowanie tooAzure AD do logowania w razie potrzeby. Ponadto adal.js automatycznie dołączać dostępu tokenu tooany Ajax żądań wysłania toohello aplikacji zaplecza.  

Witaj powyższych kroków są hello systemu od zera minimalne wymagane toobuild jednostronicowej aplikacji przy użyciu adal.js. Jednak kilka innych funkcji są przydatne w aplikacji jednej strony:

* tooexplicitly wysyłania żądań zalogowania się i wylogowania, funkcji można zdefiniować w kontrolerach, które wywołują adal.js.  W `App/Scripts/homeCtrl.js`:

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
* Możesz toopresent informacje o użytkowniku w Interfejsie użytkownika aplikacji hello. Witaj usługi ADAL został już dodany toohello `userDataCtrl` kontrolera, umożliwi dostęp hello `userInfo` skojarzony obiekt w hello widoku `App/Views/UserData.html`:

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* Istnieje wiele scenariuszy, w których należy tooknow Jeśli hello użytkownik jest zalogowany. Można również użyć hello `userInfo` obiekt toogather te informacje.  Na przykład w `index.html`, można wyświetlić albo hello **logowania** lub **wylogowania** przycisk na podstawie uwierzytelniania stanu:

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

Azure aplikacji jednostronicowej zintegrowanej z usługą AD może uwierzytelniać użytkowników, bezpiecznie wywołać jej zaplecza przy użyciu protokołu OAuth 2.0 i uzyskać podstawowe informacje o użytkowniku hello. Jeśli nie jest jeszcze teraz jest hello toopopulate czas dzierżawy z niektórych użytkowników. Uruchamianie aplikacji jednostronicowej tooDo listy, a następnie zaloguj się przy użyciu jednej z tych użytkowników. Dodawanie listy zadań do wykonania zadania toohello użytkownika, wyloguj się i zaloguj się ponownie.

Adal.js umożliwia łatwe tooincorporate wspólne funkcje tożsamości w aplikacji. Zapewnia obsługę wszystkich prac dirty hello, dla Ciebie: Zarządzanie pamięci podręcznej, obsługa protokołu OAuth, przedstawiający hello użytkownika z logowaniem interfejsu użytkownika, odświeżanie wygaśnięcia tokenów i inne.

Odwołania, jest dostępna w ukończyć powitalnych próbka (bez wartości konfiguracji) [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).

## <a name="next-steps"></a>Następne kroki
Możesz teraz przejść na tooadditional scenariuszy. Może być tootry: [wywołać mechanizmu CORS interfejsu API sieci web z aplikacji jednej strony](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
