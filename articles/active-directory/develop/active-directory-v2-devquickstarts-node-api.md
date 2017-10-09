---
title: "aaaSecure interfejs API sieci web v2.0 usługi Azure Active Directory przy użyciu środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toobuild Node.js sieci web interfejsu API, który akceptuje tokeny zarówno z osobistego konta Microsoft, jak i z konta służbowego."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a>Zabezpieczanie interfejsu API sieci web przy użyciu środowiska Node.js
> [!NOTE]
> Nie wszystkie usługi Azure Active Directory scenariusze i funkcje działają z punktem końcowym v2.0 hello. toodetermine, czy należy używać punktu końcowego v2.0 hello lub punkt końcowy 1.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 
> 

Jeśli używasz punktu końcowego v2.0 usługi Azure Active Directory (Azure AD) hello, możesz użyć [OAuth 2.0](active-directory-v2-protocols.md) tokeny dostępu tooprotect interfejsu API sieci web. Za pomocą protokołu OAuth 2.0 tokeny dostępu, użytkownicy, którzy mają zarówno osobistego konta Microsoft i pracy lub kont służbowych można bezpiecznego dostępu do interfejsu API sieci web.

*Passport* to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js. Elastyczne i moduły, usługa Passport można dyskretnie usunięty w każdym ekspresowe lub restify aplikacji sieci web. W usłudze Passport kompleksowy zestaw strategii obsługuje uwierzytelnianie przy użyciu nazwy użytkownika i hasła, Facebook, Twitter lub innych opcji. Opracowaliśmy strategię dla usługi Azure AD. W tym artykule zostanie przedstawiony zostanie sposób tooinstall hello modułu, a następnie dodaj hello Azure AD `passport-azure-ad` wtyczki.

## <a name="download"></a>Do pobrania
Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs). Samouczek hello toofollow, możesz [pobrać szkielet aplikacji hello jako plik .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), lub w klonowania hello szkielet:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

Umożliwia również wyświetlenie aplikacji hello ukończone na końcu hello tego samouczka.

## <a name="1-register-an-app"></a>1: Rejestrowanie aplikacji
Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj [te szczegółowe kroki](active-directory-v2-app-registration.md) tooregister aplikacji. Upewnij się, że:

* Kopiuj hello **identyfikator aplikacji** przypisane tooyour aplikacji. Będzie on potrzebny w tym samouczku.
* Dodaj hello **Mobile** platformy aplikacji.
* Kopiuj hello **identyfikator URI przekierowania** hello portalu. Należy użyć wartości identyfikatora URI domyślne hello `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-install-nodejs"></a>2: zainstaluj środowisko Node.js
toouse hello próbki w ramach tego samouczka, należy najpierw [instalowania programu Node.js](http://nodejs.org).

## <a name="3-install-mongodb"></a>3: Zainstaluj bazę danych MongoDB
toosuccessfully korzystać z tej próbki, należy najpierw [zainstalować bazy danych MongoDB](http://www.mongodb.org). W tym przykładzie używasz bazy danych MongoDB toomake trwałego interfejsu API REST w wystąpieniach serwera.

> [!NOTE]
> W tym artykule przyjęto założenie, użyj hello domyślnej instalacji serwera punktów końcowych i bazy danych mongodb: mongodb://localhost.
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a>4: Instalacja hello restify modułów w interfejsie API sieci web
Używamy Resitfy toobuild w interfejsie API REST. Restify jest minimalną i elastyczną Node.js aplikacji platforma, która jest pochodną Express. Moduły restify oferuje rozbudowany zestaw funkcji, których można używać toobuild interfejsów API REST na bazie usługi Connect.

### <a name="install-restify"></a>Instalacja modułu restify
1.  W wierszu polecenia Zmień katalog hello zbyt**azuread**:

    `cd azuread`

    Jeśli hello **azuread** katalog nie istnieje, utwórz go:

    `mkdir azuread`

2.  Instalacja modułu restify:

    `npm install restify`

    dane wyjściowe tego polecenia Hello powinien wyglądać następująco:

    ```
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
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a>Czy został wyświetlony komunikat o błędzie?
W niektórych systemach operacyjnych, gdy używasz hello `npm` polecenia, można napotkać tego komunikatu: `Error: EPERM, chmod '/usr/local/bin/..'`. Błąd Hello następuje żądanie wypróbować uruchomionych hello konta z uprawnieniami administratora. W takim przypadku należy użyć polecenia hello `sudo` toorun `npm` na wyższym poziomie uprawnień.

#### <a name="did-you-get-an-error-related-toodtrace"></a>Czy został wyświetlony komunikat o błędzie dotyczący tooDTrace?
Po zainstalowaniu restify, można napotkać ten komunikat:

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
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

Moduły restify ma tootrace zaawansowanym mechanizmem wywołań REST przy użyciu narzędzia DTrace. Jednak narzędzia DTrace nie jest dostępne w wielu systemach operacyjnych. Można bezpiecznie zignorować ten komunikat o błędzie.


## <a name="5-install-passportjs-in-your-web-api"></a>5: Instalacja Passport.js w interfejsie API sieci web
1.  W wierszu polecenia hello Zmień katalog hello zbyt**azuread**.

2.  Zainstaluj Passport.js:

    `npm install passport`

    dane wyjściowe polecenia hello Hello powinien wyglądać następująco:

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a>6: Dodaj interfejs API sieci web tooyour passport-azure-ad
Następnie dodaj strategię OAuth hello, za pomocą biblioteki passport-azuread. `passport-azuread`jest zestawu strategii łączących usługę Azure AD z usługą Passport. Używamy tej strategii do tokenów elementów nośnych w próbce tego interfejsu API REST.

> [!NOTE]
> Chociaż framework, w którym mogą być wystawiane dowolnego znanego typu tokenu OAuth 2.0, niektóre typy tokenów są często używane. Tokeny elementów nośnych są często używane tooprotect punktów końcowych. Tokeny elementów nośnych są najczęściej wystawiony hello typ tokenu OAuth 2.0. Wiele implementacji protokołu OAuth 2.0 założono, że tokeny elementów nośnych są jedynym typem wystawianych tokenów hello.
> 
> 

1.  W wierszu polecenia Zmień katalog hello zbyt**azuread**.

    `cd azuread`

2.  Zainstaluj hello Passport.js `passport-azure-ad` modułu:

    `npm install passport-azure-ad`

    dane wyjściowe polecenia hello Hello powinien wyglądać następująco:

    ```
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
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a>7: Dodawanie bazy danych MongoDB modułów tooyour — interfejs API sieci web
W tym przykładzie używamy bazy danych MongoDB naszych przechowywania danych. 

1.  Instalowanie wtyczki Mongoose powszechnie używaną wtyczkę, toomanage modeli i schematów: 

    `npm install mongoose`

2.  Zainstaluj hello sterownik bazy danych dla bazy danych MongoDB, który jest również noszący nazwę MongoDB:

    `npm install mongodb`

## <a name="8-install-additional-modules"></a>8: Instalowanie dodatkowych modułów
Zainstaluj pozostałe wymagane moduły hello.

1.  W wierszu polecenia Zmień katalog hello zbyt**azuread**:

    `cd azuread`

2.  Wprowadź hello następujące polecenia. polecenia Hello zainstalować następujące moduły w katalogu node_modules hello:

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a>9: Tworzenie pliku Server.js dla zależności
Plik Server.js zawiera większość hello hello funkcji serwera interfejsu API sieci web. Dodaj większość toothis pliku kodu. Do celów produkcyjnych należy Refaktoryzuj hello funkcje na mniejsze pliki, takich jak odrębne trasy i kontrolery. W tym artykule w tym celu możemy użyć Server.js.

1.  W wierszu polecenia Zmień katalog hello zbyt**azuread**:

    `cd azuread`

2.  Za pomocą dowolnego edytora, Utwórz plik Server.js. Dodaj poniższe informacje toohello plik hello:

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  Zapisz plik hello. Wkrótce będzie zwracać tooit.

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a>10: tworzenie toostore pliku konfiguracji ustawień usługi Azure AD
Ten plik kodu przekazuje parametry konfiguracji hello z tooPassport.js portalu programu Azure AD. Te wartości konfiguracji są tworzone po dodaniu portalu toohello interfejsu API sieci web hello na początku hello hello artykułu. Po skopiowaniu kodu hello wyjaśniamy jakie tooput hello wartości tych parametrów.

1.  W wierszu polecenia Zmień katalog hello zbyt**azuread**:

    `cd azuread`

2.  W edytorze Tworzenie pliku Config.js. Dodaj hello następujących informacji:

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a>Wymagane wartości

*   **IdentityMetadata**: jest to, gdy `passport-azure-ad` sprawdza dane konfiguracyjne dla hello dostawcy tożsamości (IDP) i toovalidate klucze hello hello tokenów sieci Web JSON (Jwt). Jeśli używasz usługi Azure AD, prawdopodobnie nie będzie toochange to.

*   **grupy odbiorców**: przekierowania URI hello portalu.

> [!NOTE]
> Przywróć klucze w częstych odstępach czasu. Upewnij się, że zawsze pobierać z adresu URL "openid_keys" hello i danej aplikacji hello mogą uzyskiwać dostęp do Internetu hello.
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a>11: Dodawanie pliku Server.js tooyour konfiguracji hello
Aplikacja wymaga tooread hello wartości z pliku konfiguracji hello utworzony. Dodaj plik .config hello jako wymagany zasób w aplikacji. Ustaw hello toothose zmienne globalne, które znajdują się w Config.js.

1.  W wierszu polecenia hello Zmień katalog hello zbyt**azuread**:

    `cd azuread`

2.  W edytorze Otwórz Server.js. Dodaj hello następujących informacji:

    ```Javascript
    var config = require('./config');
    ```

3.  Dodaj nowy tooServer.js sekcji:

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>12: Dodawanie informacji modelu i schemacie modułu MongoDB hello przy użyciu wtyczki Mongoose
Następnie należy połączyć z tych trzech plików w usłudze interfejsu API REST.

W tym artykule używamy toostore bazy danych MongoDB nasze zadania. Omówiono w *krok 4*.

W pliku Config.js hello utworzonego w kroku 11, nosi nazwę bazy danych *tasklist*. Która jest umieszczona na końcu hello adres URL połączenia mongoose_auth_local. Nie trzeba toocreate tej bazy danych wcześniej w module MongoDB. Witaj baza danych została utworzona na powitania najpierw uruchamiania aplikacji serwera (przy założeniu, że hello bazy danych już nie istnieje).

Zostały informację powitania serwera, jakie toouse bazy danych MongoDB. Następnie należy toowrite niektóre dodatkowy kod toocreate hello modelu i schematu dla zadań serwera.

### <a name="hello-model"></a>Witaj modelu
Witaj model schematu jest bardzo proste. Aby można ją rozszerzyć. 

model schematu Hello ma następujące wartości:

*   **NAZWA**. Hello osoby toohello przypisane zadania. Jest to **ciąg** wartość.
*   **ZADANIE**. Nazwa Hello hello zadania. Jest to **ciąg** wartość.
*   **DATA**. Data Hello przypada hello zadania. Jest to **datetime** wartość.
*   **UKOŃCZONO**. Określa, czy hello zadanie zostało ukończone. Jest to **logiczna** wartość.

### <a name="create-hello-schema-in-hello-code"></a>Tworzenie schematu hello w kodzie hello
1.  W wierszu polecenia Zmień katalog hello zbyt**azuread**:

    `cd azuread`

2.  W edytorze Otwórz Server.js. Poniżej pozycji konfiguracji hello Dodaj hello następujących informacji:

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

Ten kod łączy się z serwerem MongoDB toohello. Zwraca obiekt schematu.

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a>Przy użyciu schematu hello, tworzenie modelu w kodzie hello
Poniżej hello poprzedzających kodu Dodaj hello następującego kodu:

```Javascript
// Create a basic schema toostore your tasks and users.
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

Jak stwierdzić, z kodu hello, najpierw należy utworzyć schemat. Następnie można utworzyć obiektu modelu. Użyj toostore obiektu modelu hello danych w całym hello kodu podczas definiowania Twojej **tras**.

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a>13: Dodaj trasy dla serwera zadań interfejsu API REST
Teraz, gdy masz toowork modelu bazy danych, z dodać trasy hello, które będą używane dla serwera interfejsu API REST.

### <a name="about-routes-in-restify"></a>Informacje o trasach w restify
Trasy w restify dokładnie hello taki sam sposób jak korzystając z hello stosu Express pracy. Trasy są definiowane za pomocą hello spodziewać się powitania klienta aplikacji toocall identyfikatora URI. Zazwyczaj należy zdefiniować trasy w oddzielnym pliku. W tym samouczku testujemy naszych trasy w Server.js. Do użytku produkcyjnego zaleca się współczynnika trasy do ich własnych pliku.

Typowy wzorzec trasy modułu restify jest:

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


Jest to wzorzec hello na najbardziej podstawowym poziomie hello. Moduły restify (i Express) podaj znacznie bardziej złożone funkcje, takie jak typy aplikacji toodefine możliwości hello i złożonego routingu przez różne punkty końcowe.

#### <a name="add-default-routes-tooyour-server"></a>Dodaj serwer tooyour trasy domyślnej
Dodać podstawowe trasy CRUD hello: **utworzyć**, **pobrać**, **aktualizacji**, i **usunąć**.

1.  W wierszu polecenia Zmień katalog hello zbyt**azuread**:

    `cd azuread`

2.  W edytorze Otwórz Server.js. Poniżej hello wprowadzone wcześniej wpisy w bazie danych, należy dodać hello następujących informacji:

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
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
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in hello database. Add one!");
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

### <a name="add-error-handling-for-hello-routes"></a>Dodawanie obsługi błędów dla tras hello
Dodaj obsługę błędów, może komunikować się wstecz toohello klienta o hello problem pojawił się.

Dodaj następującego kodu poniżej hello kodu, który został już zapisany hello:

```Javascript
///--- Errors for communicating something more information back toohello client.
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


## <a name="14-create-your-server"></a>14: Tworzenie serwera
ostatni element toodo Hello jest tooadd wystąpienia serwera. wystąpienie serwera Hello zarządza wywołania.

Moduły restify (i Express) ma możliwość głębokiego dostosowania można używać z serwera interfejsu API REST. W tym samouczku używamy hello najbardziej podstawowa konfiguracja.

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a>15: dodać trasy hello (bez uwierzytelniania jest obecnie)
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
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
// Register a default '/' handler
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
## <a name="16-run-hello-server"></a>16: Uruchom powitania serwera
Jest tootest dobrze serwera przed dodaniem uwierzytelniania.

Witaj Najprostszym sposobem tootest serwera jest przy użyciu programu curl w wierszu polecenia. toodo, to należy proste narzędzie, której można tooparse danych wyjściowych w formacie JSON. 

1.  Zainstaluj narzędzie JSON hello używana w hello następujące przykłady:

    `$npm install -g jsontool`

    Spowoduje to zainstalowanie narzędzie JSON hello globalnie.

2.  Upewnij się, że wystąpienie bazy danych MongoDB zostało uruchomione:

    `$sudo mongod`

3.  Zmień katalog hello zbyt**azuread**, a następnie uruchom narzędzie curl:

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
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

4.  tooadd zadania:

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

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

5.  Listy zadań dla Brandon:

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Jeśli wszystkie te polecenia są uruchamiane bez błędów, to serwera interfejsu API REST toohello OAuth tooadd gotowe.

*Masz teraz serwerem interfejsu API REST z bazą danych MongoDB.*

## <a name="17-add-authentication-tooyour-rest-api-server"></a>17: Dodawanie serwera interfejsu API REST tooyour uwierzytelniania
Teraz, gdy masz uruchomiony interfejs API REST go skonfigurować toouse za pomocą usługi Azure AD.

W wierszu polecenia Zmień katalog hello zbyt**azuread**:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a>Użyj hello oidcbearerstrategy, który wchodzi w skład passport-azure-ad
Do tej pory zostały skompilowane typowy serwer REST TODO bez żadnej autoryzacji. Teraz Dodaj uwierzytelniania.

Najpierw należy wskazać, że ma toouse Passport. To prawo należy umieścić po wcześniejszej konfiguracji serwera:

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> Podczas pisania interfejsów API jest hello łącze tooalways dobrym rozwiązaniem, które toosomething danych niż token hello hello użytkownika nie może się podszyć. Gdy ten serwer przechowuje elementy przechowuje je na podstawie Identyfikatora subskrypcji użytkownika hello w hello tokenie (wywoływanym za pośrednictwem token.sub). W polu "właściciela" hello, możesz zaznaczyć hello token.sub. Daje to pewność, że tylko ten użytkownik może uzyskać dostęp użytkownika hello TODOs. Inni użytkownicy mogą uzyskiwać dostęp do TODOs hello, które zostały wprowadzone. Brak ma ekspozycji w hello interfejsu API dla "właściciela". Użytkownikowi zewnętrznemu zażądanie TODOs innych użytkowników, nawet po dokonaniu uwierzytelnienia.
> 
> 

Następnie użyj strategii nośnego otwarte połączenie identyfikator hello, która jest dostarczany z `passport-azure-ad`. Umieścić po wcześniejszym wkleić:

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
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
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

Usługa Passport używa podobnego wzorca do wszystkich swoich strategii (Twitter, Facebook i tak dalej). Wszystkich autorów toohello wzorca. Przekaż strategii hello `function()` używającą tokenu i `done` jako parametry. Strategia Hello jest zwracane, gdy robi swojej pracy. Użytkownik hello magazynu i token hello tymczasowym, więc nie trzeba tooask go ponownie.

> [!IMPORTANT]
> Hello poprzedni kod obejmuje wszystkich użytkowników, które można uwierzytelniać tooyour serwera. Jest to nazywane rejestracji automatycznej. Na serwerze produkcyjnym nie ma toolet każdy użytkownik bez konieczności ich przejść przez proces rejestracji, który można wybrać. Jest to zwykle wzorzec hello, które są widoczne w aplikacjach komercyjnych. Aplikacja Hello mogą zezwalać tooregister z usługą Facebook, ale następnie prosi on tooenter dodatkowe informacje. Jeśli nie korzystasz z wiersza polecenia programu w tym samouczku, można wyodrębnić hello wiadomości e-mail z hello obiektu tokena, który jest zwracany. Następnie może poprosić użytkownika hello tooenter dodatkowe informacje. Ponieważ jest to serwer testowy, Dodaj użytkownika hello bezpośrednio toohello w bazy danych pamięci.
> 
> 

### <a name="protect-endpoints"></a>Ochrona punktów końcowych
Ochrona punktów końcowych, określając hello **passport.authenticate()** wywołania z protokołem hello, które mają toouse.

Dostęp można edytować w kodzie serwera dla bardziej zaawansowanych opcji:

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a>18: Uruchom ponownie aplikację serwera
Użyj ponownie curl toosee, jeśli masz OAuth 2.0 ochrony punktów końcowych przy użyciu. Wykonaj tę operację przed uruchomieniem żadnego z zestawów SDK klienta względem tego punktu końcowego. zwrócone nagłówki Hello powinien stwierdzić, czy uwierzytelnianie działa poprawnie.

1.  Upewnij się, czy działa isntance Twojej bazy danych MongoDB:

    `$sudo mongod`

2.  Zmień toohello **azuread** katalogu, a następnie użyj curl:

    `$ cd azuread`

    `$ node server.js`

3.  Wypróbuj podstawową procedurę testową POST:

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

Uzyskanie odpowiedzi 401 wskazuje, że warstwa oprogramowania Passport hello próbuje tooredirect toohello punktu końcowego autoryzacji, który ma dokładnie.

*Masz teraz usługi interfejsu API REST, który korzysta z protokołu OAuth 2.0.*

Został usunięty w zakresie, w jakim można bez użycia klienta OAuth 2.0 zgodnego z tym serwerem. W tym konieczne będzie tooreview dodatkowe samouczka.

## <a name="next-steps"></a>Następne kroki
Odwołania, przykładowy ukończyć powitalnych (bez wartości konfiguracji) jest dostarczany jako [plik zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip). Użytkownik może ją także sklonować z serwisu GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

Teraz możesz przejść toomore Tematy zaawansowane. Może być tootry [zabezpieczenia aplikacji sieci web Node.js za pomocą punktu końcowego v2.0 hello](active-directory-v2-devquickstarts-node-web.md).

Poniżej przedstawiono dodatkowe zasoby:

* [Przewodnik dewelopera v2.0 usługi Azure AD](active-directory-appmodel-v2-overview.md)
* [Tag "azure-active-directory" przepełnienie stosu](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Pobierz aktualizacje zabezpieczeń naszych produktów
Firma Microsoft zachęca toosign się toobe powiadomienia w przypadku wystąpienia zdarzeń zabezpieczeń. Na powitania [powiadomień o zabezpieczeniach technicznych Microsoft](https://technet.microsoft.com/security/dd252948) pozycję subskrybować alerty klasyfikatory tooSecurity.

