---
title: "Aplikacja sieci web Node.js aaaAdd tooa logowania dla usługi Azure B2C | Dokumentacja firmy Microsoft"
description: "Jak toobuild aplikacji sieci web Node.js który loguje się użytkowników przy użyciu dzierżawy B2C."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a>Usługa Azure AD B2C: Dodawanie aplikacji sieci web Node.js tooa logowania

**Passport** to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js. Jest to niezwykle elastyczne i modułowe oprogramowanie, które można dyskretnie zainstalować w dowolnej aplikacji sieci Web opartej na module Express lub Restify. Kompleksowy zestaw strategii obsługuje uwierzytelnianie przy użyciu m.in. nazwy użytkownika i hasła lub kont w serwisach Facebook i Twitter.

Opracowaliśmy strategię dla usługi Azure Active Directory (Azure AD). Zostanie zainstalowaniu tego modułu, a następnie dodaj hello Azure AD `passport-azure-ad` wtyczki.

toodo, musisz:

1. Zarejestrować aplikację w usłudze Azure AD.
2. Konfigurowanie Twojej aplikacji hello toouse `passport-azure-ad` wtyczki.
3. Użyj paszportu tooissue logowania i wylogowywania żądań tooAzure AD.
4. Wydrukować dane użytkownika.

Witaj kodu w tym samouczku [jest przechowywany w serwisie GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS). toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako plik .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip). Można również sklonować szkielet hello:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

Aplikacja Hello ukończone znajduje się na końcu hello tego samouczka.

## <a name="get-an-azure-ad-b2c-directory"></a>Tworzenie katalogu usługi Azure AD B2C

Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.  Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów. Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.

## <a name="create-an-application"></a>Tworzenie aplikacji

Następnie należy toocreate aplikację w katalogu usługi B2C. Dzięki temu informacji usługi Azure AD, że wymaga ona toocommunicate bezpiecznie z aplikacją. Witaj zarówno aplikacja klienta i interfejs API sieci web będą reprezentowane przez jeden **identyfikator aplikacji**, ponieważ stanowią jedną aplikację logiczną. toocreate usługi aplikacji, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md). Należy pamiętać o wykonaniu następujących czynności:

- Obejmują **aplikacji sieci web**/**interfejs API sieci web** w aplikacji hello.
- Wprowadź `http://localhost:3000/auth/openid/return` w polu **Adres URL odpowiedzi**. Jest hello domyślny adres URL dla tego przykładu kodu.
- Utwórz **klucz tajny aplikacji** i skopiuj go. Będzie potrzebny później. Należy pamiętać, że ta wartość musi toobe [XML w znaki ucieczki](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) przed jego użyciem.
- Kopiuj hello **identyfikator aplikacji** czyli przypisanej tooyour aplikacji. On również będzie później potrzebny.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Tworzenie zasad

W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md). Ta aplikacja obejmuje trzy środowiska tożsamości: rejestracji, logowania i logowania przy użyciu konta w serwisie Facebook. Należy toocreate tych zasad każdego typu zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Podczas tworzenia trzech zbiorów zasad należy koniecznie:

- Wybierz hello **Nazwa wyświetlana** i inne atrybuty rejestracji w ramach zasad rejestracji.
- Wybierz hello **Nazwa wyświetlana** i **obiektu o identyfikatorze** oświadczenia aplikacji we wszystkich zasadach. Można również wybrać inne oświadczenia.
- Kopiuj hello **nazwa** poszczególnych zasad po jego utworzeniu. Powinien on mieć prefiks hello `b2c_1_`.  Te nazwy zasad będą potrzebne później.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Po utworzeniu trzech zbiorów zasad, wszystko jest gotowe toobuild aplikacji.

Należy pamiętać, że w tym artykule nie opisano, jak zasady hello toouse właśnie utworzony. toolearn o sposób działania zasad w usłudze Azure AD B2C, rozpoczynać hello [.NET sieci web aplikacji Wprowadzenie — samouczek](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="add-prerequisites-tooyour-directory"></a>Dodaj katalog tooyour wymagania wstępne

Z wiersza polecenia hello Zmień folder główny tooyour katalogów, jeśli nie masz już istnieje. Uruchom następujące polecenia hello:

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

Ponadto użyliśmy `passport-azure-ad` naszym podglądzie w hello szkielet hello Szybki Start.

- `npm install passport-azure-ad`

Spowoduje to zainstalowanie bibliotek hello który `passport-azure-ad` zależy.

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a>Konfigurowanie Twojej aplikacji hello toouse strategii Passport-Node.js
Skonfiguruj hello Express oprogramowanie pośredniczące toouse hello protokołu uwierzytelniania OpenID Connect. Usługi Passport jest używane tooissue żądań logowania się i wylogowania, zarządzania sesjami użytkownika i uzyskiwania informacji o użytkownikach, między innymi.

Otwórz hello `config.js` plików w katalogu głównym hello hello projektu, a następnie wprowadź wartości konfiguracji aplikacji w hello `exports.creds` sekcji.
- `clientID`: hello **identyfikator aplikacji** przypisane tooyour aplikacji w portalu rejestracji hello.
- `returnURL`: hello **identyfikator URI przekierowania** wprowadzony w portalu hello.
- `tenantName`: Nazwa dzierżawy aplikacji, na przykład hello **contoso.onmicrosoft.com**.

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Otwórz hello `app.js` pliku w katalogu głównym hello hello projektu. Dodaj następujące wywołanie tooinvoke hello hello `OIDCStrategy` strategii dołączoną `passport-azure-ad`.


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

Użyj strategii hello właśnie w odwołaniu toohandle żądań logowania.

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
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
Program Passport używa podobnego wzorca do wszystkich swoich strategii (w tym serwisów Facebook i Twitter). Wszystkich autorów toothis wzorca. Po wyświetleniu strategii hello widać, że przekazujesz ją `function()` mający token i `done` jako parametry hello. Strategia Hello wróci tooyou po wykonaniu całego zadania. Przechowywanie hello użytkownika i zwijanie hello token, dzięki czemu nie trzeba tooask go ponownie.

> [!IMPORTANT]
Witaj poprzedni kod obejmuje wszystkich użytkowników, których uwierzytelnia serwer hello. Jest to autorejestracja. Podczas korzystania z serwerów produkcyjnych, nie mają toolet wśród użytkowników, chyba że ma przeszli procesu rejestracji, które zostały skonfigurowane. Sposób ten jest często stosowany w aplikacjach dla użytkowników indywidualnych. Te pozwalają tooregister za pomocą usługi Facebook, ale następnie prosi toofill dodatkowych informacji. Jeśli aplikacja nie była próbkę, firma Microsoft może wyodrębnić adres e-mail z hello obiektu tokena, który jest zwracany, a następnie poprosić toofill użytkownika hello dodatkowych informacji. Ponieważ jest to serwer testowy, zostają po prostu dodani użytkownicy toohello w pamięci z bazy danych.

Dodaj metody hello, które umożliwiają śledzenie tookeep użytkowników, którzy zalogowali się, co jest wymagane przez usługę Passport. Obejmuje to serializację i deserializację informacji o użytkowniku:

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
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

Dodaj aparat Express hello hello kodu tooload. W następujących hello widać, że używana domyślna hello `/views` i `/routes` wzorca, który udostępnia Express.

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

Dodaj hello `POST` tras, które przekazują hello toohello rzeczywiste żądania rejestrowania `passport-azure-ad` aparatu:

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Użyj paszportu tooissue logowania i wylogowywania żądań tooAzure AD

Aplikacja jest teraz prawidłowo skonfigurowany toocommunicate z punktem końcowym v2.0 hello przy użyciu protokołu uwierzytelniania OpenID Connect hello. `passport-azure-ad`została podjęta obsługę szczegóły hello obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i podtrzymywanie sesji użytkowników. Wszystkie opcje, które pozostaje jest toogive użytkownikom toosign sposób w i znak poza i toogather dodatkowe informacje o użytkownikach, którzy zalogowali się.

Najpierw dodaj hello domyślną, logowania konta i wylogowania tooyour `app.js` pliku:

```JavaScript

//Routes (Section 4)

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

tooreview tym metodom dokładniej:
- Witaj `/` trasa przekierowuje toohello `index.ejs` przez przekazanie użytkownika hello w żądaniu hello (jeśli istnieje).
- Witaj `/account` trasy najpierw sprawdza, czy użytkownik został uwierzytelniony (to jest poniżej hello implementacji). Następnie przekazuje użytkownika hello w żądaniu hello tak, aby uzyskać dodatkowe informacje na temat hello użytkownika.
- Witaj `/login` hello wywołania trasy `azuread-openidconnect` uwierzytelniania z `passport-azure-ad`. Jeśli to się nie powiedzie, trasy hello przekierowuje użytkownika hello wstecz zbyt`/login`.
- Trasa `/logout` po prostu wywołuje widok `logout.ejs` (i jego trasę). Powoduje wyczyszczenie plików cookie, a następnie zwraca hello użytkownika z powrotem zbyt`index.ejs`.


Witaj ostatniej części `app.js`, Dodaj hello `EnsureAuthenticated` metodę, która jest używana w hello `/account` trasy.

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

Na koniec Utwórz sam serwer hello w `app.js`.

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a>Utwórz widoki hello i kieruje w Express toocall zasad

Element `app.js` jest teraz gotowy. Wystarczy tooadd hello trasy i widoki, które pozwalają hello toocall zasad logowania i rejestrowania. Obsługują one również hello `/logout` i `/login` utworzone trasy.

Utwórz hello `/routes/index.js` trasy w katalogu głównym hello.

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

Utwórz hello `/routes/user.js` trasy w katalogu głównym hello.

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

Te proste trasy przekazują żądania tooyour widoków. Obejmują one hello użytkownika, jeśli występuje.

Utwórz hello `/views/index.ejs` widoku w katalogu głównym hello. Jest to prosta strona, która wywołuje zasady dotyczące logowania się i wylogowywania. Umożliwia także go toograb informacje o koncie. Uwaga służy hello warunkowego `if (!user)` jako hello użytkownika są przekazywane w żądania hello tooprovide dowody, ten użytkownik hello jest zalogowany.

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

Utwórz hello `/views/account.ejs` Wyświetl w katalogu głównym hello, dzięki czemu można wyświetlić dodatkowe informacje który `passport-azure-ad` put w żądaniu użytkownika hello.

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
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

Teraz możesz skompilować i uruchomić aplikację.

Uruchom `node app.js` i przejdź zbyt`http://localhost:3000`


Zarejestruj się lub zaloguj się w aplikacji toohello za pomocą poczty e-mail lub usługi Facebook. Wyloguj się i zaloguj ponownie jako inny użytkownik.

##<a name="next-steps"></a>Następne kroki

Odwołania, hello ukończone próbka (bez wartości konfiguracji) [jest dostępna jako plik .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip). Można ją także sklonować z serwisu GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

Możesz teraz przejść toomore Tematy zaawansowane. Zobacz te tematy:

[Zabezpieczanie interfejsu API sieci web przy użyciu modelu hello B2C w środowisku Node.js](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
