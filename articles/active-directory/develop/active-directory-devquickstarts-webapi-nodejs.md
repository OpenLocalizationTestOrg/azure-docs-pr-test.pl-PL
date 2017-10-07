---
title: aaaAzure AD Node.js wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild interfejsu API sieci web Node.js REST który integruje się z usługą Azure AD do uwierzytelniania."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a>Rozpoczynanie pracy z interfejsów API sieci web dla środowiska Node.js
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

*Passport* to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js. Elastyczne i moduły, usługa Passport można było porzucić dyskretnie w tooany ekspresowe lub Restify aplikacji sieci web. Kompleksowy zestaw strategii obsługuje uwierzytelnianie za pomocą nazwy użytkownika i hasła, Facebook i Twitter. Opracowaliśmy strategię dla Microsoft Azure Active Directory (Azure AD). Firma Microsoft zainstalowaniu tego modułu, a następnie dodaj hello Microsoft Azure Active Directory `passport-azure-ad` wtyczki.

toodo, musisz:

1. Zarejestrować aplikację w usłudze Azure AD.
2. Konfigurowanie Twojej aplikacji toouse Passport w `passport-azure-ad` wtyczki.
3. Konfigurowanie klienta aplikacji toocall hello tooDo listy składnika web API.

Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).

> [!NOTE]
> W tym artykule nie opisano sposobu tooimplement logowania, rejestracji, lub profilu zarządzania za pomocą usługi Azure AD B2C. Uwzględniono w szczególności wywoływania interfejsów API sieci web po hello użytkownik jest już uwierzytelniony.  Zalecamy rozpocząć od [jak toointegrate przy użyciu usługi Azure Active Directory dokumentów](active-directory-how-to-integrate.md) toolearn o hello podstawy usługi Azure Active Directory.
>
>

Tak zostały opublikowane wszystkie hello kodu źródłowego w tym przykładzie uruchomionej w usłudze GitHub w ramach licencji MIT uznać wolnego tooclone (lub nawet lepiej rozwidlenia) i wyrazić swoją opinię i żądań ściągnięcia.

## <a name="about-nodejs-modules"></a>O modułach Node.js
Używamy modułów programu Node.js w tym przewodniku. Moduły są obciążana pakiety języka JavaScript, które zapewniają określonych funkcji aplikacji. Zazwyczaj należy zainstalować moduły przy użyciu hello Node.js NPM narzędzia wiersza polecenia w katalogu instalacji NPM hello. Jednak niektóre moduły, takich jak moduł HTTP hello, znajdują się w pakiecie Node.js core hello.

Zainstalowane moduły są zapisywane w hello **node_modules** katalogu głównego hello katalogu instalacji środowiska Node.js. Każdy moduł w hello **node_modules** directory zachowuje własną **node_modules** katalog, który zawiera wszystkie moduły, których ona zależy. Ponadto każdego wymaganego modułu jest **node_modules** katalogu. Ta struktura katalogów cykliczne reprezentuje hello łańcuch zależności.

Ta struktura łańcuch zależności powoduje większe zużycie aplikacji. Jednak gwarantuje również to, że spełniono wszystkie zależności i tej wersji hello hello modułów, która jest używana do rozwoju jest również używane w środowisku produkcyjnym. To zapewnia bardziej przewidywalne zachowanie aplikacji hello produkcji i zapobiega problemom z wersjami, które mogą mieć wpływ na użytkowników.

## <a name="step-1-register-an-azure-ad-tenant"></a>Krok 1: Zarejestruj dzierżawę usługi Azure AD
toouse to przykładowe, potrzebujesz dzierżawy usługi Azure Active Directory. Jeśli nie masz pewności, jakie dzierżawcy jest lub tooget, zobacz temat [jak dzierżawy tooget usługi Azure AD](active-directory-howto-tenant.md).

## <a name="step-2-create-an-application"></a>Krok 2: Tworzenie aplikacji
Następnie utwórz aplikację w katalogu, że informacji zapewnia usługi Azure AD, że wymaga ona toosecurely komunikować się z aplikacją.  Zarówno powitania klienta aplikacji, jak i interfejs API sieci web są reprezentowane przez jeden **identyfikator aplikacji** w tym przypadku, ponieważ stanowią jedną aplikację logiczną.  toocreate usługi aplikacji, wykonaj [tych instrukcji](active-directory-how-applications-are-added.md). Jeśli tworzysz aplikację z biznesowych, [te dodatkowe instrukcje mogą okazać się przydatne](../active-directory-applications-guiding-developers-for-lob-applications.md).

toocreate aplikacji:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. W menu u góry hello wybierz konto. Następnie w obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, w którym ma tooregister aplikacji.

3. W menu hello powitania po lewej stronie wybierz **więcej usług**, a następnie wybierz **usługi Azure Active Directory**.

4. Wybierz **rejestracji aplikacji**, a następnie wybierz **Dodaj**.

5. Wykonaj hello monity toocreate **aplikacji sieci Web i/lub WebAPI**.

      * Witaj **nazwa** aplikacji hello opisuje użytkownikom tooend aplikacji.

      * Witaj **adres URL logowania** jest hello podstawowy adres URL aplikacji.  Witaj domyślny adres URL hello przykładowy kod to `https://localhost:8080`.

6. Po zarejestrowaniu, usługi Azure AD przypisuje aplikacji Unikatowy identyfikator aplikacji. Potrzebujesz tej wartości w kolejnych sekcjach hello, dlatego skopiuj go ze strony aplikacji hello.

7. Z hello **ustawienia** -> **właściwości** strony dla aplikacji, aktualizacji hello identyfikator URI aplikacji. Witaj **identyfikator URI aplikacji** to unikatowy identyfikator aplikacji. Konwencja Hello jest toouse `https://<tenant-domain>/<app-name>`, na przykład: `https://contoso.onmicrosoft.com/my-first-aad-app`.

8. Utwórz **klucza** dla aplikacji hello **ustawienia** strony, a następnie skopiuj go innym. Będzie on potrzebny później.

## <a name="step-3-download-nodejs-for-your-platform"></a>Krok 3: Pobieranie środowiska Node.js dla danej platformy
toosuccessfully korzystać z tej próbki, należy dysponować działającą instalacją środowiska node.js.

Zainstaluj środowisko Node.js z [http://nodejs.org](http://nodejs.org).

## <a name="step-4-install-mongodb-on-your-platform"></a>Krok 4: Instalacja bazy danych MongoDB na platformie
toosuccessfully korzystać z tej próbki, należy dysponować działającą instalacją bazy danych mongodb. Możesz użyć bazy danych MongoDB toomake hello trwałego interfejsu API REST w wystąpieniach serwera.

Instalowanie bazy danych MongoDB z [http://mongodb.org](http://www.mongodb.org).

> [!NOTE]
> W tym przewodniku zakłada, że można używać hello domyślnej instalacji serwera punktów końcowych i bazy danych mongodb, który w czasie hello pisania tego dokumentu jest mongodb://localhost.
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a>Krok 5: Instalowanie modułów Restify hello w interfejsie API sieci web
Użyto Restify toobuild interfejsie API REST. Restify jest minimalną i elastyczną Node.js aplikacji platforma, która jest pochodną Express. Oferuje rozbudowany zestaw funkcji do tworzenia interfejsów API REST na bazie usługi Connect.

### <a name="install-restify"></a>Instalacja modułu Restify
1. W wierszu polecenia hello Zmień katalogi toohello **azuread** katalogu. Jeśli hello **azuread** katalog nie istnieje, utwórz go.

        `cd azuread - or- mkdir azuread; cd azuread`

2. Wpisz następujące polecenie hello:

    `npm install restify`

    To polecenie powoduje zainstalowanie modułu Restify.

#### <a name="did-you-get-an-error"></a>Czy został wyświetlony komunikat o błędzie?
Korzystając z programu NPM w niektórych systemach operacyjnych, zostanie zgłoszony błąd informujący o **błąd: EPERM, chmod "/ usr/lokalnej/bin /..."** i sugestię wypróbować uruchomionych hello konta z uprawnieniami administratora. W takim przypadku należy użyć toorun polecenia sudo hello NPM na wyższym poziomie uprawnień.

#### <a name="did-you-get-an-error-regarding-dtrace"></a>Czy został wyświetlony błąd dotyczący narzędzia DTRACE?
Podczas instalowania modułu Restify mogą pojawić następujący błąd:

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```
Moduł Restify zapewnia zaawansowany mechanizm śledzenia wywołań REST przy użyciu narzędzia DTrace. Jednak wiele systemów operacyjnych bez narzędzia DTrace. Można te błędy bezpiecznie zignorować.

dane wyjściowe tego polecenia Hello powinien wyglądać podobnie toohello następujące dane wyjściowe:

    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0 (mv@0.0.5)


## <a name="step-6-install-passportjs-in-your-web-api"></a>Krok 6: Zainstaluj Passport.js w interfejsie API sieci web
[Passport](http://passportjs.org/) to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js. Elastyczne i moduły, usługa Passport można było porzucić dyskretnie w tooany ekspresowe lub Restify aplikacji sieci web. Kompleksowy zestaw strategii obsługuje uwierzytelnianie za pomocą nazwy użytkownika i hasła, Facebook i Twitter.

Opracowaliśmy strategię dla usługi Azure Active Directory. Firma Microsoft zainstalowaniu tego modułu, a następnie dodaj hello Azure Active Directory wtyczki.

1. W wierszu polecenia hello Zmień katalogi toohello **azuread** katalogu.

2. tooinstall passport.js, wprowadź następujące polecenie hello:

    `npm install passport`

    Hello dane wyjściowe polecenia hello powinien wyglądać podobnie toohello następujące:

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a>Krok 7: Dodawanie interfejsu API sieci web tooyour Passport-Azure-AD
Następnie dodamy hello strategię OAuth przy użyciu `passport-azure-ad`, zestawu strategii łączących tooPassport usługi Azure Active Directory. Używamy tej strategii do tokenów elementów nośnych w próbce tego interfejsu API REST.

> [!NOTE]
> Chociaż protokół OAuth2 zapewnia framework, w którym mogą być wystawiane dowolnego znanego typu tokenu, tylko niektóre typy tokenów są często używane. Tokeny elementów nośnych są tokeny hello najczęściej używane do ochrony punktów końcowych. Są one hello najczęściej wystawiony typ tokenu protokołu OAuth2. W wielu wdrożeniach zakłada, że tokeny elementów nośnych są jedynym typem hello tokeny wystawione.
>
>

W wierszu polecenia hello Zmień katalogi toohello **azuread** katalogu.

Typ hello następujące polecenie tooinstall hello Passport.js `passport-azure-ad module`:

`npm install passport-azure-ad`

dane wyjściowe Hello hello polecenia powinny wyglądać podobnie toohello następujące dane wyjściowe:


    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a>Krok 8: Dodawanie bazy danych MongoDB modułów tooyour — interfejs API sieci web
Korzystamy z bazy danych MongoDB jako naszego magazynu danych. Z tego powodu należy tooinstall hello powszechnie używane wtyczki o nazwie modele toomanage Mongoose i schematów. Należy również sterownik bazy danych hello tooinstall bazy danych mongodb (nazywane również bazy danych MongoDB).

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a>Krok 9: Instalowanie dodatkowych modułów
Następnej instalacji hello pozostałe wymagane moduły.

1. W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje.

    `cd azuread`

2. Wprowadź następujące polecenia tooinstall hello tych modułów w Twojej **node_modules** katalogu:

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a>Krok 10: Tworzenie server.js własnymi zależnościami
pliku server.js Hello zapewnia większość funkcji powitania serwera interfejsu API sieci web. Możemy dodać większość naszego kodu toothis pliku. Do celów produkcyjnych zaleca się, że Refaktoryzuj hello funkcje na mniejsze pliki, np. odrębne trasy i kontrolery. Z tego pokazu używamy server.js dla tej funkcji.

1. W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje.

    `cd azuread`

2. Utwórz `server.js` plik w edytorze Ulubione, a następnie dodaj hello następujących informacji:

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. Zapisz plik hello. Wkrótce zostanie zwrócona tooit.

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a>Krok 11: Tworzenie toostore pliku konfiguracji ustawień usługi Azure AD
Ten plik kodu przekazuje parametry konfiguracji hello z Twojej tooPassport.js portalu usługi Azure Active Directory. Te wartości konfiguracji są tworzone po dodaniu portalu toohello interfejsu API sieci web hello w pierwszej części przewodnika hello hello. Po skopiowaniu kodu hello prezentujemy zasady jakie tooput hello wartości tych parametrów.

1. W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje.

    `cd azuread`

2. Utwórz `config.js` plik w edytorze Ulubione, a następnie dodaj hello następujących informacji:

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. Zapisz plik hello.

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a>Krok 12: Dodaj plik server.js tooyour wartości konfiguracji
Potrzebujemy tooread te wartości z pliku .config hello, który został utworzony w naszej aplikacji. toodo, możemy dodać pliku .config hello jako wymagany zasób w naszej aplikacji. Następnie możemy ustawić hello zmienne globalne toomatch hello zmiennych w dokumencie config.js hello.

1. W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje.

    `cd azuread`

2. Otwórz z `server.js` plik w edytorze Ulubione, a następnie dodaj hello następujących informacji:

    ```Javascript
    var config = require('./config');
    ```
3. Następnie dodaj nową sekcję zbyt`server.js` z hello następującego kodu:

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. Zapisz plik hello.

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Krok 13: Dodawanie hello informacje o modelu bazy danych MongoDB i schematu przy użyciu wtyczki Mongoose
Teraz tego przygotowania jest będzie toostart płatności, ponieważ połączono tych trzech plików w ramach usługi interfejsu API REST.

W ramach tego przewodnika korzystamy z bazy danych MongoDB toostore nasze zadania zgodnie z opisem w kroku 4.

W hello `config.js` pliku, że utworzyliśmy krok 11, dzwoniliśmy do naszej bazie danych `tasklist`, ponieważ został który testujemy na końcu hello naszych **mogoose_auth_local** adres URL połączenia. Nie trzeba toocreate tej bazy danych wcześniej w module MongoDB. Zamiast tego bazy danych MongoDB tworzy to firmie Microsoft na powitania najpierw uruchom naszej aplikacji serwera (przy założeniu, że hello bazy danych już nie istnieje).

Teraz, gdy mamy już informację powitania serwera bazy danych MongoDB chcielibyśmy toouse, potrzebujemy toowrite niektóre dodatkowy kod toocreate hello modelu i schematu dla naszego serwera zadań.

### <a name="discussion-of-hello-model"></a>Omówienie modelu hello
Nasz model schematu jest proste. Rozwiń go zgodnie z potrzebami.

Nazwa: Nazwa hello hello osoby, która jest przypisana toohello zadań. A **ciąg**.

ZADANIE: hello samo zadanie. A **ciąg**.

Data: hello Data zadania hello jest ukończenia. A **DATETIME**.

UKOŃCZONE: Jeśli hello zadanie zostało zakończone lub nie. A **LOGICZNA**.

### <a name="creating-hello-schema-in-hello-code"></a>Tworzenie schematu hello w kodzie hello
1. W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje.

    `cd azuread`

2. Otwórz z `server.js` plik w edytorze Ulubione, a następnie dodaj następujące informacje poniżej pozycji konfiguracji hello hello:

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
    var TaskSchema = new Schema({
        owner: String,
        task: String,
        completed: Boolean,
        date: Date
    });

    // Use hello schema tooregister a model.
    mongoose.model('Task', TaskSchema);
    var Task = mongoose.model('Task');
    ```
Jak stwierdzić, z kodu hello, utworzymy naszych schematu najpierw. Następnie utworzymy obiektu modelu, który używamy toostore naszych danych w całym hello kodu podczas definiujemy naszych **tras**.

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a>Krok 14: Dodawanie naszych tras do serwera zadań interfejsu API REST
Teraz, gdy mamy toowork modelu bazy danych, z Dodajmy trasy hello pracujemy będzie używana dla serwera interfejsu API REST.

### <a name="about-routes-in-restify"></a>Informacje o trasach w module Restify
Trasy działają w Restify hello sam sposób ich w hello Express stosu. Trasy są definiowane za pomocą hello spodziewać się powitania klienta aplikacji toocall identyfikatora URI. Zazwyczaj należy zdefiniować trasy w oddzielnym pliku. W celach naszych testujemy naszych trasy w pliku server.js hello. Firma Microsoft zaleca współczynnika te trasy do ich własnych plików do użytku produkcyjnego.

Typowy wzorzec trasy modułu Restify jest następujący:

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


Jest to wzorzec hello na najbardziej podstawowym poziomie. Moduły restify (i Express) podaj znacznie bardziej złożone funkcje, takie jak Definiowanie typów aplikacji i zapewnianie złożonego routingu przez różne punkty końcowe. Dla naszych celów możemy utrzymują te trasy proste.

### <a name="add-default-routes-tooour-server"></a>Dodaj serwer tooour trasy domyślnej
Teraz możemy dodać podstawowe trasy CRUD hello tworzenie, pobieranie, aktualizacji i usunąć.

1. W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje:

    `cd azuread`

2. Otwórz hello `server.js` plik w edytorze Ulubione, a następnie dodaj następujące informacje poniżej hello poprzednie wpisy w bazie danych, które należy podjąć hello:

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();

    _task.save(function(err) {
        if (err) {
            req.log.warn(err, 'createTask: unable toosave');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}


// Delete a task by name.

function removeTask(req, res, next) {

    Task.remove({
        task: req.params.task,
        owner: owner
    }, function(err) {
        if (err) {
            req.log.warn(err,
                'removeTask: unable toodelete %s',
                req.params.task);
            next(err);
        } else {
            log.info('Deleted task:', req.params.task);
            res.send(204);
            next();
        }
    });
}

// Delete all tasks.

function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
}


// Get a specific task based on name.

function getTask(req, res, next) {

    log.info('getTask was called for: ', owner);
    Task.find({
        owner: owner
    }, function(err, data) {
        if (err) {
            req.log.warn(err, 'get: unable tooread %s', owner);
            next(err);
            return;
        }

        res.json(data);
    });

    return next();
}

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
        }

        if (!owner) {
            log.warn(err, "You did not pass an owner when listing tasks.");
        } else {

            res.json(data);

        }
    });

    return next();
}

```

### <a name="add-error-handling-in-our-apis"></a>Dodawanie obsługi błędów w naszych interfejsów API
```

///--- Errors for communicating something interesting back toohello client.

function MissingTaskError() {
    restify.RestError.call(this, {
        statusCode: 409,
        restCode: 'MissingTask',
        message: '"task" is a required parameter',
        constructorOpt: MissingTaskError
    });

    this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);


function TaskExistsError(owner) {
    assert.string(owner, 'owner');

    restify.RestError.call(this, {
        statusCode: 409,
        restCode: 'TaskExists',
        message: owner + ' already exists',
        constructorOpt: TaskExistsError
    });

    this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);


function TaskNotFoundError(owner) {
    assert.string(owner, 'owner');

    restify.RestError.call(this, {
        statusCode: 404,
        restCode: 'TaskNotFound',
        message: owner + ' was not found',
        constructorOpt: TaskNotFoundError
    });

    this.name = 'TaskNotFoundError';
}

util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="step-15-create-your-server"></a>Krok 15: Tworzenie serwera
Zdefiniowanych naszej bazie danych i naszych tras na miejscu. Hello ostatni element toodo jest dodać hello wystąpienia serwera zarządzającego naszych wywołania.

Restify (i Express) można zrobić dużo dostosowania do serwera interfejsu API REST, ale ponownie za chwilę toouse hello najbardziej podstawowa konfiguracja dla naszych celów.

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a>Krok 16: Dodawanie hello tras toohello serwera (bez uwierzytelniania obecnie)
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler.
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a>Kroku 17: Serwer hello uruchamiania (przed dodaniem obsługi protokołu OAuth)
Przetestowanie serwera przed dodamy uwierzytelniania.

Witaj Najprostszym sposobem tootest serwera jest przy użyciu programu curl w wierszu polecenia. Zanim przejdziemy, potrzebujemy narzędzie, które pozwala nam tooparse danych wyjściowych w formacie JSON.

1. Zainstaluj powitania po narzędzie JSON (hello wszystkie następujące przykłady narzędzie to):

    `$npm install -g jsontool`

    Spowoduje to zainstalowanie narzędzie JSON hello globalnie. Teraz, gdy firma Microsoft już osiągnąć, który, teraz odtworzyć z serwerem hello:

2. Najpierw upewnij się, że wystąpienie bazy danych mongoDB jest uruchomione:

    `$sudo mongod`

3. Następnie zmień katalog toohello i uruchomić curling:

    `$ cd azuread` `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4. Następnie można dodać zadania w ten sposób:

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    odpowiedź Hello powinny być:

        ```Shell
        HTTP/1.1 201 Created
        Connection: close
        Access-Control-Allow-Origin: *
        Access-Control-Allow-Headers: X-Requested-With
        Content-Type: application/x-www-form-urlencoded
        Content-Length: 5
        Date: Tue, 04 Feb 2014 01:02:26 GMT
        Hello
        ```
    I można utworzyć listę zadań dla Brandon w ten sposób:

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Jeśli wszystko to działa, jesteśmy serwera interfejsu API REST toohello OAuth tooadd gotowe.

Masz serwera interfejsu API REST z bazy danych MongoDB.

## <a name="step-18-add-authentication-tooour-rest-api-server"></a>Krok 18: Dodawanie serwera interfejsu API REST tooour uwierzytelniania
Teraz, gdy będziemy mieć uruchomiony interfejs API REST, Zacznijmy przydatne z usługą Azure AD.

W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje.

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Użyj hello OIDCBearerStrategy dołączonej usługi passport-azure-ad
Do tej pory nawiązaliśmy typowy serwer REST TODO bez żadnej autoryzacji. Jest to, gdzie Rozpoczniemy, który zestawienie.

1. Najpierw należy tooindicate czy chcemy toouse Passport. To prawo należy umieścić po konfiguracji serwera:

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > Podczas pisania interfejsów API, zalecamy zawsze połączyć toosomething danych hello unikatowy z tokenu hello hello użytkownika nie może się podszyć. Gdy ten serwer przechowuje elementy przechowuje je na podstawie Identyfikatora obiektu hello użytkownika hello w hello tokenie (wywoływanym za pośrednictwem token.oid), który testujemy w polu "właściciela" hello. Daje to pewność, że tylko ten użytkownik ma dostęp do ich TODOs. Nie ma ekspozycji w hello interfejsu API "właściciela", dlatego użytkownikowi zewnętrznemu zażądanie hello TODOs innych nawet po dokonaniu uwierzytelnienia.                    

2. Następny Użyjmy hello strategii elementu nośnego, który jest dostarczany z `passport-azure-ad`. Sprawdź kod hello teraz i wyjaśniamy hello rest wkrótce. Umieścić po wkleić powyżej:

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
    **/

    var findById = function(id, fn) {
        for (var i = 0, len = users.length; i < len; i++) {
            var user = users[i];
            if (user.sub === id) {
                log.info('Found user: ', user);
                return fn(null, user);
            }
        }
        return fn(null, null);
    };


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

Usługa Passport używa podobnego wzorca do wszystkich swoich strategii (Twitter, Facebook itd.) zgodne ze wszyscy twórcy kodu strategii. Spojrzenie na powitania strategii, zobacz możemy przebiegu on funkcję, która ma token i gotowe jako parametry hello. Witaj strategia ponownie toous po jego działa. Po tak, przechowujemy hello użytkownika i token hello tymczasowym potrzebujemy nie tooask go ponownie.

> [!IMPORTANT]
> Witaj poprzedni kod obejmuje wszystkich użytkowników, wykonywanej tooauthenticate tooour serwera. Jest to nazywane rejestracji automatycznej. W przypadku serwerów produkcyjnych, firma Microsoft zaleca, aby nie zezwolić każda osoba, która bez konieczności ich przejściu przez proces rejestracji, który podjęciu decyzji o. Jest to zwykle wzorzec hello, które są widoczne w aplikacjach komercyjnych, które pozwalają tooregister z usługą Facebook, ale następnie poprosić toofill dodatkowych informacji. Jeśli to nie programu wiersza polecenia, być może wyodrębniono hello wiadomości e-mail z hello obiektu tokena, który został zwrócony, a następnie zadawane toofill użytkownika hello dodatkowych informacji. Ponieważ jest to serwer testowy, możemy po prostu dodane toohello bazy danych w pamięci.
>
>

### <a name="protect-some-endpoints"></a>Ochrona niektórych punktów końcowych
Ochrona punktów końcowych, określając hello `passport.authenticate()` wywołania z protokołem hello, które mają toouse.

toomake naszego kodu serwera zrobić coś więcej interesujące umożliwia edytowanie hello trasy.

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a>Krok 19: Uruchom ponownie aplikację serwera i upewnij się, że użytkownik jest odrzucany
Użyjmy `curl` ponownie toosee, jeśli mamy teraz OAuth2 ochrony przed naszych punktów końcowych. Możemy przeprowadzić ten test przed uruchomieniem żadnego z zestawów SDK klientów przed tym punktem końcowym. Hello zwrócone nagłówki powinny być za mało tootell nam Jeśli chcemy dół hello prawidłową ścieżkę.

1. Najpierw upewnij się, że wystąpienie bazy danych mongoDB jest uruchomione:

    `$sudo mongod`

2. Następnie zmień katalog toohello i uruchomić curling.

      `$ cd azuread` `$ node server.js`

3. Spróbuj podstawową procedurę testową POST.

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

401 jest odpowiedź hello, którego szukasz tutaj. Odpowiedź wskazuje, że że warstwa oprogramowania Passport hello próbuje tooredirect toohello autoryzacji punktu końcowego, który ma dokładnie.

## <a name="next-steps"></a>Następne kroki
Został usunięty w zakresie, w jakim można z tego serwera bez użycia klienta zgodne OAuth2. Konieczne będzie toogo za pośrednictwem dodatkowe wskazówki.

Znasz już teraz jak tooimplement przy użyciu interfejsu API REST Restify i protokołu OAuth2. Masz wystarczająco tookeep kodu opracowywania usługi i uczenia jak toobuild w tym przykładzie.

Jeśli interesuje Cię w następnych krokach hello w podróży ADAL, poniżej przedstawiono niektóre, firma Microsoft zaleca, aby kontynuować pracę z obsługiwanych klientów biblioteki ADAL.

Klonuj maszynę developer tooyour i skonfigurować zgodnie z opisem w przewodniku hello.

[Biblioteka ADAL dla systemu iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[ADAL dla systemu Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
