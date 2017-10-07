---
title: aaaAzure AD Node.js wprowadzenie | Dokumentacja firmy Microsoft
description: "Jak toobuild interfejsu API sieci web Node.js REST który integruje się z usługą Azure AD do uwierzytelniania."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="944a8-103">Rozpoczynanie pracy z interfejsów API sieci web dla środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="944a8-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="944a8-104">*Passport* to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="944a8-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="944a8-105">Elastyczne i moduły, usługa Passport można było porzucić dyskretnie w tooany ekspresowe lub Restify aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="944a8-105">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="944a8-106">Kompleksowy zestaw strategii obsługuje uwierzytelnianie za pomocą nazwy użytkownika i hasła, Facebook i Twitter.</span><span class="sxs-lookup"><span data-stu-id="944a8-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="944a8-107">Opracowaliśmy strategię dla Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="944a8-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="944a8-108">Firma Microsoft zainstalowaniu tego modułu, a następnie dodaj hello Microsoft Azure Active Directory `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="944a8-108">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="944a8-109">toodo, musisz:</span><span class="sxs-lookup"><span data-stu-id="944a8-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="944a8-110">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="944a8-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="944a8-111">Konfigurowanie Twojej aplikacji toouse Passport w `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="944a8-111">Set up your app toouse Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="944a8-112">Konfigurowanie klienta aplikacji toocall hello tooDo listy składnika web API.</span><span class="sxs-lookup"><span data-stu-id="944a8-112">Configure a client application toocall hello tooDo List web API.</span></span>

<span data-ttu-id="944a8-113">Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="944a8-113">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="944a8-114">W tym artykule nie opisano sposobu tooimplement logowania, rejestracji, lub profilu zarządzania za pomocą usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="944a8-114">This article doesn't cover how tooimplement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="944a8-115">Uwzględniono w szczególności wywoływania interfejsów API sieci web po hello użytkownik jest już uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="944a8-115">It focuses on calling web APIs after hello user is already authenticated.</span></span>  <span data-ttu-id="944a8-116">Zalecamy rozpocząć od [jak toointegrate przy użyciu usługi Azure Active Directory dokumentów](active-directory-how-to-integrate.md) toolearn o hello podstawy usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="944a8-116">We recommend that you start with [How toointegrate with Azure Active Directory document](active-directory-how-to-integrate.md) toolearn about hello basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="944a8-117">Tak zostały opublikowane wszystkie hello kodu źródłowego w tym przykładzie uruchomionej w usłudze GitHub w ramach licencji MIT uznać wolnego tooclone (lub nawet lepiej rozwidlenia) i wyrazić swoją opinię i żądań ściągnięcia.</span><span class="sxs-lookup"><span data-stu-id="944a8-117">We've released all hello source code for this running example in GitHub under an MIT license, so feel free tooclone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="944a8-118">O modułach Node.js</span><span class="sxs-lookup"><span data-stu-id="944a8-118">About Node.js modules</span></span>
<span data-ttu-id="944a8-119">Używamy modułów programu Node.js w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="944a8-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="944a8-120">Moduły są obciążana pakiety języka JavaScript, które zapewniają określonych funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="944a8-121">Zazwyczaj należy zainstalować moduły przy użyciu hello Node.js NPM narzędzia wiersza polecenia w katalogu instalacji NPM hello.</span><span class="sxs-lookup"><span data-stu-id="944a8-121">You usually install modules by using hello Node.js an NPM command-line tool in hello NPM installation directory.</span></span> <span data-ttu-id="944a8-122">Jednak niektóre moduły, takich jak moduł HTTP hello, znajdują się w pakiecie Node.js core hello.</span><span class="sxs-lookup"><span data-stu-id="944a8-122">However, some modules, such as hello HTTP module, are included in hello core Node.js package.</span></span>

<span data-ttu-id="944a8-123">Zainstalowane moduły są zapisywane w hello **node_modules** katalogu głównego hello katalogu instalacji środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="944a8-123">Installed modules are saved in hello **node_modules** directory at hello root of your Node.js installation directory.</span></span> <span data-ttu-id="944a8-124">Każdy moduł w hello **node_modules** directory zachowuje własną **node_modules** katalog, który zawiera wszystkie moduły, których ona zależy.</span><span class="sxs-lookup"><span data-stu-id="944a8-124">Each module in hello **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="944a8-125">Ponadto każdego wymaganego modułu jest **node_modules** katalogu.</span><span class="sxs-lookup"><span data-stu-id="944a8-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="944a8-126">Ta struktura katalogów cykliczne reprezentuje hello łańcuch zależności.</span><span class="sxs-lookup"><span data-stu-id="944a8-126">This recursive directory structure represents hello dependency chain.</span></span>

<span data-ttu-id="944a8-127">Ta struktura łańcuch zależności powoduje większe zużycie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="944a8-128">Jednak gwarantuje również to, że spełniono wszystkie zależności i tej wersji hello hello modułów, która jest używana do rozwoju jest również używane w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="944a8-128">But it also guarantees that all dependencies are met and that hello version of hello modules that's used in development is also used in production.</span></span> <span data-ttu-id="944a8-129">To zapewnia bardziej przewidywalne zachowanie aplikacji hello produkcji i zapobiega problemom z wersjami, które mogą mieć wpływ na użytkowników.</span><span class="sxs-lookup"><span data-stu-id="944a8-129">This makes hello production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="944a8-130">Krok 1: Zarejestruj dzierżawę usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="944a8-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="944a8-131">toouse to przykładowe, potrzebujesz dzierżawy usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="944a8-131">toouse this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="944a8-132">Jeśli nie masz pewności, jakie dzierżawcy jest lub tooget, zobacz temat [jak dzierżawy tooget usługi Azure AD](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="944a8-132">If you're not sure what a tenant is or how tooget one, see [How tooget an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="944a8-133">Krok 2: Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="944a8-133">Step 2: Create an application</span></span>
<span data-ttu-id="944a8-134">Następnie utwórz aplikację w katalogu, że informacji zapewnia usługi Azure AD, że wymaga ona toosecurely komunikować się z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="944a8-134">Next you create an app in your directory that gives Azure AD information that it needs toosecurely communicate with your app.</span></span>  <span data-ttu-id="944a8-135">Zarówno powitania klienta aplikacji, jak i interfejs API sieci web są reprezentowane przez jeden **identyfikator aplikacji** w tym przypadku, ponieważ stanowią jedną aplikację logiczną.</span><span class="sxs-lookup"><span data-stu-id="944a8-135">Both hello client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="944a8-136">toocreate usługi aplikacji, wykonaj [tych instrukcji](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="944a8-136">toocreate an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="944a8-137">Jeśli tworzysz aplikację z biznesowych, [te dodatkowe instrukcje mogą okazać się przydatne](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="944a8-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="944a8-138">toocreate aplikacji:</span><span class="sxs-lookup"><span data-stu-id="944a8-138">toocreate an application:</span></span>

1. <span data-ttu-id="944a8-139">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="944a8-139">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="944a8-140">W menu u góry hello wybierz konto.</span><span class="sxs-lookup"><span data-stu-id="944a8-140">On hello top menu, select your account.</span></span> <span data-ttu-id="944a8-141">Następnie w obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, w którym ma tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-141">Then, under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="944a8-142">W menu hello powitania po lewej stronie wybierz **więcej usług**, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="944a8-142">In hello menu on hello left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="944a8-143">Wybierz **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="944a8-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="944a8-144">Wykonaj hello monity toocreate **aplikacji sieci Web i/lub WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="944a8-144">Follow hello prompts toocreate a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="944a8-145">Witaj **nazwa** aplikacji hello opisuje użytkownikom tooend aplikacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-145">hello **name** of hello application describes your application tooend users.</span></span>

      * <span data-ttu-id="944a8-146">Witaj **adres URL logowania** jest hello podstawowy adres URL aplikacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-146">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="944a8-147">Witaj domyślny adres URL hello przykładowy kod to `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="944a8-147">hello default URL of hello sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="944a8-148">Po zarejestrowaniu, usługi Azure AD przypisuje aplikacji Unikatowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="944a8-149">Potrzebujesz tej wartości w kolejnych sekcjach hello, dlatego skopiuj go ze strony aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="944a8-149">You need this value in hello next sections, so copy it from hello application page.</span></span>

7. <span data-ttu-id="944a8-150">Z hello **ustawienia** -> **właściwości** strony dla aplikacji, aktualizacji hello identyfikator URI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-150">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="944a8-151">Witaj **identyfikator URI aplikacji** to unikatowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-151">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="944a8-152">Konwencja Hello jest toouse `https://<tenant-domain>/<app-name>`, na przykład: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="944a8-152">hello convention is toouse `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="944a8-153">Utwórz **klucza** dla aplikacji hello **ustawienia** strony, a następnie skopiuj go innym.</span><span class="sxs-lookup"><span data-stu-id="944a8-153">Create a **Key** for your application from hello **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="944a8-154">Będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="944a8-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="944a8-155">Krok 3: Pobieranie środowiska Node.js dla danej platformy</span><span class="sxs-lookup"><span data-stu-id="944a8-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="944a8-156">toosuccessfully korzystać z tej próbki, należy dysponować działającą instalacją środowiska node.js.</span><span class="sxs-lookup"><span data-stu-id="944a8-156">toosuccessfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="944a8-157">Zainstaluj środowisko Node.js z [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="944a8-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="944a8-158">Krok 4: Instalacja bazy danych MongoDB na platformie</span><span class="sxs-lookup"><span data-stu-id="944a8-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="944a8-159">toosuccessfully korzystać z tej próbki, należy dysponować działającą instalacją bazy danych mongodb.</span><span class="sxs-lookup"><span data-stu-id="944a8-159">toosuccessfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="944a8-160">Możesz użyć bazy danych MongoDB toomake hello trwałego interfejsu API REST w wystąpieniach serwera.</span><span class="sxs-lookup"><span data-stu-id="944a8-160">You use MongoDB toomake hello REST API persistent across server instances.</span></span>

<span data-ttu-id="944a8-161">Instalowanie bazy danych MongoDB z [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="944a8-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="944a8-162">W tym przewodniku zakłada, że można używać hello domyślnej instalacji serwera punktów końcowych i bazy danych mongodb, który w czasie hello pisania tego dokumentu jest mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="944a8-162">This walkthrough assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="944a8-163">Krok 5: Instalowanie modułów Restify hello w interfejsie API sieci web</span><span class="sxs-lookup"><span data-stu-id="944a8-163">Step 5: Install hello Restify modules in your web API</span></span>
<span data-ttu-id="944a8-164">Użyto Restify toobuild interfejsie API REST.</span><span class="sxs-lookup"><span data-stu-id="944a8-164">We are using Restify toobuild our REST API.</span></span> <span data-ttu-id="944a8-165">Restify jest minimalną i elastyczną Node.js aplikacji platforma, która jest pochodną Express.</span><span class="sxs-lookup"><span data-stu-id="944a8-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="944a8-166">Oferuje rozbudowany zestaw funkcji do tworzenia interfejsów API REST na bazie usługi Connect.</span><span class="sxs-lookup"><span data-stu-id="944a8-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="944a8-167">Instalacja modułu Restify</span><span class="sxs-lookup"><span data-stu-id="944a8-167">Install Restify</span></span>
1. <span data-ttu-id="944a8-168">W wierszu polecenia hello Zmień katalogi toohello **azuread** katalogu.</span><span class="sxs-lookup"><span data-stu-id="944a8-168">From hello command line, change directories toohello **azuread** directory.</span></span> <span data-ttu-id="944a8-169">Jeśli hello **azuread** katalog nie istnieje, utwórz go.</span><span class="sxs-lookup"><span data-stu-id="944a8-169">If hello **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="944a8-170">Wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="944a8-170">Type hello following command:</span></span>

    `npm install restify`

    <span data-ttu-id="944a8-171">To polecenie powoduje zainstalowanie modułu Restify.</span><span class="sxs-lookup"><span data-stu-id="944a8-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="944a8-172">Czy został wyświetlony komunikat o błędzie?</span><span class="sxs-lookup"><span data-stu-id="944a8-172">Did you get an error?</span></span>
<span data-ttu-id="944a8-173">Korzystając z programu NPM w niektórych systemach operacyjnych, zostanie zgłoszony błąd informujący o **błąd: EPERM, chmod "/ usr/lokalnej/bin /..."**</span><span class="sxs-lookup"><span data-stu-id="944a8-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="944a8-174">i sugestię wypróbować uruchomionych hello konta z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="944a8-174">and a suggestion that you try running hello account as an administrator.</span></span> <span data-ttu-id="944a8-175">W takim przypadku należy użyć toorun polecenia sudo hello NPM na wyższym poziomie uprawnień.</span><span class="sxs-lookup"><span data-stu-id="944a8-175">If this occurs, use hello sudo command toorun NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="944a8-176">Czy został wyświetlony błąd dotyczący narzędzia DTRACE?</span><span class="sxs-lookup"><span data-stu-id="944a8-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="944a8-177">Podczas instalowania modułu Restify mogą pojawić następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="944a8-177">You might see an error like this when installing Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
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
<span data-ttu-id="944a8-178">Moduł Restify zapewnia zaawansowany mechanizm śledzenia wywołań REST przy użyciu narzędzia DTrace.</span><span class="sxs-lookup"><span data-stu-id="944a8-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="944a8-179">Jednak wiele systemów operacyjnych bez narzędzia DTrace.</span><span class="sxs-lookup"><span data-stu-id="944a8-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="944a8-180">Można te błędy bezpiecznie zignorować.</span><span class="sxs-lookup"><span data-stu-id="944a8-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="944a8-181">dane wyjściowe tego polecenia Hello powinien wyglądać podobnie toohello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="944a8-181">hello output of this command should look similar toohello following output:</span></span>

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
    └── bunyan@0.22.0 (mv@0.0.5)


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="944a8-182">Krok 6: Zainstaluj Passport.js w interfejsie API sieci web</span><span class="sxs-lookup"><span data-stu-id="944a8-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="944a8-183">[Passport](http://passportjs.org/) to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="944a8-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="944a8-184">Elastyczne i moduły, usługa Passport można było porzucić dyskretnie w tooany ekspresowe lub Restify aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="944a8-184">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="944a8-185">Kompleksowy zestaw strategii obsługuje uwierzytelnianie za pomocą nazwy użytkownika i hasła, Facebook i Twitter.</span><span class="sxs-lookup"><span data-stu-id="944a8-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="944a8-186">Opracowaliśmy strategię dla usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="944a8-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="944a8-187">Firma Microsoft zainstalowaniu tego modułu, a następnie dodaj hello Azure Active Directory wtyczki.</span><span class="sxs-lookup"><span data-stu-id="944a8-187">We install this module and then add hello Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="944a8-188">W wierszu polecenia hello Zmień katalogi toohello **azuread** katalogu.</span><span class="sxs-lookup"><span data-stu-id="944a8-188">From hello command line, change directories toohello **azuread** directory.</span></span>

2. <span data-ttu-id="944a8-189">tooinstall passport.js, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="944a8-189">tooinstall passport.js, enter hello following command :</span></span>

    `npm install passport`

    <span data-ttu-id="944a8-190">Hello dane wyjściowe polecenia hello powinien wyglądać podobnie toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="944a8-190">hello output of hello command should look similar toohello following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="944a8-191">Krok 7: Dodawanie interfejsu API sieci web tooyour Passport-Azure-AD</span><span class="sxs-lookup"><span data-stu-id="944a8-191">Step 7: Add Passport-Azure-AD tooyour web API</span></span>
<span data-ttu-id="944a8-192">Następnie dodamy hello strategię OAuth przy użyciu `passport-azure-ad`, zestawu strategii łączących tooPassport usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="944a8-192">Next we add hello OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory tooPassport.</span></span> <span data-ttu-id="944a8-193">Używamy tej strategii do tokenów elementów nośnych w próbce tego interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="944a8-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="944a8-194">Chociaż protokół OAuth2 zapewnia framework, w którym mogą być wystawiane dowolnego znanego typu tokenu, tylko niektóre typy tokenów są często używane.</span><span class="sxs-lookup"><span data-stu-id="944a8-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="944a8-195">Tokeny elementów nośnych są tokeny hello najczęściej używane do ochrony punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="944a8-195">Bearer tokens are hello most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="944a8-196">Są one hello najczęściej wystawiony typ tokenu protokołu OAuth2.</span><span class="sxs-lookup"><span data-stu-id="944a8-196">They are hello most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="944a8-197">W wielu wdrożeniach zakłada, że tokeny elementów nośnych są jedynym typem hello tokeny wystawione.</span><span class="sxs-lookup"><span data-stu-id="944a8-197">Many implementations assume that bearer tokens are hello only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="944a8-198">W wierszu polecenia hello Zmień katalogi toohello **azuread** katalogu.</span><span class="sxs-lookup"><span data-stu-id="944a8-198">From hello command line, change directories toohello **azuread** directory.</span></span>

<span data-ttu-id="944a8-199">Typ hello następujące polecenie tooinstall hello Passport.js `passport-azure-ad module`:</span><span class="sxs-lookup"><span data-stu-id="944a8-199">Type hello following command tooinstall hello Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="944a8-200">dane wyjściowe Hello hello polecenia powinny wyglądać podobnie toohello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="944a8-200">hello output of hello command should look similar toohello following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="944a8-201">Krok 8: Dodawanie bazy danych MongoDB modułów tooyour — interfejs API sieci web</span><span class="sxs-lookup"><span data-stu-id="944a8-201">Step 8: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="944a8-202">Korzystamy z bazy danych MongoDB jako naszego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="944a8-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="944a8-203">Z tego powodu należy tooinstall hello powszechnie używane wtyczki o nazwie modele toomanage Mongoose i schematów.</span><span class="sxs-lookup"><span data-stu-id="944a8-203">For that reason, we need tooinstall hello widely used plug-in called Mongoose toomanage models and schemas.</span></span> <span data-ttu-id="944a8-204">Należy również sterownik bazy danych hello tooinstall bazy danych mongodb (nazywane również bazy danych MongoDB).</span><span class="sxs-lookup"><span data-stu-id="944a8-204">We also need tooinstall hello database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="944a8-205">Krok 9: Instalowanie dodatkowych modułów</span><span class="sxs-lookup"><span data-stu-id="944a8-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="944a8-206">Następnej instalacji hello pozostałe wymagane moduły.</span><span class="sxs-lookup"><span data-stu-id="944a8-206">Next we install hello remaining required modules.</span></span>

1. <span data-ttu-id="944a8-207">W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="944a8-207">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="944a8-208">Wprowadź następujące polecenia tooinstall hello tych modułów w Twojej **node_modules** katalogu:</span><span class="sxs-lookup"><span data-stu-id="944a8-208">Enter hello following commands tooinstall these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="944a8-209">Krok 10: Tworzenie server.js własnymi zależnościami</span><span class="sxs-lookup"><span data-stu-id="944a8-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="944a8-210">pliku server.js Hello zapewnia większość funkcji powitania serwera interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="944a8-210">hello server.js file provides most of hello functionality for our web API server.</span></span> <span data-ttu-id="944a8-211">Możemy dodać większość naszego kodu toothis pliku.</span><span class="sxs-lookup"><span data-stu-id="944a8-211">We add most of our code toothis file.</span></span> <span data-ttu-id="944a8-212">Do celów produkcyjnych zaleca się, że Refaktoryzuj hello funkcje na mniejsze pliki, np. odrębne trasy i kontrolery.</span><span class="sxs-lookup"><span data-stu-id="944a8-212">For production purposes, we recommend that you refactor hello functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="944a8-213">Z tego pokazu używamy server.js dla tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="944a8-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="944a8-214">W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="944a8-214">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="944a8-215">Utwórz `server.js` plik w edytorze Ulubione, a następnie dodaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="944a8-215">Create a `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. <span data-ttu-id="944a8-216">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="944a8-216">Save hello file.</span></span> <span data-ttu-id="944a8-217">Wkrótce zostanie zwrócona tooit.</span><span class="sxs-lookup"><span data-stu-id="944a8-217">We'll return tooit shortly.</span></span>

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="944a8-218">Krok 11: Tworzenie toostore pliku konfiguracji ustawień usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="944a8-218">Step 11: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="944a8-219">Ten plik kodu przekazuje parametry konfiguracji hello z Twojej tooPassport.js portalu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="944a8-219">This code file passes hello configuration parameters from your Azure Active Directory portal tooPassport.js.</span></span> <span data-ttu-id="944a8-220">Te wartości konfiguracji są tworzone po dodaniu portalu toohello interfejsu API sieci web hello w pierwszej części przewodnika hello hello.</span><span class="sxs-lookup"><span data-stu-id="944a8-220">You created these configuration values when you added hello web API toohello portal in hello first part of hello walkthrough.</span></span> <span data-ttu-id="944a8-221">Po skopiowaniu kodu hello prezentujemy zasady jakie tooput hello wartości tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="944a8-221">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

1. <span data-ttu-id="944a8-222">W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="944a8-222">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="944a8-223">Utwórz `config.js` plik w edytorze Ulubione, a następnie dodaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="944a8-223">Create a `config.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. <span data-ttu-id="944a8-224">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="944a8-224">Save hello file.</span></span>

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a><span data-ttu-id="944a8-225">Krok 12: Dodaj plik server.js tooyour wartości konfiguracji</span><span class="sxs-lookup"><span data-stu-id="944a8-225">Step 12: Add configuration values tooyour server.js file</span></span>
<span data-ttu-id="944a8-226">Potrzebujemy tooread te wartości z pliku .config hello, który został utworzony w naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-226">We need tooread these values from hello .config file that you created across our application.</span></span> <span data-ttu-id="944a8-227">toodo, możemy dodać pliku .config hello jako wymagany zasób w naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-227">toodo this, we add hello .config file as a required resource in our application.</span></span> <span data-ttu-id="944a8-228">Następnie możemy ustawić hello zmienne globalne toomatch hello zmiennych w dokumencie config.js hello.</span><span class="sxs-lookup"><span data-stu-id="944a8-228">Then we set hello global variables toomatch hello variables in hello config.js document.</span></span>

1. <span data-ttu-id="944a8-229">W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="944a8-229">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="944a8-230">Otwórz z `server.js` plik w edytorze Ulubione, a następnie dodaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="944a8-230">Open your `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="944a8-231">Następnie dodaj nową sekcję zbyt`server.js` z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="944a8-231">Then add a new section too`server.js` with hello following code:</span></span>

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="944a8-232">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="944a8-232">Save hello file.</span></span>

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="944a8-233">Krok 13: Dodawanie hello informacje o modelu bazy danych MongoDB i schematu przy użyciu wtyczki Mongoose</span><span class="sxs-lookup"><span data-stu-id="944a8-233">Step 13: Add hello MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="944a8-234">Teraz tego przygotowania jest będzie toostart płatności, ponieważ połączono tych trzech plików w ramach usługi interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="944a8-234">Now all this preparation is going toostart paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="944a8-235">W ramach tego przewodnika korzystamy z bazy danych MongoDB toostore nasze zadania zgodnie z opisem w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="944a8-235">For this walkthrough, we use MongoDB toostore our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="944a8-236">W hello `config.js` pliku, że utworzyliśmy krok 11, dzwoniliśmy do naszej bazie danych `tasklist`, ponieważ został który testujemy na końcu hello naszych **mogoose_auth_local** adres URL połączenia.</span><span class="sxs-lookup"><span data-stu-id="944a8-236">In hello `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at hello end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="944a8-237">Nie trzeba toocreate tej bazy danych wcześniej w module MongoDB.</span><span class="sxs-lookup"><span data-stu-id="944a8-237">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="944a8-238">Zamiast tego bazy danych MongoDB tworzy to firmie Microsoft na powitania najpierw uruchom naszej aplikacji serwera (przy założeniu, że hello bazy danych już nie istnieje).</span><span class="sxs-lookup"><span data-stu-id="944a8-238">Instead, MongoDB creates this for us on hello first run of our server application (assuming that hello database doesn't already exist).</span></span>

<span data-ttu-id="944a8-239">Teraz, gdy mamy już informację powitania serwera bazy danych MongoDB chcielibyśmy toouse, potrzebujemy toowrite niektóre dodatkowy kod toocreate hello modelu i schematu dla naszego serwera zadań.</span><span class="sxs-lookup"><span data-stu-id="944a8-239">Now that we've told hello server which MongoDB database we'd like toouse, we need toowrite some additional code toocreate hello model and schema for our server's tasks.</span></span>

### <a name="discussion-of-hello-model"></a><span data-ttu-id="944a8-240">Omówienie modelu hello</span><span class="sxs-lookup"><span data-stu-id="944a8-240">Discussion of hello model</span></span>
<span data-ttu-id="944a8-241">Nasz model schematu jest proste.</span><span class="sxs-lookup"><span data-stu-id="944a8-241">Our schema model is simple.</span></span> <span data-ttu-id="944a8-242">Rozwiń go zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="944a8-242">You expand it as required.</span></span>

<span data-ttu-id="944a8-243">Nazwa: Nazwa hello hello osoby, która jest przypisana toohello zadań.</span><span class="sxs-lookup"><span data-stu-id="944a8-243">NAME: hello name of hello person who is assigned toohello task.</span></span> <span data-ttu-id="944a8-244">A **ciąg**.</span><span class="sxs-lookup"><span data-stu-id="944a8-244">A **String**.</span></span>

<span data-ttu-id="944a8-245">ZADANIE: hello samo zadanie.</span><span class="sxs-lookup"><span data-stu-id="944a8-245">TASK: hello task itself.</span></span> <span data-ttu-id="944a8-246">A **ciąg**.</span><span class="sxs-lookup"><span data-stu-id="944a8-246">A **String**.</span></span>

<span data-ttu-id="944a8-247">Data: hello Data zadania hello jest ukończenia.</span><span class="sxs-lookup"><span data-stu-id="944a8-247">DATE: hello date that hello task is due.</span></span> <span data-ttu-id="944a8-248">A **DATETIME**.</span><span class="sxs-lookup"><span data-stu-id="944a8-248">A **DATETIME**.</span></span>

<span data-ttu-id="944a8-249">UKOŃCZONE: Jeśli hello zadanie zostało zakończone lub nie.</span><span class="sxs-lookup"><span data-stu-id="944a8-249">COMPLETED: If hello task has been completed or not.</span></span> <span data-ttu-id="944a8-250">A **LOGICZNA**.</span><span class="sxs-lookup"><span data-stu-id="944a8-250">A **BOOLEAN**.</span></span>

### <a name="creating-hello-schema-in-hello-code"></a><span data-ttu-id="944a8-251">Tworzenie schematu hello w kodzie hello</span><span class="sxs-lookup"><span data-stu-id="944a8-251">Creating hello schema in hello code</span></span>
1. <span data-ttu-id="944a8-252">W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="944a8-252">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="944a8-253">Otwórz z `server.js` plik w edytorze Ulubione, a następnie dodaj następujące informacje poniżej pozycji konfiguracji hello hello:</span><span class="sxs-lookup"><span data-stu-id="944a8-253">Open your `server.js` file in your favorite editor, and then add hello following information below hello configuration entry:</span></span>

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="944a8-254">Jak stwierdzić, z kodu hello, utworzymy naszych schematu najpierw.</span><span class="sxs-lookup"><span data-stu-id="944a8-254">As you can tell from hello code, we create our schema first.</span></span> <span data-ttu-id="944a8-255">Następnie utworzymy obiektu modelu, który używamy toostore naszych danych w całym hello kodu podczas definiujemy naszych **tras**.</span><span class="sxs-lookup"><span data-stu-id="944a8-255">Then we create a model object that we use toostore our data throughout hello code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="944a8-256">Krok 14: Dodawanie naszych tras do serwera zadań interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="944a8-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="944a8-257">Teraz, gdy mamy toowork modelu bazy danych, z Dodajmy trasy hello pracujemy będzie używana dla serwera interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="944a8-257">Now that we have a database model toowork with, let's add hello routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="944a8-258">Informacje o trasach w module Restify</span><span class="sxs-lookup"><span data-stu-id="944a8-258">About routes in Restify</span></span>
<span data-ttu-id="944a8-259">Trasy działają w Restify hello sam sposób ich w hello Express stosu.</span><span class="sxs-lookup"><span data-stu-id="944a8-259">Routes work in Restify hello same way they do in hello Express stack.</span></span> <span data-ttu-id="944a8-260">Trasy są definiowane za pomocą hello spodziewać się powitania klienta aplikacji toocall identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="944a8-260">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="944a8-261">Zazwyczaj należy zdefiniować trasy w oddzielnym pliku.</span><span class="sxs-lookup"><span data-stu-id="944a8-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="944a8-262">W celach naszych testujemy naszych trasy w pliku server.js hello.</span><span class="sxs-lookup"><span data-stu-id="944a8-262">For our purposes, we put our routes in hello server.js file.</span></span> <span data-ttu-id="944a8-263">Firma Microsoft zaleca współczynnika te trasy do ich własnych plików do użytku produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="944a8-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="944a8-264">Typowy wzorzec trasy modułu Restify jest następujący:</span><span class="sxs-lookup"><span data-stu-id="944a8-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="944a8-265">Jest to wzorzec hello na najbardziej podstawowym poziomie.</span><span class="sxs-lookup"><span data-stu-id="944a8-265">This is hello pattern at its most basic level.</span></span> <span data-ttu-id="944a8-266">Moduły restify (i Express) podaj znacznie bardziej złożone funkcje, takie jak Definiowanie typów aplikacji i zapewnianie złożonego routingu przez różne punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="944a8-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="944a8-267">Dla naszych celów możemy utrzymują te trasy proste.</span><span class="sxs-lookup"><span data-stu-id="944a8-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-tooour-server"></a><span data-ttu-id="944a8-268">Dodaj serwer tooour trasy domyślnej</span><span class="sxs-lookup"><span data-stu-id="944a8-268">Add default routes tooour server</span></span>
<span data-ttu-id="944a8-269">Teraz możemy dodać podstawowe trasy CRUD hello tworzenie, pobieranie, aktualizacji i usunąć.</span><span class="sxs-lookup"><span data-stu-id="944a8-269">We now add hello basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="944a8-270">W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje:</span><span class="sxs-lookup"><span data-stu-id="944a8-270">From hello command line, change directories toohello **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="944a8-271">Otwórz hello `server.js` plik w edytorze Ulubione, a następnie dodaj następujące informacje poniżej hello poprzednie wpisy w bazie danych, które należy podjąć hello:</span><span class="sxs-lookup"><span data-stu-id="944a8-271">Open hello `server.js` file in your favorite editor, and then add hello following information below hello previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="944a8-272">Dodawanie obsługi błędów w naszych interfejsów API</span><span class="sxs-lookup"><span data-stu-id="944a8-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="944a8-273">Krok 15: Tworzenie serwera</span><span class="sxs-lookup"><span data-stu-id="944a8-273">Step 15: Create your server</span></span>
<span data-ttu-id="944a8-274">Zdefiniowanych naszej bazie danych i naszych tras na miejscu.</span><span class="sxs-lookup"><span data-stu-id="944a8-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="944a8-275">Hello ostatni element toodo jest dodać hello wystąpienia serwera zarządzającego naszych wywołania.</span><span class="sxs-lookup"><span data-stu-id="944a8-275">hello last thing toodo is add hello server instance that manages our calls.</span></span>

<span data-ttu-id="944a8-276">Restify (i Express) można zrobić dużo dostosowania do serwera interfejsu API REST, ale ponownie za chwilę toouse hello najbardziej podstawowa konfiguracja dla naszych celów.</span><span class="sxs-lookup"><span data-stu-id="944a8-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going toouse hello most basic setup for our purposes.</span></span>

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a><span data-ttu-id="944a8-277">Krok 16: Dodawanie hello tras toohello serwera (bez uwierzytelniania obecnie)</span><span class="sxs-lookup"><span data-stu-id="944a8-277">Step 16: Add hello routes toohello server (without authentication for now)</span></span>
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a><span data-ttu-id="944a8-278">Kroku 17: Serwer hello uruchamiania (przed dodaniem obsługi protokołu OAuth)</span><span class="sxs-lookup"><span data-stu-id="944a8-278">Step 17: Run hello server (before adding OAuth support)</span></span>
<span data-ttu-id="944a8-279">Przetestowanie serwera przed dodamy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="944a8-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="944a8-280">Witaj Najprostszym sposobem tootest serwera jest przy użyciu programu curl w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="944a8-280">hello easiest way tootest your server is by using curl in a command line.</span></span> <span data-ttu-id="944a8-281">Zanim przejdziemy, potrzebujemy narzędzie, które pozwala nam tooparse danych wyjściowych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="944a8-281">Before we do that, we need a utility that allows us tooparse output as JSON.</span></span>

1. <span data-ttu-id="944a8-282">Zainstaluj powitania po narzędzie JSON (hello wszystkie następujące przykłady narzędzie to):</span><span class="sxs-lookup"><span data-stu-id="944a8-282">Install hello following JSON tool (all hello following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="944a8-283">Spowoduje to zainstalowanie narzędzie JSON hello globalnie.</span><span class="sxs-lookup"><span data-stu-id="944a8-283">This installs hello JSON tool globally.</span></span> <span data-ttu-id="944a8-284">Teraz, gdy firma Microsoft już osiągnąć, który, teraz odtworzyć z serwerem hello:</span><span class="sxs-lookup"><span data-stu-id="944a8-284">Now that we’ve accomplished that, let’s play with hello server:</span></span>

2. <span data-ttu-id="944a8-285">Najpierw upewnij się, że wystąpienie bazy danych mongoDB jest uruchomione:</span><span class="sxs-lookup"><span data-stu-id="944a8-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="944a8-286">Następnie zmień katalog toohello i uruchomić curling:</span><span class="sxs-lookup"><span data-stu-id="944a8-286">Then, change toohello directory and start curling:</span></span>

    <span data-ttu-id="944a8-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="944a8-287">`$ cd azuread` `$ node server.js`</span></span>

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. <span data-ttu-id="944a8-288">Następnie można dodać zadania w ten sposób:</span><span class="sxs-lookup"><span data-stu-id="944a8-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="944a8-289">odpowiedź Hello powinny być:</span><span class="sxs-lookup"><span data-stu-id="944a8-289">hello response should be:</span></span>

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
    <span data-ttu-id="944a8-290">I można utworzyć listę zadań dla Brandon w ten sposób:</span><span class="sxs-lookup"><span data-stu-id="944a8-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="944a8-291">Jeśli wszystko to działa, jesteśmy serwera interfejsu API REST toohello OAuth tooadd gotowe.</span><span class="sxs-lookup"><span data-stu-id="944a8-291">If all this works, we're ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="944a8-292">Masz serwera interfejsu API REST z bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="944a8-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-tooour-rest-api-server"></a><span data-ttu-id="944a8-293">Krok 18: Dodawanie serwera interfejsu API REST tooour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="944a8-293">Step 18: Add authentication tooour REST API server</span></span>
<span data-ttu-id="944a8-294">Teraz, gdy będziemy mieć uruchomiony interfejs API REST, Zacznijmy przydatne z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="944a8-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="944a8-295">W wierszu polecenia hello Zmień katalogi toohello **azuread** folderu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="944a8-295">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="944a8-296">Użyj hello OIDCBearerStrategy dołączonej usługi passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="944a8-296">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="944a8-297">Do tej pory nawiązaliśmy typowy serwer REST TODO bez żadnej autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="944a8-298">Jest to, gdzie Rozpoczniemy, który zestawienie.</span><span class="sxs-lookup"><span data-stu-id="944a8-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="944a8-299">Najpierw należy tooindicate czy chcemy toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="944a8-299">First, we need tooindicate that we want toouse Passport.</span></span> <span data-ttu-id="944a8-300">To prawo należy umieścić po konfiguracji serwera:</span><span class="sxs-lookup"><span data-stu-id="944a8-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="944a8-301">Podczas pisania interfejsów API, zalecamy zawsze połączyć toosomething danych hello unikatowy z tokenu hello hello użytkownika nie może się podszyć.</span><span class="sxs-lookup"><span data-stu-id="944a8-301">When you write APIs, we recommend that you always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="944a8-302">Gdy ten serwer przechowuje elementy przechowuje je na podstawie Identyfikatora obiektu hello użytkownika hello w hello tokenie (wywoływanym za pośrednictwem token.oid), który testujemy w polu "właściciela" hello.</span><span class="sxs-lookup"><span data-stu-id="944a8-302">When this server stores TODO items, it stores them based on hello object ID of hello user in hello token (called through token.oid), which we put in hello “owner” field.</span></span> <span data-ttu-id="944a8-303">Daje to pewność, że tylko ten użytkownik ma dostęp do ich TODOs.</span><span class="sxs-lookup"><span data-stu-id="944a8-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="944a8-304">Nie ma ekspozycji w hello interfejsu API "właściciela", dlatego użytkownikowi zewnętrznemu zażądanie hello TODOs innych nawet po dokonaniu uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="944a8-304">There is no exposure in hello API of “owner,” so an external user can request hello TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="944a8-305">Następny Użyjmy hello strategii elementu nośnego, który jest dostarczany z `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="944a8-305">Next let’s use hello bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="944a8-306">Sprawdź kod hello teraz i wyjaśniamy hello rest wkrótce.</span><span class="sxs-lookup"><span data-stu-id="944a8-306">Look at hello code for now and we'll explain hello rest shortly.</span></span> <span data-ttu-id="944a8-307">Umieścić po wkleić powyżej:</span><span class="sxs-lookup"><span data-stu-id="944a8-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

<span data-ttu-id="944a8-308">Usługa Passport używa podobnego wzorca do wszystkich swoich strategii (Twitter, Facebook itd.) zgodne ze wszyscy twórcy kodu strategii.</span><span class="sxs-lookup"><span data-stu-id="944a8-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="944a8-309">Spojrzenie na powitania strategii, zobacz możemy przebiegu on funkcję, która ma token i gotowe jako parametry hello.</span><span class="sxs-lookup"><span data-stu-id="944a8-309">Looking at hello strategy, you see we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="944a8-310">Witaj strategia ponownie toous po jego działa.</span><span class="sxs-lookup"><span data-stu-id="944a8-310">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="944a8-311">Po tak, przechowujemy hello użytkownika i token hello tymczasowym potrzebujemy nie tooask go ponownie.</span><span class="sxs-lookup"><span data-stu-id="944a8-311">After it does, we store hello user and stash hello token so we won’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="944a8-312">Witaj poprzedni kod obejmuje wszystkich użytkowników, wykonywanej tooauthenticate tooour serwera.</span><span class="sxs-lookup"><span data-stu-id="944a8-312">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="944a8-313">Jest to nazywane rejestracji automatycznej.</span><span class="sxs-lookup"><span data-stu-id="944a8-313">This is known as auto-registration.</span></span> <span data-ttu-id="944a8-314">W przypadku serwerów produkcyjnych, firma Microsoft zaleca, aby nie zezwolić każda osoba, która bez konieczności ich przejściu przez proces rejestracji, który podjęciu decyzji o.</span><span class="sxs-lookup"><span data-stu-id="944a8-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="944a8-315">Jest to zwykle wzorzec hello, które są widoczne w aplikacjach komercyjnych, które pozwalają tooregister z usługą Facebook, ale następnie poprosić toofill dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-315">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="944a8-316">Jeśli to nie programu wiersza polecenia, być może wyodrębniono hello wiadomości e-mail z hello obiektu tokena, który został zwrócony, a następnie zadawane toofill użytkownika hello dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="944a8-316">If this wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="944a8-317">Ponieważ jest to serwer testowy, możemy po prostu dodane toohello bazy danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="944a8-317">Because this is a test server, we simply add them toohello in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="944a8-318">Ochrona niektórych punktów końcowych</span><span class="sxs-lookup"><span data-stu-id="944a8-318">Protect some endpoints</span></span>
<span data-ttu-id="944a8-319">Ochrona punktów końcowych, określając hello `passport.authenticate()` wywołania z protokołem hello, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="944a8-319">You protect endpoints by specifying hello `passport.authenticate()` call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="944a8-320">toomake naszego kodu serwera zrobić coś więcej interesujące umożliwia edytowanie hello trasy.</span><span class="sxs-lookup"><span data-stu-id="944a8-320">toomake our server code do something more interesting, let’s edit hello route.</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="944a8-321">Krok 19: Uruchom ponownie aplikację serwera i upewnij się, że użytkownik jest odrzucany</span><span class="sxs-lookup"><span data-stu-id="944a8-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="944a8-322">Użyjmy `curl` ponownie toosee, jeśli mamy teraz OAuth2 ochrony przed naszych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="944a8-322">Let's use `curl` again toosee if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="944a8-323">Możemy przeprowadzić ten test przed uruchomieniem żadnego z zestawów SDK klientów przed tym punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="944a8-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="944a8-324">Hello zwrócone nagłówki powinny być za mało tootell nam Jeśli chcemy dół hello prawidłową ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="944a8-324">hello headers that are returned should be enough tootell us if we're going down hello right path.</span></span>

1. <span data-ttu-id="944a8-325">Najpierw upewnij się, że wystąpienie bazy danych mongoDB jest uruchomione:</span><span class="sxs-lookup"><span data-stu-id="944a8-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="944a8-326">Następnie zmień katalog toohello i uruchomić curling.</span><span class="sxs-lookup"><span data-stu-id="944a8-326">Then, change toohello directory and start curling.</span></span>

      <span data-ttu-id="944a8-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="944a8-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="944a8-328">Spróbuj podstawową procedurę testową POST.</span><span class="sxs-lookup"><span data-stu-id="944a8-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="944a8-329">401 jest odpowiedź hello, którego szukasz tutaj.</span><span class="sxs-lookup"><span data-stu-id="944a8-329">A 401 is hello response you are looking for here.</span></span> <span data-ttu-id="944a8-330">Odpowiedź wskazuje, że że warstwa oprogramowania Passport hello próbuje tooredirect toohello autoryzacji punktu końcowego, który ma dokładnie.</span><span class="sxs-lookup"><span data-stu-id="944a8-330">This response indicates that hello Passport layer is trying tooredirect toohello authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="944a8-331">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="944a8-331">Next steps</span></span>
<span data-ttu-id="944a8-332">Został usunięty w zakresie, w jakim można z tego serwera bez użycia klienta zgodne OAuth2.</span><span class="sxs-lookup"><span data-stu-id="944a8-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="944a8-333">Konieczne będzie toogo za pośrednictwem dodatkowe wskazówki.</span><span class="sxs-lookup"><span data-stu-id="944a8-333">You will need toogo through an additional walkthrough.</span></span>

<span data-ttu-id="944a8-334">Znasz już teraz jak tooimplement przy użyciu interfejsu API REST Restify i protokołu OAuth2.</span><span class="sxs-lookup"><span data-stu-id="944a8-334">You've now learned how tooimplement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="944a8-335">Masz wystarczająco tookeep kodu opracowywania usługi i uczenia jak toobuild w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="944a8-335">You also have more than enough code tookeep developing your service and learning how toobuild on this example.</span></span>

<span data-ttu-id="944a8-336">Jeśli interesuje Cię w następnych krokach hello w podróży ADAL, poniżej przedstawiono niektóre, firma Microsoft zaleca, aby kontynuować pracę z obsługiwanych klientów biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="944a8-336">If you are interested in hello next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="944a8-337">Klonuj maszynę developer tooyour i skonfigurować zgodnie z opisem w przewodniku hello.</span><span class="sxs-lookup"><span data-stu-id="944a8-337">Clone down tooyour developer machine and configure as described in hello walkthrough.</span></span>

[<span data-ttu-id="944a8-338">Biblioteka ADAL dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="944a8-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="944a8-339">ADAL dla systemu Android</span><span class="sxs-lookup"><span data-stu-id="944a8-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
