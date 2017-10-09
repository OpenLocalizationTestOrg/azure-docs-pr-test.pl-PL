---
title: aaaAzure AD Cordova wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild aplikacji Cordova integruje się z usługą Azure AD, logowania i wywołuje Azure interfejsów API, które są chronione przez usługi AD za pomocą uwierzytelniania OAuth."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a>Integrowanie usługi Azure AD z Apache aplikacji Cordova
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Można użyć oprogramowania Apache Cordova toodevelop HTML5/JavaScript aplikacji, które można uruchamiać na urządzeniach przenośnych jako pełni funkcjonalnymi natywnych aplikacji. Usłudze Azure Active Directory (Azure AD) można dodać aplikacje Cordova tooyour możliwości uwierzytelniania korporacyjnej.

Wtyczka Cordova opakowuje Azure AD natywnych zestawów SDK w systemach iOS, Android, Sklep Windows i Windows Phone. Za pomocą, że dodatek plug-in, można rozszerzyć aplikacji toosupport logowanie przy użyciu kont usługi Active Directory systemu Windows Server użytkowników, uzyskanie dostępu do tooOffice 365 i interfejsów API usługi Azure, a nawet chronić wywołania tooyour własny niestandardowy interfejs API sieci web.

W tym samouczku użyjemy hello Apache Cordova wtyczki dla Active Directory Authentication Library (ADAL) tooimprove prostej aplikacji przez dodanie hello następujące funkcje:

* Przy użyciu kilku wierszy kodu uwierzytelniania użytkownika i uzyskania tokenu.
* Użyj tego tokenu tooinvoke hello interfejsu API programu Graph tooquery tego katalogu i wyświetlić wyniki hello.  
* Użyj hello pamięci podręcznej tokenu ADAL toominimize uwierzytelniania wyświetli monit dla użytkownika hello.

toomake tych ulepszeń, konieczne jest:

1. Zarejestrować aplikację w usłudze Azure AD.
2. Dodaj kod tooyour aplikacji toorequest tokenów.
3. Dodaj token hello toouse kodu na potrzeby zapytań hello interfejsu API programu Graph i wyświetlić wyniki.
4. Utwórz projekt wdrożenia oprogramowania Cordova hello na wszystkich platformach hello mają tootarget, Dodaj hello ADAL Cordova wtyczki i testować rozwiązanie hello w emulatory.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka należy:

* Dzierżawa usługi Azure AD, gdzie masz konto z uprawnieniami rozwoju aplikacji.
* Środowisko deweloperskie, który skonfigurował toouse Apache Cordova.  

Jeśli masz zarówno już skonfigurowany, przejdź bezpośrednio toostep 1.

Jeśli nie masz dzierżawę usługi Azure AD, użyj hello [instrukcje na temat tooget jedną](active-directory-howto-tenant.md).

Jeśli nie masz Apache Cordova na komputerze, należy zainstalować następujące hello:

* [Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.js](https://nodejs.org/download/)
* [Interfejs Cordova CLI](https://cordova.apache.org/) (można łatwo zainstalować za pomocą Menedżera pakietów NPM: `npm install -g cordova`)

Witaj poprzedzających instalacji powinny działać zarówno na powitania komputerze i na powitania Mac.

Każda platforma docelowa ma inne wymagania wstępne:

* toobuild i uruchom aplikację dla komputerów typu Tablet z systemem Windows lub Windows Phone:
  * Zainstaluj [programu Visual Studio 2013 dla systemu Windows z Update 2 lub nowszym](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express lub inna wersja) lub [programu Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).

* toobuild i uruchom aplikację dla systemu iOS:

  * Zainstaluj program Xcode 6.x lub nowszego. Pobierz go z hello [witryny dla deweloperów firmy Apple](http://developer.apple.com/downloads) lub hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).
  * Zainstaluj [ios-sim](https://www.npmjs.org/package/ios-sim). Umożliwia aplikacji systemu iOS toostart w symulatorze systemu iOS z wiersza polecenia hello. (Można łatwo zainstalować ją za pomocą hello terminala: `npm install -g ios-sim`.)
* toobuild i uruchom aplikację dla systemu Android:

  * Zainstaluj [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) lub nowszym. Upewnij się, że `JAVA_HOME` (zmienną środowiskową) jest prawidłowo ustawiona zgodnie z ścieżki instalacji JDK toohello (na przykład C:\Program Files\Java\jdk1.7.0_75).
  * Zainstaluj [zestawu SDK systemu Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) i Dodaj hello `<android-sdk-location>\tools` tooyour lokalizacji (na przykład C:\tools\Android\android-sdk\tools) `PATH` zmiennej środowiskowej.
  * Otwórz Menedżera zestawu SDK systemu Android (na przykład za pośrednictwem hello terminala: `android`) i zainstalować:
    * *5.0.1 systemu android (interfejs API 21)* zestawu SDK platformy
    * *Narzędzia kompilacji zestawu SDK dla systemu android* wersji 19.1.0 lub nowszej
    * *Obsługa systemu android repozytorium* (dodatki)

  Witaj zestawu SDK systemu Android nie zapewnia żadnych domyślne wystąpienie emulatora. Utworzyć, uruchamiając `android avd` z hello terminali, a następnie wybierając **Utwórz**, jeśli chcesz, aby toorun hello aplikacji systemu Android na emulatorze. Zaleca się poziom interfejsu API 19 lub nowszej. Aby uzyskać więcej informacji na temat hello Android opcje emulatora i tworzenia, zobacz [Menedżera AVD](http://developer.android.com/tools/help/avd-manager.html) na powitania witryny systemu Android.

## <a name="step-1-register-an-application-with-azure-ad"></a>Krok 1: Rejestrowanie aplikacji w usłudze Azure AD
Ten krok jest opcjonalny. Ten samouczek zawiera wstępnie przygotowany wartości, których można używać toosee hello przykładowe działanie bez wykonywania żadnych alokacji w własne dzierżawy. Jednak zaleca się wykonać ten krok i zapoznać się z procesem hello, ponieważ będzie wymagane podczas tworzenia własnych aplikacji.

Usługa Azure AD wystawia tokeny tooonly znane aplikacje. Zanim użyjesz usługi Azure AD z aplikacji, należy toocreate wpis dla niego w dzierżawie. tooregister nową aplikację w dzierżawie:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na górnym pasku powitania kliknij swoje konto. W hello **katalogu** wybierz dzierżawy usługi Azure AD hello miejscu tooregister aplikacji.
3. Kliknij przycisk **więcej usług** w lewym okienku hello, a następnie wybierz **usługi Azure Active Directory**.
4. Kliknij przycisk **rejestracji aplikacji**, a następnie wybierz **Dodaj**.
5. Postępuj zgodnie z monitami hello i Utwórz **natywną aplikację kliencką**. (Chociaż aplikacje Cordova HTML na podstawie, tworzymy aplikację native client w tym miejscu. Witaj **natywną aplikację kliencką** musi być zaznaczona opcja lub aplikacji hello nie będzie działać.)
  * **Nazwa** opisuje toousers Twojej aplikacji.
  * **Identyfikator URI przekierowania** jest hello identyfikator URI, który został użyty tooreturn tokenów tooyour aplikacji. Wprowadź **http://MyDirectorySearcherApp**.

Po zakończeniu rejestracji usługi Azure AD przypisuje aplikacji Unikatowy identyfikator tooyour aplikacji. Tę wartość w kolejnych sekcjach hello jest potrzebny. Znajdziesz ją na karcie aplikacji hello hello nowo utworzona aplikacja.

toorun `DirSearchClient Sample`, przyznaj hello nowo utworzona aplikacja uprawnienia tooquery hello Azure AD Graph API:

1. Z hello **ustawienia** wybierz pozycję **wymagane uprawnienia**, a następnie wybierz **Dodaj**.  
2. Hello aplikacji usługi Azure Active Directory, można wybrać **Microsoft Graph** jako hello interfejsu API i Dodaj hello **dostępu do katalogu hello jako hello zalogowanego użytkownika** uprawnienie w obszarze **delegowani Uprawnienia**.  Dzięki temu Twojej hello tooquery aplikacji interfejsu API programu Graph dla użytkowników.

## <a name="step-2-clone-hello-sample-app-repository"></a>Krok 2: Klonuj repozytorium aplikacji przykładowej hello
Z powłoki lub wiersza polecenia wpisz hello następujące polecenie:

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a>Krok 3: Tworzenie aplikacji platformy Cordova hello
Istnieje wiele sposobów toocreate Cordova aplikacji. W tym samouczku użyjemy hello Cordova-interfejsu wiersza polecenia (CLI).

1. Z powłoki lub wiersza polecenia wpisz hello następujące polecenie:

        cordova create DirSearchClient

   To polecenie tworzy hello struktury folderów i funkcją szkieletów dla projektu Cordova hello.

2. Przenieść nowego folderu DirSearchClient toohello:

        cd .\DirSearchClient

3. Skopiuj zawartość hello hello początkowego projektu w podfolderze www hello przy użyciu Menedżera plików lub hello następujące polecenia powłoki:

  * System Windows:`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`
  * Mac:`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`

4. Dodaj dozwolonych hello wtyczki. Jest to konieczne do wywoływania hello interfejsu API programu Graph.

        cordova plugin add cordova-plugin-whitelist

5. Dodaj wszystkie platformy hello, które mają toosupport. toohave próbki roboczej, należy tooexecute co najmniej jeden hello następujące polecenia. Może nie być możliwe tooemulate z systemem iOS w systemie Windows lub emulacji systemu Windows na komputerach Mac.

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. Dodaj hello biblioteki ADAL dla projektu tooyour wtyczki Cordova:

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a>Krok 4: Dodaj kod tooauthenticate użytkowników i uzyskać tokeny z usługi Azure AD
Projektujesz w tym samouczku aplikacji Hello zapewni funkcji wyszukiwania prostego katalogu. Użytkownik Hello może, a następnie wpisz alias hello każdego użytkownika w katalogu hello i wizualizacji niektóre podstawowe atrybuty. Projekt starter Hello zawiera definicję hello hello podstawowy interfejs użytkownika aplikacji hello (w www/index.html) i rusztowania hello, który tworzącej zdarzeń Podstawowa aplikacja cykli powiązania interfejsu użytkownika i powoduje wyświetlanie logikę (www/js/index.js). Witaj zadań tylko dla Ciebie w lewo jest tooadd hello logikę, która implementuje zadania tożsamości.

Witaj najpierw należy toodo w kodzie jest wprowadzenie wartości protokołu hello, używane do identyfikacji aplikacji usługi Azure AD i hello zasoby docelowe. Te wartości będą używane tooconstruct hello token żądania później. Wstaw powitania po fragment u góry pliku index.js hello hello:

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

Witaj `redirectUri` i `clientId` wartości powinna być zgodna hello wartości, które opisują aplikacji w usłudze Azure AD. Można znaleźć od hello **Konfiguruj** karcie hello portalu Azure, zgodnie z opisem w kroku 1 we wcześniejszej części tego samouczka.

> [!NOTE]
> Jeśli zostanie wybrana opcja nie rejestruje nową aplikację w dzierżawie własnych, możesz po prostu wkleić hello wstępnie wartości, ponieważ jest. Możesz sprawdzić hello uruchomiona próbki, że należy zawsze tworzyć własne wejścia dla aplikacji, które są przeznaczone do produkcji.

Następnie dodaj kod, hello żądania tokenu. Wstaw powitania po fragment między hello `search` i `renderData` definicje:

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
Przeanalizujmy tej funkcji, dzieląc go w dwie główne części.
Ten przykład jest zaprojektowana toowork z dowolnej dzierżawy jako min. toobeing powiązane tooa jedna z nich. Używa powitania "/ wspólnej" punktu końcowego, który umożliwia tooenter użytkownika hello dowolne konto podczas uwierzytelniania i kieruje hello żądania toohello dzierżawy, w której należy.

To pierwsza część metody hello sprawdza hello toosee pamięci podręcznej biblioteki ADAL, jeśli token jest już zapisana. Jeśli tak, metoda hello używa dzierżaw hello gdzie hello token pochodzeniu dla ponowne zainicjowanie biblioteki ADAL. To jest konieczne tooavoid dodatkowych monitów, ponieważ hello Użyj "/ wspólnej" zawsze powoduje pytaniem hello tooenter użytkownika, nowe konto.

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
Hello drugiej części hello metoda wykonuje hello odpowiednie żądania tokenu. Hello `acquireTokenSilentAsync` metody wprowadza się ADAL tooreturn token hello określony zasób bez wyświetlania dowolnego UX. Który może się zdarzyć, jeśli hello pamięci podręcznej ma już token dostępu odpowiedniego przechowywane, lub Jeśli token odświeżania mogą być używane tooget nowy token dostępu bez wyświetlania dowolnego wiersza. Jeśli kończy się niepowodzeniem, które firma Microsoft może wrócić `acquireTokenAsync`— które monituje widoczny hello tooauthenticate użytkownika.

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
Teraz, gdy mamy hello token możemy koniec wywołania interfejsu API programu Graph hello i wykonywać zapytania wyszukiwania hello, która ma. Wstaw powitania po fragment poniżej hello `authenticate` definicji:

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
pliki punktu początkowego Hello dostarczona proste UX wprowadzania alias użytkownika w polu tekstowym. Ta metoda używa tego tooconstruct wartości zapytania, połączyć ją z tokenu dostępu hello przesyła tooMicrosoft wykres i przeanalizować hello wyników. Witaj `renderData` metody już istnieje w pliku punktu początkowego hello, zajmuje się wizualizacja wyników hello.

## <a name="step-5-run-hello-app"></a>Krok 5: Uruchamianie aplikacji hello
Aplikacja jest gotowy na koniec toorun. Jego działania jest prosty: po uruchomieniu aplikacji hello wprowadź hello alias użytkownika hello ma toolook w górę, a następnie kliknij przycisk hello. Zostanie wyświetlony monit o uwierzytelnienie. Po pomyślnym uwierzytelnieniu i pomyślne wyszukiwania hello atrybuty użytkownika hello przeszukiwane są wyświetlane.

Kolejnych uruchomieniach wykona wyszukiwania hello bez wyświetlania dowolnego wiersza, dzięki toohello obecności hello wcześniej uzyskać token w pamięci podręcznej.

konkretne kroki Hello do uruchamiania aplikacji hello zależy od platformy.

### <a name="windows-10"></a>Windows 10
   Komputer typu Tablet:`cordova run windows --archs=x64 -- --appx=uap`

   Urządzenie przenośne (wymaga systemu Windows 10 Mobile urządzenie podłączone tooa PC):`cordova run windows --archs=arm -- --appx=uap --phone`

   > [!NOTE]
   > Podczas pierwszego uruchomienia hello może zostać poproszony toosign w licencji dewelopera. Aby uzyskać więcej informacji, zobacz [licencji dewelopera](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-81-tabletpc"></a>Komputer typu Tablet Windows 8.1
   `cordova run windows`

   > [!NOTE]
   > Podczas pierwszego uruchomienia hello może zostać poproszony toosign w licencji dewelopera. Aby uzyskać więcej informacji, zobacz [licencji dewelopera](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-phone-81"></a>Windows Phone 8.1
   toorun na połączonym urządzeniu:`cordova run windows --device -- --phone`

   toorun na powitania emulatorem domyślnym:`cordova emulate windows -- --phone`

   Użyj `cordova run windows --list -- --phone` toosee wszystkich dostępnych elementów docelowych i `cordova run windows --target=<target_name> -- --phone` aplikacji hello toorun określonego urządzenia lub emulatora (na przykład `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).

### <a name="android"></a>Android
   toorun na połączonym urządzeniu:`cordova run android --device`

   toorun na powitania emulatorem domyślnym:`cordova emulate android`

   Upewnij się, że po utworzeniu wystąpienia emulatora za pomocą Menedżera AVD, jak opisano wcześniej w sekcji "Wymagania wstępne" hello.

   Użyj `cordova run android --list` toosee wszystkich dostępnych elementów docelowych i `cordova run android --target=<target_name>` aplikacji hello toorun określonego urządzenia lub emulatora (na przykład `cordova run android --target="Nexus4_emulator"`).

### <a name="ios"></a>iOS
   toorun na połączonym urządzeniu:`cordova run ios --device`

   toorun na powitania emulatorem domyślnym:`cordova emulate ios`

   > [!NOTE]
   > Upewnij się, że masz hello `ios-sim` toorun zainstalowanym pakietem hello emulatora. Aby uzyskać więcej informacji, zobacz hello "wymagania wstępne" sekcji.

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a>Następne kroki
Odwołania, jest dostępna w ukończyć powitalnych próbka (bez wartości konfiguracji) [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).

Możesz teraz scenariusze przeniesienia na toomore Zaawansowane (i inne ciekawe). Może być tootry: [zabezpieczyć interfejs API sieci Web Node.js w usłudze Azure AD](active-directory-devquickstarts-webapi-nodejs.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
