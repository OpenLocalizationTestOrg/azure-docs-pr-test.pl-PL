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
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="f7b4f-103">Usługa Azure AD B2C: Dodawanie aplikacji sieci web Node.js tooa logowania</span><span class="sxs-lookup"><span data-stu-id="f7b4f-103">Azure AD B2C: Add sign-in tooa Node.js web app</span></span>

<span data-ttu-id="f7b4f-104">**Passport** to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="f7b4f-105">Jest to niezwykle elastyczne i modułowe oprogramowanie, które można dyskretnie zainstalować w dowolnej aplikacji sieci Web opartej na module Express lub Restify.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="f7b4f-106">Kompleksowy zestaw strategii obsługuje uwierzytelnianie przy użyciu m.in. nazwy użytkownika i hasła lub kont w serwisach Facebook i Twitter.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="f7b4f-107">Opracowaliśmy strategię dla usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f7b4f-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f7b4f-108">Zostanie zainstalowaniu tego modułu, a następnie dodaj hello Azure AD `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-108">You will install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="f7b4f-109">toodo, musisz:</span><span class="sxs-lookup"><span data-stu-id="f7b4f-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="f7b4f-110">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="f7b4f-111">Konfigurowanie Twojej aplikacji hello toouse `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-111">Set up your app toouse hello `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="f7b4f-112">Użyj paszportu tooissue logowania i wylogowywania żądań tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-112">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="f7b4f-113">Wydrukować dane użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-113">Print user data.</span></span>

<span data-ttu-id="f7b4f-114">Witaj kodu w tym samouczku [jest przechowywany w serwisie GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="f7b4f-114">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="f7b4f-115">toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako plik .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="f7b4f-115">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="f7b4f-116">Można również sklonować szkielet hello:</span><span class="sxs-lookup"><span data-stu-id="f7b4f-116">You can also clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="f7b4f-117">Aplikacja Hello ukończone znajduje się na końcu hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-117">hello completed application is provided at hello end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="f7b4f-118">Tworzenie katalogu usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="f7b4f-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="f7b4f-119">Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="f7b4f-120">Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="f7b4f-121">Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="f7b4f-122">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f7b4f-122">Create an application</span></span>

<span data-ttu-id="f7b4f-123">Następnie należy toocreate aplikację w katalogu usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-123">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="f7b4f-124">Dzięki temu informacji usługi Azure AD, że wymaga ona toocommunicate bezpiecznie z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-124">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="f7b4f-125">Witaj zarówno aplikacja klienta i interfejs API sieci web będą reprezentowane przez jeden **identyfikator aplikacji**, ponieważ stanowią jedną aplikację logiczną.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-125">Both hello client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="f7b4f-126">toocreate usługi aplikacji, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f7b4f-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="f7b4f-127">Należy pamiętać o wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="f7b4f-127">Be sure to:</span></span>

- <span data-ttu-id="f7b4f-128">Obejmują **aplikacji sieci web**/**interfejs API sieci web** w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-128">Include a **web app**/**web API** in hello application.</span></span>
- <span data-ttu-id="f7b4f-129">Wprowadź `http://localhost:3000/auth/openid/return` w polu **Adres URL odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="f7b4f-130">Jest hello domyślny adres URL dla tego przykładu kodu.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-130">It is hello default URL for this code sample.</span></span>
- <span data-ttu-id="f7b4f-131">Utwórz **klucz tajny aplikacji** i skopiuj go.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="f7b4f-132">Będzie potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-132">You will need it later.</span></span> <span data-ttu-id="f7b4f-133">Należy pamiętać, że ta wartość musi toobe [XML w znaki ucieczki](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) przed jego użyciem.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="f7b4f-134">Kopiuj hello **identyfikator aplikacji** czyli przypisanej tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="f7b4f-135">On również będzie później potrzebny.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="f7b4f-136">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="f7b4f-136">Create your policies</span></span>

<span data-ttu-id="f7b4f-137">W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f7b4f-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f7b4f-138">Ta aplikacja obejmuje trzy środowiska tożsamości: rejestracji, logowania i logowania przy użyciu konta w serwisie Facebook.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="f7b4f-139">Należy toocreate tych zasad każdego typu zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="f7b4f-139">You need toocreate this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="f7b4f-140">Podczas tworzenia trzech zbiorów zasad należy koniecznie:</span><span class="sxs-lookup"><span data-stu-id="f7b4f-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="f7b4f-141">Wybierz hello **Nazwa wyświetlana** i inne atrybuty rejestracji w ramach zasad rejestracji.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="f7b4f-142">Wybierz hello **Nazwa wyświetlana** i **obiektu o identyfikatorze** oświadczenia aplikacji we wszystkich zasadach.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="f7b4f-143">Można również wybrać inne oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="f7b4f-144">Kopiuj hello **nazwa** poszczególnych zasad po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-144">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="f7b4f-145">Powinien on mieć prefiks hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="f7b4f-146">Te nazwy zasad będą potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="f7b4f-147">Po utworzeniu trzech zbiorów zasad, wszystko jest gotowe toobuild aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-147">After you create your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="f7b4f-148">Należy pamiętać, że w tym artykule nie opisano, jak zasady hello toouse właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-148">Note that this article does not cover how toouse hello policies you just created.</span></span> <span data-ttu-id="f7b4f-149">toolearn o sposób działania zasad w usłudze Azure AD B2C, rozpoczynać hello [.NET sieci web aplikacji Wprowadzenie — samouczek](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f7b4f-149">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-tooyour-directory"></a><span data-ttu-id="f7b4f-150">Dodaj katalog tooyour wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f7b4f-150">Add prerequisites tooyour directory</span></span>

<span data-ttu-id="f7b4f-151">Z wiersza polecenia hello Zmień folder główny tooyour katalogów, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-151">From hello command line, change directories tooyour root folder, if you're not already there.</span></span> <span data-ttu-id="f7b4f-152">Uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="f7b4f-152">Run hello following commands:</span></span>

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

<span data-ttu-id="f7b4f-153">Ponadto użyliśmy `passport-azure-ad` naszym podglądzie w hello szkielet hello Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-153">In addition, we used `passport-azure-ad` for our preview in hello skeleton of hello Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="f7b4f-154">Spowoduje to zainstalowanie bibliotek hello który `passport-azure-ad` zależy.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-154">This will install hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a><span data-ttu-id="f7b4f-155">Konfigurowanie Twojej aplikacji hello toouse strategii Passport-Node.js</span><span class="sxs-lookup"><span data-stu-id="f7b4f-155">Set up your app toouse hello Passport-Node.js strategy</span></span>
<span data-ttu-id="f7b4f-156">Skonfiguruj hello Express oprogramowanie pośredniczące toouse hello protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-156">Configure hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="f7b4f-157">Usługi Passport jest używane tooissue żądań logowania się i wylogowania, zarządzania sesjami użytkownika i uzyskiwania informacji o użytkownikach, między innymi.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-157">Passport will be used tooissue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="f7b4f-158">Otwórz hello `config.js` plików w katalogu głównym hello hello projektu, a następnie wprowadź wartości konfiguracji aplikacji w hello `exports.creds` sekcji.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-158">Open hello `config.js` file in hello root of hello project and enter your app's configuration values in hello `exports.creds` section.</span></span>
- <span data-ttu-id="f7b4f-159">`clientID`: hello **identyfikator aplikacji** przypisane tooyour aplikacji w portalu rejestracji hello.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-159">`clientID`: hello **Application ID** assigned tooyour app in hello registration portal.</span></span>
- <span data-ttu-id="f7b4f-160">`returnURL`: hello **identyfikator URI przekierowania** wprowadzony w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-160">`returnURL`: hello **Redirect URI** you entered in hello portal.</span></span>
- <span data-ttu-id="f7b4f-161">`tenantName`: Nazwa dzierżawy aplikacji, na przykład hello **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-161">`tenantName`: hello tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="f7b4f-162">Otwórz hello `app.js` pliku w katalogu głównym hello hello projektu.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-162">Open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="f7b4f-163">Dodaj następujące wywołanie tooinvoke hello hello `OIDCStrategy` strategii dołączoną `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-163">Add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="f7b4f-164">Użyj strategii hello właśnie w odwołaniu toohandle żądań logowania.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-164">Use hello strategy you just referenced toohandle sign-in requests.</span></span>

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
<span data-ttu-id="f7b4f-165">Program Passport używa podobnego wzorca do wszystkich swoich strategii (w tym serwisów Facebook i Twitter).</span><span class="sxs-lookup"><span data-stu-id="f7b4f-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="f7b4f-166">Wszystkich autorów toothis wzorca.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-166">All strategy writers adhere toothis pattern.</span></span> <span data-ttu-id="f7b4f-167">Po wyświetleniu strategii hello widać, że przekazujesz ją `function()` mający token i `done` jako parametry hello.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-167">When you look at hello strategy, you can see that you pass it a `function()` that has a token and a `done` as hello parameters.</span></span> <span data-ttu-id="f7b4f-168">Strategia Hello wróci tooyou po wykonaniu całego zadania.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-168">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="f7b4f-169">Przechowywanie hello użytkownika i zwijanie hello token, dzięki czemu nie trzeba tooask go ponownie.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-169">Store hello user and stash hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="f7b4f-170">Witaj poprzedni kod obejmuje wszystkich użytkowników, których uwierzytelnia serwer hello.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-170">hello preceding code takes all users whom hello server authenticates.</span></span> <span data-ttu-id="f7b4f-171">Jest to autorejestracja.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-171">This is autoregistration.</span></span> <span data-ttu-id="f7b4f-172">Podczas korzystania z serwerów produkcyjnych, nie mają toolet wśród użytkowników, chyba że ma przeszli procesu rejestracji, które zostały skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-172">When you use production servers, you don’t want toolet in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="f7b4f-173">Sposób ten jest często stosowany w aplikacjach dla użytkowników indywidualnych.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="f7b4f-174">Te pozwalają tooregister za pomocą usługi Facebook, ale następnie prosi toofill dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-174">These allow you tooregister by using Facebook, but then they ask you toofill out additional information.</span></span> <span data-ttu-id="f7b4f-175">Jeśli aplikacja nie była próbkę, firma Microsoft może wyodrębnić adres e-mail z hello obiektu tokena, który jest zwracany, a następnie poprosić toofill użytkownika hello dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-175">If our application wasn’t a sample, we could extract an email address from hello token object that is returned, and then ask hello user toofill out additional information.</span></span> <span data-ttu-id="f7b4f-176">Ponieważ jest to serwer testowy, zostają po prostu dodani użytkownicy toohello w pamięci z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-176">Because this is a test server, we simply add users toohello in-memory database.</span></span>

<span data-ttu-id="f7b4f-177">Dodaj metody hello, które umożliwiają śledzenie tookeep użytkowników, którzy zalogowali się, co jest wymagane przez usługę Passport.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-177">Add hello methods that allow you tookeep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="f7b4f-178">Obejmuje to serializację i deserializację informacji o użytkowniku:</span><span class="sxs-lookup"><span data-stu-id="f7b4f-178">This includes serializing and deserializing user information:</span></span>

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

<span data-ttu-id="f7b4f-179">Dodaj aparat Express hello hello kodu tooload.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-179">Add hello code tooload hello Express engine.</span></span> <span data-ttu-id="f7b4f-180">W następujących hello widać, że używana domyślna hello `/views` i `/routes` wzorca, który udostępnia Express.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-180">In hello following, you can see that we use hello default `/views` and `/routes` pattern that Express provides.</span></span>

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

<span data-ttu-id="f7b4f-181">Dodaj hello `POST` tras, które przekazują hello toohello rzeczywiste żądania rejestrowania `passport-azure-ad` aparatu:</span><span class="sxs-lookup"><span data-stu-id="f7b4f-181">Add hello `POST` routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

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

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="f7b4f-182">Użyj paszportu tooissue logowania i wylogowywania żądań tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="f7b4f-182">Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>

<span data-ttu-id="f7b4f-183">Aplikacja jest teraz prawidłowo skonfigurowany toocommunicate z punktem końcowym v2.0 hello przy użyciu protokołu uwierzytelniania OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-183">Your app is now properly configured toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="f7b4f-184">`passport-azure-ad`została podjęta obsługę szczegóły hello obsługuje tworzenie komunikatów uwierzytelniania, sprawdzanie poprawności tokenów z usługi Azure AD i podtrzymywanie sesji użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-184">`passport-azure-ad` has taken care of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="f7b4f-185">Wszystkie opcje, które pozostaje jest toogive użytkownikom toosign sposób w i znak poza i toogather dodatkowe informacje o użytkownikach, którzy zalogowali się.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-185">All that remains is toogive your users a way toosign in and sign out, and toogather additional information on users who have signed in.</span></span>

<span data-ttu-id="f7b4f-186">Najpierw dodaj hello domyślną, logowania konta i wylogowania tooyour `app.js` pliku:</span><span class="sxs-lookup"><span data-stu-id="f7b4f-186">First, add hello default, sign-in, account, and sign-out methods tooyour `app.js` file:</span></span>

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

<span data-ttu-id="f7b4f-187">tooreview tym metodom dokładniej:</span><span class="sxs-lookup"><span data-stu-id="f7b4f-187">tooreview these methods in detail:</span></span>
- <span data-ttu-id="f7b4f-188">Witaj `/` trasa przekierowuje toohello `index.ejs` przez przekazanie użytkownika hello w żądaniu hello (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="f7b4f-188">hello `/` route redirects toohello `index.ejs` view by passing hello user in hello request (if it exists).</span></span>
- <span data-ttu-id="f7b4f-189">Witaj `/account` trasy najpierw sprawdza, czy użytkownik został uwierzytelniony (to jest poniżej hello implementacji).</span><span class="sxs-lookup"><span data-stu-id="f7b4f-189">hello `/account` route first verifies that you are authenticated (hello implementation for this is below).</span></span> <span data-ttu-id="f7b4f-190">Następnie przekazuje użytkownika hello w żądaniu hello tak, aby uzyskać dodatkowe informacje na temat hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-190">It then passes hello user in hello request so that you can get additional information about hello user.</span></span>
- <span data-ttu-id="f7b4f-191">Witaj `/login` hello wywołania trasy `azuread-openidconnect` uwierzytelniania z `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-191">hello `/login` route calls hello `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="f7b4f-192">Jeśli to się nie powiedzie, trasy hello przekierowuje użytkownika hello wstecz zbyt`/login`.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-192">If it doesn't succeed, hello route redirects hello user back too`/login`.</span></span>
- <span data-ttu-id="f7b4f-193">Trasa `/logout` po prostu wywołuje widok `logout.ejs` (i jego trasę).</span><span class="sxs-lookup"><span data-stu-id="f7b4f-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="f7b4f-194">Powoduje wyczyszczenie plików cookie, a następnie zwraca hello użytkownika z powrotem zbyt`index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-194">This clears cookies and then returns hello user back too`index.ejs`.</span></span>


<span data-ttu-id="f7b4f-195">Witaj ostatniej części `app.js`, Dodaj hello `EnsureAuthenticated` metodę, która jest używana w hello `/account` trasy.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-195">For hello last part of `app.js`, add hello `EnsureAuthenticated` method that is used in hello `/account` route.</span></span>

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

<span data-ttu-id="f7b4f-196">Na koniec Utwórz sam serwer hello w `app.js`.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-196">Finally, create hello server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a><span data-ttu-id="f7b4f-197">Utwórz widoki hello i kieruje w Express toocall zasad</span><span class="sxs-lookup"><span data-stu-id="f7b4f-197">Create hello views and routes in Express toocall your policies</span></span>

<span data-ttu-id="f7b4f-198">Element `app.js` jest teraz gotowy.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="f7b4f-199">Wystarczy tooadd hello trasy i widoki, które pozwalają hello toocall zasad logowania i rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-199">You just need tooadd hello routes and views that allow you toocall hello sign-in and sign-up policies.</span></span> <span data-ttu-id="f7b4f-200">Obsługują one również hello `/logout` i `/login` utworzone trasy.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-200">These also handle hello `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="f7b4f-201">Utwórz hello `/routes/index.js` trasy w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-201">Create hello `/routes/index.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="f7b4f-202">Utwórz hello `/routes/user.js` trasy w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-202">Create hello `/routes/user.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="f7b4f-203">Te proste trasy przekazują żądania tooyour widoków.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-203">These simple routes pass along requests tooyour views.</span></span> <span data-ttu-id="f7b4f-204">Obejmują one hello użytkownika, jeśli występuje.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-204">They include hello user, if one is present.</span></span>

<span data-ttu-id="f7b4f-205">Utwórz hello `/views/index.ejs` widoku w katalogu głównym hello.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-205">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="f7b4f-206">Jest to prosta strona, która wywołuje zasady dotyczące logowania się i wylogowywania. Umożliwia także go toograb informacje o koncie.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-206">This is a simple page that calls policies for sign-in and sign-out. You can also use it toograb account information.</span></span> <span data-ttu-id="f7b4f-207">Uwaga służy hello warunkowego `if (!user)` jako hello użytkownika są przekazywane w żądania hello tooprovide dowody, ten użytkownik hello jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-207">Note that you can use hello conditional `if (!user)` as hello user is passed through in hello request tooprovide evidence that hello user is signed in.</span></span>

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

<span data-ttu-id="f7b4f-208">Utwórz hello `/views/account.ejs` Wyświetl w katalogu głównym hello, dzięki czemu można wyświetlić dodatkowe informacje który `passport-azure-ad` put w żądaniu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-208">Create hello `/views/account.ejs` view under hello root directory so that you can view additional information that `passport-azure-ad` put in hello user request.</span></span>

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

<span data-ttu-id="f7b4f-209">Teraz możesz skompilować i uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-209">You can now build and run your app.</span></span>

<span data-ttu-id="f7b4f-210">Uruchom `node app.js` i przejdź zbyt`http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="f7b4f-210">Run `node app.js` and navigate too`http://localhost:3000`</span></span>


<span data-ttu-id="f7b4f-211">Zarejestruj się lub zaloguj się w aplikacji toohello za pomocą poczty e-mail lub usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-211">Sign up or sign in toohello app by using email or Facebook.</span></span> <span data-ttu-id="f7b4f-212">Wyloguj się i zaloguj ponownie jako inny użytkownik.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-212">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="f7b4f-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7b4f-213">Next steps</span></span>

<span data-ttu-id="f7b4f-214">Odwołania, hello ukończone próbka (bez wartości konfiguracji) [jest dostępna jako plik .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f7b4f-214">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="f7b4f-215">Można ją także sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="f7b4f-215">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="f7b4f-216">Możesz teraz przejść toomore Tematy zaawansowane.</span><span class="sxs-lookup"><span data-stu-id="f7b4f-216">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="f7b4f-217">Zobacz te tematy:</span><span class="sxs-lookup"><span data-stu-id="f7b4f-217">You might try:</span></span>

[<span data-ttu-id="f7b4f-218">Zabezpieczanie interfejsu API sieci web przy użyciu modelu hello B2C w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="f7b4f-218">Secure a web API by using hello B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
