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
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="91ce0-103">Aplikacja sieci web node.js logowania i wylogowywania z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="91ce0-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="91ce0-104">W tym miejscu możemy użyć usługi Passport:</span><span class="sxs-lookup"><span data-stu-id="91ce0-104">Here we use Passport to:</span></span>

* <span data-ttu-id="91ce0-105">Znak hello użytkownika w aplikacji toohello za pomocą usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91ce0-105">Sign hello user in toohello app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="91ce0-106">Wyświetl informacje o użytkowniku hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-106">Display information about hello user.</span></span>
* <span data-ttu-id="91ce0-107">Znak hello użytkownika poza aplikacją hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-107">Sign hello user out of hello app.</span></span>

<span data-ttu-id="91ce0-108">Usługa Passport to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="91ce0-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="91ce0-109">Elastyczne i moduły, usługa Passport można było porzucić dyskretnie w tooany ekspresowe lub restify aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="91ce0-109">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or restify web application.</span></span> <span data-ttu-id="91ce0-110">Kompleksowy zestaw strategii obsługuje uwierzytelniania przy użyciu nazwy użytkownika i hasła, Facebook i Twitter.</span><span class="sxs-lookup"><span data-stu-id="91ce0-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="91ce0-111">Opracowaliśmy strategię dla usługi Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="91ce0-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="91ce0-112">Firma Microsoft zainstalowaniu tego modułu, a następnie dodaj hello Microsoft Azure Active Directory `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="91ce0-112">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="91ce0-113">toodo tego hello wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="91ce0-113">toodo this, take hello following steps:</span></span>

1. <span data-ttu-id="91ce0-114">Rejestrowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91ce0-114">Register an app.</span></span>
2. <span data-ttu-id="91ce0-115">Konfigurowanie Twojej aplikacji hello toouse `passport-azure-ad` strategii.</span><span class="sxs-lookup"><span data-stu-id="91ce0-115">Set up your app toouse hello `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="91ce0-116">Użyj paszportu tooissue logowania i wylogowywania żądań tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="91ce0-116">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="91ce0-117">Dane o użytkowniku hello wydruku.</span><span class="sxs-lookup"><span data-stu-id="91ce0-117">Print data about hello user.</span></span>

<span data-ttu-id="91ce0-118">Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="91ce0-118">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="91ce0-119">toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako plik .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) lub klonowania hello szkielet:</span><span class="sxs-lookup"><span data-stu-id="91ce0-119">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="91ce0-120">Aplikacja Hello ukończone znajduje się na końcu hello również w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="91ce0-120">hello completed application is provided at hello end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="91ce0-121">Krok 1: Rejestrowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="91ce0-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="91ce0-122">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91ce0-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="91ce0-123">W menu hello u góry strony hello hello wybierz konta.</span><span class="sxs-lookup"><span data-stu-id="91ce0-123">In hello menu at hello top of hello page, select your account.</span></span> <span data-ttu-id="91ce0-124">W obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, w którym ma tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91ce0-124">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="91ce0-125">Wybierz **więcej usług** w hello menu na powitania po lewej stronie ekranu hello, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="91ce0-125">Select **More Services** in hello menu on hello left side of hello screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="91ce0-126">Wybierz **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="91ce0-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="91ce0-127">Wykonaj hello monity toocreate **aplikacji sieci Web** i/lub **WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="91ce0-127">Follow hello prompts toocreate a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="91ce0-128">Witaj **nazwa** aplikacji hello opisuje toousers Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91ce0-128">hello **name** of hello application describes your application toousers.</span></span>

  * <span data-ttu-id="91ce0-129">Witaj **adres URL logowania** jest hello podstawowy adres URL aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91ce0-129">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="91ce0-130">Hello szkielet przez domyślną jest "http://localhost: 3000/auth/openid/powrotu".</span><span class="sxs-lookup"><span data-stu-id="91ce0-130">hello skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="91ce0-131">Po zarejestrowaniu, usługi Azure AD przypisuje aplikacji identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="91ce0-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="91ce0-132">Potrzebujesz tej wartości w hello następujące sekcje, dlatego skopiuj go ze strony aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-132">You need this value in hello following sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="91ce0-133">Z hello **ustawienia** -> **właściwości** strony dla aplikacji, aktualizacji hello identyfikator URI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91ce0-133">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="91ce0-134">Witaj **identyfikator URI aplikacji** to unikatowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91ce0-134">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="91ce0-135">Konwencja Hello jest toouse hello format `https://<tenant-domain>/<app-name>`, na przykład: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="91ce0-135">hello convention is toouse hello format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-tooyour-directory"></a><span data-ttu-id="91ce0-136">Krok 2: Dodaj katalog tooyour wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="91ce0-136">Step 2: Add prerequisites tooyour directory</span></span>
1. <span data-ttu-id="91ce0-137">Z wiersza polecenia hello, Zmień folder główny tooyour katalogów, jeśli nie masz już istnieje, a następnie hello uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="91ce0-137">From hello command line, change directories tooyour root folder if you're not already there, and then run hello following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="91ce0-138">Ponadto należy `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="91ce0-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="91ce0-139">Spowoduje to zainstalowanie bibliotek hello który `passport-azure-ad` zależy.</span><span class="sxs-lookup"><span data-stu-id="91ce0-139">This installs hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="91ce0-140">Krok 3: Konfigurowanie strategii passport-node-js hello toouse aplikacji</span><span class="sxs-lookup"><span data-stu-id="91ce0-140">Step 3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="91ce0-141">W tym miejscu możemy skonfigurować Express toouse hello protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="91ce0-141">Here, we configure Express toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="91ce0-142">Usługa Passport jest używana toodo różne elementy, włącznie z żądaniami logowania i wylogowywania problem, zarządzanie sesji użytkownika hello i uzyskiwania informacji o hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="91ce0-142">Passport is used toodo various things, including issue sign-in and sign-out requests, manage hello user's session, and get information about hello user.</span></span>

1. <span data-ttu-id="91ce0-143">toobegin, otwórz hello `config.js` o hello katalog główny projektu hello plików, a następnie wprowadź wartości konfiguracji aplikacji w hello `exports.creds` sekcji.</span><span class="sxs-lookup"><span data-stu-id="91ce0-143">toobegin, open hello `config.js` file at hello root of hello project, and then enter your app's configuration values in hello `exports.creds` section.</span></span>

  * <span data-ttu-id="91ce0-144">Witaj `clientID` jest hello **identyfikator aplikacji** jest przypisany tooyour aplikacji w portalu rejestracji hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-144">hello `clientID` is hello **Application Id** that's assigned tooyour app in hello registration portal.</span></span>

  * <span data-ttu-id="91ce0-145">Witaj `returnURL` jest hello **identyfikator Uri przekierowania** wprowadzony w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-145">hello `returnURL` is hello **Redirect Uri** that you entered in hello portal.</span></span>

  * <span data-ttu-id="91ce0-146">Witaj `clientSecret` jest klucz tajny hello wygenerowane w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-146">hello `clientSecret` is hello secret that you generated in hello portal.</span></span>

2. <span data-ttu-id="91ce0-147">Następnie otwórz folder hello `app.js` pliku w katalogu głównym hello hello projektu.</span><span class="sxs-lookup"><span data-stu-id="91ce0-147">Next, open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="91ce0-148">Następnie dodaj następujące wywołanie tooinvoke hello hello `OIDCStrategy` strategii dołączoną `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="91ce0-148">Then add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="91ce0-149">Po wykonaniu tej Użyj strategii hello możemy właśnie w odwołaniu toohandle naszych żądań logowania.</span><span class="sxs-lookup"><span data-stu-id="91ce0-149">After that, use hello strategy we just referenced toohandle our sign-in requests.</span></span>

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
<span data-ttu-id="91ce0-150">Usługa Passport używa podobnego wzorca do wszystkich swoich strategii (Twitter, Facebook itd.) zgodne ze wszyscy twórcy kodu strategii.</span><span class="sxs-lookup"><span data-stu-id="91ce0-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="91ce0-151">Patrzeć strategii hello, możesz sprawdzić, czy jest przekazywana on funkcję, która ma token i gotowe jako parametry hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-151">Looking at hello strategy, you see that we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="91ce0-152">Witaj strategia ponownie toous po jego działa.</span><span class="sxs-lookup"><span data-stu-id="91ce0-152">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="91ce0-153">Następnie chcemy toostore hello użytkownika i token hello tymczasowym potrzebujemy nie tooask go ponownie.</span><span class="sxs-lookup"><span data-stu-id="91ce0-153">Then we want toostore hello user and stash hello token so we don't need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="91ce0-154">Witaj poprzedni kod obejmuje wszystkich użytkowników, wykonywanej tooauthenticate tooour serwera.</span><span class="sxs-lookup"><span data-stu-id="91ce0-154">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="91ce0-155">Jest to nazywane rejestracji automatycznej.</span><span class="sxs-lookup"><span data-stu-id="91ce0-155">This is known as auto-registration.</span></span> <span data-ttu-id="91ce0-156">Zaleca się, że nie zezwala każdy uwierzytelniania serwera produkcyjnego tooa bez uprzedniego je zarejestrować za pośrednictwem procesu, który podjęciu decyzji o.</span><span class="sxs-lookup"><span data-stu-id="91ce0-156">We    recommend that you don't let anyone authenticate tooa production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="91ce0-157">Jest to zwykle wzorzec hello, które widać w aplikacjach komercyjnych, które pozwalają tooregister z usługą Facebook, ale następnie poprosić tooprovide dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="91ce0-157">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you tooprovide additional information.</span></span> <span data-ttu-id="91ce0-158">Jeśli to nie zostały przykładowej aplikacji, być może wyodrębniono adres e-mail użytkownika hello z hello obiektu tokena, który został zwrócony, a następnie zadawane toofill użytkownika hello dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="91ce0-158">If this weren't a sample application, we could have extracted hello user's email address from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="91ce0-159">Ponieważ jest to serwer testowy, możemy dodać je toohello bazy danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="91ce0-159">Because this is a test server, we add them toohello in-memory database.</span></span>


4. <span data-ttu-id="91ce0-160">Następnie możemy dodać metody hello, pozwalających nam tootrack hello zalogowanych użytkowników, co jest wymagane przez usługi Passport.</span><span class="sxs-lookup"><span data-stu-id="91ce0-160">Next, let's add hello methods that enable us tootrack hello signed-in users as required by Passport.</span></span> <span data-ttu-id="91ce0-161">Te metody obejmują serializację i deserializację informacji o użytkowniku hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-161">These methods include serializing and deserializing hello user's information.</span></span>

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

5.  <span data-ttu-id="91ce0-162">Następnie możemy dodać aparat Express hello hello kodu tooload.</span><span class="sxs-lookup"><span data-stu-id="91ce0-162">Next, let's add hello code tooload hello Express engine.</span></span> <span data-ttu-id="91ce0-163">Tutaj używamy hello domyślne /views i zapewnia wzorzec /routes Express.</span><span class="sxs-lookup"><span data-stu-id="91ce0-163">Here we use hello default /views and /routes pattern that Express provides.</span></span>

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

6. <span data-ttu-id="91ce0-164">Ponadto możemy dodać hello kieruje tego Dostarcz hello rzeczywiste żądania rejestrowania toohello `passport-azure-ad` aparatu:</span><span class="sxs-lookup"><span data-stu-id="91ce0-164">Finally, let's add hello routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>


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


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="91ce0-165">Krok 4: Użycie usługi Passport tooissue logowania i wylogowywania żądań tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="91ce0-165">Step 4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="91ce0-166">Aplikacja jest teraz prawidłowo skonfigurowana toocommunicate z punktem końcowym hello przy użyciu protokołu uwierzytelniania OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-166">Your app is now properly configured toocommunicate with hello endpoint by using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="91ce0-167">`passport-azure-ad`ma podjąć obsługę wszystkich szczegółów hello obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i utrzymywanie sesji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="91ce0-167">`passport-azure-ad` has taken care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="91ce0-168">Wszystkie opcje, które pozostaje przyznawanie użytkownikom toosign sposób w i wylogowaniu i zbieranie dodatkowych informacji na temat hello zalogowanych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="91ce0-168">All that remains is giving your users a way toosign in and sign out, and gathering additional information about hello signed-in users.</span></span>

1. <span data-ttu-id="91ce0-169">Po pierwsze możemy dodać hello domyślną, logowania konta i wylogowania tooour `app.js` pliku:</span><span class="sxs-lookup"><span data-stu-id="91ce0-169">First, let's add hello default, sign-in, account, and sign-out methods tooour `app.js` file:</span></span>

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

2.  <span data-ttu-id="91ce0-170">Przejrzyj te szczegółowo umożliwia:</span><span class="sxs-lookup"><span data-stu-id="91ce0-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="91ce0-171">Witaj `/`trasa przekierowuje widoku index.ejs toohello przekazywanie hello użytkownika w żądaniu hello (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="91ce0-171">hello `/`route redirects toohello index.ejs view, passing hello user in hello request (if it exists).</span></span>
  * <span data-ttu-id="91ce0-172">Witaj `/account` trasy najpierw *temu firma Microsoft są uwierzytelniani* (wdrożymy który w hello poniższy przykład), a następnie przekazuje hello użytkownika w żądaniu hello tak, aby firma Microsoft może uzyskać dodatkowe informacje o hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="91ce0-172">hello `/account` route first *ensures we are authenticated* (we implement that in hello following example), and then passes hello user in hello request so that we can get additional information about hello user.</span></span>
  * <span data-ttu-id="91ce0-173">Witaj `/login` trasy wywołuje naszych uwierzytelniania azuread openidconnect z `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="91ce0-173">hello `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="91ce0-174">Jeśli które się nie powiedzie, przekierowuje hello wstecz zbyt/dane logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="91ce0-174">If that doesn't succeed, it redirects hello user back too/login.</span></span>
  * <span data-ttu-id="91ce0-175">Witaj `/logout` trasy po prostu wywołuje hello logout.ejs (i trasę), które czyści plików cookie, a następnie zwraca hello tooindex.ejs wstecz użytkownika.</span><span class="sxs-lookup"><span data-stu-id="91ce0-175">hello `/logout` route simply calls hello logout.ejs (and route), which clears cookies and then returns hello user back tooindex.ejs.</span></span>

3. <span data-ttu-id="91ce0-176">Witaj ostatniej części `app.js`, Dodajmy hello **EnsureAuthenticated** metodę, która jest używana w `/account`, jak pokazano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="91ce0-176">For hello last part of `app.js`, let's add hello **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

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

4. <span data-ttu-id="91ce0-177">Na koniec Utwórz sam serwer hello w `app.js`:</span><span class="sxs-lookup"><span data-stu-id="91ce0-177">Finally, let's create hello server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a><span data-ttu-id="91ce0-178">Krok 5: toodisplay naszych użytkowników w witrynie internetowej hello, tworzenie hello widoków i tras w Express</span><span class="sxs-lookup"><span data-stu-id="91ce0-178">Step 5: toodisplay our user in hello website, create hello views and routes in Express</span></span>
<span data-ttu-id="91ce0-179">Teraz `app.js` została ukończona.</span><span class="sxs-lookup"><span data-stu-id="91ce0-179">Now `app.js` is complete.</span></span> <span data-ttu-id="91ce0-180">Firma Microsoft po prostu muszą tooadd hello tras i wyświetla te informacje hello Pokaż możemy pobrać toohello użytkownika, jak również obsługiwać hello `/logout` i `/login` tras, na których utworzyliśmy.</span><span class="sxs-lookup"><span data-stu-id="91ce0-180">We simply need tooadd hello routes and views that show hello information we get toohello user, as well as handle hello `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="91ce0-181">Utwórz hello `/routes/index.js` trasy w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-181">Create hello `/routes/index.js` route under hello root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="91ce0-182">Utwórz hello `/routes/user.js` trasy w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-182">Create hello `/routes/user.js` route under hello root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="91ce0-183">Te przekazują hello żądania tooour widoków, w tym hello użytkownika, jeśli jest obecny.</span><span class="sxs-lookup"><span data-stu-id="91ce0-183">These pass along hello request tooour views, including hello user if present.</span></span>

3. <span data-ttu-id="91ce0-184">Utwórz hello `/views/index.ejs` widoku w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-184">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="91ce0-185">Jest to prosta strona, która wywołuje metody naszych zalogowania i wylogowania i pozwala nam informacje o koncie toograb.</span><span class="sxs-lookup"><span data-stu-id="91ce0-185">This is a simple page that calls our login and logout methods and enables us toograb account information.</span></span> <span data-ttu-id="91ce0-186">Należy zauważyć, że możemy użyć hello warunkowego `if (!user)` hello użytkownika są przekazywane w żądaniu hello jest dowód mamy zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="91ce0-186">Notice that we can use hello conditional `if (!user)` as hello user being passed through in hello request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="91ce0-187">Utwórz hello `/views/account.ejs` wyświetlać w katalogu głównym hello, co możemy wyświetlić dodatkowe informacje który `passport-azuread` umieścił w żądaniu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="91ce0-187">Create hello `/views/account.ejs` view under hello root directory so that we can view additional information that `passport-azuread` has put in hello user request.</span></span>

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

5. <span data-ttu-id="91ce0-188">Upewnijmy to wygląd dobrej przez dodanie układ.</span><span class="sxs-lookup"><span data-stu-id="91ce0-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="91ce0-189">Utwórz hello "/ views/layout.ejs widok w obszarze hello katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="91ce0-189">Create hello '/views/layout.ejs' view under hello root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="91ce0-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91ce0-190">Next steps</span></span>
<span data-ttu-id="91ce0-191">Na koniec Skompiluj i uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="91ce0-191">Finally, build and run your app.</span></span> <span data-ttu-id="91ce0-192">Uruchom `node app.js`, a następnie przejdź zbyt`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="91ce0-192">Run `node app.js`, and then go too`http://localhost:3000`.</span></span>

<span data-ttu-id="91ce0-193">Zaloguj się za pomocą osobistego konta Microsoft lub konta służbowego i zwróć uwagę, jak tożsamość użytkownika hello jest widoczny w hello /account listy.</span><span class="sxs-lookup"><span data-stu-id="91ce0-193">Sign in with either a personal Microsoft account or a work or school account, and notice how hello user's identity is reflected in hello /account list.</span></span> <span data-ttu-id="91ce0-194">Masz teraz zabezpieczone przy użyciu standardowych protokołach branżowych, uwierzytelniających użytkowników przy użyciu ich osobistych i pracy/służbowego konta aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="91ce0-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="91ce0-195">Odwołania, hello ukończone próbka (bez wartości konfiguracji) [jest dostępna jako plik .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="91ce0-195">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="91ce0-196">Alternatywnie można ją sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="91ce0-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="91ce0-197">Możesz teraz przejść do bardziej zaawansowanych tematów.</span><span class="sxs-lookup"><span data-stu-id="91ce0-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="91ce0-198">Może być tootry:</span><span class="sxs-lookup"><span data-stu-id="91ce0-198">You might want tootry:</span></span>

[<span data-ttu-id="91ce0-199">Zabezpieczanie interfejsu API za pomocą usługi Azure AD w sieci Web</span><span class="sxs-lookup"><span data-stu-id="91ce0-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
