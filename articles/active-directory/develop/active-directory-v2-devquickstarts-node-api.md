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
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="b36fa-103">Zabezpieczanie interfejsu API sieci web przy użyciu środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="b36fa-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="b36fa-104">Nie wszystkie usługi Azure Active Directory scenariusze i funkcje działają z punktem końcowym v2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="b36fa-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="b36fa-105">toodetermine, czy należy używać punktu końcowego v2.0 hello lub punkt końcowy 1.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="b36fa-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="b36fa-106">Jeśli używasz punktu końcowego v2.0 usługi Azure Active Directory (Azure AD) hello, możesz użyć [OAuth 2.0](active-directory-v2-protocols.md) tokeny dostępu tooprotect interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="b36fa-106">When you use hello Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens tooprotect your web API.</span></span> <span data-ttu-id="b36fa-107">Za pomocą protokołu OAuth 2.0 tokeny dostępu, użytkownicy, którzy mają zarówno osobistego konta Microsoft i pracy lub kont służbowych można bezpiecznego dostępu do interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="b36fa-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="b36fa-108">*Passport* to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="b36fa-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="b36fa-109">Elastyczne i moduły, usługa Passport można dyskretnie usunięty w każdym ekspresowe lub restify aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b36fa-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="b36fa-110">W usłudze Passport kompleksowy zestaw strategii obsługuje uwierzytelnianie przy użyciu nazwy użytkownika i hasła, Facebook, Twitter lub innych opcji.</span><span class="sxs-lookup"><span data-stu-id="b36fa-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="b36fa-111">Opracowaliśmy strategię dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b36fa-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="b36fa-112">W tym artykule zostanie przedstawiony zostanie sposób tooinstall hello modułu, a następnie dodaj hello Azure AD `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="b36fa-112">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="b36fa-113">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="b36fa-113">Download</span></span>
<span data-ttu-id="b36fa-114">Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="b36fa-114">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="b36fa-115">Samouczek hello toofollow, możesz [pobrać szkielet aplikacji hello jako plik .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), lub w klonowania hello szkielet:</span><span class="sxs-lookup"><span data-stu-id="b36fa-115">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="b36fa-116">Umożliwia również wyświetlenie aplikacji hello ukończone na końcu hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="b36fa-116">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="b36fa-117">1: Rejestrowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b36fa-117">1: Register an app</span></span>
<span data-ttu-id="b36fa-118">Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj [te szczegółowe kroki](active-directory-v2-app-registration.md) tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b36fa-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="b36fa-119">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="b36fa-119">Make sure you:</span></span>

* <span data-ttu-id="b36fa-120">Kopiuj hello **identyfikator aplikacji** przypisane tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b36fa-120">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="b36fa-121">Będzie on potrzebny w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b36fa-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="b36fa-122">Dodaj hello **Mobile** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b36fa-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="b36fa-123">Kopiuj hello **identyfikator URI przekierowania** hello portalu.</span><span class="sxs-lookup"><span data-stu-id="b36fa-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="b36fa-124">Należy użyć wartości identyfikatora URI domyślne hello `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="b36fa-124">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="b36fa-125">2: zainstaluj środowisko Node.js</span><span class="sxs-lookup"><span data-stu-id="b36fa-125">2: Install Node.js</span></span>
<span data-ttu-id="b36fa-126">toouse hello próbki w ramach tego samouczka, należy najpierw [instalowania programu Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="b36fa-126">toouse hello sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="b36fa-127">3: Zainstaluj bazę danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="b36fa-127">3: Install MongoDB</span></span>
<span data-ttu-id="b36fa-128">toosuccessfully korzystać z tej próbki, należy najpierw [zainstalować bazy danych MongoDB](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="b36fa-128">toosuccessfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="b36fa-129">W tym przykładzie używasz bazy danych MongoDB toomake trwałego interfejsu API REST w wystąpieniach serwera.</span><span class="sxs-lookup"><span data-stu-id="b36fa-129">In this sample, you use MongoDB toomake your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="b36fa-130">W tym artykule przyjęto założenie, użyj hello domyślnej instalacji serwera punktów końcowych i bazy danych mongodb: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="b36fa-130">In this article, we assume that you use hello default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="b36fa-131">4: Instalacja hello restify modułów w interfejsie API sieci web</span><span class="sxs-lookup"><span data-stu-id="b36fa-131">4: Install hello restify modules in your web API</span></span>
<span data-ttu-id="b36fa-132">Używamy Resitfy toobuild w interfejsie API REST.</span><span class="sxs-lookup"><span data-stu-id="b36fa-132">We use Resitfy toobuild our REST API.</span></span> <span data-ttu-id="b36fa-133">Restify jest minimalną i elastyczną Node.js aplikacji platforma, która jest pochodną Express.</span><span class="sxs-lookup"><span data-stu-id="b36fa-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="b36fa-134">Moduły restify oferuje rozbudowany zestaw funkcji, których można używać toobuild interfejsów API REST na bazie usługi Connect.</span><span class="sxs-lookup"><span data-stu-id="b36fa-134">Restify has a robust set of features that you can use toobuild REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="b36fa-135">Instalacja modułu restify</span><span class="sxs-lookup"><span data-stu-id="b36fa-135">Install restify</span></span>
1.  <span data-ttu-id="b36fa-136">W wierszu polecenia Zmień katalog hello zbyt**azuread**:</span><span class="sxs-lookup"><span data-stu-id="b36fa-136">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="b36fa-137">Jeśli hello **azuread** katalog nie istnieje, utwórz go:</span><span class="sxs-lookup"><span data-stu-id="b36fa-137">If hello **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="b36fa-138">Instalacja modułu restify:</span><span class="sxs-lookup"><span data-stu-id="b36fa-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="b36fa-139">dane wyjściowe tego polecenia Hello powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="b36fa-139">hello output of this command should look like this:</span></span>

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

#### <a name="did-you-get-an-error"></a><span data-ttu-id="b36fa-140">Czy został wyświetlony komunikat o błędzie?</span><span class="sxs-lookup"><span data-stu-id="b36fa-140">Did you get an error?</span></span>
<span data-ttu-id="b36fa-141">W niektórych systemach operacyjnych, gdy używasz hello `npm` polecenia, można napotkać tego komunikatu: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="b36fa-141">On some operating systems, when you use hello `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="b36fa-142">Błąd Hello następuje żądanie wypróbować uruchomionych hello konta z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="b36fa-142">hello error is followed by a request that you try running hello account as an administrator.</span></span> <span data-ttu-id="b36fa-143">W takim przypadku należy użyć polecenia hello `sudo` toorun `npm` na wyższym poziomie uprawnień.</span><span class="sxs-lookup"><span data-stu-id="b36fa-143">If this occurs, use hello command `sudo` toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-toodtrace"></a><span data-ttu-id="b36fa-144">Czy został wyświetlony komunikat o błędzie dotyczący tooDTrace?</span><span class="sxs-lookup"><span data-stu-id="b36fa-144">Did you get an error related tooDTrace?</span></span>
<span data-ttu-id="b36fa-145">Po zainstalowaniu restify, można napotkać ten komunikat:</span><span class="sxs-lookup"><span data-stu-id="b36fa-145">When you install restify, you might see this message:</span></span>

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

<span data-ttu-id="b36fa-146">Moduły restify ma tootrace zaawansowanym mechanizmem wywołań REST przy użyciu narzędzia DTrace.</span><span class="sxs-lookup"><span data-stu-id="b36fa-146">Restify has a powerful mechanism tootrace REST calls by using DTrace.</span></span> <span data-ttu-id="b36fa-147">Jednak narzędzia DTrace nie jest dostępne w wielu systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="b36fa-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="b36fa-148">Można bezpiecznie zignorować ten komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="b36fa-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="b36fa-149">5: Instalacja Passport.js w interfejsie API sieci web</span><span class="sxs-lookup"><span data-stu-id="b36fa-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="b36fa-150">W wierszu polecenia hello Zmień katalog hello zbyt**azuread**.</span><span class="sxs-lookup"><span data-stu-id="b36fa-150">At hello command prompt, change hello directory too**azuread**.</span></span>

2.  <span data-ttu-id="b36fa-151">Zainstaluj Passport.js:</span><span class="sxs-lookup"><span data-stu-id="b36fa-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="b36fa-152">dane wyjściowe polecenia hello Hello powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="b36fa-152">hello output of hello command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="b36fa-153">6: Dodaj interfejs API sieci web tooyour passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="b36fa-153">6: Add passport-azure-ad tooyour web API</span></span>
<span data-ttu-id="b36fa-154">Następnie dodaj strategię OAuth hello, za pomocą biblioteki passport-azuread.</span><span class="sxs-lookup"><span data-stu-id="b36fa-154">Next, add hello OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="b36fa-155">`passport-azuread`jest zestawu strategii łączących usługę Azure AD z usługą Passport.</span><span class="sxs-lookup"><span data-stu-id="b36fa-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="b36fa-156">Używamy tej strategii do tokenów elementów nośnych w próbce tego interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b36fa-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="b36fa-157">Chociaż framework, w którym mogą być wystawiane dowolnego znanego typu tokenu OAuth 2.0, niektóre typy tokenów są często używane.</span><span class="sxs-lookup"><span data-stu-id="b36fa-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="b36fa-158">Tokeny elementów nośnych są często używane tooprotect punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="b36fa-158">Bearer tokens are commonly used tooprotect endpoints.</span></span> <span data-ttu-id="b36fa-159">Tokeny elementów nośnych są najczęściej wystawiony hello typ tokenu OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="b36fa-159">Bearer tokens are hello most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="b36fa-160">Wiele implementacji protokołu OAuth 2.0 założono, że tokeny elementów nośnych są jedynym typem wystawianych tokenów hello.</span><span class="sxs-lookup"><span data-stu-id="b36fa-160">Many OAuth 2.0 implementations assume that bearer tokens are hello only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="b36fa-161">W wierszu polecenia Zmień katalog hello zbyt**azuread**.</span><span class="sxs-lookup"><span data-stu-id="b36fa-161">At a command prompt, change hello directory too**azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="b36fa-162">Zainstaluj hello Passport.js `passport-azure-ad` modułu:</span><span class="sxs-lookup"><span data-stu-id="b36fa-162">Install hello Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="b36fa-163">dane wyjściowe polecenia hello Hello powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="b36fa-163">hello output of hello command should look like this:</span></span>

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

## <a name="7-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="b36fa-164">7: Dodawanie bazy danych MongoDB modułów tooyour — interfejs API sieci web</span><span class="sxs-lookup"><span data-stu-id="b36fa-164">7: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="b36fa-165">W tym przykładzie używamy bazy danych MongoDB naszych przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="b36fa-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="b36fa-166">Instalowanie wtyczki Mongoose powszechnie używaną wtyczkę, toomanage modeli i schematów:</span><span class="sxs-lookup"><span data-stu-id="b36fa-166">Install Mongoose, a widely used plug-in, toomanage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="b36fa-167">Zainstaluj hello sterownik bazy danych dla bazy danych MongoDB, który jest również noszący nazwę MongoDB:</span><span class="sxs-lookup"><span data-stu-id="b36fa-167">Install hello database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="b36fa-168">8: Instalowanie dodatkowych modułów</span><span class="sxs-lookup"><span data-stu-id="b36fa-168">8: Install additional modules</span></span>
<span data-ttu-id="b36fa-169">Zainstaluj pozostałe wymagane moduły hello.</span><span class="sxs-lookup"><span data-stu-id="b36fa-169">Install hello remaining required modules.</span></span>

1.  <span data-ttu-id="b36fa-170">W wierszu polecenia Zmień katalog hello zbyt**azuread**:</span><span class="sxs-lookup"><span data-stu-id="b36fa-170">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="b36fa-171">Wprowadź hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="b36fa-171">Enter hello following commands.</span></span> <span data-ttu-id="b36fa-172">polecenia Hello zainstalować następujące moduły w katalogu node_modules hello:</span><span class="sxs-lookup"><span data-stu-id="b36fa-172">hello commands install hello following modules in your node_modules directory:</span></span>

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

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="b36fa-173">9: Tworzenie pliku Server.js dla zależności</span><span class="sxs-lookup"><span data-stu-id="b36fa-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="b36fa-174">Plik Server.js zawiera większość hello hello funkcji serwera interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="b36fa-174">A Server.js file holds hello majority of hello functionality for your web API server.</span></span> <span data-ttu-id="b36fa-175">Dodaj większość toothis pliku kodu.</span><span class="sxs-lookup"><span data-stu-id="b36fa-175">Add most of your code toothis file.</span></span> <span data-ttu-id="b36fa-176">Do celów produkcyjnych należy Refaktoryzuj hello funkcje na mniejsze pliki, takich jak odrębne trasy i kontrolery.</span><span class="sxs-lookup"><span data-stu-id="b36fa-176">For production purposes, you can refactor hello functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="b36fa-177">W tym artykule w tym celu możemy użyć Server.js.</span><span class="sxs-lookup"><span data-stu-id="b36fa-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="b36fa-178">W wierszu polecenia Zmień katalog hello zbyt**azuread**:</span><span class="sxs-lookup"><span data-stu-id="b36fa-178">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="b36fa-179">Za pomocą dowolnego edytora, Utwórz plik Server.js.</span><span class="sxs-lookup"><span data-stu-id="b36fa-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="b36fa-180">Dodaj poniższe informacje toohello plik hello:</span><span class="sxs-lookup"><span data-stu-id="b36fa-180">Add hello following information toohello file:</span></span>

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

3.  <span data-ttu-id="b36fa-181">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="b36fa-181">Save hello file.</span></span> <span data-ttu-id="b36fa-182">Wkrótce będzie zwracać tooit.</span><span class="sxs-lookup"><span data-stu-id="b36fa-182">You will return tooit shortly.</span></span>

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="b36fa-183">10: tworzenie toostore pliku konfiguracji ustawień usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b36fa-183">10: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="b36fa-184">Ten plik kodu przekazuje parametry konfiguracji hello z tooPassport.js portalu programu Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b36fa-184">This code file passes hello configuration parameters from your Azure AD portal tooPassport.js.</span></span> <span data-ttu-id="b36fa-185">Te wartości konfiguracji są tworzone po dodaniu portalu toohello interfejsu API sieci web hello na początku hello hello artykułu.</span><span class="sxs-lookup"><span data-stu-id="b36fa-185">You created these configuration values when you added hello web API toohello portal at hello beginning of hello article.</span></span> <span data-ttu-id="b36fa-186">Po skopiowaniu kodu hello wyjaśniamy jakie tooput hello wartości tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="b36fa-186">After you copy hello code, we'll explain what tooput in hello values of these parameters.</span></span>

1.  <span data-ttu-id="b36fa-187">W wierszu polecenia Zmień katalog hello zbyt**azuread**:</span><span class="sxs-lookup"><span data-stu-id="b36fa-187">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="b36fa-188">W edytorze Tworzenie pliku Config.js.</span><span class="sxs-lookup"><span data-stu-id="b36fa-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="b36fa-189">Dodaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="b36fa-189">Add hello following information:</span></span>

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="b36fa-190">Wymagane wartości</span><span class="sxs-lookup"><span data-stu-id="b36fa-190">Required values</span></span>

*   <span data-ttu-id="b36fa-191">**IdentityMetadata**: jest to, gdy `passport-azure-ad` sprawdza dane konfiguracyjne dla hello dostawcy tożsamości (IDP) i toovalidate klucze hello hello tokenów sieci Web JSON (Jwt).</span><span class="sxs-lookup"><span data-stu-id="b36fa-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for hello identity provider (IDP) and hello keys toovalidate hello JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="b36fa-192">Jeśli używasz usługi Azure AD, prawdopodobnie nie będzie toochange to.</span><span class="sxs-lookup"><span data-stu-id="b36fa-192">If you are using Azure AD, you probably don't want toochange this.</span></span>

*   <span data-ttu-id="b36fa-193">**grupy odbiorców**: przekierowania URI hello portalu.</span><span class="sxs-lookup"><span data-stu-id="b36fa-193">**audience**: Your redirect URI from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b36fa-194">Przywróć klucze w częstych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="b36fa-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="b36fa-195">Upewnij się, że zawsze pobierać z adresu URL "openid_keys" hello i danej aplikacji hello mogą uzyskiwać dostęp do Internetu hello.</span><span class="sxs-lookup"><span data-stu-id="b36fa-195">Be sure that you always pull from hello "openid_keys" URL, and that hello app can access hello Internet.</span></span>
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a><span data-ttu-id="b36fa-196">11: Dodawanie pliku Server.js tooyour konfiguracji hello</span><span class="sxs-lookup"><span data-stu-id="b36fa-196">11: Add hello configuration tooyour Server.js file</span></span>
<span data-ttu-id="b36fa-197">Aplikacja wymaga tooread hello wartości z pliku konfiguracji hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="b36fa-197">Your application needs tooread hello values from hello config file you just created.</span></span> <span data-ttu-id="b36fa-198">Dodaj plik .config hello jako wymagany zasób w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b36fa-198">Add hello .config file as a required resource in your application.</span></span> <span data-ttu-id="b36fa-199">Ustaw hello toothose zmienne globalne, które znajdują się w Config.js.</span><span class="sxs-lookup"><span data-stu-id="b36fa-199">Set hello global variables toothose that are in Config.js.</span></span>

1.  <span data-ttu-id="b36fa-200">W wierszu polecenia hello Zmień katalog hello zbyt**azuread**:</span><span class="sxs-lookup"><span data-stu-id="b36fa-200">At hello command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="b36fa-201">W edytorze Otwórz Server.js.</span><span class="sxs-lookup"><span data-stu-id="b36fa-201">In an editor, open Server.js.</span></span> <span data-ttu-id="b36fa-202">Dodaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="b36fa-202">Add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="b36fa-203">Dodaj nowy tooServer.js sekcji:</span><span class="sxs-lookup"><span data-stu-id="b36fa-203">Add a new section tooServer.js:</span></span>

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

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="b36fa-204">12: Dodawanie informacji modelu i schemacie modułu MongoDB hello przy użyciu wtyczki Mongoose</span><span class="sxs-lookup"><span data-stu-id="b36fa-204">12: Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="b36fa-205">Następnie należy połączyć z tych trzech plików w usłudze interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b36fa-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="b36fa-206">W tym artykule używamy toostore bazy danych MongoDB nasze zadania.</span><span class="sxs-lookup"><span data-stu-id="b36fa-206">In this article, we use MongoDB toostore our tasks.</span></span> <span data-ttu-id="b36fa-207">Omówiono w *krok 4*.</span><span class="sxs-lookup"><span data-stu-id="b36fa-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="b36fa-208">W pliku Config.js hello utworzonego w kroku 11, nosi nazwę bazy danych *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="b36fa-208">In hello Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="b36fa-209">Która jest umieszczona na końcu hello adres URL połączenia mongoose_auth_local.</span><span class="sxs-lookup"><span data-stu-id="b36fa-209">That was what you put at hello end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="b36fa-210">Nie trzeba toocreate tej bazy danych wcześniej w module MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b36fa-210">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="b36fa-211">Witaj baza danych została utworzona na powitania najpierw uruchamiania aplikacji serwera (przy założeniu, że hello bazy danych już nie istnieje).</span><span class="sxs-lookup"><span data-stu-id="b36fa-211">hello database is created on hello first run of your server application (assuming hello database does not already exist).</span></span>

<span data-ttu-id="b36fa-212">Zostały informację powitania serwera, jakie toouse bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b36fa-212">You've told hello server what MongoDB database toouse.</span></span> <span data-ttu-id="b36fa-213">Następnie należy toowrite niektóre dodatkowy kod toocreate hello modelu i schematu dla zadań serwera.</span><span class="sxs-lookup"><span data-stu-id="b36fa-213">Next, you need toowrite some additional code toocreate hello model and schema for your server's tasks.</span></span>

### <a name="hello-model"></a><span data-ttu-id="b36fa-214">Witaj modelu</span><span class="sxs-lookup"><span data-stu-id="b36fa-214">hello model</span></span>
<span data-ttu-id="b36fa-215">Witaj model schematu jest bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="b36fa-215">hello schema model is very basic.</span></span> <span data-ttu-id="b36fa-216">Aby można ją rozszerzyć.</span><span class="sxs-lookup"><span data-stu-id="b36fa-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="b36fa-217">model schematu Hello ma następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="b36fa-217">hello schema model has these values:</span></span>

*   <span data-ttu-id="b36fa-218">**NAZWA**.</span><span class="sxs-lookup"><span data-stu-id="b36fa-218">**NAME**.</span></span> <span data-ttu-id="b36fa-219">Hello osoby toohello przypisane zadania.</span><span class="sxs-lookup"><span data-stu-id="b36fa-219">hello person assigned toohello task.</span></span> <span data-ttu-id="b36fa-220">Jest to **ciąg** wartość.</span><span class="sxs-lookup"><span data-stu-id="b36fa-220">This is a **string** value.</span></span>
*   <span data-ttu-id="b36fa-221">**ZADANIE**.</span><span class="sxs-lookup"><span data-stu-id="b36fa-221">**TASK**.</span></span> <span data-ttu-id="b36fa-222">Nazwa Hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="b36fa-222">hello name of hello task.</span></span> <span data-ttu-id="b36fa-223">Jest to **ciąg** wartość.</span><span class="sxs-lookup"><span data-stu-id="b36fa-223">This is a **string** value.</span></span>
*   <span data-ttu-id="b36fa-224">**DATA**.</span><span class="sxs-lookup"><span data-stu-id="b36fa-224">**DATE**.</span></span> <span data-ttu-id="b36fa-225">Data Hello przypada hello zadania.</span><span class="sxs-lookup"><span data-stu-id="b36fa-225">hello date that hello task is due.</span></span> <span data-ttu-id="b36fa-226">Jest to **datetime** wartość.</span><span class="sxs-lookup"><span data-stu-id="b36fa-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="b36fa-227">**UKOŃCZONO**.</span><span class="sxs-lookup"><span data-stu-id="b36fa-227">**COMPLETED**.</span></span> <span data-ttu-id="b36fa-228">Określa, czy hello zadanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="b36fa-228">Whether hello task is completed.</span></span> <span data-ttu-id="b36fa-229">Jest to **logiczna** wartość.</span><span class="sxs-lookup"><span data-stu-id="b36fa-229">This is a **Boolean** value.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="b36fa-230">Tworzenie schematu hello w kodzie hello</span><span class="sxs-lookup"><span data-stu-id="b36fa-230">Create hello schema in hello code</span></span>
1.  <span data-ttu-id="b36fa-231">W wierszu polecenia Zmień katalog hello zbyt**azuread**:</span><span class="sxs-lookup"><span data-stu-id="b36fa-231">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="b36fa-232">W edytorze Otwórz Server.js.</span><span class="sxs-lookup"><span data-stu-id="b36fa-232">In your editor, open Server.js.</span></span> <span data-ttu-id="b36fa-233">Poniżej pozycji konfiguracji hello Dodaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="b36fa-233">Below hello configuration entry, add hello following information:</span></span>

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

<span data-ttu-id="b36fa-234">Ten kod łączy się z serwerem MongoDB toohello.</span><span class="sxs-lookup"><span data-stu-id="b36fa-234">This code connects toohello MongoDB server.</span></span> <span data-ttu-id="b36fa-235">Zwraca obiekt schematu.</span><span class="sxs-lookup"><span data-stu-id="b36fa-235">It also returns a schema object.</span></span>

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a><span data-ttu-id="b36fa-236">Przy użyciu schematu hello, tworzenie modelu w kodzie hello</span><span class="sxs-lookup"><span data-stu-id="b36fa-236">Using hello schema, create your model in hello code</span></span>
<span data-ttu-id="b36fa-237">Poniżej hello poprzedzających kodu Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="b36fa-237">Below hello preceding code, add hello following code:</span></span>

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

<span data-ttu-id="b36fa-238">Jak stwierdzić, z kodu hello, najpierw należy utworzyć schemat.</span><span class="sxs-lookup"><span data-stu-id="b36fa-238">As you can tell from hello code, first you create your schema.</span></span> <span data-ttu-id="b36fa-239">Następnie można utworzyć obiektu modelu.</span><span class="sxs-lookup"><span data-stu-id="b36fa-239">Next, you create a model object.</span></span> <span data-ttu-id="b36fa-240">Użyj toostore obiektu modelu hello danych w całym hello kodu podczas definiowania Twojej **tras**.</span><span class="sxs-lookup"><span data-stu-id="b36fa-240">You use hello model object toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="b36fa-241">13: Dodaj trasy dla serwera zadań interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="b36fa-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="b36fa-242">Teraz, gdy masz toowork modelu bazy danych, z dodać trasy hello, które będą używane dla serwera interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b36fa-242">Now that you have a database model toowork with, add hello routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="b36fa-243">Informacje o trasach w restify</span><span class="sxs-lookup"><span data-stu-id="b36fa-243">About routes in restify</span></span>
<span data-ttu-id="b36fa-244">Trasy w restify dokładnie hello taki sam sposób jak korzystając z hello stosu Express pracy.</span><span class="sxs-lookup"><span data-stu-id="b36fa-244">Routes in restify work exactly hello same way they do when you use hello Express stack.</span></span> <span data-ttu-id="b36fa-245">Trasy są definiowane za pomocą hello spodziewać się powitania klienta aplikacji toocall identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="b36fa-245">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="b36fa-246">Zazwyczaj należy zdefiniować trasy w oddzielnym pliku.</span><span class="sxs-lookup"><span data-stu-id="b36fa-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="b36fa-247">W tym samouczku testujemy naszych trasy w Server.js.</span><span class="sxs-lookup"><span data-stu-id="b36fa-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="b36fa-248">Do użytku produkcyjnego zaleca się współczynnika trasy do ich własnych pliku.</span><span class="sxs-lookup"><span data-stu-id="b36fa-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="b36fa-249">Typowy wzorzec trasy modułu restify jest:</span><span class="sxs-lookup"><span data-stu-id="b36fa-249">A typical pattern for a restify route is:</span></span>

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


<span data-ttu-id="b36fa-250">Jest to wzorzec hello na najbardziej podstawowym poziomie hello.</span><span class="sxs-lookup"><span data-stu-id="b36fa-250">This is hello pattern at hello most basic level.</span></span> <span data-ttu-id="b36fa-251">Moduły restify (i Express) podaj znacznie bardziej złożone funkcje, takie jak typy aplikacji toodefine możliwości hello i złożonego routingu przez różne punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="b36fa-251">Restify (and Express) provide much deeper functionality, like hello ability toodefine application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="b36fa-252">Dodaj serwer tooyour trasy domyślnej</span><span class="sxs-lookup"><span data-stu-id="b36fa-252">Add default routes tooyour server</span></span>
<span data-ttu-id="b36fa-253">Dodać podstawowe trasy CRUD hello: **utworzyć**, **pobrać**, **aktualizacji**, i **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="b36fa-253">Add hello basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="b36fa-254">W wierszu polecenia Zmień katalog hello zbyt**azuread**:</span><span class="sxs-lookup"><span data-stu-id="b36fa-254">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="b36fa-255">W edytorze Otwórz Server.js.</span><span class="sxs-lookup"><span data-stu-id="b36fa-255">In an editor, open Server.js.</span></span> <span data-ttu-id="b36fa-256">Poniżej hello wprowadzone wcześniej wpisy w bazie danych, należy dodać hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="b36fa-256">Below hello database entries you made earlier, add hello following information:</span></span>

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

### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="b36fa-257">Dodawanie obsługi błędów dla tras hello</span><span class="sxs-lookup"><span data-stu-id="b36fa-257">Add error handling for hello routes</span></span>
<span data-ttu-id="b36fa-258">Dodaj obsługę błędów, może komunikować się wstecz toohello klienta o hello problem pojawił się.</span><span class="sxs-lookup"><span data-stu-id="b36fa-258">Add some error handling so you can communicate back toohello client about hello problem you encountered.</span></span>

<span data-ttu-id="b36fa-259">Dodaj następującego kodu poniżej hello kodu, który został już zapisany hello:</span><span class="sxs-lookup"><span data-stu-id="b36fa-259">Add hello following code below hello code, which you've already written:</span></span>

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


## <a name="14-create-your-server"></a><span data-ttu-id="b36fa-260">14: Tworzenie serwera</span><span class="sxs-lookup"><span data-stu-id="b36fa-260">14: Create your server</span></span>
<span data-ttu-id="b36fa-261">ostatni element toodo Hello jest tooadd wystąpienia serwera.</span><span class="sxs-lookup"><span data-stu-id="b36fa-261">hello last thing toodo is tooadd your server instance.</span></span> <span data-ttu-id="b36fa-262">wystąpienie serwera Hello zarządza wywołania.</span><span class="sxs-lookup"><span data-stu-id="b36fa-262">hello server instance manages your calls.</span></span>

<span data-ttu-id="b36fa-263">Moduły restify (i Express) ma możliwość głębokiego dostosowania można używać z serwera interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b36fa-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="b36fa-264">W tym samouczku używamy hello najbardziej podstawowa konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="b36fa-264">In this tutorial, we use hello most basic setup.</span></span>

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
## <a name="15-add-hello-routes-without-authentication-for-now"></a><span data-ttu-id="b36fa-265">15: dodać trasy hello (bez uwierzytelniania jest obecnie)</span><span class="sxs-lookup"><span data-stu-id="b36fa-265">15: Add hello routes (without authentication, for now)</span></span>
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
## <a name="16-run-hello-server"></a><span data-ttu-id="b36fa-266">16: Uruchom powitania serwera</span><span class="sxs-lookup"><span data-stu-id="b36fa-266">16: Run hello server</span></span>
<span data-ttu-id="b36fa-267">Jest tootest dobrze serwera przed dodaniem uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b36fa-267">It's a good idea tootest your server before you add authentication.</span></span>

<span data-ttu-id="b36fa-268">Witaj Najprostszym sposobem tootest serwera jest przy użyciu programu curl w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="b36fa-268">hello easiest way tootest your server is by using curl at a command prompt.</span></span> <span data-ttu-id="b36fa-269">toodo, to należy proste narzędzie, której można tooparse danych wyjściowych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="b36fa-269">toodo this, you need a simple utility that you can use tooparse output as JSON.</span></span> 

1.  <span data-ttu-id="b36fa-270">Zainstaluj narzędzie JSON hello używana w hello następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="b36fa-270">Install hello JSON tool that we use in hello following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="b36fa-271">Spowoduje to zainstalowanie narzędzie JSON hello globalnie.</span><span class="sxs-lookup"><span data-stu-id="b36fa-271">This installs hello JSON tool globally.</span></span>

2.  <span data-ttu-id="b36fa-272">Upewnij się, że wystąpienie bazy danych MongoDB zostało uruchomione:</span><span class="sxs-lookup"><span data-stu-id="b36fa-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="b36fa-273">Zmień katalog hello zbyt**azuread**, a następnie uruchom narzędzie curl:</span><span class="sxs-lookup"><span data-stu-id="b36fa-273">Change hello directory too**azuread**, and then run curl:</span></span>

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

4.  <span data-ttu-id="b36fa-274">tooadd zadania:</span><span class="sxs-lookup"><span data-stu-id="b36fa-274">tooadd a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="b36fa-275">odpowiedź Hello powinny być:</span><span class="sxs-lookup"><span data-stu-id="b36fa-275">hello response should be:</span></span>

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

5.  <span data-ttu-id="b36fa-276">Listy zadań dla Brandon:</span><span class="sxs-lookup"><span data-stu-id="b36fa-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="b36fa-277">Jeśli wszystkie te polecenia są uruchamiane bez błędów, to serwera interfejsu API REST toohello OAuth tooadd gotowe.</span><span class="sxs-lookup"><span data-stu-id="b36fa-277">If all these commands run without errors, you are ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="b36fa-278">*Masz teraz serwerem interfejsu API REST z bazą danych MongoDB.*</span><span class="sxs-lookup"><span data-stu-id="b36fa-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="b36fa-279">17: Dodawanie serwera interfejsu API REST tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="b36fa-279">17: Add authentication tooyour REST API server</span></span>
<span data-ttu-id="b36fa-280">Teraz, gdy masz uruchomiony interfejs API REST go skonfigurować toouse za pomocą usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b36fa-280">Now that you have a running REST API, set it up toouse it with Azure AD.</span></span>

<span data-ttu-id="b36fa-281">W wierszu polecenia Zmień katalog hello zbyt**azuread**:</span><span class="sxs-lookup"><span data-stu-id="b36fa-281">At a command prompt, change hello directory too**azuread**:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="b36fa-282">Użyj hello oidcbearerstrategy, który wchodzi w skład passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="b36fa-282">Use hello oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="b36fa-283">Do tej pory zostały skompilowane typowy serwer REST TODO bez żadnej autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="b36fa-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="b36fa-284">Teraz Dodaj uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b36fa-284">Now, add authentication.</span></span>

<span data-ttu-id="b36fa-285">Najpierw należy wskazać, że ma toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="b36fa-285">First,  indicate that you want toouse Passport.</span></span> <span data-ttu-id="b36fa-286">To prawo należy umieścić po wcześniejszej konfiguracji serwera:</span><span class="sxs-lookup"><span data-stu-id="b36fa-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="b36fa-287">Podczas pisania interfejsów API jest hello łącze tooalways dobrym rozwiązaniem, które toosomething danych niż token hello hello użytkownika nie może się podszyć.</span><span class="sxs-lookup"><span data-stu-id="b36fa-287">When you write APIs, it's a good idea tooalways link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="b36fa-288">Gdy ten serwer przechowuje elementy przechowuje je na podstawie Identyfikatora subskrypcji użytkownika hello w hello tokenie (wywoływanym za pośrednictwem token.sub).</span><span class="sxs-lookup"><span data-stu-id="b36fa-288">When this server stores TODO items, it stores them based on hello user subscription ID in hello token (called through token.sub).</span></span> <span data-ttu-id="b36fa-289">W polu "właściciela" hello, możesz zaznaczyć hello token.sub.</span><span class="sxs-lookup"><span data-stu-id="b36fa-289">You put hello token.sub in hello “owner” field.</span></span> <span data-ttu-id="b36fa-290">Daje to pewność, że tylko ten użytkownik może uzyskać dostęp użytkownika hello TODOs.</span><span class="sxs-lookup"><span data-stu-id="b36fa-290">This ensures that only that user can access hello user's TODOs.</span></span> <span data-ttu-id="b36fa-291">Inni użytkownicy mogą uzyskiwać dostęp do TODOs hello, które zostały wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="b36fa-291">No one else can access hello TODOs that were entered.</span></span> <span data-ttu-id="b36fa-292">Brak ma ekspozycji w hello interfejsu API dla "właściciela".</span><span class="sxs-lookup"><span data-stu-id="b36fa-292">There is no exposure in hello API for “owner.”</span></span> <span data-ttu-id="b36fa-293">Użytkownikowi zewnętrznemu zażądanie TODOs innych użytkowników, nawet po dokonaniu uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="b36fa-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="b36fa-294">Następnie użyj strategii nośnego otwarte połączenie identyfikator hello, która jest dostarczany z `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="b36fa-294">Next, use hello Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="b36fa-295">Umieścić po wcześniejszym wkleić:</span><span class="sxs-lookup"><span data-stu-id="b36fa-295">Put this after what you pasted earlier:</span></span>

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

<span data-ttu-id="b36fa-296">Usługa Passport używa podobnego wzorca do wszystkich swoich strategii (Twitter, Facebook i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="b36fa-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="b36fa-297">Wszystkich autorów toohello wzorca.</span><span class="sxs-lookup"><span data-stu-id="b36fa-297">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="b36fa-298">Przekaż strategii hello `function()` używającą tokenu i `done` jako parametry.</span><span class="sxs-lookup"><span data-stu-id="b36fa-298">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="b36fa-299">Strategia Hello jest zwracane, gdy robi swojej pracy.</span><span class="sxs-lookup"><span data-stu-id="b36fa-299">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="b36fa-300">Użytkownik hello magazynu i token hello tymczasowym, więc nie trzeba tooask go ponownie.</span><span class="sxs-lookup"><span data-stu-id="b36fa-300">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b36fa-301">Hello poprzedni kod obejmuje wszystkich użytkowników, które można uwierzytelniać tooyour serwera.</span><span class="sxs-lookup"><span data-stu-id="b36fa-301">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="b36fa-302">Jest to nazywane rejestracji automatycznej.</span><span class="sxs-lookup"><span data-stu-id="b36fa-302">This is known as auto-registration.</span></span> <span data-ttu-id="b36fa-303">Na serwerze produkcyjnym nie ma toolet każdy użytkownik bez konieczności ich przejść przez proces rejestracji, który można wybrać.</span><span class="sxs-lookup"><span data-stu-id="b36fa-303">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="b36fa-304">Jest to zwykle wzorzec hello, które są widoczne w aplikacjach komercyjnych.</span><span class="sxs-lookup"><span data-stu-id="b36fa-304">This is usually hello pattern you see in consumer apps.</span></span> <span data-ttu-id="b36fa-305">Aplikacja Hello mogą zezwalać tooregister z usługą Facebook, ale następnie prosi on tooenter dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="b36fa-305">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="b36fa-306">Jeśli nie korzystasz z wiersza polecenia programu w tym samouczku, można wyodrębnić hello wiadomości e-mail z hello obiektu tokena, który jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="b36fa-306">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="b36fa-307">Następnie może poprosić użytkownika hello tooenter dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="b36fa-307">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="b36fa-308">Ponieważ jest to serwer testowy, Dodaj użytkownika hello bezpośrednio toohello w bazy danych pamięci.</span><span class="sxs-lookup"><span data-stu-id="b36fa-308">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="b36fa-309">Ochrona punktów końcowych</span><span class="sxs-lookup"><span data-stu-id="b36fa-309">Protect endpoints</span></span>
<span data-ttu-id="b36fa-310">Ochrona punktów końcowych, określając hello **passport.authenticate()** wywołania z protokołem hello, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="b36fa-310">Protect endpoints by specifying hello **passport.authenticate()** call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="b36fa-311">Dostęp można edytować w kodzie serwera dla bardziej zaawansowanych opcji:</span><span class="sxs-lookup"><span data-stu-id="b36fa-311">You can edit your route in your server code for a more advanced option:</span></span>

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

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="b36fa-312">18: Uruchom ponownie aplikację serwera</span><span class="sxs-lookup"><span data-stu-id="b36fa-312">18: Run your server application again</span></span>
<span data-ttu-id="b36fa-313">Użyj ponownie curl toosee, jeśli masz OAuth 2.0 ochrony punktów końcowych przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="b36fa-313">Use curl again toosee if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="b36fa-314">Wykonaj tę operację przed uruchomieniem żadnego z zestawów SDK klienta względem tego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="b36fa-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="b36fa-315">zwrócone nagłówki Hello powinien stwierdzić, czy uwierzytelnianie działa poprawnie.</span><span class="sxs-lookup"><span data-stu-id="b36fa-315">hello headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="b36fa-316">Upewnij się, czy działa isntance Twojej bazy danych MongoDB:</span><span class="sxs-lookup"><span data-stu-id="b36fa-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="b36fa-317">Zmień toohello **azuread** katalogu, a następnie użyj curl:</span><span class="sxs-lookup"><span data-stu-id="b36fa-317">Change toohello **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="b36fa-318">Wypróbuj podstawową procedurę testową POST:</span><span class="sxs-lookup"><span data-stu-id="b36fa-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="b36fa-319">Uzyskanie odpowiedzi 401 wskazuje, że warstwa oprogramowania Passport hello próbuje tooredirect toohello punktu końcowego autoryzacji, który ma dokładnie.</span><span class="sxs-lookup"><span data-stu-id="b36fa-319">A 401 response indicates that hello Passport layer is trying tooredirect toohello authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="b36fa-320">*Masz teraz usługi interfejsu API REST, który korzysta z protokołu OAuth 2.0.*</span><span class="sxs-lookup"><span data-stu-id="b36fa-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="b36fa-321">Został usunięty w zakresie, w jakim można bez użycia klienta OAuth 2.0 zgodnego z tym serwerem.</span><span class="sxs-lookup"><span data-stu-id="b36fa-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="b36fa-322">W tym konieczne będzie tooreview dodatkowe samouczka.</span><span class="sxs-lookup"><span data-stu-id="b36fa-322">For that, you will need tooreview an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b36fa-323">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b36fa-323">Next steps</span></span>
<span data-ttu-id="b36fa-324">Odwołania, przykładowy ukończyć powitalnych (bez wartości konfiguracji) jest dostarczany jako [plik zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="b36fa-324">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="b36fa-325">Użytkownik może ją także sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="b36fa-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="b36fa-326">Teraz możesz przejść toomore Tematy zaawansowane.</span><span class="sxs-lookup"><span data-stu-id="b36fa-326">Now, you can move on toomore advanced topics.</span></span> <span data-ttu-id="b36fa-327">Może być tootry [zabezpieczenia aplikacji sieci web Node.js za pomocą punktu końcowego v2.0 hello](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="b36fa-327">You might want tootry [Secure a Node.js web app using hello v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="b36fa-328">Poniżej przedstawiono dodatkowe zasoby:</span><span class="sxs-lookup"><span data-stu-id="b36fa-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="b36fa-329">Przewodnik dewelopera v2.0 usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b36fa-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="b36fa-330">Tag "azure-active-directory" przepełnienie stosu</span><span class="sxs-lookup"><span data-stu-id="b36fa-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="b36fa-331">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="b36fa-331">Get security updates for our products</span></span>
<span data-ttu-id="b36fa-332">Firma Microsoft zachęca toosign się toobe powiadomienia w przypadku wystąpienia zdarzeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b36fa-332">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="b36fa-333">Na powitania [powiadomień o zabezpieczeniach technicznych Microsoft](https://technet.microsoft.com/security/dd252948) pozycję subskrybować alerty klasyfikatory tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="b36fa-333">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

