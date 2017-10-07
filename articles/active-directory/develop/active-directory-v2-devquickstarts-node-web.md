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
# <a name="add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="88b16-103">Dodawanie aplikacji sieci web Node.js tooa logowania</span><span class="sxs-lookup"><span data-stu-id="88b16-103">Add sign-in tooa Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="88b16-104">Nie wszystkie usługi Azure Active Directory scenariusze i funkcje działają z punktem końcowym v2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="88b16-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="88b16-105">toodetermine, czy należy używać punktu końcowego v2.0 hello lub punkt końcowy 1.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="88b16-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="88b16-106">W tym samouczku używamy hello toodo Passport następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="88b16-106">In this tutorial, we use Passport toodo hello following tasks:</span></span>

* <span data-ttu-id="88b16-107">W aplikacji sieci web logowania użytkownika hello przy użyciu usługi Azure Active Directory (Azure AD) i hello punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="88b16-107">In a web app, sign in hello user by using Azure Active Directory (Azure AD) and hello v2.0 endpoint.</span></span>
* <span data-ttu-id="88b16-108">Wyświetl informacje o użytkowniku hello.</span><span class="sxs-lookup"><span data-stu-id="88b16-108">Display information about hello user.</span></span>
* <span data-ttu-id="88b16-109">Znak hello użytkownika poza aplikacją hello.</span><span class="sxs-lookup"><span data-stu-id="88b16-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="88b16-110">**Passport** to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="88b16-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="88b16-111">Elastyczne i moduły, usługa Passport można dyskretnie usunięty w każdym ekspresowe lub restify aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="88b16-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="88b16-112">W usłudze Passport kompleksowy zestaw strategii obsługuje uwierzytelnianie przy użyciu nazwy użytkownika i hasła, Facebook, Twitter lub innych opcji.</span><span class="sxs-lookup"><span data-stu-id="88b16-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="88b16-113">Opracowaliśmy strategię dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88b16-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="88b16-114">W tym artykule zostanie przedstawiony zostanie sposób tooinstall hello modułu, a następnie dodaj hello Azure AD `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="88b16-114">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="88b16-115">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="88b16-115">Download</span></span>
<span data-ttu-id="88b16-116">Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="88b16-116">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="88b16-117">Samouczek hello toofollow, możesz [pobrać szkielet aplikacji hello jako plik .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) lub klonowania hello szkielet:</span><span class="sxs-lookup"><span data-stu-id="88b16-117">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="88b16-118">Umożliwia również wyświetlenie aplikacji hello ukończone na końcu hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="88b16-118">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="88b16-119">1: Rejestrowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="88b16-119">1: Register an app</span></span>
<span data-ttu-id="88b16-120">Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj [te szczegółowe kroki](active-directory-v2-app-registration.md) tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88b16-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="88b16-121">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="88b16-121">Make sure you:</span></span>

* <span data-ttu-id="88b16-122">Kopiuj hello **identyfikator aplikacji** przypisane tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88b16-122">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="88b16-123">Należy go w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="88b16-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="88b16-124">Dodaj hello **Web** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88b16-124">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="88b16-125">Kopiuj hello **identyfikator URI przekierowania** hello portalu.</span><span class="sxs-lookup"><span data-stu-id="88b16-125">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="88b16-126">Należy użyć wartości identyfikatora URI domyślne hello `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="88b16-126">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-tooyour-directory"></a><span data-ttu-id="88b16-127">2: Dodaj katalog tooyour wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="88b16-127">2: Add prerequisities tooyour directory</span></span>
<span data-ttu-id="88b16-128">W wierszu polecenia Zmień folder główny tooyour toogo katalogów, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="88b16-128">At a command prompt, change directories toogo tooyour root folder, if you are not already there.</span></span> <span data-ttu-id="88b16-129">Uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="88b16-129">Run hello following commands:</span></span>

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

<span data-ttu-id="88b16-130">Ponadto możemy użyć `passport-azure-ad` w hello szkielet hello Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="88b16-130">In addition, we use `passport-azure-ad` in hello skeleton of hello quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="88b16-131">Spowoduje to zainstalowanie bibliotek hello który `passport-azure-ad` używa.</span><span class="sxs-lookup"><span data-stu-id="88b16-131">This installs hello libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="88b16-132">3: Konfigurowanie strategii passport-node-js hello toouse aplikacji</span><span class="sxs-lookup"><span data-stu-id="88b16-132">3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="88b16-133">Konfigurowanie hello Express oprogramowanie pośredniczące toouse hello protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="88b16-133">Set up hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="88b16-134">Użyj żądania logowania i wylogowywania tooissue Passport, zarządzanie sesji użytkownika hello i uzyskać informacje o użytkowniku hello, między innymi.</span><span class="sxs-lookup"><span data-stu-id="88b16-134">You use Passport tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, among other things.</span></span>

1.  <span data-ttu-id="88b16-135">Witaj katalog główny projektu hello Otwórz hello pliku Config.js.</span><span class="sxs-lookup"><span data-stu-id="88b16-135">In hello root of hello project, open hello Config.js file.</span></span> <span data-ttu-id="88b16-136">W hello `exports.creds` wprowadź wartości konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88b16-136">In hello `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="88b16-137">`clientID`: hello **identyfikator aplikacji** jest przypisany tooyour aplikacji w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="88b16-137">`clientID`: hello **Application Id** that's assigned tooyour app in hello Azure portal.</span></span>
  * <span data-ttu-id="88b16-138">`returnURL`: hello **identyfikator URI przekierowania** wprowadzony w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="88b16-138">`returnURL`: hello **Redirect URI** that you entered in hello portal.</span></span>
  * <span data-ttu-id="88b16-139">`clientSecret`: hello hasło wygenerowane w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="88b16-139">`clientSecret`: hello secret that you generated in hello portal.</span></span>

2.  <span data-ttu-id="88b16-140">W kluczu głównym hello hello projektu otwórz plik App.js hello.</span><span class="sxs-lookup"><span data-stu-id="88b16-140">In hello root of hello project, open hello App.js file.</span></span> <span data-ttu-id="88b16-141">tooinvoke hello OIDCStrategy stratey, który jest dostarczany z `passport-azure-ad`, Dodaj następujące wywołanie hello:</span><span class="sxs-lookup"><span data-stu-id="88b16-141">tooinvoke hello OIDCStrategy stratey, which comes with `passport-azure-ad`, add hello following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="88b16-142">toohandle żądań logowania, użyj strategii hello, który właśnie w odwołaniu:</span><span class="sxs-lookup"><span data-stu-id="88b16-142">toohandle your sign-in requests, use hello strategy you just referenced:</span></span>

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

<span data-ttu-id="88b16-143">Usługa Passport używa podobnego wzorca do wszystkich swoich strategii (Twitter, Facebook i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="88b16-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="88b16-144">Wszystkich autorów toohello wzorca.</span><span class="sxs-lookup"><span data-stu-id="88b16-144">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="88b16-145">Przekaż strategii hello `function()` używającą tokenu i `done` jako parametry.</span><span class="sxs-lookup"><span data-stu-id="88b16-145">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="88b16-146">Strategia Hello jest zwracane, gdy robi swojej pracy.</span><span class="sxs-lookup"><span data-stu-id="88b16-146">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="88b16-147">Użytkownik hello magazynu i token hello tymczasowym, więc nie trzeba tooask go ponownie.</span><span class="sxs-lookup"><span data-stu-id="88b16-147">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="88b16-148">Hello poprzedni kod obejmuje wszystkich użytkowników, które można uwierzytelniać tooyour serwera.</span><span class="sxs-lookup"><span data-stu-id="88b16-148">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="88b16-149">Jest to nazywane rejestracji automatycznej.</span><span class="sxs-lookup"><span data-stu-id="88b16-149">This is known as auto-registration.</span></span> <span data-ttu-id="88b16-150">Na serwerze produkcyjnym nie ma toolet każdy użytkownik bez konieczności ich przejść przez proces rejestracji, który można wybrać.</span><span class="sxs-lookup"><span data-stu-id="88b16-150">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="88b16-151">Jest to zwykle hello wzorzec, który pojawi się w aplikacjach dla użytkowników indywidualnych.</span><span class="sxs-lookup"><span data-stu-id="88b16-151">This is usually hello pattern that you see in consumer apps.</span></span> <span data-ttu-id="88b16-152">Aplikacja Hello mogą zezwalać tooregister z usługą Facebook, ale następnie prosi on tooenter dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="88b16-152">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="88b16-153">Jeśli nie korzystasz z wiersza polecenia programu w tym samouczku, można wyodrębnić hello wiadomości e-mail z hello obiektu tokena, który jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="88b16-153">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="88b16-154">Następnie może poprosić użytkownika hello tooenter dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="88b16-154">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="88b16-155">Ponieważ jest to serwer testowy, Dodaj użytkownika hello bezpośrednio toohello w bazy danych pamięci.</span><span class="sxs-lookup"><span data-stu-id="88b16-155">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="88b16-156">Dodaj metody hello użycie tookeep śledzenie użytkowników, którym jest zalogowany, zgodnie z żądaniem usługi Passport.</span><span class="sxs-lookup"><span data-stu-id="88b16-156">Add hello methods that you use tookeep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="88b16-157">Obejmuje to serializację i deserializację informacji o użytkowniku hello:</span><span class="sxs-lookup"><span data-stu-id="88b16-157">This includes serializing and deserializing hello user's information:</span></span>

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

5.  <span data-ttu-id="88b16-158">Dodaj kod hello, który ładuje hello aparat Express.</span><span class="sxs-lookup"><span data-stu-id="88b16-158">Add hello code that loads hello Express engine.</span></span> <span data-ttu-id="88b16-159">Użyj /views domyślne hello i wzorzec /routes Express zapewnia:</span><span class="sxs-lookup"><span data-stu-id="88b16-159">You use hello default /views and /routes pattern that Express provides:</span></span>

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

6.  <span data-ttu-id="88b16-160">Dodaj hello POST kieruje tego Dostarcz hello rzeczywiste żądania rejestrowania toohello `passport-azure-ad` aparatu:</span><span class="sxs-lookup"><span data-stu-id="88b16-160">Add hello POST routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

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

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="88b16-161">4: użycie usługi Passport tooissue logowania i wylogowywania żądań tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="88b16-161">4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="88b16-162">Aplikacja jest teraz skonfigurowane toocommunicate z punktem końcowym v2.0 hello przy użyciu protokołu uwierzytelniania OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="88b16-162">Your app is now set up toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="88b16-163">Witaj `passport-azure-ad` strategii zajmuje się wszystkie szczegóły hello obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i podtrzymywanie sesji użytkowników hello.</span><span class="sxs-lookup"><span data-stu-id="88b16-163">hello `passport-azure-ad` strategy takes care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining hello user session.</span></span> <span data-ttu-id="88b16-164">Wszystkie pozostało toodo jest toogive użytkownikom toosign sposób w i znak poza i toogather więcej informacji na temat hello, użytkownik jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="88b16-164">All that is left toodo is toogive your users a way toosign in and sign out, and toogather more information about hello user who is signed in.</span></span>

1.  <span data-ttu-id="88b16-165">Dodaj hello **domyślne**, **logowania**, **konta**, i **wylogowania** pliku App.js tooyour metod:</span><span class="sxs-lookup"><span data-stu-id="88b16-165">Add hello **default**, **login**, **account**, and **logout** methods tooyour App.js file:</span></span>

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

  <span data-ttu-id="88b16-166">Poniżej przedstawiono szczegóły hello:</span><span class="sxs-lookup"><span data-stu-id="88b16-166">Here are hello details:</span></span>
    
    * <span data-ttu-id="88b16-167">Witaj `/` trasa przekierowuje toohello index.ejs widoku.</span><span class="sxs-lookup"><span data-stu-id="88b16-167">hello `/` route redirects toohello index.ejs view.</span></span> <span data-ttu-id="88b16-168">Przekazuje ono hello użytkownika w żądaniu hello (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="88b16-168">It passes hello user in hello request (if it exists).</span></span>
    * <span data-ttu-id="88b16-169">Witaj `/account` trasy najpierw *gwarantuje, że użytkownik jest uwierzytelniony* (zaimplementowaniem który w hello następującego kodu).</span><span class="sxs-lookup"><span data-stu-id="88b16-169">hello `/account` route first *ensures that you are authenticated* (you implement that in hello following code).</span></span> <span data-ttu-id="88b16-170">Następnie przekazuje użytkownika hello w żądaniu hello.</span><span class="sxs-lookup"><span data-stu-id="88b16-170">Then, it passes hello user in hello request.</span></span> <span data-ttu-id="88b16-171">Jest to, dzięki czemu możesz uzyskać więcej informacji na temat hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="88b16-171">This is so you can get more information about hello user.</span></span>
    * <span data-ttu-id="88b16-172">Witaj `/login` trasy wywołania z `azuread-openidconnect` uwierzytelniania z `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="88b16-172">hello `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="88b16-173">Jeśli które się nie powiedzie, zbyt przekierowuje użytkownika hello ponownie`/login`.</span><span class="sxs-lookup"><span data-stu-id="88b16-173">If that doesn't succeed, it redirects hello user back too`/login`.</span></span>
    * <span data-ttu-id="88b16-174">Witaj `/logout` trasy wywołuje hello logout.ejs widoku (i trasę).</span><span class="sxs-lookup"><span data-stu-id="88b16-174">hello `/logout` route calls hello logout.ejs view (and route).</span></span> <span data-ttu-id="88b16-175">Powoduje wyczyszczenie plików cookie, a następnie zwraca hello tooindex.ejs wstecz użytkownika.</span><span class="sxs-lookup"><span data-stu-id="88b16-175">This clears cookies, and then returns hello user back tooindex.ejs.</span></span>

2.  <span data-ttu-id="88b16-176">Dodaj hello **EnsureAuthenticated** metody użytej wcześniej wcześniej w `/account`:</span><span class="sxs-lookup"><span data-stu-id="88b16-176">Add hello **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

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

3.  <span data-ttu-id="88b16-177">W App.js Utwórz powitania serwera:</span><span class="sxs-lookup"><span data-stu-id="88b16-177">In App.js, create hello server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a><span data-ttu-id="88b16-178">5: tworzenie hello widoków i tras w Express przedstawia użytkownikowi na powitania witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="88b16-178">5: Create hello views and routes in Express that you show your user on hello website</span></span>
<span data-ttu-id="88b16-179">Dodawanie tras hello i widoków przedstawiających informacje toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="88b16-179">Add hello routes and views that show information toohello user.</span></span> <span data-ttu-id="88b16-180">Witaj trasy i widoki również obsługiwać hello `/logout` i `/login` tras, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="88b16-180">hello routes and views also handle hello `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="88b16-181">W katalogu głównym hello, Utwórz hello `/routes/index.js` trasy.</span><span class="sxs-lookup"><span data-stu-id="88b16-181">In hello root directory, create hello `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="88b16-182">W katalogu głównym hello, Utwórz hello `/routes/user.js` trasy.</span><span class="sxs-lookup"><span data-stu-id="88b16-182">In hello root directory, create hello `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="88b16-183">`/routes/index.js`i `/routes/user.js` są proste trasy przekazują hello żądania tooyour widoków, w tym hello użytkownika, jeśli jest obecny.</span><span class="sxs-lookup"><span data-stu-id="88b16-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along hello request tooyour views, including hello user, if present.</span></span>

3.  <span data-ttu-id="88b16-184">W katalogu głównym hello, Utwórz hello `/views/index.ejs` widoku.</span><span class="sxs-lookup"><span data-stu-id="88b16-184">In hello root directory, create hello `/views/index.ejs` view.</span></span> <span data-ttu-id="88b16-185">Ta strona wymaga programu **logowania** i **wylogowania** metody.</span><span class="sxs-lookup"><span data-stu-id="88b16-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="88b16-186">Możesz również użyć hello `/views/index.ejs` Wyświetl informacje o koncie toocapture.</span><span class="sxs-lookup"><span data-stu-id="88b16-186">You also use hello `/views/index.ejs` view toocapture account information.</span></span> <span data-ttu-id="88b16-187">Można użyć hello warunkowego `if (!user)` jako użytkownik hello są przekazywane w żądaniu hello.</span><span class="sxs-lookup"><span data-stu-id="88b16-187">You can use hello conditional `if (!user)` as hello user being passed through in hello request.</span></span> <span data-ttu-id="88b16-188">Jest dowód, że zalogowany użytkownik.</span><span class="sxs-lookup"><span data-stu-id="88b16-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="88b16-189">W katalogu głównym hello, Utwórz hello `/views/account.ejs` widoku.</span><span class="sxs-lookup"><span data-stu-id="88b16-189">In hello root directory, create hello `/views/account.ejs` view.</span></span> <span data-ttu-id="88b16-190">Witaj `/views/account.ejs` widok umożliwia dodatkowe informacje tooview który `passport-azuread` umieszcza w żądaniu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="88b16-190">hello `/views/account.ejs` view allows you tooview additional information that `passport-azuread` puts in hello user request.</span></span>

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

5.  <span data-ttu-id="88b16-191">Dodawanie układu.</span><span class="sxs-lookup"><span data-stu-id="88b16-191">Add a layout.</span></span> <span data-ttu-id="88b16-192">W katalogu głównym hello, Utwórz hello `/views/layout.ejs` widoku.</span><span class="sxs-lookup"><span data-stu-id="88b16-192">In hello root directory, create hello `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="88b16-193">toobuild i uruchom aplikację, uruchom `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="88b16-193">toobuild and run your app, run `node app.js`.</span></span> <span data-ttu-id="88b16-194">Następnie przejdź zbyt`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="88b16-194">Then, go too`http://localhost:3000`.</span></span>

7.  <span data-ttu-id="88b16-195">Zaloguj się za pomocą osobistego konta Microsoft lub konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="88b16-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="88b16-196">Należy pamiętać, że tożsamość użytkownika hello jest odzwierciedlana hello /account liście.</span><span class="sxs-lookup"><span data-stu-id="88b16-196">Note that hello user's identity is reflected in hello /account list.</span></span> 

<span data-ttu-id="88b16-197">Masz teraz aplikacji sieci web, który jest zabezpieczony za pomocą standardowych protokołach branżowych.</span><span class="sxs-lookup"><span data-stu-id="88b16-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="88b16-198">Użytkownicy mogą uwierzytelniać w aplikacji za pomocą ich kont osobistych i służbowych.</span><span class="sxs-lookup"><span data-stu-id="88b16-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88b16-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88b16-199">Next steps</span></span>
<span data-ttu-id="88b16-200">Odwołania, przykładowy ukończyć powitalnych (bez wartości konfiguracji) jest dostarczany jako [plik zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="88b16-200">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="88b16-201">Użytkownik może ją także sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="88b16-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="88b16-202">Następnie można przenieść na toomore Tematy zaawansowane.</span><span class="sxs-lookup"><span data-stu-id="88b16-202">Next, you can move on toomore advanced topics.</span></span> <span data-ttu-id="88b16-203">Może być tootry:</span><span class="sxs-lookup"><span data-stu-id="88b16-203">You might want tootry:</span></span>

[<span data-ttu-id="88b16-204">Zabezpieczanie interfejsu API sieci web Node.js za pomocą punktu końcowego v2.0 hello</span><span class="sxs-lookup"><span data-stu-id="88b16-204">Secure a Node.js web API by using hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="88b16-205">Poniżej przedstawiono dodatkowe zasoby:</span><span class="sxs-lookup"><span data-stu-id="88b16-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="88b16-206">Przewodnik dewelopera v2.0 usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="88b16-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="88b16-207">Tag "azure-active-directory" przepełnienie stosu</span><span class="sxs-lookup"><span data-stu-id="88b16-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="88b16-208">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="88b16-208">Get security updates for our products</span></span>
<span data-ttu-id="88b16-209">Firma Microsoft zachęca toosign się toobe powiadomienia w przypadku wystąpienia zdarzeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="88b16-209">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="88b16-210">Na powitania [powiadomień o zabezpieczeniach technicznych Microsoft](https://technet.microsoft.com/security/dd252948) pozycję subskrybować alerty klasyfikatory tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="88b16-210">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

