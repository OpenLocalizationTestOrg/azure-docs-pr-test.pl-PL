---
title: "Logowanie aplikacji sieci web Node.js w wersji 2.0 usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toobuild Node.js web app, który loguje się użytkownik, używając osobistego konta Microsoft i konto służbowe."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f8ce6e2b841c215cb14e82bcf444fe849634cc88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-nodejs-web-app"></a>Dodawanie aplikacji sieci web Node.js tooa logowania

> [!NOTE]
> Nie wszystkie usługi Azure Active Directory scenariusze i funkcje działają z punktem końcowym v2.0 hello. toodetermine, czy należy używać punktu końcowego v2.0 hello lub punkt końcowy 1.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 

W tym samouczku używamy hello toodo Passport następujące zadania:

* W aplikacji sieci web logowania użytkownika hello przy użyciu usługi Azure Active Directory (Azure AD) i hello punktu końcowego v2.0.
* Wyświetl informacje o użytkowniku hello.
* Znak hello użytkownika poza aplikacją hello.

**Passport** to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js. Elastyczne i moduły, usługa Passport można dyskretnie usunięty w każdym ekspresowe lub restify aplikacji sieci web. W usłudze Passport kompleksowy zestaw strategii obsługuje uwierzytelnianie przy użyciu nazwy użytkownika i hasła, Facebook, Twitter lub innych opcji. Opracowaliśmy strategię dla usługi Azure AD. W tym artykule zostanie przedstawiony zostanie sposób tooinstall hello modułu, a następnie dodaj hello Azure AD `passport-azure-ad` wtyczki.

## <a name="download"></a>Do pobrania
Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs). Samouczek hello toofollow, możesz [pobrać szkielet aplikacji hello jako plik .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) lub klonowania hello szkielet:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Umożliwia również wyświetlenie aplikacji hello ukończone na końcu hello tego samouczka.

## <a name="1-register-an-app"></a>1: Rejestrowanie aplikacji
Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj [te szczegółowe kroki](active-directory-v2-app-registration.md) tooregister aplikacji. Upewnij się, że:

* Kopiuj hello **identyfikator aplikacji** przypisane tooyour aplikacji. Należy go w tym samouczku.
* Dodaj hello **Web** platformy aplikacji.
* Kopiuj hello **identyfikator URI przekierowania** hello portalu. Należy użyć wartości identyfikatora URI domyślne hello `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-add-prerequisities-tooyour-directory"></a>2: Dodaj katalog tooyour wymagania wstępne
W wierszu polecenia Zmień folder główny tooyour toogo katalogów, jeśli nie masz już istnieje. Uruchom następujące polecenia hello:

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`

Ponadto możemy użyć `passport-azure-ad` w hello szkielet hello Szybki Start:

* `npm install passport-azure-ad`

Spowoduje to zainstalowanie bibliotek hello który `passport-azure-ad` używa.

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>3: Konfigurowanie strategii passport-node-js hello toouse aplikacji
Konfigurowanie hello Express oprogramowanie pośredniczące toouse hello protokołu uwierzytelniania OpenID Connect. Użyj żądania logowania i wylogowywania tooissue Passport, zarządzanie sesji użytkownika hello i uzyskać informacje o użytkowniku hello, między innymi.

1.  Witaj katalog główny projektu hello Otwórz hello pliku Config.js. W hello `exports.creds` wprowadź wartości konfiguracji aplikacji.
  
  * `clientID`: hello **identyfikator aplikacji** jest przypisany tooyour aplikacji w hello portalu Azure.
  * `returnURL`: hello **identyfikator URI przekierowania** wprowadzony w portalu hello.
  * `clientSecret`: hello hasło wygenerowane w portalu hello.

2.  W kluczu głównym hello hello projektu otwórz plik App.js hello. tooinvoke hello OIDCStrategy stratey, który jest dostarczany z `passport-azure-ad`, Dodaj następujące wywołanie hello:

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  toohandle żądań logowania, użyj strategii hello, który właśnie w odwołaniu:

  ```JavaScript
  // Use hello OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. hello function accepts
  //   credentials (in this case, an OpenID identifier), and invokes a callback
  //   with a user object.
  passport.use( new OIDCStrategy({
      callbackURL: config.creds.returnURL,
      realm: config.creds.realm,
      clientID: config.creds.clientID,
      clientSecret: config.creds.clientSecret,
      oidcIssuer: config.creds.issuer,
      identityMetadata: config.creds.identityMetadata,
      responseType: config.creds.responseType,
      responseMode: config.creds.responseMode,
      skipUserProfile: config.creds.skipUserProfile
      scope: config.creds.scope
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
      log.info('Example: Email address we received was: ', profile.email);
      // Asynchronous verification, for effect...
      process.nextTick(function () {
        findByEmail(profile.email, function(err, user) {
          if (err) {
            return done(err);
          }
          if (!user) {
            // "Auto-registration"
            users.push(profile);
            return done(null, profile);
          }
          return done(null, user);
        });
      });
    }
  ));
  ```

Usługa Passport używa podobnego wzorca do wszystkich swoich strategii (Twitter, Facebook i tak dalej). Wszystkich autorów toohello wzorca. Przekaż strategii hello `function()` używającą tokenu i `done` jako parametry. Strategia Hello jest zwracane, gdy robi swojej pracy. Użytkownik hello magazynu i token hello tymczasowym, więc nie trzeba tooask go ponownie.

  > [!IMPORTANT]
  > Hello poprzedni kod obejmuje wszystkich użytkowników, które można uwierzytelniać tooyour serwera. Jest to nazywane rejestracji automatycznej. Na serwerze produkcyjnym nie ma toolet każdy użytkownik bez konieczności ich przejść przez proces rejestracji, który można wybrać. Jest to zwykle hello wzorzec, który pojawi się w aplikacjach dla użytkowników indywidualnych. Aplikacja Hello mogą zezwalać tooregister z usługą Facebook, ale następnie prosi on tooenter dodatkowe informacje. Jeśli nie korzystasz z wiersza polecenia programu w tym samouczku, można wyodrębnić hello wiadomości e-mail z hello obiektu tokena, który jest zwracany. Następnie może poprosić użytkownika hello tooenter dodatkowe informacje. Ponieważ jest to serwer testowy, Dodaj użytkownika hello bezpośrednio toohello w bazy danych pamięci.
  > 
  > 

4.  Dodaj metody hello użycie tookeep śledzenie użytkowników, którym jest zalogowany, zgodnie z żądaniem usługi Passport. Obejmuje to serializację i deserializację informacji o użytkowniku hello:

  ```JavaScript

  // Passport session setup (section 2)

  //   toosupport persistent login sessions, Passport needs toobe able to
  //   serialize users into, and deserialize users out of, hello session. Typically,
  //   this is as simple as storing hello user ID when serializing, and finding
  //   hello user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array toohold signed-in users
  var users = [];

  var findByEmail = function(email, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
      var user = users[i];
      log.info('we are using user: ', user);
      if (user.email === email) {
        return fn(null, user);
      }
    }
    return fn(null, null);
  };
  ```

5.  Dodaj kod hello, który ładuje hello aparat Express. Użyj /views domyślne hello i wzorzec /routes Express zapewnia:

  ```JavaScript

  // Set up Express (section 2)

  var app = express();

  app.configure(function() {
    app.set('views', __dirname + '/views');
    app.set('view engine', 'ejs');
    app.use(express.logger());
    app.use(express.methodOverride());
    app.use(cookieParser());
    app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
    app.use(bodyParser.urlencoded({ extended : true }));
    // Initialize Passport!  Also use passport.session() middleware, toosupport
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  Dodaj hello POST kieruje tego Dostarcz hello rzeczywiste żądania rejestrowania toohello `passport-azure-ad` aparatu:

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. hello first step in OpenID authentication involves redirecting
  //   hello user toohello user's OpenID provider. After authenticating, hello OpenID
  //   provider redirects hello user back toothis application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in hello sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called.
  //   In this example, it redirects hello user toohello home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called. 
  //   In this example, it redirects hello user toohello home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>4: użycie usługi Passport tooissue logowania i wylogowywania żądań tooAzure AD
Aplikacja jest teraz skonfigurowane toocommunicate z punktem końcowym v2.0 hello przy użyciu protokołu uwierzytelniania OpenID Connect hello. Witaj `passport-azure-ad` strategii zajmuje się wszystkie szczegóły hello obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i podtrzymywanie sesji użytkowników hello. Wszystkie pozostało toodo jest toogive użytkownikom toosign sposób w i znak poza i toogather więcej informacji na temat hello, użytkownik jest zalogowany.

1.  Dodaj hello **domyślne**, **logowania**, **konta**, i **wylogowania** pliku App.js tooyour metod:

  ```JavaScript

  //Routes (section 4)

  app.get('/', function(req, res){
    res.render('index', { user: req.user });
  });

  app.get('/account', ensureAuthenticated, function(req, res){
    res.render('account', { user: req.user });
  });

  app.get('/login',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Login was called in hello sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  Poniżej przedstawiono szczegóły hello:
    
    * Witaj `/` trasa przekierowuje toohello index.ejs widoku. Przekazuje ono hello użytkownika w żądaniu hello (jeśli istnieje).
    * Witaj `/account` trasy najpierw *gwarantuje, że użytkownik jest uwierzytelniony* (zaimplementowaniem który w hello następującego kodu). Następnie przekazuje użytkownika hello w żądaniu hello. Jest to, dzięki czemu możesz uzyskać więcej informacji na temat hello użytkownika.
    * Witaj `/login` trasy wywołania z `azuread-openidconnect` uwierzytelniania z `passport-azuread`. Jeśli które się nie powiedzie, zbyt przekierowuje użytkownika hello ponownie`/login`.
    * Witaj `/logout` trasy wywołuje hello logout.ejs widoku (i trasę). Powoduje wyczyszczenie plików cookie, a następnie zwraca hello tooindex.ejs wstecz użytkownika.

2.  Dodaj hello **EnsureAuthenticated** metody użytej wcześniej wcześniej w `/account`:

  ```JavaScript

  // Route middleware tooensure hello user is authenticated (section 4)

  //   Use this route middleware on any resource that needs toobe protected. If
  //   hello request is authenticated (typically via a persistent login session),
  //   hello request proceeds. Otherwise, hello user is redirected toothe
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  W App.js Utwórz powitania serwera:

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a>5: tworzenie hello widoków i tras w Express przedstawia użytkownikowi na powitania witryny sieci Web
Dodawanie tras hello i widoków przedstawiających informacje toohello użytkownika. Witaj trasy i widoki również obsługiwać hello `/logout` i `/login` tras, które zostały utworzone.

1. W katalogu głównym hello, Utwórz hello `/routes/index.js` trasy.

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  W katalogu głównym hello, Utwórz hello `/routes/user.js` trasy.

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  `/routes/index.js`i `/routes/user.js` są proste trasy przekazują hello żądania tooyour widoków, w tym hello użytkownika, jeśli jest obecny.

3.  W katalogu głównym hello, Utwórz hello `/views/index.ejs` widoku. Ta strona wymaga programu **logowania** i **wylogowania** metody. Możesz również użyć hello `/views/index.ejs` Wyświetl informacje o koncie toocapture. Można użyć hello warunkowego `if (!user)` jako użytkownik hello są przekazywane w żądaniu hello. Jest dowód, że zalogowany użytkownik.

  ```JavaScript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
      <h2>Hello, <%= user.displayName %>.</h2>
      <a href="/account">Account info</a></br>
      <a href="/logout">Sign out</a>
  <% } %>
  ```

4.  W katalogu głównym hello, Utwórz hello `/views/account.ejs` widoku. Witaj `/views/account.ejs` widok umożliwia dodatkowe informacje tooview który `passport-azuread` umieszcza w żądaniu użytkownika hello.

  ```Javascript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
  <p>displayName: <%= user.displayName %></p>
  <p>givenName: <%= user.name.givenName %></p>
  <p>familyName: <%= user.name.familyName %></p>
  <p>UPN: <%= user._json.upn %></p>
  <p>Profile ID: <%= user.id %></p>
  <p>Full Claimes</p>
  <%- JSON.stringify(user) %>
  <p></p>
  <a href="/logout">Sign out</a>
  <% } %>
  ```

5.  Dodawanie układu. W katalogu głównym hello, Utwórz hello `/views/layout.ejs` widoku.

  ```HTML

  <!DOCTYPE html>
  <html>
      <head>
          <title>Passport-OpenID Example</title>
      </head>
      <body>
          <% if (!user) { %>
              <p>
              <a href="/">Home</a> |
              <a href="/login">Sign in</a>
              </p>
          <% } else { %>
              <p>
              <a href="/">Home</a> |
              <a href="/account">Account</a> |
              <a href="/logout">Sign out</a>
              </p>
          <% } %>
          <%- body %>
      </body>
  </html>
  ```

6.  toobuild i uruchom aplikację, uruchom `node app.js`. Następnie przejdź zbyt`http://localhost:3000`.

7.  Zaloguj się za pomocą osobistego konta Microsoft lub konta służbowego. Należy pamiętać, że tożsamość użytkownika hello jest odzwierciedlana hello /account liście. 

Masz teraz aplikacji sieci web, który jest zabezpieczony za pomocą standardowych protokołach branżowych. Użytkownicy mogą uwierzytelniać w aplikacji za pomocą ich kont osobistych i służbowych.

## <a name="next-steps"></a>Następne kroki
Odwołania, przykładowy ukończyć powitalnych (bez wartości konfiguracji) jest dostarczany jako [plik zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip). Użytkownik może ją także sklonować z serwisu GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Następnie można przenieść na toomore Tematy zaawansowane. Może być tootry:

[Zabezpieczanie interfejsu API sieci web Node.js za pomocą punktu końcowego v2.0 hello](active-directory-v2-devquickstarts-node-api.md)

Poniżej przedstawiono dodatkowe zasoby:

* [Przewodnik dewelopera v2.0 usługi Azure AD](active-directory-appmodel-v2-overview.md)
* [Tag "azure-active-directory" przepełnienie stosu](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Pobierz aktualizacje zabezpieczeń naszych produktów
Firma Microsoft zachęca toosign się toobe powiadomienia w przypadku wystąpienia zdarzeń zabezpieczeń. Na powitania [powiadomień o zabezpieczeniach technicznych Microsoft](https://technet.microsoft.com/security/dd252948) pozycję subskrybować alerty klasyfikatory tooSecurity.

