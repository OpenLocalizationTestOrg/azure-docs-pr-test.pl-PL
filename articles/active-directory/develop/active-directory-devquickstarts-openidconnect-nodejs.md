---
title: "Wprowadzenie do korzystania z usługi Azure AD, logowania i wylogowywania, przy użyciu środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia aplikacji sieci web Node.js Express MVC, która integruje się z usługą Azure AD dla logowania."
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
ms.openlocfilehash: 13317b016f9ff3955f376b858645c42668b0de42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="25967-103">Aplikacja sieci web node.js logowania i wylogowywania z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="25967-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="25967-104">W tym miejscu możemy użyć usługi Passport:</span><span class="sxs-lookup"><span data-stu-id="25967-104">Here we use Passport to:</span></span>

* <span data-ttu-id="25967-105">Zalogować użytkownika do aplikacji w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="25967-105">Sign the user in to the app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="25967-106">Wyświetl informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="25967-106">Display information about the user.</span></span>
* <span data-ttu-id="25967-107">Zaloguj użytkownika poza aplikacją.</span><span class="sxs-lookup"><span data-stu-id="25967-107">Sign the user out of the app.</span></span>

<span data-ttu-id="25967-108">Usługa Passport to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="25967-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="25967-109">Elastyczne i moduły, usługa Passport można dyskretnie usunięty każdym Express opartą na lub restify aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="25967-109">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or restify web application.</span></span> <span data-ttu-id="25967-110">Kompleksowy zestaw strategii obsługuje uwierzytelniania przy użyciu nazwy użytkownika i hasła, Facebook i Twitter.</span><span class="sxs-lookup"><span data-stu-id="25967-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="25967-111">Opracowaliśmy strategię dla usługi Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="25967-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="25967-112">Firma Microsoft zainstalowaniu tego modułu, a następnie dodaj Microsoft Azure Active Directory `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="25967-112">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="25967-113">W tym celu należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="25967-113">To do this, take the following steps:</span></span>

1. <span data-ttu-id="25967-114">Rejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25967-114">Register an app.</span></span>
2. <span data-ttu-id="25967-115">Konfigurowanie aplikacji do użycia `passport-azure-ad` strategii.</span><span class="sxs-lookup"><span data-stu-id="25967-115">Set up your app to use the `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="25967-116">Użyć programu Passport do wysyłania do usługi Azure AD żądań zalogowania się i wylogowania.</span><span class="sxs-lookup"><span data-stu-id="25967-116">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="25967-117">Wydrukować dane o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="25967-117">Print data about the user.</span></span>

<span data-ttu-id="25967-118">Kod używany w tym samouczku jest przechowywany [ w serwisie GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="25967-118">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="25967-119">Aby z niego skorzystać, można [pobrać szkielet aplikacji w pliku .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) lub sklonować szkielet:</span><span class="sxs-lookup"><span data-stu-id="25967-119">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="25967-120">Ukończona aplikacja znajduje się na końcu również w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="25967-120">The completed application is provided at the end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="25967-121">Krok 1: Rejestrowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="25967-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="25967-122">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="25967-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="25967-123">W menu w górnej części strony wybierz konto.</span><span class="sxs-lookup"><span data-stu-id="25967-123">In the menu at the top of the page, select your account.</span></span> <span data-ttu-id="25967-124">W obszarze **katalogu** wybierz dzierżawy usługi Active Directory, które chcesz zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="25967-124">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="25967-125">Wybierz **więcej usług** w menu po lewej stronie ekranu, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="25967-125">Select **More Services** in the menu on the left side of the screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="25967-126">Wybierz **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="25967-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="25967-127">Postępuj zgodnie z monitami, aby utworzyć **aplikacji sieci Web** i/lub **WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="25967-127">Follow the prompts to create a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="25967-128">**Nazwa** aplikacji opisuje aplikacji dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="25967-128">The **name** of the application describes your application to users.</span></span>

  * <span data-ttu-id="25967-129">**Adres URL logowania** jest podstawowy adres URL aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25967-129">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="25967-130">Domyślnie szkielet "http://localhost: 3000/auth/openid/powrotu".</span><span class="sxs-lookup"><span data-stu-id="25967-130">The skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="25967-131">Po zarejestrowaniu, usługi Azure AD przypisuje aplikacji identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="25967-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="25967-132">Potrzebujesz tej wartości w poniższych sekcjach, dlatego skopiuj go ze strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25967-132">You need this value in the following sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="25967-133">Z **ustawienia** -> **właściwości** strony dla aplikacji, zaktualizuj identyfikator URI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25967-133">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="25967-134">**Identyfikator URI aplikacji** to unikatowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25967-134">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="25967-135">Konwencji jest użycie formatu `https://<tenant-domain>/<app-name>`, na przykład: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="25967-135">The convention is to use the format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-to-your-directory"></a><span data-ttu-id="25967-136">Krok 2: Dodawanie wymagań wstępnych do katalogu</span><span class="sxs-lookup"><span data-stu-id="25967-136">Step 2: Add prerequisites to your directory</span></span>
1. <span data-ttu-id="25967-137">W wierszu polecenia Zmień katalog na folder główny, jeśli nie masz już istnieje, a następnie uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="25967-137">From the command line, change directories to your root folder if you're not already there, and then run the following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="25967-138">Ponadto należy `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="25967-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="25967-139">Spowoduje to zainstalowanie bibliotek który `passport-azure-ad` zależy.</span><span class="sxs-lookup"><span data-stu-id="25967-139">This installs the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="25967-140">Krok 3: Konfigurowanie aplikacji do użycia strategii passport-node-js</span><span class="sxs-lookup"><span data-stu-id="25967-140">Step 3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="25967-141">W tym miejscu możemy skonfigurować Express do używania protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="25967-141">Here, we configure Express to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="25967-142">Usługa Passport umożliwia wykonywanie różnych czynności, włącznie z żądaniami logowania i wylogowywania problem, zarządzanie sesji użytkownika i uzyskać informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="25967-142">Passport is used to do various things, including issue sign-in and sign-out requests, manage the user's session, and get information about the user.</span></span>

1. <span data-ttu-id="25967-143">Aby rozpocząć, otwórz `config.js` plików w katalogu głównym projektu, a następnie wprowadź wartości konfiguracji aplikacji w `exports.creds` sekcji.</span><span class="sxs-lookup"><span data-stu-id="25967-143">To begin, open the `config.js` file at the root of the project, and then enter your app's configuration values in the `exports.creds` section.</span></span>

  * <span data-ttu-id="25967-144">`clientID` Jest **identyfikator aplikacji** przypisany do aplikacji w portalu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="25967-144">The `clientID` is the **Application Id** that's assigned to your app in the registration portal.</span></span>

  * <span data-ttu-id="25967-145">`returnURL` Jest **identyfikator Uri przekierowania** wprowadzony w portalu.</span><span class="sxs-lookup"><span data-stu-id="25967-145">The `returnURL` is the **Redirect Uri** that you entered in the portal.</span></span>

  * <span data-ttu-id="25967-146">`clientSecret` Jest klucz tajny, który wygenerował w portalu.</span><span class="sxs-lookup"><span data-stu-id="25967-146">The `clientSecret` is the secret that you generated in the portal.</span></span>

2. <span data-ttu-id="25967-147">Następnie otwórz folder `app.js` w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="25967-147">Next, open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="25967-148">Następnie dodaj następujące wywołanie do wywołania `OIDCStrategy` strategii dołączoną `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="25967-148">Then add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="25967-149">Po wykonaniu tej Użyj strategii możemy właśnie w odwołaniu do obsługi żądań logowania naszych.</span><span class="sxs-lookup"><span data-stu-id="25967-149">After that, use the strategy we just referenced to handle our sign-in requests.</span></span>

    ```JavaScript
    // Use the OIDCStrategy within Passport. (Section 2)
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
<span data-ttu-id="25967-150">Usługa Passport używa podobnego wzorca do wszystkich swoich strategii (Twitter, Facebook itd.) zgodne ze wszyscy twórcy kodu strategii.</span><span class="sxs-lookup"><span data-stu-id="25967-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="25967-151">Spojrzenie na strategii, możesz sprawdzić, czy możemy przekazać je funkcję, która ma token i gotowe jako parametry.</span><span class="sxs-lookup"><span data-stu-id="25967-151">Looking at the strategy, you see that we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="25967-152">Strategia zostanie zwrócona do nas po jego działa.</span><span class="sxs-lookup"><span data-stu-id="25967-152">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="25967-153">Następnie chcemy przechować dane użytkownika i Zapisz token, więc nie należy zażądać go ponownie.</span><span class="sxs-lookup"><span data-stu-id="25967-153">Then we want to store the user and stash the token so we don't need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="25967-154">Poprzedni kod obejmuje wszystkich użytkowników, która do uwierzytelniania serwera.</span><span class="sxs-lookup"><span data-stu-id="25967-154">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="25967-155">Jest to nazywane rejestracji automatycznej.</span><span class="sxs-lookup"><span data-stu-id="25967-155">This is known as auto-registration.</span></span> <span data-ttu-id="25967-156">Zaleca się, że nie zezwala każdy uwierzytelnienia na serwerze produkcyjnym bez uprzedniego je zarejestrować za pośrednictwem procesu, który podjęciu decyzji o.</span><span class="sxs-lookup"><span data-stu-id="25967-156">We    recommend that you don't let anyone authenticate to a production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="25967-157">Jest to zwykle wzorzec, które są widoczne w aplikacjach komercyjnych, dzięki której można zarejestrować w usłudze Facebook, ale następnie wyświetlony monit o podanie dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="25967-157">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to provide additional information.</span></span> <span data-ttu-id="25967-158">Jeśli to nie zostały przykładowej aplikacji, być może wyodrębniono adres e-mail użytkownika z obiektu tokena, który został zwrócony, a następnie monit użytkownika o podanie dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="25967-158">If this weren't a sample application, we could have extracted the user's email address from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="25967-159">Ponieważ jest to serwer testowy, możemy dodać je do bazy danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="25967-159">Because this is a test server, we add them to the in-memory database.</span></span>


4. <span data-ttu-id="25967-160">Następnie możemy dodać metody, które umożliwiają śledzenie zalogowanych użytkowników zgodnie z wymaganiami programu Passport.</span><span class="sxs-lookup"><span data-stu-id="25967-160">Next, let's add the methods that enable us to track the signed-in users as required by Passport.</span></span> <span data-ttu-id="25967-161">Te metody obejmują serializację i deserializację informacji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25967-161">These methods include serializing and deserializing the user's information.</span></span>

    ```JavaScript

            // Passport session setup. (Section 2)

            //   To support persistent sign-in sessions, Passport needs to be able to
            //   serialize users into the session and deserialize them out of the session. Typically,
            //   this is done simply by storing the user ID when serializing and finding
            //   the user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array to hold signed-in users
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

5.  <span data-ttu-id="25967-162">Następnie możemy dodać kod, aby załadować aparat Express.</span><span class="sxs-lookup"><span data-stu-id="25967-162">Next, let's add the code to load the Express engine.</span></span> <span data-ttu-id="25967-163">W tym miejscu użyjemy /views domyślne i zapewnia wzorzec /routes Express.</span><span class="sxs-lookup"><span data-stu-id="25967-163">Here we use the default /views and /routes pattern that Express provides.</span></span>

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
          // Initialize Passport!  Also use passport.session() middleware, to support
          // persistent login sessions (recommended).
          app.use(passport.initialize());
          app.use(passport.session());
          app.use(app.router);
          app.use(express.static(__dirname + '/../../public'));
        });

    ```

6. <span data-ttu-id="25967-164">Ponadto możemy dodać trasy, które przekazują rzeczywiste żądania rejestrowania do `passport-azure-ad` aparatu:</span><span class="sxs-lookup"><span data-stu-id="25967-164">Finally, let's add the routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware to authenticate the
        //   request. The first step in OpenID authentication involves redirecting
        //   the user to their OpenID provider. After authenticating, the OpenID
        //   provider redirects the user back to this application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in the Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="25967-165">Krok 4: Użyj Passport do wysyłania żądań zalogowania się i wylogowania do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="25967-165">Step 4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="25967-166">Aplikacji jest teraz prawidłowo skonfigurowana do komunikowania się z punktem końcowym przy użyciu protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="25967-166">Your app is now properly configured to communicate with the endpoint by using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="25967-167">`passport-azure-ad`ma podjąć obsługę wszystkich szczegółów obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i pozostawienie sesji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25967-167">`passport-azure-ad` has taken care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="25967-168">Wszystkie punkty, które pozostaje przyznawanie użytkownikom możliwość zalogować się i wylogowywania i zbieranie dodatkowych informacji na temat zalogowanych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="25967-168">All that remains is giving your users a way to sign in and sign out, and gathering additional information about the signed-in users.</span></span>

1. <span data-ttu-id="25967-169">Po pierwsze Dodajmy domyślną, logowania, konta i wylogowania metody naszych `app.js` pliku:</span><span class="sxs-lookup"><span data-stu-id="25967-169">First, let's add the default, sign-in, account, and sign-out methods to our `app.js` file:</span></span>

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
            log.info('Login was called in the Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  <span data-ttu-id="25967-170">Przejrzyj te szczegółowo umożliwia:</span><span class="sxs-lookup"><span data-stu-id="25967-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="25967-171">`/`Trasa przekierowuje do widoku index.ejs przekazanie użytkownika w żądaniu (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="25967-171">The `/`route redirects to the index.ejs view, passing the user in the request (if it exists).</span></span>
  * <span data-ttu-id="25967-172">`/account` Trasy najpierw *temu firma Microsoft są uwierzytelniani* (wdrożymy który w poniższym przykładzie) i następnie przekazuje użytkownika w żądaniu, dzięki czemu możemy uzyskać dodatkowe informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="25967-172">The `/account` route first *ensures we are authenticated* (we implement that in the following example), and then passes the user in the request so that we can get additional information about the user.</span></span>
  * <span data-ttu-id="25967-173">`/login` Trasy wywołuje naszych uwierzytelniania azuread openidconnect z `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="25967-173">The `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="25967-174">Jeśli które się nie powiedzie, przekierowuje użytkownika do /login.</span><span class="sxs-lookup"><span data-stu-id="25967-174">If that doesn't succeed, it redirects the user back to /login.</span></span>
  * <span data-ttu-id="25967-175">`/logout` Po prostu wywołania logout.ejs (i trasę), które powoduje wyczyszczenie plików cookie, a następnie wróci użytkownika index.ejs trasy.</span><span class="sxs-lookup"><span data-stu-id="25967-175">The `/logout` route simply calls the logout.ejs (and route), which clears cookies and then returns the user back to index.ejs.</span></span>

3. <span data-ttu-id="25967-176">Ostatnia część `app.js`, Dodajmy **EnsureAuthenticated** metodę, która jest używana w `/account`, jak pokazano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="25967-176">For the last part of `app.js`, let's add the **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

    ```JavaScript

        // Simple route middleware to ensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs to be protected. If
        //   the request is authenticated (typically via a persistent sign-in session),
        //   the request proceeds. Otherwise, the user is redirected to the
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. <span data-ttu-id="25967-177">Na koniec Utwórz sam serwer w `app.js`:</span><span class="sxs-lookup"><span data-stu-id="25967-177">Finally, let's create the server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-to-display-our-user-in-the-website-create-the-views-and-routes-in-express"></a><span data-ttu-id="25967-178">Krok 5: Aby wyświetlić naszych użytkowników w witrynie internetowej, tworzenie widoków i tras w Express</span><span class="sxs-lookup"><span data-stu-id="25967-178">Step 5: To display our user in the website, create the views and routes in Express</span></span>
<span data-ttu-id="25967-179">Teraz `app.js` została ukończona.</span><span class="sxs-lookup"><span data-stu-id="25967-179">Now `app.js` is complete.</span></span> <span data-ttu-id="25967-180">Należy dodać trasy i widoki, które zawierają informacje, możemy uzyskać dostęp do użytkownika, jak również obsługiwać `/logout` i `/login` tras, na których utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="25967-180">We simply need to add the routes and views that show the information we get to the user, as well as handle the `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="25967-181">Utwórz trasę `/routes/index.js` w obszarze katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="25967-181">Create the `/routes/index.js` route under the root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="25967-182">Utwórz trasę `/routes/user.js` w obszarze katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="25967-182">Create the `/routes/user.js` route under the root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="25967-183">Te przekazują żądania do naszych widoków, w tym użytkownika, jeśli jest obecny.</span><span class="sxs-lookup"><span data-stu-id="25967-183">These pass along the request to our views, including the user if present.</span></span>

3. <span data-ttu-id="25967-184">Utwórz widok `/views/index.ejs` w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="25967-184">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="25967-185">Jest to prosta strona, która wywołuje metody naszych zalogowania i wylogowania i umożliwia firmie Microsoft w celu pobrania informacji o koncie.</span><span class="sxs-lookup"><span data-stu-id="25967-185">This is a simple page that calls our login and logout methods and enables us to grab account information.</span></span> <span data-ttu-id="25967-186">Powiadomienie, że możemy użyć spójnika `if (!user)` jako użytkownik, są przekazywane w żądaniu jest dowód mamy zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25967-186">Notice that we can use the conditional `if (!user)` as the user being passed through in the request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="25967-187">Utwórz `/views/account.ejs` wyświetlać w katalogu głównym, co możemy wyświetlić dodatkowe informacje który `passport-azuread` umieścił w żądaniu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25967-187">Create the `/views/account.ejs` view under the root directory so that we can view additional information that `passport-azuread` has put in the user request.</span></span>

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

5. <span data-ttu-id="25967-188">Upewnijmy to wygląd dobrej przez dodanie układ.</span><span class="sxs-lookup"><span data-stu-id="25967-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="25967-189">Utwórz ' / views/layout.ejs' widoku w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="25967-189">Create the '/views/layout.ejs' view under the root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="25967-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25967-190">Next steps</span></span>
<span data-ttu-id="25967-191">Na koniec Skompiluj i uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="25967-191">Finally, build and run your app.</span></span> <span data-ttu-id="25967-192">Uruchom `node app.js`, a następnie przejdź do `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="25967-192">Run `node app.js`, and then go to `http://localhost:3000`.</span></span>

<span data-ttu-id="25967-193">Zaloguj się za pomocą osobistego konta Microsoft lub konta służbowego i zwróć uwagę, jak tożsamość użytkowników jest odzwierciedlone na liście /account.</span><span class="sxs-lookup"><span data-stu-id="25967-193">Sign in with either a personal Microsoft account or a work or school account, and notice how the user's identity is reflected in the /account list.</span></span> <span data-ttu-id="25967-194">Masz teraz zabezpieczone przy użyciu standardowych protokołach branżowych, uwierzytelniających użytkowników przy użyciu ich osobistych i pracy/służbowego konta aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="25967-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="25967-195">Gotowa próbka (bez wartości konfiguracji) [jest dostępna w pliku .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="25967-195">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="25967-196">Alternatywnie można ją sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="25967-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="25967-197">Możesz teraz przejść do bardziej zaawansowanych tematów.</span><span class="sxs-lookup"><span data-stu-id="25967-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="25967-198">Można spróbować:</span><span class="sxs-lookup"><span data-stu-id="25967-198">You might want to try:</span></span>

[<span data-ttu-id="25967-199">Zabezpieczanie interfejsu API za pomocą usługi Azure AD w sieci Web</span><span class="sxs-lookup"><span data-stu-id="25967-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
