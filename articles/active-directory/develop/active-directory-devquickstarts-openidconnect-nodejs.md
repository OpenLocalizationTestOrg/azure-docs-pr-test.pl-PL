---
title: "aaaGetting uruchomiony z logowania w usłudze Azure AD i wylogowania, przy użyciu środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toobuild Node.js Express MVC sieci web aplikacji, która integruje się z usługą Azure AD dla logowania."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 81deecec-dbe2-4e75-8bc0-cf3788645f99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 26481899c74741743b947bd891b65ff24ffc43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a>Aplikacja sieci web node.js logowania i wylogowywania z usługą Azure AD
W tym miejscu możemy użyć usługi Passport:

* Znak hello użytkownika w aplikacji toohello za pomocą usługi Azure Active Directory (Azure AD).
* Wyświetl informacje o użytkowniku hello.
* Znak hello użytkownika poza aplikacją hello.

Usługa Passport to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js. Elastyczne i moduły, usługa Passport można było porzucić dyskretnie w tooany ekspresowe lub restify aplikacji sieci web. Kompleksowy zestaw strategii obsługuje uwierzytelniania przy użyciu nazwy użytkownika i hasła, Facebook i Twitter. Opracowaliśmy strategię dla usługi Microsoft Azure Active Directory. Firma Microsoft zainstalowaniu tego modułu, a następnie dodaj hello Microsoft Azure Active Directory `passport-azure-ad` wtyczki.

toodo tego hello wykonaj następujące kroki:

1. Rejestrowanie aplikacji.
2. Konfigurowanie Twojej aplikacji hello toouse `passport-azure-ad` strategii.
3. Użyj paszportu tooissue logowania i wylogowywania żądań tooAzure AD.
4. Dane o użytkowniku hello wydruku.

Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).  toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako plik .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) lub klonowania hello szkielet:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

Aplikacja Hello ukończone znajduje się na końcu hello również w tym samouczku.

## <a name="step-1-register-an-app"></a>Krok 1: Rejestrowanie aplikacji
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. W menu hello u góry strony hello hello wybierz konta. W obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, w którym ma tooregister aplikacji.

3. Wybierz **więcej usług** w hello menu na powitania po lewej stronie ekranu hello, a następnie wybierz **usługi Azure Active Directory**.

4. Wybierz **rejestracji aplikacji**, a następnie wybierz **Dodaj**.

5. Wykonaj hello monity toocreate **aplikacji sieci Web** i/lub **WebAPI**.
  * Witaj **nazwa** aplikacji hello opisuje toousers Twojej aplikacji.

  * Witaj **adres URL logowania** jest hello podstawowy adres URL aplikacji.  Hello szkielet przez domyślną jest "http://localhost: 3000/auth/openid/powrotu".

6. Po zarejestrowaniu, usługi Azure AD przypisuje aplikacji identyfikatora aplikacji Potrzebujesz tej wartości w hello następujące sekcje, dlatego skopiuj go ze strony aplikacji hello.
7. Z hello **ustawienia** -> **właściwości** strony dla aplikacji, aktualizacji hello identyfikator URI aplikacji. Witaj **identyfikator URI aplikacji** to unikatowy identyfikator aplikacji. Konwencja Hello jest toouse hello format `https://<tenant-domain>/<app-name>`, na przykład: `https://contoso.onmicrosoft.com/my-first-aad-app`.

## <a name="step-2-add-prerequisites-tooyour-directory"></a>Krok 2: Dodaj katalog tooyour wymagania wstępne
1. Z wiersza polecenia hello, Zmień folder główny tooyour katalogów, jeśli nie masz już istnieje, a następnie hello uruchom następujące polecenia:

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. Ponadto należy `passport-azure-ad`:
    * `npm install passport-azure-ad`

Spowoduje to zainstalowanie bibliotek hello który `passport-azure-ad` zależy.

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>Krok 3: Konfigurowanie strategii passport-node-js hello toouse aplikacji
W tym miejscu możemy skonfigurować Express toouse hello protokołu uwierzytelniania OpenID Connect.  Usługa Passport jest używana toodo różne elementy, włącznie z żądaniami logowania i wylogowywania problem, zarządzanie sesji użytkownika hello i uzyskiwania informacji o hello użytkownika.

1. toobegin, otwórz hello `config.js` o hello katalog główny projektu hello plików, a następnie wprowadź wartości konfiguracji aplikacji w hello `exports.creds` sekcji.

  * Witaj `clientID` jest hello **identyfikator aplikacji** jest przypisany tooyour aplikacji w portalu rejestracji hello.

  * Witaj `returnURL` jest hello **identyfikator Uri przekierowania** wprowadzony w portalu hello.

  * Witaj `clientSecret` jest klucz tajny hello wygenerowane w portalu hello.

2. Następnie otwórz folder hello `app.js` pliku w katalogu głównym hello hello projektu. Następnie dodaj następujące wywołanie tooinvoke hello hello `OIDCStrategy` strategii dołączoną `passport-azure-ad`.

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. Po wykonaniu tej Użyj strategii hello możemy właśnie w odwołaniu toohandle naszych żądań logowania.

    ```JavaScript
    // Use hello OIDCStrategy within Passport. (Section 2)
    //
    //   Strategies in passport require a `validate` function that accepts
    //   credentials (in this case, an OpenID identifier), and invokes a callback
    //   with a user object.
    passport.use(new OIDCStrategy({
        callbackURL: config.creds.returnURL,
        realm: config.creds.realm,
        clientID: config.creds.clientID,
        clientSecret: config.creds.clientSecret,
        oidcIssuer: config.creds.issuer,
        identityMetadata: config.creds.identityMetadata,
        skipUserProfile: config.creds.skipUserProfile,
        responseType: config.creds.responseType,
        responseMode: config.creds.responseMode
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
        if (!profile.email) {
        return done(new Error("No email found"), null);
        }
        // asynchronous verification, for effect...
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
Usługa Passport używa podobnego wzorca do wszystkich swoich strategii (Twitter, Facebook itd.) zgodne ze wszyscy twórcy kodu strategii. Patrzeć strategii hello, możesz sprawdzić, czy jest przekazywana on funkcję, która ma token i gotowe jako parametry hello. Witaj strategia ponownie toous po jego działa. Następnie chcemy toostore hello użytkownika i token hello tymczasowym potrzebujemy nie tooask go ponownie.

> [!IMPORTANT]
Witaj poprzedni kod obejmuje wszystkich użytkowników, wykonywanej tooauthenticate tooour serwera. Jest to nazywane rejestracji automatycznej. Zaleca się, że nie zezwala każdy uwierzytelniania serwera produkcyjnego tooa bez uprzedniego je zarejestrować za pośrednictwem procesu, który podjęciu decyzji o. Jest to zwykle wzorzec hello, które widać w aplikacjach komercyjnych, które pozwalają tooregister z usługą Facebook, ale następnie poprosić tooprovide dodatkowe informacje. Jeśli to nie zostały przykładowej aplikacji, być może wyodrębniono adres e-mail użytkownika hello z hello obiektu tokena, który został zwrócony, a następnie zadawane toofill użytkownika hello dodatkowych informacji. Ponieważ jest to serwer testowy, możemy dodać je toohello bazy danych w pamięci.


4. Następnie możemy dodać metody hello, pozwalających nam tootrack hello zalogowanych użytkowników, co jest wymagane przez usługi Passport. Te metody obejmują serializację i deserializację informacji o użytkowniku hello.

    ```JavaScript

            // Passport session setup. (Section 2)

            //   toosupport persistent sign-in sessions, Passport needs toobe able to
            //   serialize users into hello session and deserialize them out of hello session. Typically,
            //   this is done simply by storing hello user ID when serializing and finding
            //   hello user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array toohold signed-in users
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

5.  Następnie możemy dodać aparat Express hello hello kodu tooload. Tutaj używamy hello domyślne /views i zapewnia wzorzec /routes Express.

    ```JavaScript

        // configure Express (section 2)

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

6. Ponadto możemy dodać hello kieruje tego Dostarcz hello rzeczywiste żądania rejestrowania toohello `passport-azure-ad` aparatu:


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware tooauthenticate the
        //   request. hello first step in OpenID authentication involves redirecting
        //   hello user tootheir OpenID provider. After authenticating, hello OpenID
        //   provider redirects hello user back toothis application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in hello Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Krok 4: Użycie usługi Passport tooissue logowania i wylogowywania żądań tooAzure AD
Aplikacja jest teraz prawidłowo skonfigurowana toocommunicate z punktem końcowym hello przy użyciu protokołu uwierzytelniania OpenID Connect hello.  `passport-azure-ad`ma podjąć obsługę wszystkich szczegółów hello obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i utrzymywanie sesji użytkownika. Wszystkie opcje, które pozostaje przyznawanie użytkownikom toosign sposób w i wylogowaniu i zbieranie dodatkowych informacji na temat hello zalogowanych użytkowników.

1. Po pierwsze możemy dodać hello domyślną, logowania konta i wylogowania tooour `app.js` pliku:

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
            log.info('Login was called in hello Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  Przejrzyj te szczegółowo umożliwia:

  * Witaj `/`trasa przekierowuje widoku index.ejs toohello przekazywanie hello użytkownika w żądaniu hello (jeśli istnieje).
  * Witaj `/account` trasy najpierw *temu firma Microsoft są uwierzytelniani* (wdrożymy który w hello poniższy przykład), a następnie przekazuje hello użytkownika w żądaniu hello tak, aby firma Microsoft może uzyskać dodatkowe informacje o hello użytkownika.
  * Witaj `/login` trasy wywołuje naszych uwierzytelniania azuread openidconnect z `passport-azuread`. Jeśli które się nie powiedzie, przekierowuje hello wstecz zbyt/dane logowania użytkownika.
  * Witaj `/logout` trasy po prostu wywołuje hello logout.ejs (i trasę), które czyści plików cookie, a następnie zwraca hello tooindex.ejs wstecz użytkownika.

3. Witaj ostatniej części `app.js`, Dodajmy hello **EnsureAuthenticated** metodę, która jest używana w `/account`, jak pokazano wcześniej.

    ```JavaScript

        // Simple route middleware tooensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs toobe protected. If
        //   hello request is authenticated (typically via a persistent sign-in session),
        //   hello request proceeds. Otherwise, hello user is redirected toothe
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. Na koniec Utwórz sam serwer hello w `app.js`:

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a>Krok 5: toodisplay naszych użytkowników w witrynie internetowej hello, tworzenie hello widoków i tras w Express
Teraz `app.js` została ukończona. Firma Microsoft po prostu muszą tooadd hello tras i wyświetla te informacje hello Pokaż możemy pobrać toohello użytkownika, jak również obsługiwać hello `/logout` i `/login` tras, na których utworzyliśmy.

1. Utwórz hello `/routes/index.js` trasy w katalogu głównym hello.

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. Utwórz hello `/routes/user.js` trasy w katalogu głównym hello.

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 Te przekazują hello żądania tooour widoków, w tym hello użytkownika, jeśli jest obecny.

3. Utwórz hello `/views/index.ejs` widoku w katalogu głównym hello. Jest to prosta strona, która wywołuje metody naszych zalogowania i wylogowania i pozwala nam informacje o koncie toograb. Należy zauważyć, że możemy użyć hello warunkowego `if (!user)` hello użytkownika są przekazywane w żądaniu hello jest dowód mamy zalogowanego użytkownika.

    ```JavaScript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
        <h2>Hello, <%= user.displayName %>.</h2>
        <a href="/account">Account Info</a></br>
        <a href="/logout">Log Out</a>
    <% } %>
    ```

4. Utwórz hello `/views/account.ejs` wyświetlać w katalogu głównym hello, co możemy wyświetlić dodatkowe informacje który `passport-azuread` umieścił w żądaniu użytkownika hello.

    ```Javascript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
    <p>displayName: <%= user.displayName %></p>
    <p>givenName: <%= user.name.givenName %></p>
    <p>familyName: <%= user.name.familyName %></p>
    <p>UPN: <%= user._json.upn %></p>
    <p>Profile ID: <%= user.id %></p>
  ##Next steps  <p>Full Claimes</p>
    <%- JSON.stringify(user) %>
    <p></p>
    <a href="/logout">Log Out</a>
    <% } %>
    ```

5. Upewnijmy to wygląd dobrej przez dodanie układ. Utwórz hello "/ views/layout.ejs widok w obszarze hello katalogu głównego.

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
                <a href="/login">Log In</a>
                </p>
            <% } else { %>
                <p>
                <a href="/">Home</a> |
                <a href="/account">Account</a> |
                <a href="/logout">Log Out</a>
                </p>
            <% } %>
            <%- body %>
        </body>
    </html>
    ```

##<a name="next-steps"></a>Następne kroki
Na koniec Skompiluj i uruchom aplikację. Uruchom `node app.js`, a następnie przejdź zbyt`http://localhost:3000`.

Zaloguj się za pomocą osobistego konta Microsoft lub konta służbowego i zwróć uwagę, jak tożsamość użytkownika hello jest widoczny w hello /account listy. Masz teraz zabezpieczone przy użyciu standardowych protokołach branżowych, uwierzytelniających użytkowników przy użyciu ich osobistych i pracy/służbowego konta aplikacji sieci web.

Odwołania, hello ukończone próbka (bez wartości konfiguracji) [jest dostępna jako plik .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip). Alternatywnie można ją sklonować z serwisu GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

Możesz teraz przejść do bardziej zaawansowanych tematów. Może być tootry:

[Zabezpieczanie interfejsu API za pomocą usługi Azure AD w sieci Web](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
