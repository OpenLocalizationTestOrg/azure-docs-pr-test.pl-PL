---
title: Azure Active Directory v2.0 logowanie aplikacji sieci web Node.js | Dokumentacja firmy Microsoft
description: "Informacje o sposobie tworzenia aplikacji sieci web Node.js, który loguje się użytkownik, używając osobistego konta Microsoft i konta firmowego lub szkolnego."
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
ms.openlocfilehash: 6d49c742f72440e22830915c90de009d9188db2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="770cf-103">Dodaj logowanie do aplikacji sieci web Node.js</span><span class="sxs-lookup"><span data-stu-id="770cf-103">Add sign-in to a Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="770cf-104">Nie wszystkie usługi Azure Active Directory scenariusze i funkcje działają z punktem końcowym v2.0.</span><span class="sxs-lookup"><span data-stu-id="770cf-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="770cf-105">Aby ustalić, czy należy używać punktu końcowego v2.0 lub punkt końcowy w wersji 1.0, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="770cf-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="770cf-106">W tym samouczku używamy Passport do wykonywania następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="770cf-106">In this tutorial, we use Passport to do the following tasks:</span></span>

* <span data-ttu-id="770cf-107">W aplikacji sieci web logowania użytkownika, przy użyciu usługi Azure Active Directory (Azure AD) i punktu końcowego v2.0.</span><span class="sxs-lookup"><span data-stu-id="770cf-107">In a web app, sign in the user by using Azure Active Directory (Azure AD) and the v2.0 endpoint.</span></span>
* <span data-ttu-id="770cf-108">Wyświetl informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="770cf-108">Display information about the user.</span></span>
* <span data-ttu-id="770cf-109">Zaloguj użytkownika poza aplikacją.</span><span class="sxs-lookup"><span data-stu-id="770cf-109">Sign the user out of the app.</span></span>

<span data-ttu-id="770cf-110">**Passport** to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="770cf-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="770cf-111">Elastyczne i moduły, usługa Passport można dyskretnie usunięty w każdym ekspresowe lub restify aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="770cf-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="770cf-112">W usłudze Passport kompleksowy zestaw strategii obsługuje uwierzytelnianie przy użyciu nazwy użytkownika i hasła, Facebook, Twitter lub innych opcji.</span><span class="sxs-lookup"><span data-stu-id="770cf-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="770cf-113">Opracowaliśmy strategię dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="770cf-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="770cf-114">W tym artykule, firma Microsoft opisano, jak zainstalować moduł, a następnie dodaj usługi Azure AD `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="770cf-114">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="770cf-115">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="770cf-115">Download</span></span>
<span data-ttu-id="770cf-116">Kod używany w tym samouczku jest przechowywany [ w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="770cf-116">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="770cf-117">Aby użyć tego samouczka, możesz [pobrać szkielet aplikacji w pliku .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) lub sklonować szkielet:</span><span class="sxs-lookup"><span data-stu-id="770cf-117">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="770cf-118">Możesz również uzyskać ukończona aplikacja na końcu tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="770cf-118">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="770cf-119">1: Rejestrowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="770cf-119">1: Register an app</span></span>
<span data-ttu-id="770cf-120">Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj [te szczegółowe kroki](active-directory-v2-app-registration.md) zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="770cf-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="770cf-121">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="770cf-121">Make sure you:</span></span>

* <span data-ttu-id="770cf-122">Kopiuj **identyfikator aplikacji** przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="770cf-122">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="770cf-123">Należy go w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="770cf-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="770cf-124">Dodaj **Web** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="770cf-124">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="770cf-125">Kopiuj **identyfikator URI przekierowania** z portalu.</span><span class="sxs-lookup"><span data-stu-id="770cf-125">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="770cf-126">Należy używać domyślnej wartości identyfikatora URI z `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="770cf-126">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-to-your-directory"></a><span data-ttu-id="770cf-127">2: Dodawanie Konfigurator do katalogu</span><span class="sxs-lookup"><span data-stu-id="770cf-127">2: Add prerequisities to your directory</span></span>
<span data-ttu-id="770cf-128">W wierszu polecenia przejdź do przejdź do folderu głównego, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="770cf-128">At a command prompt, change directories to go to your root folder, if you are not already there.</span></span> <span data-ttu-id="770cf-129">Uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="770cf-129">Run the following commands:</span></span>

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

<span data-ttu-id="770cf-130">Ponadto możemy użyć `passport-azure-ad` w przewodniku Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="770cf-130">In addition, we use `passport-azure-ad` in the skeleton of the quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="770cf-131">Spowoduje to zainstalowanie bibliotek który `passport-azure-ad` używa.</span><span class="sxs-lookup"><span data-stu-id="770cf-131">This installs the libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="770cf-132">3: Konfigurowanie aplikacji do użycia strategii passport-node-js</span><span class="sxs-lookup"><span data-stu-id="770cf-132">3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="770cf-133">Konfigurowanie oprogramowania pośredniczącego Express do używania protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="770cf-133">Set up the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="770cf-134">Możesz użyć programu Passport do wysyłania żądań zalogowania się i wylogowania, zarządzania sesji użytkownika i uzyskać informacje o użytkowniku, między innymi.</span><span class="sxs-lookup"><span data-stu-id="770cf-134">You use Passport to issue sign-in and sign-out requests, manage the user's session, and get information about the user, among other things.</span></span>

1.  <span data-ttu-id="770cf-135">W katalogu głównym projektu otwórz plik Config.js.</span><span class="sxs-lookup"><span data-stu-id="770cf-135">In the root of the project, open the Config.js file.</span></span> <span data-ttu-id="770cf-136">W `exports.creds` wprowadź wartości konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="770cf-136">In the `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="770cf-137">`clientID`: **Identyfikator aplikacji** przypisany do aplikacji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="770cf-137">`clientID`: The **Application Id** that's assigned to your app in the Azure portal.</span></span>
  * <span data-ttu-id="770cf-138">`returnURL`: **Identyfikator URI przekierowania** wprowadzony w portalu.</span><span class="sxs-lookup"><span data-stu-id="770cf-138">`returnURL`: The **Redirect URI** that you entered in the portal.</span></span>
  * <span data-ttu-id="770cf-139">`clientSecret`Klucz tajny, który wygenerował w portalu.</span><span class="sxs-lookup"><span data-stu-id="770cf-139">`clientSecret`: The secret that you generated in the portal.</span></span>

2.  <span data-ttu-id="770cf-140">W katalogu głównym projektu otwórz plik App.js.</span><span class="sxs-lookup"><span data-stu-id="770cf-140">In the root of the project, open the App.js file.</span></span> <span data-ttu-id="770cf-141">Aby wywołać stratey OIDCStrategy, który jest dostarczany z `passport-azure-ad`, Dodaj następujące wywołanie:</span><span class="sxs-lookup"><span data-stu-id="770cf-141">To invoke the OIDCStrategy stratey, which comes with `passport-azure-ad`, add the following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="770cf-142">Do obsługi żądań logowania, użyj strategii, które właśnie w odwołaniu:</span><span class="sxs-lookup"><span data-stu-id="770cf-142">To handle your sign-in requests, use the strategy you just referenced:</span></span>

  ```JavaScript
  // Use the OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. The function accepts
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

<span data-ttu-id="770cf-143">Usługa Passport używa podobnego wzorca do wszystkich swoich strategii (Twitter, Facebook i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="770cf-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="770cf-144">Wszyscy twórcy kodu strategii jest zgodna z wzorcem.</span><span class="sxs-lookup"><span data-stu-id="770cf-144">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="770cf-145">Przekaż strategii `function()` używającą tokenu i `done` jako parametry.</span><span class="sxs-lookup"><span data-stu-id="770cf-145">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="770cf-146">Strategia jest zwracane, gdy istnieje swojej pracy.</span><span class="sxs-lookup"><span data-stu-id="770cf-146">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="770cf-147">Przechowaj dane użytkownika i Zapisz token, więc nie trzeba było zażądać go ponownie.</span><span class="sxs-lookup"><span data-stu-id="770cf-147">Store the user and stash the token so you don’t need to ask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="770cf-148">Poprzedni kod obejmuje każdy użytkownik, który może uwierzytelniać się z serwerem.</span><span class="sxs-lookup"><span data-stu-id="770cf-148">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="770cf-149">Jest to nazywane rejestracji automatycznej.</span><span class="sxs-lookup"><span data-stu-id="770cf-149">This is known as auto-registration.</span></span> <span data-ttu-id="770cf-150">Na serwerze produkcyjnym nie mają mieć możliwość każda osoba, która bez konieczności ich przejść przez proces rejestracji, który można wybrać.</span><span class="sxs-lookup"><span data-stu-id="770cf-150">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="770cf-151">Jest to zwykle wzorzec, który pojawi się w aplikacjach dla użytkowników indywidualnych.</span><span class="sxs-lookup"><span data-stu-id="770cf-151">This is usually the pattern that you see in consumer apps.</span></span> <span data-ttu-id="770cf-152">Aplikacja może pozwala zarejestrować się w serwisie Facebook, ale następnie prosi o podanie dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="770cf-152">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="770cf-153">Jeśli nie korzystasz z wiersza polecenia programu w tym samouczku, można wyodrębnić wiadomości e-mail z obiektu tokena, który jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="770cf-153">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="770cf-154">Następnie może poprosić użytkownika o podanie dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="770cf-154">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="770cf-155">Ponieważ jest to serwer testowy, możesz dodać użytkownika bezpośrednio do bazy danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="770cf-155">Because this is a test server, you add the user directly to the in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="770cf-156">Dodaj metody, które służą do śledzenia użytkowników, którzy są podpisane, zgodnie z żądaniem usługi Passport.</span><span class="sxs-lookup"><span data-stu-id="770cf-156">Add the methods that you use to keep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="770cf-157">Obejmuje to serializację i deserializację informacji użytkownika:</span><span class="sxs-lookup"><span data-stu-id="770cf-157">This includes serializing and deserializing the user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   To support persistent login sessions, Passport needs to be able to
  //   serialize users into, and deserialize users out of, the session. Typically,
  //   this is as simple as storing the user ID when serializing, and finding
  //   the user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array to hold signed-in users
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

5.  <span data-ttu-id="770cf-158">Dodaj kod, który ładuje aparat Express.</span><span class="sxs-lookup"><span data-stu-id="770cf-158">Add the code that loads the Express engine.</span></span> <span data-ttu-id="770cf-159">Użyj /views domyślne i zawiera wzorzec /routes Express:</span><span class="sxs-lookup"><span data-stu-id="770cf-159">You use the default /views and /routes pattern that Express provides:</span></span>

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
    // Initialize Passport!  Also use passport.session() middleware, to support
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="770cf-160">Dodaj WPIS kieruje tego Dostarcz rzeczywiste żądania rejestrowania do `passport-azure-ad` aparatu:</span><span class="sxs-lookup"><span data-stu-id="770cf-160">Add the POST routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. The first step in OpenID authentication involves redirecting
  //   the user to the user's OpenID provider. After authenticating, the OpenID
  //   provider redirects the user back to this application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in the sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called.
  //   In this example, it redirects the user to the home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called. 
  //   In this example, it redirects the user to the home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="770cf-161">4: Użyj Passport do wysyłania żądań zalogowania się i wylogowania do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="770cf-161">4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="770cf-162">Aplikacja jest teraz skonfigurowane do komunikacji z punktem końcowym v2.0 za pomocą protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="770cf-162">Your app is now set up to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="770cf-163">`passport-azure-ad` Strategii zajmuje się wszystkie szczegóły obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i podtrzymywanie sesji użytkowników.</span><span class="sxs-lookup"><span data-stu-id="770cf-163">The `passport-azure-ad` strategy takes care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining the user session.</span></span> <span data-ttu-id="770cf-164">Pozostało celu ma zapewnić użytkownikom taki sposób, aby zalogować się i wylogowywania oraz zebrać więcej informacji na temat użytkownika, który jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="770cf-164">All that is left to do is to give your users a way to sign in and sign out, and to gather more information about the user who is signed in.</span></span>

1.  <span data-ttu-id="770cf-165">Dodaj **domyślne**, **logowania**, **konta**, i **wylogowania** metod do pliku App.js:</span><span class="sxs-lookup"><span data-stu-id="770cf-165">Add the **default**, **login**, **account**, and **logout** methods to your App.js file:</span></span>

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
      log.info('Login was called in the sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="770cf-166">Oto szczegóły:</span><span class="sxs-lookup"><span data-stu-id="770cf-166">Here are the details:</span></span>
    
    * <span data-ttu-id="770cf-167">`/` Trasa przekierowuje do widoku index.ejs.</span><span class="sxs-lookup"><span data-stu-id="770cf-167">The `/` route redirects to the index.ejs view.</span></span> <span data-ttu-id="770cf-168">Przekazuje użytkownika w żądaniu (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="770cf-168">It passes the user in the request (if it exists).</span></span>
    * <span data-ttu-id="770cf-169">`/account` Trasy najpierw *gwarantuje, że użytkownik jest uwierzytelniony* (zaimplementowaniem który w poniższym kodzie).</span><span class="sxs-lookup"><span data-stu-id="770cf-169">The `/account` route first *ensures that you are authenticated* (you implement that in the following code).</span></span> <span data-ttu-id="770cf-170">Następnie przekazuje użytkownika w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="770cf-170">Then, it passes the user in the request.</span></span> <span data-ttu-id="770cf-171">Jest to, aby uzyskać więcej informacji o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="770cf-171">This is so you can get more information about the user.</span></span>
    * <span data-ttu-id="770cf-172">`/login` Trasy wywołania z `azuread-openidconnect` uwierzytelniania z `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="770cf-172">The `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="770cf-173">Jeśli które się nie powiedzie, przekierowuje użytkownika do `/login`.</span><span class="sxs-lookup"><span data-stu-id="770cf-173">If that doesn't succeed, it redirects the user back to `/login`.</span></span>
    * <span data-ttu-id="770cf-174">`/logout` Trasy wywołuje logout.ejs widoku (i trasę).</span><span class="sxs-lookup"><span data-stu-id="770cf-174">The `/logout` route calls the logout.ejs view (and route).</span></span> <span data-ttu-id="770cf-175">Powoduje wyczyszczenie plików cookie, a następnie wróci użytkownika index.ejs.</span><span class="sxs-lookup"><span data-stu-id="770cf-175">This clears cookies, and then returns the user back to index.ejs.</span></span>

2.  <span data-ttu-id="770cf-176">Dodaj **EnsureAuthenticated** metody użytej wcześniej wcześniej w `/account`:</span><span class="sxs-lookup"><span data-stu-id="770cf-176">Add the **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware to ensure the user is authenticated (section 4)

  //   Use this route middleware on any resource that needs to be protected. If
  //   the request is authenticated (typically via a persistent login session),
  //   the request proceeds. Otherwise, the user is redirected to the
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="770cf-177">W App.js należy utworzyć serwer:</span><span class="sxs-lookup"><span data-stu-id="770cf-177">In App.js, create the server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-the-views-and-routes-in-express-that-you-show-your-user-on-the-website"></a><span data-ttu-id="770cf-178">5: tworzenie widoków i tras w Express przedstawia użytkownikowi w witrynie sieci Web</span><span class="sxs-lookup"><span data-stu-id="770cf-178">5: Create the views and routes in Express that you show your user on the website</span></span>
<span data-ttu-id="770cf-179">Dodaj trasy i widoki, które zawierają informacje dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="770cf-179">Add the routes and views that show information to the user.</span></span> <span data-ttu-id="770cf-180">Trasy i widoki również obsługiwać `/logout` i `/login` tras, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="770cf-180">The routes and views also handle the `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="770cf-181">W katalogu głównym, należy utworzyć `/routes/index.js` trasy.</span><span class="sxs-lookup"><span data-stu-id="770cf-181">In the root directory, create the `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="770cf-182">W katalogu głównym, należy utworzyć `/routes/user.js` trasy.</span><span class="sxs-lookup"><span data-stu-id="770cf-182">In the root directory, create the `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="770cf-183">`/routes/index.js`i `/routes/user.js` są proste trasy przekazują żądania do widoków, w tym użytkownika, jeśli jest obecny.</span><span class="sxs-lookup"><span data-stu-id="770cf-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along the request to your views, including the user, if present.</span></span>

3.  <span data-ttu-id="770cf-184">W katalogu głównym, należy utworzyć `/views/index.ejs` widoku.</span><span class="sxs-lookup"><span data-stu-id="770cf-184">In the root directory, create the `/views/index.ejs` view.</span></span> <span data-ttu-id="770cf-185">Ta strona wymaga programu **logowania** i **wylogowania** metody.</span><span class="sxs-lookup"><span data-stu-id="770cf-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="770cf-186">Można również użyć `/views/index.ejs` widok, aby przechwycić informacje o koncie.</span><span class="sxs-lookup"><span data-stu-id="770cf-186">You also use the `/views/index.ejs` view to capture account information.</span></span> <span data-ttu-id="770cf-187">Możesz użyć spójnika `if (!user)` jako użytkownik, są przekazywane w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="770cf-187">You can use the conditional `if (!user)` as the user being passed through in the request.</span></span> <span data-ttu-id="770cf-188">Jest dowód, że zalogowany użytkownik.</span><span class="sxs-lookup"><span data-stu-id="770cf-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="770cf-189">W katalogu głównym, należy utworzyć `/views/account.ejs` widoku.</span><span class="sxs-lookup"><span data-stu-id="770cf-189">In the root directory, create the `/views/account.ejs` view.</span></span> <span data-ttu-id="770cf-190">`/views/account.ejs` Widoku umożliwia wyświetlanie dodatkowych informacji który `passport-azuread` umieszcza w żądaniu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="770cf-190">The `/views/account.ejs` view allows you to view additional information that `passport-azuread` puts in the user request.</span></span>

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

5.  <span data-ttu-id="770cf-191">Dodawanie układu.</span><span class="sxs-lookup"><span data-stu-id="770cf-191">Add a layout.</span></span> <span data-ttu-id="770cf-192">W katalogu głównym, należy utworzyć `/views/layout.ejs` widoku.</span><span class="sxs-lookup"><span data-stu-id="770cf-192">In the root directory, create the `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="770cf-193">Aby skompilować i uruchomić aplikację, uruchom `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="770cf-193">To build and run your app, run `node app.js`.</span></span> <span data-ttu-id="770cf-194">Następnie przejdź do `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="770cf-194">Then, go to `http://localhost:3000`.</span></span>

7.  <span data-ttu-id="770cf-195">Zaloguj się za pomocą osobistego konta Microsoft lub konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="770cf-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="770cf-196">Należy pamiętać, że tożsamość użytkownika jest odzwierciedlone na liście /account.</span><span class="sxs-lookup"><span data-stu-id="770cf-196">Note that the user's identity is reflected in the /account list.</span></span> 

<span data-ttu-id="770cf-197">Masz teraz aplikacji sieci web, który jest zabezpieczony za pomocą standardowych protokołach branżowych.</span><span class="sxs-lookup"><span data-stu-id="770cf-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="770cf-198">Użytkownicy mogą uwierzytelniać w aplikacji za pomocą ich kont osobistych i służbowych.</span><span class="sxs-lookup"><span data-stu-id="770cf-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="770cf-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="770cf-199">Next steps</span></span>
<span data-ttu-id="770cf-200">Odwołania, ukończonych próbka (bez wartości konfiguracji) jest dostępna jako [plik zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="770cf-200">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="770cf-201">Użytkownik może ją także sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="770cf-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="770cf-202">Następnie możesz przejść do bardziej zaawansowanych tematów.</span><span class="sxs-lookup"><span data-stu-id="770cf-202">Next, you can move on to more advanced topics.</span></span> <span data-ttu-id="770cf-203">Można spróbować:</span><span class="sxs-lookup"><span data-stu-id="770cf-203">You might want to try:</span></span>

[<span data-ttu-id="770cf-204">Zabezpieczanie interfejsu API sieci web Node.js za pomocą punktu końcowego v2.0</span><span class="sxs-lookup"><span data-stu-id="770cf-204">Secure a Node.js web API by using the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="770cf-205">Poniżej przedstawiono dodatkowe zasoby:</span><span class="sxs-lookup"><span data-stu-id="770cf-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="770cf-206">Przewodnik dewelopera v2.0 usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="770cf-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="770cf-207">Tag "azure-active-directory" przepełnienie stosu</span><span class="sxs-lookup"><span data-stu-id="770cf-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="770cf-208">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="770cf-208">Get security updates for our products</span></span>
<span data-ttu-id="770cf-209">Firma Microsoft zachęca do Zarejestruj się, aby otrzymać powiadomienie, gdy występujących incydentach zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="770cf-209">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="770cf-210">Na [powiadomień o zabezpieczeniach technicznych Microsoft](https://technet.microsoft.com/security/dd252948) strony, należy subskrybować alerty klasyfikatory zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="770cf-210">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

