---
title: "Usługa Azure AD B2C: zabezpieczanie interfejsu API sieci Web przy użyciu środowiska Node.js | Microsoft Docs"
description: "W jaki sposób toobuild Node.js interfejs API sieci web, która akceptuje tokeny od dzierżawcy usługi B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a>Usługa Azure AD B2C: zabezpieczanie interfejsu API sieci Web przy użyciu środowiska Node.js
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

Usługa Azure Active Directory (Azure AD) B2C umożliwia zabezpieczanie interfejsu API sieci Web za pomocą tokenów dostępu protokołu OAuth 2.0. Tokeny te aplikacjom klienckim korzystających z interfejsu API toohello tooauthenticate usługi Azure AD B2C. W tym artykule opisano, jak toocreate interfejs API "Lista zadań do wykonania" umożliwiająca użytkownikom tooadd i listy zadań. Interfejs API sieci web Hello jest zabezpieczone przy użyciu usługi Azure AD B2C i tylko umożliwia toomanage uwierzytelnionym użytkownikom ich listy zadań do wykonania.

> [!NOTE]
> Ta próbka została zapisana przy użyciu tooby toobe połączone naszych [B2C systemu iOS Przykładowa aplikacja](active-directory-b2c-devquickstarts-ios.md). Najpierw hello bieżący samouczek, a następnie kontynuować pracę z próbką.
>
>

**Passport** to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js. Jest to elastyczne i modułowe oprogramowanie, które można dyskretnie zainstalować w dowolnej aplikacji sieci Web opartej na module Express lub Restify. Kompleksowy zestaw strategii obsługuje uwierzytelnianie przy użyciu m.in. nazwy użytkownika i hasła lub kont w serwisach Facebook i Twitter. Opracowaliśmy strategię dla usługi Azure Active Directory (Azure AD). Zainstaluj ten moduł, a następnie dodaj hello Azure AD `passport-azure-ad` wtyczki.

toodo tej próbki, należy:

1. Zarejestrować aplikację w usłudze Azure AD.
2. Konfigurowanie Twojej aplikacji toouse Passport w `azure-ad-passport` wtyczki.
3. Konfigurowanie klienta aplikacji toocall hello "Lista zadań do wykonania" składnika web API.

## <a name="get-an-azure-ad-b2c-directory"></a>Tworzenie katalogu usługi Azure AD B2C
Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.  Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów.  Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.

## <a name="create-an-application"></a>Tworzenie aplikacji
Następnie należy toocreate aplikację w katalogu B2C, która zapewnia usługi Azure AD pewne informacje, że wymaga ona toosecurely komunikacji z aplikacją. W takim przypadku zarówno aplikacja kliencka hello, jak i interfejs API sieci web są reprezentowane przez jeden **identyfikator aplikacji**, ponieważ stanowią jedną aplikację logiczną. toocreate usługi aplikacji, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md). Należy pamiętać o wykonaniu następujących czynności:

* Obejmują **sieci web w sieci web i aplikacji interfejsu api** w aplikacji hello
* Wprowadź `http://localhost/TodoListService` w polu **Adres URL odpowiedzi**. Jest hello domyślny adres URL dla tego przykładu kodu.
* Utwórz **klucz tajny aplikacji** i skopiuj go. Te dane będą potrzebne później. Należy pamiętać, że ta wartość musi toobe [XML w znaki ucieczki](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) przed jego użyciem.
* Kopiuj hello **identyfikator aplikacji** czyli przypisanej tooyour aplikacji. Te dane będą potrzebne później.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Tworzenie zasad
W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md). Ta aplikacja zawiera dwa elementy dotyczące tożsamości: rejestracja i logowanie. Należy jedna zasada toocreate każdego typu zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).  Podczas tworzenia trzech zbiorów zasad należy koniecznie:

* Wybierz hello **Nazwa wyświetlana** i inne atrybuty rejestracji w ramach zasad rejestracji.
* Wybierz hello **Nazwa wyświetlana** i **obiektu o identyfikatorze** oświadczenia aplikacji we wszystkich zasadach.  Można również wybrać inne oświadczenia.
* Skopiuj hello **nazwa** poszczególnych zasad po jego utworzeniu. Powinien on mieć prefiks hello `b2c_1_`.  Te nazwy zasad będą potrzebne później.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Po utworzeniu trzech zbiorów zasad, wszystko jest gotowe toobuild aplikacji.

toolearn o sposób działania zasad w usłudze Azure AD B2C, rozpoczynać hello [.NET sieci web aplikacji Wprowadzenie — samouczek](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="download-hello-code"></a>Pobierz kod hello
Witaj kodu w tym samouczku [jest przechowywany w serwisie GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS). Przykładowe hello toobuild podczas przejść, możesz [pobrać szkielet projektu jako plik .zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip). Można również sklonować szkielet hello:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

Aplikacja Hello ukończone jest również [dostępny jako plik zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) lub na powitania `complete` gałęzi hello tego samego repozytorium.

## <a name="download-nodejs-for-your-platform"></a>Pobieranie środowiska Node.js dla platformy
toosuccessfully korzystać z tej próbki, należy działającą instalacją środowiska Node.js.

Zainstaluj środowisko Node.js z witryny [nodejs.org](http://nodejs.org).

## <a name="install-mongodb-for-your-platform"></a>Instalowanie bazy danych MongoDB dla platformy
toosuccessfully korzystać z tej próbki, należy działającą instalacją bazy danych MongoDB. Korzystamy z bazy danych MongoDB toomake trwałego interfejsu API REST w wystąpieniach serwera.

Zainstaluj bazę danych MongoDB z witryny [mongodb.org](http://www.mongodb.org).

> [!NOTE]
> W tym przewodniku zakłada, użyj hello domyślnej instalacji serwera punktów końcowych i bazy danych mongodb, który w czasie hello pisania tego dokumentu jest `mongodb://localhost`.
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a>Instalowanie modułów Restify hello w interfejsie API sieci web
Używamy Restify toobuild interfejsu API REST. Restify jest minimalną i elastyczną strukturą aplikacji w środowisku Node.js, która pochodzi z modułu Express. Oferuje rozbudowany zestaw funkcji do tworzenia interfejsów API REST na bazie usługi Connect.

### <a name="install-restify"></a>Instalacja modułu Restify
W wierszu polecenia hello, zmień katalog zbyt`azuread`. Jeśli hello `azuread` katalog nie istnieje, utwórz go.

`cd azuread` lub `mkdir azuread;`

Wprowadź hello następujące polecenie:

`npm install restify`

To polecenie powoduje zainstalowanie modułu Restify.

#### <a name="did-you-get-an-error"></a>Czy został wyświetlony komunikat o błędzie?
W niektórych systemach operacyjnych, korzystając z `npm`, może zostać wyświetlony błąd hello `Error: EPERM, chmod '/usr/local/bin/..'` i żądania uruchomienia hello konta z uprawnieniami administratora. Jeśli wystąpi ten problem, użyj hello `sudo` toorun polecenia `npm` na wyższym poziomie uprawnień.

#### <a name="did-you-get-a-dtrace-error"></a>Czy został wyświetlony błąd narzędzia DTrace?
Po zainstalowaniu modułu Restify może zostać wyświetlony następujący tekst:

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

Moduł Restify zapewnia zaawansowany mechanizm śledzenia wywołań REST przy użyciu narzędzia DTrace. Jednak w wielu systemach operacyjnych narzędzie DTrace jest niedostępne. Można te błędy bezpiecznie zignorować.

Hello dane wyjściowe polecenia hello powinna wyglądać podobnie tekst toothis:

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

## <a name="install-passport-in-your-web-api"></a>Instalacja oprogramowania Passport w interfejsie API sieci Web
W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje.

Instalacja oprogramowania Passport przy użyciu hello następujące polecenie:

`npm install passport`

dane wyjściowe polecenia hello Hello powinny być podobne toothis tekst:

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a>Dodawanie biblioteki passport-azuread tooyour — interfejs API sieci web
Następnie dodaj strategię OAuth hello przy użyciu `passport-azuread`, zestawu strategii łączących usługę Azure AD z usługą Passport. Użyj tej strategii do tokenów elementów nośnych w próbce interfejsu API REST hello.

> [!NOTE]
> Chociaż protokół OAuth2 zapewnia platformę umożliwiającą wystawienie dowolnego znanego typu tokenu, tylko niektóre typy tokenów weszły do powszechnego użycia. tokeny Hello punkty końcowe są tokenami elementów nośnych. Te typy tokenów są hello najczęściej wystawiony protokołu oauth2. W wielu wdrożeniach zakłada, że tokeny elementów nośnych są jedynym typem wystawianych tokenów hello.
>
>

W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje.

Zainstaluj hello Passport `passport-azure-ad` modułu przy użyciu hello następujące polecenie:

`npm install passport-azure-ad`

dane wyjściowe polecenia hello Hello powinny być podobne toothis tekst:

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a>Dodawanie bazy danych MongoDB modułów tooyour — interfejs API sieci web
W tej próbce moduł MongoDB będzie używany jako magazyn danych. W tym celu zainstaluj oprogramowanie Mongoose — powszechnie używaną wtyczkę do zarządzania modelami i schematami.

* `npm install mongoose`

## <a name="install-additional-modules"></a>Instalowanie dodatkowych modułów
Następnie zainstaluj pozostałe wymagane moduły hello.

W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:

`cd azuread`

Instalowanie modułów hello w Twojej `node_modules` katalogu:

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a>Tworzenie pliku server.js z własnymi zależnościami
Witaj `server.js` plik zawiera większość hello hello funkcji serwera interfejsu API sieci Web.

W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:

`cd azuread`

Utwórz plik `server.js` w edytorze. Dodaj hello następujących informacji:

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

Zapisz plik hello. Tooit wróć później.

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a>Utwórz toostore pliku config.js ustawienia usługi Azure AD
Ten plik kodu przekazuje parametry konfiguracji hello z toohello z portalu Azure AD `Passport.js` pliku. Te wartości konfiguracji są tworzone po dodaniu portalu toohello interfejsu API sieci web hello w pierwszej części przewodnika hello hello. Po skopiowaniu kodu hello prezentujemy zasady jakie tooput hello wartości tych parametrów.

W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:

`cd azuread`

Utwórz plik `config.js` w edytorze. Dodaj hello następujących informacji:

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a>Wymagane wartości
`clientID`: hello identyfikator klienta aplikacji interfejsu API sieci Web.

`IdentityMetadata`: To jest where `passport-azure-ad` sprawdza dane konfiguracyjne dla hello dostawcy tożsamości. Wyszukuje również toovalidate klucze hello hello tokenów sieci web JSON.

`audience`: hello identyfikator uniform resource identifier (URI) z portalu hello, który identyfikuje wywoływania aplikacji.

`tenantName`: nazwa dzierżawy (na przykład **contoso.onmicrosoft.com**).

`policyName`: hello zasady, które chcesz toovalidate hello tokenów przychodzących tooyour serwera. Ta zasada powinna być hello te same zasady używanego na powitania klienta aplikacji do logowania.

> [!NOTE]
> Na razie użyj hello takie same zasady przez klienta i serwera konfiguracji. Jeśli zostały już wykonane w ramach tego przewodnika i utworzyć zasady, nie potrzebujesz toodo więc ponownie. Ponieważ ukończono przewodnik hello, nie ma potrzeby tooset się nowych zasad dla przewodników klienta na powitania lokacji.
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a>Dodawanie pliku server.js tooyour konfiguracji
wartości hello tooread z hello `config.js` utworzonego pliku, Dodaj hello `.config` pliku jako wymagany zasób w aplikacji, a następnie ustaw toothose zmienne globalne hello w hello `config.js` dokumentu.

W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:

`cd azuread`

Otwórz hello `server.js` plik w edytorze. Dodaj hello następujących informacji:

```Javascript
var config = require('./config');
```
Dodaj nową sekcję zbyt`server.js` zawierającą hello następującego kodu:

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

Następnie możemy dodać niektóre symbole zastępcze dla użytkowników hello otrzymane od naszych wywoływania aplikacji.

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

Utwórzmy także naszego rejestratora.

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Dodawanie informacji modelu i schemacie modułu MongoDB hello przy użyciu wtyczki Mongoose
Witaj wcześniejsze przygotowania pozwoli zaoszczędzić czas podczas łączenia tych trzech plików w usłudze interfejsu API REST.

Na potrzeby tego przewodnika Użyj bazy danych MongoDB toostore zadań, zgodnie z wcześniejszym opisem.

W hello `config.js` plik, nazwę bazy danych **tasklist**. Ta nazwa została ona również umieszczona na końcu hello hello `mongoose_auth_local` adres URL połączenia. Nie trzeba toocreate tej bazy danych wcześniej w module MongoDB. Tworzy hello bazy danych dla Ciebie na powitania pierwszym uruchomieniu aplikacji serwera.

Po przekazaniu powitania serwera które toouse bazy danych MongoDB należy toowrite niektóre dodatkowy kod toocreate hello modelu i schematu dla zadań serwera.

### <a name="expand-hello-model"></a>Rozwiń węzeł hello modelu
Ten model schematu jest prosty. Można go rozszerzyć w zależności od potrzeb.

`owner`: Kto jest przydzielony toohello zadań. Ten obiekt to **ciąg**.  

`Text`: samo zadanie hello. Ten obiekt to **ciąg**.

`date`: hello Data przypada hello zadania. Ten obiekt to **data i godzina**.

`completed`: Jeśli hello zadanie zostało ukończone. Ten obiekt to **dane logiczne**.

### <a name="create-hello-schema-in-hello-code"></a>Tworzenie schematu hello w kodzie hello
W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:

`cd azuread`

Otwórz hello `server.js` plik w edytorze. Dodaj następujące informacje poniżej pozycji konfiguracji hello hello:

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
Najpierw utworzyć hello schematu, a następnie utwórz obiekt modelu używanego danych w całym hello kodu podczas definiowania toostore Twojego **tras**.

## <a name="add-routes-for-your-rest-api-task-server"></a>Dodawanie tras do serwera zadań interfejsu API REST
Teraz, gdy masz toowork modelu bazy danych, z Dodaj hello trasy, używanego serwera interfejsu API REST.

### <a name="about-routes-in-restify"></a>Informacje o trasach w module Restify
Trasy działają w module Restify w hello sam sposób, jak przy korzystaniu z hello Express stosu. Trasy są definiowane za pomocą hello spodziewać się powitania klienta aplikacji toocall identyfikatora URI.

Oto typowy wzorzec trasy modułu Restify:

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

Moduły Restify i Express mogą zapewniać o wiele bardziej złożone funkcje, takie jak definiowanie typów aplikacji i wykonywanie złożonego routingu przez różne punkty końcowe. Do celów tego samouczka hello możemy proste trasy.

#### <a name="add-default-routes-tooyour-server"></a>Dodaj serwer tooyour trasy domyślnej
Teraz Dodaj hello podstawowe trasy CRUD **utworzyć** i **listy** na interfejsie API REST. Innych tras znajdują się w hello `complete` gałęzi hello próbki.

W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:

`cd azuread`

Otwórz hello `server.js` plik w edytorze. Poniżej wpisy w bazie danych hello wprowadzone powyżej Dodaj hello następujących informacji:

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a>Dodawanie obsługi błędów dla tras hello
Dodać niektóre Obsługa błędów i może komunikować się wszelkie problemy wystąpią klienta toohello Wstecz w taki sposób, który może zrozumieć.

Dodaj hello następującego kodu:

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a>Tworzenie serwera
Baza danych została zdefiniowana, a trasy — określone. ostatnim zadaniem Hello toodo możesz jest wystąpienie serwera hello tooadd, która zarządza wywołania.

Moduły restify i Express oferują możliwość głębokiego dostosowania do serwera interfejsu API REST, ale używana hello najbardziej podstawowa konfiguracja tutaj.

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a>Dodaj serwer toohello trasy hello (bez uwierzytelniania)
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a>Dodawanie serwera interfejsu API REST tooyour uwierzytelniania
Działający serwer interfejsu API REST można wykorzystać do celów usługi Azure AD.

W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Użyj hello OIDCBearerStrategy dołączonej usługi passport-azure-ad
> [!TIP]
> Podczas pisania interfejsów API, należy zawsze połączyć toosomething danych hello unikatowy z tokenu hello hello użytkownika nie może się podszyć. Gdy serwer hello przechowuje elementy, tak więc na powitania podstawie **oid** użytkownika hello w hello tokenie (wywoływanym za pośrednictwem token.oid), który znajduje się w polu "hello"właściciela". Ta wartość zapewnia, że tylko ten użytkownik może uzyskać dostęp do własnych zadań do wykonania. Nie ma ekspozycji w hello interfejsu API "właściciela", dlatego użytkownikowi zewnętrznemu zażądanie innych zadań do wykonania nawet po dokonaniu uwierzytelnienia.
>
>

Następnie użyj strategii elementu nośnego hello dołączoną `passport-azure-ad`.

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

Passport używa hello wzorca takie same dla wszystkich swoich strategii. Zawiera on polecenie `function()` z parametrami `token` i `done`. Strategia Hello wróci tooyou po wykonaniu całego zadania. A następnie należy przechowywać hello użytkownika i zapisać hello token, tak aby nie trzeba tooask go ponownie.

> [!IMPORTANT]
> Powyższy kod Hello obejmuje żadnych użytkowników, którzy tooauthenticate tooyour serwera. Ten proces jest nazywany autorejestracją. W przypadku serwerów produkcyjnych nie umożliwiają w interfejsie API hello żadnych użytkowników dostęp bez konieczności ich przechodzą przez proces rejestracji. Ten proces jest zwykle wzorzec hello, które są widoczne w aplikacjach komercyjnych, który pozwala tooregister za pomocą usługi Facebook, ale następnie poprosić toofill dodatkowych informacji. Jeśli ten program nie programu wiersza polecenia, być może wyodrębniono hello wiadomości e-mail z hello obiektu tokena, który został zwrócony, a następnie zadawane toofill użytkowników dodatkowych informacji. Ponieważ to jest przykład możemy dodać je tooan bazy danych w pamięci.
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a>Uruchom tooverify aplikacji z serwera jego odrzuca możesz
Można użyć `curl` toosee, jeśli masz teraz OAuth2 ochrony punktów końcowych przy użyciu. Hello zwrócone nagłówki powinny być za mało tootell że znajdują się na powitania prawidłową ścieżkę.

Upewnij się, że wystąpienie bazy danych MongoDB zostało uruchomione:

    $sudo mongodb

Zmień katalog toohello i hello uruchomienia serwera:

    $ cd azuread
    $ node server.js

W nowym oknie terminala uruchom polecenie `curl`

Wypróbuj podstawową procedurę testową POST:

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

Odpowiedzi na powitania jest błąd 401. Wskazuje, że warstwa oprogramowania Passport hello próbuje tooredirect toohello punktu końcowego autoryzacji.

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a>Efektem jest usługa interfejsu API REST korzystająca z protokołu OAuth2
Udało Ci się wdrożyć interfejs API REST przy użyciu modułu Restify i strategii OAuth! Teraz masz kod wystarczające, dzięki czemu można kontynuować toodevelop usługi i kompilacji w tym przykładzie. W przypadku tego serwera nie można wykonać żadnych dalszych czynności bez użycia klienta zgodnego z protokołem OAuth2. Dla tego kroku dalej używać jest dodatkowy przewodnik, takich jak naszym [połączyć tooa interfejsu API sieci web przy użyciu systemu iOS z usługi B2C](active-directory-b2c-devquickstarts-ios.md) wskazówki.

## <a name="next-steps"></a>Następne kroki
Możesz teraz przejść toomore zaawansowanych tematów, takich jak:

[Połącz tooa interfejsu API sieci web przy użyciu systemu iOS z usługi B2C](active-directory-b2c-devquickstarts-ios.md)
