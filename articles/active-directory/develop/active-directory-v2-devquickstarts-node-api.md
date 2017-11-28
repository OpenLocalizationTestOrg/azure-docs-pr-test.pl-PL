---
title: "Zabezpiecz interfejs API web v2.0 usługi Azure Active Directory przy użyciu środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia sieci web Node.js interfejsu API, który akceptuje tokeny zarówno z osobistego konta Microsoft, jak i w pracy lub szkołą kont."
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
ms.openlocfilehash: 94e945a52b9df7c495de1611baa08083357670c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="6918b-103">Zabezpieczanie interfejsu API sieci web przy użyciu środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="6918b-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="6918b-104">Nie wszystkie usługi Azure Active Directory scenariusze i funkcje działają z punktem końcowym v2.0.</span><span class="sxs-lookup"><span data-stu-id="6918b-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="6918b-105">Aby ustalić, czy należy używać punktu końcowego v2.0 lub punkt końcowy w wersji 1.0, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="6918b-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="6918b-106">Jeśli używasz punktu końcowego v2.0 usługi Azure Active Directory (Azure AD), możesz użyć [OAuth 2.0](active-directory-v2-protocols.md) dostęp do tokenów do ochrony interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="6918b-106">When you use the Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens to protect your web API.</span></span> <span data-ttu-id="6918b-107">Za pomocą protokołu OAuth 2.0 tokeny dostępu, użytkownicy, którzy mają zarówno osobistego konta Microsoft i pracy lub kont służbowych można bezpiecznego dostępu do interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="6918b-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="6918b-108">*Passport* to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="6918b-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="6918b-109">Elastyczne i moduły, usługa Passport można dyskretnie usunięty w każdym ekspresowe lub restify aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6918b-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="6918b-110">W usłudze Passport kompleksowy zestaw strategii obsługuje uwierzytelnianie przy użyciu nazwy użytkownika i hasła, Facebook, Twitter lub innych opcji.</span><span class="sxs-lookup"><span data-stu-id="6918b-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="6918b-111">Opracowaliśmy strategię dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6918b-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="6918b-112">W tym artykule, firma Microsoft opisano, jak zainstalować moduł, a następnie dodaj usługi Azure AD `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="6918b-112">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="6918b-113">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="6918b-113">Download</span></span>
<span data-ttu-id="6918b-114">Kod używany w tym samouczku jest przechowywany [ w serwisie GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="6918b-114">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="6918b-115">Aby użyć tego samouczka, możesz [pobrać szkielet aplikacji w pliku .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), lub sklonować szkielet:</span><span class="sxs-lookup"><span data-stu-id="6918b-115">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="6918b-116">Możesz również uzyskać ukończona aplikacja na końcu tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="6918b-116">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="6918b-117">1: Rejestrowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="6918b-117">1: Register an app</span></span>
<span data-ttu-id="6918b-118">Utwórz nową aplikację na [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj [te szczegółowe kroki](active-directory-v2-app-registration.md) zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="6918b-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="6918b-119">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="6918b-119">Make sure you:</span></span>

* <span data-ttu-id="6918b-120">Kopiuj **identyfikator aplikacji** przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6918b-120">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="6918b-121">Będzie on potrzebny w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="6918b-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="6918b-122">Dodaj **Mobile** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6918b-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="6918b-123">Kopiuj **identyfikator URI przekierowania** z portalu.</span><span class="sxs-lookup"><span data-stu-id="6918b-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="6918b-124">Należy używać domyślnej wartości identyfikatora URI z `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="6918b-124">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="6918b-125">2: zainstaluj środowisko Node.js</span><span class="sxs-lookup"><span data-stu-id="6918b-125">2: Install Node.js</span></span>
<span data-ttu-id="6918b-126">Aby użyć przykładowego dla tego samouczka, należy najpierw [instalowania programu Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="6918b-126">To use the sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="6918b-127">3: Zainstaluj bazę danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="6918b-127">3: Install MongoDB</span></span>
<span data-ttu-id="6918b-128">Aby pomyślnie korzystać z tej próbki, należy [zainstalować bazy danych MongoDB](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="6918b-128">To successfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="6918b-129">W tym przykładzie używasz bazy danych MongoDB ustawienia interfejsu API REST trwałego w wystąpieniach serwera.</span><span class="sxs-lookup"><span data-stu-id="6918b-129">In this sample, you use MongoDB to make your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="6918b-130">W tym artykule przyjęto założenie, Użyj domyślnych punktów instalacji i serwera, końcowych bazy danych mongodb: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="6918b-130">In this article, we assume that you use the default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="6918b-131">4: instalowanie modułów restify w interfejsie API sieci web</span><span class="sxs-lookup"><span data-stu-id="6918b-131">4: Install the restify modules in your web API</span></span>
<span data-ttu-id="6918b-132">Używamy Resitfy do kompilacji w interfejsie API REST.</span><span class="sxs-lookup"><span data-stu-id="6918b-132">We use Resitfy to build our REST API.</span></span> <span data-ttu-id="6918b-133">Restify jest minimalną i elastyczną Node.js aplikacji platforma, która jest pochodną Express.</span><span class="sxs-lookup"><span data-stu-id="6918b-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="6918b-134">Moduły restify oferuje rozbudowany zestaw funkcji, które służą do tworzenia interfejsów API REST na bazie usługi Connect.</span><span class="sxs-lookup"><span data-stu-id="6918b-134">Restify has a robust set of features that you can use to build REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="6918b-135">Instalacja modułu restify</span><span class="sxs-lookup"><span data-stu-id="6918b-135">Install restify</span></span>
1.  <span data-ttu-id="6918b-136">W wierszu polecenia Zmień katalog na **azuread**:</span><span class="sxs-lookup"><span data-stu-id="6918b-136">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="6918b-137">Jeśli **azuread** katalog nie istnieje, utwórz go:</span><span class="sxs-lookup"><span data-stu-id="6918b-137">If the **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="6918b-138">Instalacja modułu restify:</span><span class="sxs-lookup"><span data-stu-id="6918b-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="6918b-139">Dane wyjściowe tego polecenia powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="6918b-139">The output of this command should look like this:</span></span>

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

#### <a name="did-you-get-an-error"></a><span data-ttu-id="6918b-140">Czy został wyświetlony komunikat o błędzie?</span><span class="sxs-lookup"><span data-stu-id="6918b-140">Did you get an error?</span></span>
<span data-ttu-id="6918b-141">W niektórych systemach operacyjnych, korzystając z `npm` polecenia, można napotkać tego komunikatu: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="6918b-141">On some operating systems, when you use the `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="6918b-142">Błąd następuje żądanie spróbuj konto uruchamiania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6918b-142">The error is followed by a request that you try running the account as an administrator.</span></span> <span data-ttu-id="6918b-143">W takim przypadku należy użyć polecenia `sudo` do uruchomienia `npm` na wyższym poziomie uprawnień.</span><span class="sxs-lookup"><span data-stu-id="6918b-143">If this occurs, use the command `sudo` to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-to-dtrace"></a><span data-ttu-id="6918b-144">Czy został wyświetlony komunikat o błędzie dotyczący do narzędzia DTrace?</span><span class="sxs-lookup"><span data-stu-id="6918b-144">Did you get an error related to DTrace?</span></span>
<span data-ttu-id="6918b-145">Po zainstalowaniu restify, można napotkać ten komunikat:</span><span class="sxs-lookup"><span data-stu-id="6918b-145">When you install restify, you might see this message:</span></span>

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

<span data-ttu-id="6918b-146">Moduły restify ma zaawansowany mechanizm śledzenia wywołań REST przy użyciu narzędzia DTrace.</span><span class="sxs-lookup"><span data-stu-id="6918b-146">Restify has a powerful mechanism to trace REST calls by using DTrace.</span></span> <span data-ttu-id="6918b-147">Jednak narzędzia DTrace nie jest dostępne w wielu systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="6918b-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="6918b-148">Można bezpiecznie zignorować ten komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="6918b-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="6918b-149">5: Instalacja Passport.js w interfejsie API sieci web</span><span class="sxs-lookup"><span data-stu-id="6918b-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="6918b-150">W wierszu polecenia Zmień katalog na **azuread**.</span><span class="sxs-lookup"><span data-stu-id="6918b-150">At the command prompt, change the directory to **azuread**.</span></span>

2.  <span data-ttu-id="6918b-151">Zainstaluj Passport.js:</span><span class="sxs-lookup"><span data-stu-id="6918b-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="6918b-152">Dane wyjściowe polecenia powinny wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="6918b-152">The output of the command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="6918b-153">6: Dodaj passport-azure-ad do interfejsu API sieci web</span><span class="sxs-lookup"><span data-stu-id="6918b-153">6: Add passport-azure-ad to your web API</span></span>
<span data-ttu-id="6918b-154">Następnie dodaj strategię OAuth przy użyciu biblioteki passport-azuread.</span><span class="sxs-lookup"><span data-stu-id="6918b-154">Next, add the OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="6918b-155">`passport-azuread`jest zestawu strategii łączących usługę Azure AD z usługą Passport.</span><span class="sxs-lookup"><span data-stu-id="6918b-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="6918b-156">Używamy tej strategii do tokenów elementów nośnych w próbce tego interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="6918b-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="6918b-157">Chociaż framework, w którym mogą być wystawiane dowolnego znanego typu tokenu OAuth 2.0, niektóre typy tokenów są często używane.</span><span class="sxs-lookup"><span data-stu-id="6918b-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="6918b-158">Tokenów elementu nośnego są często używane do ochrony punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="6918b-158">Bearer tokens are commonly used to protect endpoints.</span></span> <span data-ttu-id="6918b-159">Tokeny elementów nośnych są najczęściej wystawiany typ tokenu OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="6918b-159">Bearer tokens are the most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="6918b-160">Wiele implementacji protokołu OAuth 2.0 założono, że tokeny elementów nośnych są jedynym typem wystawianych tokenów.</span><span class="sxs-lookup"><span data-stu-id="6918b-160">Many OAuth 2.0 implementations assume that bearer tokens are the only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="6918b-161">W wierszu polecenia Zmień katalog na **azuread**.</span><span class="sxs-lookup"><span data-stu-id="6918b-161">At a command prompt, change the directory to **azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="6918b-162">Zainstaluj Passport.js `passport-azure-ad` modułu:</span><span class="sxs-lookup"><span data-stu-id="6918b-162">Install the Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="6918b-163">Dane wyjściowe polecenia powinny wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="6918b-163">The output of the command should look like this:</span></span>

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

## <a name="7-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="6918b-164">7: Dodawanie modułów MongoDB do interfejsu API sieci web</span><span class="sxs-lookup"><span data-stu-id="6918b-164">7: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="6918b-165">W tym przykładzie używamy bazy danych MongoDB naszych przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="6918b-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="6918b-166">Instalowanie wtyczki Mongoose powszechnie używaną wtyczkę do zarządzania zabezpieczeniami:</span><span class="sxs-lookup"><span data-stu-id="6918b-166">Install Mongoose, a widely used plug-in, to manage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="6918b-167">Zainstaluj sterownik bazy danych dla bazy danych MongoDB, który jest również noszący nazwę MongoDB:</span><span class="sxs-lookup"><span data-stu-id="6918b-167">Install the database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="6918b-168">8: Instalowanie dodatkowych modułów</span><span class="sxs-lookup"><span data-stu-id="6918b-168">8: Install additional modules</span></span>
<span data-ttu-id="6918b-169">Zainstaluj pozostałe wymagane moduły.</span><span class="sxs-lookup"><span data-stu-id="6918b-169">Install the remaining required modules.</span></span>

1.  <span data-ttu-id="6918b-170">W wierszu polecenia Zmień katalog na **azuread**:</span><span class="sxs-lookup"><span data-stu-id="6918b-170">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="6918b-171">Wprowadź następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="6918b-171">Enter the following commands.</span></span> <span data-ttu-id="6918b-172">Polecenia należy zainstalować w katalogu node_modules następujących modułów:</span><span class="sxs-lookup"><span data-stu-id="6918b-172">The commands install the following modules in your node_modules directory:</span></span>

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

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="6918b-173">9: Tworzenie pliku Server.js dla zależności</span><span class="sxs-lookup"><span data-stu-id="6918b-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="6918b-174">Plik Server.js zawiera większość funkcjonalności serwera interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="6918b-174">A Server.js file holds the majority of the functionality for your web API server.</span></span> <span data-ttu-id="6918b-175">Większość kod należy dodać do tego pliku.</span><span class="sxs-lookup"><span data-stu-id="6918b-175">Add most of your code to this file.</span></span> <span data-ttu-id="6918b-176">Do celów produkcyjnych należy refaktoryzować funkcje na mniejsze pliki, takich jak odrębne trasy i kontrolery.</span><span class="sxs-lookup"><span data-stu-id="6918b-176">For production purposes, you can refactor the functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="6918b-177">W tym artykule w tym celu możemy użyć Server.js.</span><span class="sxs-lookup"><span data-stu-id="6918b-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="6918b-178">W wierszu polecenia Zmień katalog na **azuread**:</span><span class="sxs-lookup"><span data-stu-id="6918b-178">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="6918b-179">Za pomocą dowolnego edytora, Utwórz plik Server.js.</span><span class="sxs-lookup"><span data-stu-id="6918b-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="6918b-180">Dodaj następujące informacje do pliku:</span><span class="sxs-lookup"><span data-stu-id="6918b-180">Add the following information to the file:</span></span>

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

3.  <span data-ttu-id="6918b-181">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="6918b-181">Save the file.</span></span> <span data-ttu-id="6918b-182">Nastąpi powrót do niego później.</span><span class="sxs-lookup"><span data-stu-id="6918b-182">You will return to it shortly.</span></span>

## <a name="10-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="6918b-183">10: Utwórz plik konfiguracji do przechowywania ustawień usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6918b-183">10: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="6918b-184">Ten plik kodu przekazuje parametry konfiguracji w portalu usługi Azure AD do Passport.js.</span><span class="sxs-lookup"><span data-stu-id="6918b-184">This code file passes the configuration parameters from your Azure AD portal to Passport.js.</span></span> <span data-ttu-id="6918b-185">Te wartości konfiguracji są tworzone po dodaniu interfejsu API sieci web do portalu na początku tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="6918b-185">You created these configuration values when you added the web API to the portal at the beginning of the article.</span></span> <span data-ttu-id="6918b-186">Po skopiowaniu kodu wyjaśniamy co należy umieścić w wartościach tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="6918b-186">After you copy the code, we'll explain what to put in the values of these parameters.</span></span>

1.  <span data-ttu-id="6918b-187">W wierszu polecenia Zmień katalog na **azuread**:</span><span class="sxs-lookup"><span data-stu-id="6918b-187">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="6918b-188">W edytorze Tworzenie pliku Config.js.</span><span class="sxs-lookup"><span data-stu-id="6918b-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="6918b-189">Dodaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="6918b-189">Add the following information:</span></span>

    ```Javascript
    // Don't commit this file to your public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need to change this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="6918b-190">Wymagane wartości</span><span class="sxs-lookup"><span data-stu-id="6918b-190">Required values</span></span>

*   <span data-ttu-id="6918b-191">**IdentityMetadata**: jest to, gdy `passport-azure-ad` sprawdza dane konfiguracyjne dla dostawcy tożsamości (IDP) i klucze do sprawdzania poprawności tokenów sieci Web JSON (Jwt).</span><span class="sxs-lookup"><span data-stu-id="6918b-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for the identity provider (IDP) and the keys to validate the JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="6918b-192">Jeśli używasz usługi Azure AD, prawdopodobnie nie chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="6918b-192">If you are using Azure AD, you probably don't want to change this.</span></span>

*   <span data-ttu-id="6918b-193">**grupy odbiorców**: przekierowania URI z portalu.</span><span class="sxs-lookup"><span data-stu-id="6918b-193">**audience**: Your redirect URI from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6918b-194">Przywróć klucze w częstych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="6918b-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="6918b-195">Upewnij się, że należy zawsze ściąganie danych z adresu URL "openid_keys" i że aplikacja może uzyskać dostęp do Internetu.</span><span class="sxs-lookup"><span data-stu-id="6918b-195">Be sure that you always pull from the "openid_keys" URL, and that the app can access the Internet.</span></span>
> 
> 

## <a name="11-add-the-configuration-to-your-serverjs-file"></a><span data-ttu-id="6918b-196">11: Dodaj konfigurację do pliku Server.js</span><span class="sxs-lookup"><span data-stu-id="6918b-196">11: Add the configuration to your Server.js file</span></span>
<span data-ttu-id="6918b-197">Aplikacja wymaga można odczytać wartości z pliku konfiguracji, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="6918b-197">Your application needs to read the values from the config file you just created.</span></span> <span data-ttu-id="6918b-198">Dodaj plik .config jako wymagany zasób w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6918b-198">Add the .config file as a required resource in your application.</span></span> <span data-ttu-id="6918b-199">Ustaw zmienne globalne do tych, które znajdują się w Config.js.</span><span class="sxs-lookup"><span data-stu-id="6918b-199">Set the global variables to those that are in Config.js.</span></span>

1.  <span data-ttu-id="6918b-200">W wierszu polecenia Zmień katalog na **azuread**:</span><span class="sxs-lookup"><span data-stu-id="6918b-200">At the command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="6918b-201">W edytorze Otwórz Server.js.</span><span class="sxs-lookup"><span data-stu-id="6918b-201">In an editor, open Server.js.</span></span> <span data-ttu-id="6918b-202">Dodaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="6918b-202">Add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="6918b-203">Dodaj nową sekcję do Server.js:</span><span class="sxs-lookup"><span data-stu-id="6918b-203">Add a new section to Server.js:</span></span>

    ```Javascript
    // Pass these options in to the ODICBearerStrategy.
    var options = {
    // The URL of the metadata document for your app. Put the keys for token validation from the URL found in the jwks_uri tag in the metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array to hold signed-in users and the current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="6918b-204">12: Dodaj informacje o modelu i schematu bazy danych MongoDB przy użyciu wtyczki Mongoose</span><span class="sxs-lookup"><span data-stu-id="6918b-204">12: Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="6918b-205">Następnie należy połączyć z tych trzech plików w usłudze interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="6918b-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="6918b-206">W tym artykule używamy bazy danych MongoDB do przechowywania nasze zadania.</span><span class="sxs-lookup"><span data-stu-id="6918b-206">In this article, we use MongoDB to store our tasks.</span></span> <span data-ttu-id="6918b-207">Omówiono w *krok 4*.</span><span class="sxs-lookup"><span data-stu-id="6918b-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="6918b-208">W pliku Config.js został utworzony w kroku 11, nosi nazwę bazy danych *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="6918b-208">In the Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="6918b-209">Która jest umieszczona na końcu mongoose_auth_local adres URL połączenia.</span><span class="sxs-lookup"><span data-stu-id="6918b-209">That was what you put at the end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="6918b-210">Nie trzeba tworzyć wcześniej tej bazy danych w module MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6918b-210">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="6918b-211">Baza danych została utworzona przy pierwszym uruchomieniu aplikacji serwera (przy założeniu, że bazy danych już nie istnieje).</span><span class="sxs-lookup"><span data-stu-id="6918b-211">The database is created on the first run of your server application (assuming the database does not already exist).</span></span>

<span data-ttu-id="6918b-212">Serwer został informację której bazy danych MongoDB bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6918b-212">You've told the server what MongoDB database to use.</span></span> <span data-ttu-id="6918b-213">Następnie należy napisać dodatkowy kod w celu utworzenia modelu i schematu dla zadań serwera.</span><span class="sxs-lookup"><span data-stu-id="6918b-213">Next, you need to write some additional code to create the model and schema for your server's tasks.</span></span>

### <a name="the-model"></a><span data-ttu-id="6918b-214">Model</span><span class="sxs-lookup"><span data-stu-id="6918b-214">The model</span></span>
<span data-ttu-id="6918b-215">Model schematu jest bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="6918b-215">The schema model is very basic.</span></span> <span data-ttu-id="6918b-216">Aby można ją rozszerzyć.</span><span class="sxs-lookup"><span data-stu-id="6918b-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="6918b-217">Model schematu ma następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="6918b-217">The schema model has these values:</span></span>

*   <span data-ttu-id="6918b-218">**NAZWA**.</span><span class="sxs-lookup"><span data-stu-id="6918b-218">**NAME**.</span></span> <span data-ttu-id="6918b-219">Osoba przypisana do zadania.</span><span class="sxs-lookup"><span data-stu-id="6918b-219">The person assigned to the task.</span></span> <span data-ttu-id="6918b-220">Jest to **ciąg** wartość.</span><span class="sxs-lookup"><span data-stu-id="6918b-220">This is a **string** value.</span></span>
*   <span data-ttu-id="6918b-221">**ZADANIE**.</span><span class="sxs-lookup"><span data-stu-id="6918b-221">**TASK**.</span></span> <span data-ttu-id="6918b-222">Nazwa zadania.</span><span class="sxs-lookup"><span data-stu-id="6918b-222">The name of the task.</span></span> <span data-ttu-id="6918b-223">Jest to **ciąg** wartość.</span><span class="sxs-lookup"><span data-stu-id="6918b-223">This is a **string** value.</span></span>
*   <span data-ttu-id="6918b-224">**DATA**.</span><span class="sxs-lookup"><span data-stu-id="6918b-224">**DATE**.</span></span> <span data-ttu-id="6918b-225">Data przypada zadania.</span><span class="sxs-lookup"><span data-stu-id="6918b-225">The date that the task is due.</span></span> <span data-ttu-id="6918b-226">Jest to **datetime** wartość.</span><span class="sxs-lookup"><span data-stu-id="6918b-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="6918b-227">**UKOŃCZONO**.</span><span class="sxs-lookup"><span data-stu-id="6918b-227">**COMPLETED**.</span></span> <span data-ttu-id="6918b-228">Określa, czy zadanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="6918b-228">Whether the task is completed.</span></span> <span data-ttu-id="6918b-229">Jest to **logiczna** wartość.</span><span class="sxs-lookup"><span data-stu-id="6918b-229">This is a **Boolean** value.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="6918b-230">Tworzenie schematu w kodzie</span><span class="sxs-lookup"><span data-stu-id="6918b-230">Create the schema in the code</span></span>
1.  <span data-ttu-id="6918b-231">W wierszu polecenia Zmień katalog na **azuread**:</span><span class="sxs-lookup"><span data-stu-id="6918b-231">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="6918b-232">W edytorze Otwórz Server.js.</span><span class="sxs-lookup"><span data-stu-id="6918b-232">In your editor, open Server.js.</span></span> <span data-ttu-id="6918b-233">Poniżej pozycji konfiguracji należy dodać następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="6918b-233">Below the configuration entry, add the following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="6918b-234">Ten kod łączy się z serwerem bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6918b-234">This code connects to the MongoDB server.</span></span> <span data-ttu-id="6918b-235">Zwraca obiekt schematu.</span><span class="sxs-lookup"><span data-stu-id="6918b-235">It also returns a schema object.</span></span>

#### <a name="using-the-schema-create-your-model-in-the-code"></a><span data-ttu-id="6918b-236">Za pomocą schematu, tworzenie modelu w kodzie</span><span class="sxs-lookup"><span data-stu-id="6918b-236">Using the schema, create your model in the code</span></span>
<span data-ttu-id="6918b-237">Poniżej poprzednim kodzie Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="6918b-237">Below the preceding code, add the following code:</span></span>

```Javascript
// Create a basic schema to store your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use the schema to register a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="6918b-238">Jak stwierdzić, z kodu, najpierw należy utworzyć schemat.</span><span class="sxs-lookup"><span data-stu-id="6918b-238">As you can tell from the code, first you create your schema.</span></span> <span data-ttu-id="6918b-239">Następnie można utworzyć obiektu modelu.</span><span class="sxs-lookup"><span data-stu-id="6918b-239">Next, you create a model object.</span></span> <span data-ttu-id="6918b-240">Obiekt modelu używany do przechowywania danych w całym kodzie podczas definiowania Twojej **tras**.</span><span class="sxs-lookup"><span data-stu-id="6918b-240">You use the model object to store your data throughout the code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="6918b-241">13: Dodaj trasy dla serwera zadań interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="6918b-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="6918b-242">Teraz, gdy masz model bazy danych do pracy z dodać trasy, które będą używane dla serwera interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="6918b-242">Now that you have a database model to work with, add the routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="6918b-243">Informacje o trasach w restify</span><span class="sxs-lookup"><span data-stu-id="6918b-243">About routes in restify</span></span>
<span data-ttu-id="6918b-244">Praca restify trasy w taki sam sposób jak korzystania ze stosu Express.</span><span class="sxs-lookup"><span data-stu-id="6918b-244">Routes in restify work exactly the same way they do when you use the Express stack.</span></span> <span data-ttu-id="6918b-245">Trasy są definiowane za pomocą identyfikatora URI, który ma być wywoływany przez aplikacje klienta.</span><span class="sxs-lookup"><span data-stu-id="6918b-245">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="6918b-246">Zazwyczaj należy zdefiniować trasy w oddzielnym pliku.</span><span class="sxs-lookup"><span data-stu-id="6918b-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="6918b-247">W tym samouczku testujemy naszych trasy w Server.js.</span><span class="sxs-lookup"><span data-stu-id="6918b-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="6918b-248">Do użytku produkcyjnego zaleca się współczynnika trasy do ich własnych pliku.</span><span class="sxs-lookup"><span data-stu-id="6918b-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="6918b-249">Typowy wzorzec trasy modułu restify jest:</span><span class="sxs-lookup"><span data-stu-id="6918b-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep the server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="6918b-250">Jest to wzorzec na najbardziej podstawowym poziomie.</span><span class="sxs-lookup"><span data-stu-id="6918b-250">This is the pattern at the most basic level.</span></span> <span data-ttu-id="6918b-251">Moduły restify (i Express) podaj znacznie bardziej złożone funkcje, takie jak możliwość definiowania typy aplikacji i złożonego routingu przez różne punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="6918b-251">Restify (and Express) provide much deeper functionality, like the ability to define application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="6918b-252">Dodawanie tras domyślnych do serwera</span><span class="sxs-lookup"><span data-stu-id="6918b-252">Add default routes to your server</span></span>
<span data-ttu-id="6918b-253">Dodać podstawowe trasy CRUD: **utworzyć**, **pobrać**, **aktualizacji**, i **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="6918b-253">Add the basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="6918b-254">W wierszu polecenia Zmień katalog na **azuread**:</span><span class="sxs-lookup"><span data-stu-id="6918b-254">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="6918b-255">W edytorze Otwórz Server.js.</span><span class="sxs-lookup"><span data-stu-id="6918b-255">In an editor, open Server.js.</span></span> <span data-ttu-id="6918b-256">Poniżej pozycji bazy danych, wprowadzone wcześniej, Dodaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="6918b-256">Below the database entries you made earlier, add the following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow you to use MongoDB Server as your response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it to MongoDB.
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
    req.log.warn(err, 'createTask: unable to save');
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
    'removeTask: unable to delete %s',
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
    req.log.warn(err, 'get: unable to read %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns the list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow us to use MongoDB Server as our response to any origin.
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
    log.warn(err, "There are no tasks in the database. Add one!");
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

### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="6918b-257">Dodawanie obsługi błędów dla tras</span><span class="sxs-lookup"><span data-stu-id="6918b-257">Add error handling for the routes</span></span>
<span data-ttu-id="6918b-258">Dodaj obsługę błędów, może komunikować się do klienta o napotkany problem.</span><span class="sxs-lookup"><span data-stu-id="6918b-258">Add some error handling so you can communicate back to the client about the problem you encountered.</span></span>

<span data-ttu-id="6918b-259">Dodaj następujący kod poniżej kodu, który został już zapisany:</span><span class="sxs-lookup"><span data-stu-id="6918b-259">Add the following code below the code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back to the client.
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


## <a name="14-create-your-server"></a><span data-ttu-id="6918b-260">14: Tworzenie serwera</span><span class="sxs-lookup"><span data-stu-id="6918b-260">14: Create your server</span></span>
<span data-ttu-id="6918b-261">Ostatnim etapem jest można dodać wystąpienia serwera.</span><span class="sxs-lookup"><span data-stu-id="6918b-261">The last thing to do is to add your server instance.</span></span> <span data-ttu-id="6918b-262">Wystąpienie serwera zarządza wywołania.</span><span class="sxs-lookup"><span data-stu-id="6918b-262">The server instance manages your calls.</span></span>

<span data-ttu-id="6918b-263">Moduły restify (i Express) ma możliwość głębokiego dostosowania można używać z serwera interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="6918b-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="6918b-264">W tym samouczku używamy najbardziej podstawowa konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="6918b-264">In this tutorial, we use the most basic setup.</span></span>

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
// Allow 5 requests/second by IP address, and burst to 10.
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
## <a name="15-add-the-routes-without-authentication-for-now"></a><span data-ttu-id="6918b-265">15: dodać trasy (bez uwierzytelniania jest obecnie)</span><span class="sxs-lookup"><span data-stu-id="6918b-265">15: Add the routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD to add the real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in the pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need to maintain session state. You can experiment with removing API protection.
/* To do this, remove the passport.authenticate() method:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-the-server"></a><span data-ttu-id="6918b-266">16: uruchamianie serwera</span><span class="sxs-lookup"><span data-stu-id="6918b-266">16: Run the server</span></span>
<span data-ttu-id="6918b-267">Jest warto przetestować serwer przed dodaniem uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="6918b-267">It's a good idea to test your server before you add authentication.</span></span>

<span data-ttu-id="6918b-268">Najprostszym sposobem przetestować serwer jest przy użyciu programu curl w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="6918b-268">The easiest way to test your server is by using curl at a command prompt.</span></span> <span data-ttu-id="6918b-269">Aby to zrobić, należy proste narzędzie, które służy do analizy danych wyjściowych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="6918b-269">To do this, you need a simple utility that you can use to parse output as JSON.</span></span> 

1.  <span data-ttu-id="6918b-270">Zainstaluj narzędzie JSON, który używamy w poniższych przykładach:</span><span class="sxs-lookup"><span data-stu-id="6918b-270">Install the JSON tool that we use in the following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="6918b-271">Narzędzie JSON zostanie zainstalowane globalnie.</span><span class="sxs-lookup"><span data-stu-id="6918b-271">This installs the JSON tool globally.</span></span>

2.  <span data-ttu-id="6918b-272">Upewnij się, że wystąpienie bazy danych MongoDB zostało uruchomione:</span><span class="sxs-lookup"><span data-stu-id="6918b-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="6918b-273">Zmień katalog na **azuread**, a następnie uruchom narzędzie curl:</span><span class="sxs-lookup"><span data-stu-id="6918b-273">Change the directory to **azuread**, and then run curl:</span></span>

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

4.  <span data-ttu-id="6918b-274">Aby dodać zadania:</span><span class="sxs-lookup"><span data-stu-id="6918b-274">To add a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="6918b-275">Odpowiedź powinna wyglądać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6918b-275">The response should be:</span></span>

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

5.  <span data-ttu-id="6918b-276">Listy zadań dla Brandon:</span><span class="sxs-lookup"><span data-stu-id="6918b-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="6918b-277">Jeśli wszystkie te polecenia są uruchamiane bez błędów, wszystko jest gotowe do dodania OAuth do serwera interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="6918b-277">If all these commands run without errors, you are ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="6918b-278">*Masz teraz serwerem interfejsu API REST z bazą danych MongoDB.*</span><span class="sxs-lookup"><span data-stu-id="6918b-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-to-your-rest-api-server"></a><span data-ttu-id="6918b-279">17: Dodawanie uwierzytelniania do serwera interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="6918b-279">17: Add authentication to your REST API server</span></span>
<span data-ttu-id="6918b-280">Teraz, gdy masz uruchomiony interfejs API REST, skonfigurować go do używania go z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6918b-280">Now that you have a running REST API, set it up to use it with Azure AD.</span></span>

<span data-ttu-id="6918b-281">W wierszu polecenia Zmień katalog na **azuread**:</span><span class="sxs-lookup"><span data-stu-id="6918b-281">At a command prompt, change the directory to **azuread**:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="6918b-282">Użyj oidcbearerstrategy, który wchodzi w skład passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="6918b-282">Use the oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="6918b-283">Do tej pory zostały skompilowane typowy serwer REST TODO bez żadnej autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="6918b-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="6918b-284">Teraz Dodaj uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="6918b-284">Now, add authentication.</span></span>

<span data-ttu-id="6918b-285">Najpierw należy wskazać chcesz korzystać z usługi Passport.</span><span class="sxs-lookup"><span data-stu-id="6918b-285">First,  indicate that you want to use Passport.</span></span> <span data-ttu-id="6918b-286">To prawo należy umieścić po wcześniejszej konfiguracji serwera:</span><span class="sxs-lookup"><span data-stu-id="6918b-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="6918b-287">Podczas pisania interfejsów API jest dobrym pomysłem jest zawsze połączyć dane z unikatowym z tokenu, który użytkownik nie może się podszyć.</span><span class="sxs-lookup"><span data-stu-id="6918b-287">When you write APIs, it's a good idea to always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="6918b-288">Gdy ten serwer przechowuje elementy przechowuje je na podstawie Identyfikatora subskrypcji użytkownika w tokenie (wywoływanym za pośrednictwem token.sub).</span><span class="sxs-lookup"><span data-stu-id="6918b-288">When this server stores TODO items, it stores them based on the user subscription ID in the token (called through token.sub).</span></span> <span data-ttu-id="6918b-289">Token.sub należy umieścić w polu "właściciela".</span><span class="sxs-lookup"><span data-stu-id="6918b-289">You put the token.sub in the “owner” field.</span></span> <span data-ttu-id="6918b-290">Daje to pewność, że tylko ten użytkownik może uzyskać dostęp TODOs użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6918b-290">This ensures that only that user can access the user's TODOs.</span></span> <span data-ttu-id="6918b-291">Inni użytkownicy mogą uzyskiwać dostęp do TODOs, które zostały wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="6918b-291">No one else can access the TODOs that were entered.</span></span> <span data-ttu-id="6918b-292">Brak ma ekspozycji w interfejsie API dla "właściciela".</span><span class="sxs-lookup"><span data-stu-id="6918b-292">There is no exposure in the API for “owner.”</span></span> <span data-ttu-id="6918b-293">Użytkownikowi zewnętrznemu zażądanie TODOs innych użytkowników, nawet po dokonaniu uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="6918b-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="6918b-294">Następnie użyj strategii Otwórz elementu Identyfikatora połączenia nośnego dołączonej `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="6918b-294">Next, use the Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="6918b-295">Umieścić po wcześniejszym wkleić:</span><span class="sxs-lookup"><span data-stu-id="6918b-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling the OIDCBearerStrategy and managing users.
/*
/* Because of the Passport pattern, you need to manage users and info tokens
/* with a FindorCreate() method. The method must be provided by the implementor.
/* In the following code, you autoregister any user and implement a FindById().
/* It's a good idea to do something more advanced.
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
log.info('verifying the user');
log.info(token, 'was the token retrieved');
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

<span data-ttu-id="6918b-296">Usługa Passport używa podobnego wzorca do wszystkich swoich strategii (Twitter, Facebook i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="6918b-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="6918b-297">Wszyscy twórcy kodu strategii jest zgodna z wzorcem.</span><span class="sxs-lookup"><span data-stu-id="6918b-297">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="6918b-298">Przekaż strategii `function()` używającą tokenu i `done` jako parametry.</span><span class="sxs-lookup"><span data-stu-id="6918b-298">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="6918b-299">Strategia jest zwracane, gdy istnieje swojej pracy.</span><span class="sxs-lookup"><span data-stu-id="6918b-299">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="6918b-300">Przechowaj dane użytkownika i Zapisz token, więc nie trzeba było zażądać go ponownie.</span><span class="sxs-lookup"><span data-stu-id="6918b-300">Store the user and stash the token so you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6918b-301">Poprzedni kod obejmuje każdy użytkownik, który może uwierzytelniać się z serwerem.</span><span class="sxs-lookup"><span data-stu-id="6918b-301">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="6918b-302">Jest to nazywane rejestracji automatycznej.</span><span class="sxs-lookup"><span data-stu-id="6918b-302">This is known as auto-registration.</span></span> <span data-ttu-id="6918b-303">Na serwerze produkcyjnym nie mają mieć możliwość każda osoba, która bez konieczności ich przejść przez proces rejestracji, który można wybrać.</span><span class="sxs-lookup"><span data-stu-id="6918b-303">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="6918b-304">Jest to zwykle wzorzec występujący w aplikacjach dla użytkowników indywidualnych.</span><span class="sxs-lookup"><span data-stu-id="6918b-304">This is usually the pattern you see in consumer apps.</span></span> <span data-ttu-id="6918b-305">Aplikacja może pozwala zarejestrować się w serwisie Facebook, ale następnie prosi o podanie dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="6918b-305">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="6918b-306">Jeśli nie korzystasz z wiersza polecenia programu w tym samouczku, można wyodrębnić wiadomości e-mail z obiektu tokena, który jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="6918b-306">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="6918b-307">Następnie może poprosić użytkownika o podanie dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="6918b-307">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="6918b-308">Ponieważ jest to serwer testowy, możesz dodać użytkownika bezpośrednio do bazy danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="6918b-308">Because this is a test server, you add the user directly to the in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="6918b-309">Ochrona punktów końcowych</span><span class="sxs-lookup"><span data-stu-id="6918b-309">Protect endpoints</span></span>
<span data-ttu-id="6918b-310">Ochrona punktów końcowych, określając **passport.authenticate()** wywołania z protokołem, którego chcesz używać.</span><span class="sxs-lookup"><span data-stu-id="6918b-310">Protect endpoints by specifying the **passport.authenticate()** call with the protocol that you want to use.</span></span>

<span data-ttu-id="6918b-311">Dostęp można edytować w kodzie serwera dla bardziej zaawansowanych opcji:</span><span class="sxs-lookup"><span data-stu-id="6918b-311">You can edit your route in your server code for a more advanced option:</span></span>

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

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="6918b-312">18: Uruchom ponownie aplikację serwera</span><span class="sxs-lookup"><span data-stu-id="6918b-312">18: Run your server application again</span></span>
<span data-ttu-id="6918b-313">Użyj ponownie curl, aby zobaczyć, jeśli masz OAuth 2.0 ochrony punktów końcowych przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="6918b-313">Use curl again to see if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="6918b-314">Wykonaj tę operację przed uruchomieniem żadnego z zestawów SDK klienta względem tego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="6918b-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="6918b-315">Zwrócone nagłówki powinny stwierdzić, czy uwierzytelnianie działa poprawnie.</span><span class="sxs-lookup"><span data-stu-id="6918b-315">The headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="6918b-316">Upewnij się, czy działa isntance Twojej bazy danych MongoDB:</span><span class="sxs-lookup"><span data-stu-id="6918b-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="6918b-317">Zmień na **azuread** katalogu, a następnie użyj curl:</span><span class="sxs-lookup"><span data-stu-id="6918b-317">Change to the **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="6918b-318">Wypróbuj podstawową procedurę testową POST:</span><span class="sxs-lookup"><span data-stu-id="6918b-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="6918b-319">Uzyskanie odpowiedzi 401 wskazuje, że warstwa oprogramowania Passport podejmuje próbę przekierowania do punktu końcowego autoryzacji, który ma dokładnie.</span><span class="sxs-lookup"><span data-stu-id="6918b-319">A 401 response indicates that the Passport layer is trying to redirect to the authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="6918b-320">*Masz teraz usługi interfejsu API REST, który korzysta z protokołu OAuth 2.0.*</span><span class="sxs-lookup"><span data-stu-id="6918b-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="6918b-321">Został usunięty w zakresie, w jakim można bez użycia klienta OAuth 2.0 zgodnego z tym serwerem.</span><span class="sxs-lookup"><span data-stu-id="6918b-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="6918b-322">W tym należy przejrzeć dodatkowe samouczka.</span><span class="sxs-lookup"><span data-stu-id="6918b-322">For that, you will need to review an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6918b-323">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6918b-323">Next steps</span></span>
<span data-ttu-id="6918b-324">Odwołania, ukończonych próbka (bez wartości konfiguracji) jest dostępna jako [plik zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="6918b-324">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="6918b-325">Użytkownik może ją także sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="6918b-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="6918b-326">Teraz możesz przejść do bardziej zaawansowanych tematów.</span><span class="sxs-lookup"><span data-stu-id="6918b-326">Now, you can move on to more advanced topics.</span></span> <span data-ttu-id="6918b-327">Możesz spróbować [zabezpieczenia aplikacji sieci web Node.js za pomocą punktu końcowego v2.0](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="6918b-327">You might want to try [Secure a Node.js web app using the v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="6918b-328">Poniżej przedstawiono dodatkowe zasoby:</span><span class="sxs-lookup"><span data-stu-id="6918b-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="6918b-329">Przewodnik dewelopera v2.0 usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6918b-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="6918b-330">Tag "azure-active-directory" przepełnienie stosu</span><span class="sxs-lookup"><span data-stu-id="6918b-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="6918b-331">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="6918b-331">Get security updates for our products</span></span>
<span data-ttu-id="6918b-332">Firma Microsoft zachęca do Zarejestruj się, aby otrzymać powiadomienie, gdy występujących incydentach zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="6918b-332">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="6918b-333">Na [powiadomień o zabezpieczeniach technicznych Microsoft](https://technet.microsoft.com/security/dd252948) strony, należy subskrybować alerty klasyfikatory zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="6918b-333">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

