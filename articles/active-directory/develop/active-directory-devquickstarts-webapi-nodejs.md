---
title: "Azure AD środowiska Node.js wprowadzenie | Dokumentacja firmy Microsoft"
description: "Jak utworzyć sieci web Node.js REST API, która integruje się z usługą Azure AD do uwierzytelniania."
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
ms.openlocfilehash: 4f58177f540c14172d7ece8b4bc8c8a2b9787f8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="b8132-103">Rozpoczynanie pracy z interfejsów API sieci web dla środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="b8132-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="b8132-104">*Passport* to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="b8132-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="b8132-105">Elastyczne i moduły, usługa Passport można dyskretnie usunięty każdym Express opartą na lub Restify aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b8132-105">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="b8132-106">Kompleksowy zestaw strategii obsługuje uwierzytelnianie za pomocą nazwy użytkownika i hasła, Facebook i Twitter.</span><span class="sxs-lookup"><span data-stu-id="b8132-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="b8132-107">Opracowaliśmy strategię dla Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b8132-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="b8132-108">Firma Microsoft zainstalowaniu tego modułu, a następnie dodaj Microsoft Azure Active Directory `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="b8132-108">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="b8132-109">W tym celu należy:</span><span class="sxs-lookup"><span data-stu-id="b8132-109">To do this, you need to:</span></span>

1. <span data-ttu-id="b8132-110">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8132-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="b8132-111">Konfigurowanie aplikacji do użycia w usłudze Passport `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="b8132-111">Set up your app to use Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="b8132-112">Skonfigurować aplikację klienta do wywołania interfejsu API sieci web listy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="b8132-112">Configure a client application to call the To Do List web API.</span></span>

<span data-ttu-id="b8132-113">Kod używany w tym samouczku jest przechowywany [ w serwisie GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="b8132-113">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="b8132-114">W tym artykule nie opisano sposobu wdrażania logowania, rejestracji lub profil zarządzania za pomocą usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="b8132-114">This article doesn't cover how to implement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="b8132-115">Uwzględniono w szczególności wywoływania interfejsów API sieci web po użytkownik jest już uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="b8132-115">It focuses on calling web APIs after the user is already authenticated.</span></span>  <span data-ttu-id="b8132-116">Zalecamy rozpocząć od [sposobu integracji z usługą Azure Active Directory dokumentem](active-directory-how-to-integrate.md) się podstawowe informacje na temat usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8132-116">We recommend that you start with [How to integrate with Azure Active Directory document](active-directory-how-to-integrate.md) to learn about the basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="b8132-117">Zostały Opublikowano kod źródłowy w tym przykładzie uruchomionej w usłudze GitHub MIT licencji, tak się klonowania (lub nawet lepiej rozwidlenia) i wyrazić swoją opinię oraz żądań ściągnięcia.</span><span class="sxs-lookup"><span data-stu-id="b8132-117">We've released all the source code for this running example in GitHub under an MIT license, so feel free to clone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="b8132-118">O modułach Node.js</span><span class="sxs-lookup"><span data-stu-id="b8132-118">About Node.js modules</span></span>
<span data-ttu-id="b8132-119">Używamy modułów programu Node.js w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="b8132-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="b8132-120">Moduły są obciążana pakiety języka JavaScript, które zapewniają określonych funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b8132-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="b8132-121">Zazwyczaj należy zainstalować moduły przy użyciu środowiska Node.js NPM narzędzia wiersza polecenia w katalogu instalacyjnym programu NPM.</span><span class="sxs-lookup"><span data-stu-id="b8132-121">You usually install modules by using the Node.js an NPM command-line tool in the NPM installation directory.</span></span> <span data-ttu-id="b8132-122">Jednak niektóre moduły, takich jak moduł HTTP znajdują się w pakiecie Node.js core.</span><span class="sxs-lookup"><span data-stu-id="b8132-122">However, some modules, such as the HTTP module, are included in the core Node.js package.</span></span>

<span data-ttu-id="b8132-123">Zainstalowane moduły są zapisywane w **node_modules** katalogu w głównym katalogu instalacji środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="b8132-123">Installed modules are saved in the **node_modules** directory at the root of your Node.js installation directory.</span></span> <span data-ttu-id="b8132-124">Każdy moduł w **node_modules** directory zachowuje własną **node_modules** katalog, który zawiera wszystkie moduły, których ona zależy.</span><span class="sxs-lookup"><span data-stu-id="b8132-124">Each module in the **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="b8132-125">Ponadto każdego wymaganego modułu jest **node_modules** katalogu.</span><span class="sxs-lookup"><span data-stu-id="b8132-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="b8132-126">Ta struktura katalogów cykliczne reprezentuje łańcuch zależności.</span><span class="sxs-lookup"><span data-stu-id="b8132-126">This recursive directory structure represents the dependency chain.</span></span>

<span data-ttu-id="b8132-127">Ta struktura łańcuch zależności powoduje większe zużycie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b8132-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="b8132-128">Jednak gwarantuje również to, że wszystkie zależności są spełnione i że wersji modułów, która jest używana do rozwoju jest również używany w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="b8132-128">But it also guarantees that all dependencies are met and that the version of the modules that's used in development is also used in production.</span></span> <span data-ttu-id="b8132-129">To zapewnia bardziej przewidywalne zachowanie aplikacji produkcyjnych i zapobiega problemom z wersjami, które mogą mieć wpływ na użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b8132-129">This makes the production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="b8132-130">Krok 1: Zarejestruj dzierżawę usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8132-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="b8132-131">Aby korzystać z tej próbki, należy dzierżawy usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8132-131">To use this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="b8132-132">Jeśli nie masz pewności jakie dzierżawcy jest lub sposobie pobierania, zobacz [jak uzyskać dzierżawę usługi Azure AD](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b8132-132">If you're not sure what a tenant is or how to get one, see [How to get an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="b8132-133">Krok 2: Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b8132-133">Step 2: Create an application</span></span>
<span data-ttu-id="b8132-134">Następnie utwórz aplikację w katalogu zawiera informacje wymagane do bezpiecznego komunikowania się z aplikacji Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8132-134">Next you create an app in your directory that gives Azure AD information that it needs to securely communicate with your app.</span></span>  <span data-ttu-id="b8132-135">Zarówno aplikacja klienta, jak i interfejsu API sieci web są reprezentowane przez jeden **identyfikator aplikacji** w tym przypadku, ponieważ stanowią jedną aplikację logiczną.</span><span class="sxs-lookup"><span data-stu-id="b8132-135">Both the client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="b8132-136">Aby utworzyć aplikację, postępuj zgodnie z [tymi instrukcjami](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="b8132-136">To create an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="b8132-137">Jeśli tworzysz aplikację z biznesowych, [te dodatkowe instrukcje mogą okazać się przydatne](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="b8132-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="b8132-138">Aby utworzyć aplikację:</span><span class="sxs-lookup"><span data-stu-id="b8132-138">To create an application:</span></span>

1. <span data-ttu-id="b8132-139">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8132-139">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="b8132-140">W górnym menu wybierz konto.</span><span class="sxs-lookup"><span data-stu-id="b8132-140">On the top menu, select your account.</span></span> <span data-ttu-id="b8132-141">Następnie w obszarze **katalogu** wybierz dzierżawy usługi Active Directory, które chcesz zarejestrować aplikację.</span><span class="sxs-lookup"><span data-stu-id="b8132-141">Then, under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="b8132-142">W menu po lewej stronie wybierz **więcej usług**, a następnie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b8132-142">In the menu on the left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="b8132-143">Wybierz **rejestracji aplikacji**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="b8132-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="b8132-144">Postępuj zgodnie z monitami, aby utworzyć **aplikacji sieci Web i/lub WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="b8132-144">Follow the prompts to create a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="b8132-145">**Nazwa** aplikacji opisuje aplikacji dla użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="b8132-145">The **name** of the application describes your application to end users.</span></span>

      * <span data-ttu-id="b8132-146">**Adres URL logowania** jest podstawowy adres URL aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b8132-146">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="b8132-147">Jest to domyślny adres URL w przykładowym kodzie `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="b8132-147">The default URL of the sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="b8132-148">Po zarejestrowaniu, usługi Azure AD przypisuje aplikacji Unikatowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b8132-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="b8132-149">Potrzebujesz tej wartości w kolejnych sekcjach, dlatego skopiuj go ze strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b8132-149">You need this value in the next sections, so copy it from the application page.</span></span>

7. <span data-ttu-id="b8132-150">Z **ustawienia** -> **właściwości** strony dla aplikacji, zaktualizuj identyfikator URI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b8132-150">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="b8132-151">**Identyfikator URI aplikacji** to unikatowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b8132-151">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="b8132-152">Konwencji jest użycie `https://<tenant-domain>/<app-name>`, na przykład: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="b8132-152">The convention is to use `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="b8132-153">Utwórz **klucza** aplikacji z **ustawienia** strony, a następnie skopiuj go innym.</span><span class="sxs-lookup"><span data-stu-id="b8132-153">Create a **Key** for your application from the **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="b8132-154">Będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="b8132-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="b8132-155">Krok 3: Pobieranie środowiska Node.js dla danej platformy</span><span class="sxs-lookup"><span data-stu-id="b8132-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="b8132-156">Aby pomyślnie korzystać z tej próbki, należy dysponować działającą instalacją środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="b8132-156">To successfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="b8132-157">Zainstaluj środowisko Node.js z [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="b8132-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="b8132-158">Krok 4: Instalacja bazy danych MongoDB na platformie</span><span class="sxs-lookup"><span data-stu-id="b8132-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="b8132-159">Aby pomyślnie korzystać z tej próbki, należy dysponować działającą instalacją bazy danych mongodb.</span><span class="sxs-lookup"><span data-stu-id="b8132-159">To successfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="b8132-160">Używasz bazy danych MongoDB ustawienia interfejsu API REST trwałego w wystąpieniach serwera.</span><span class="sxs-lookup"><span data-stu-id="b8132-160">You use MongoDB to make the REST API persistent across server instances.</span></span>

<span data-ttu-id="b8132-161">Instalowanie bazy danych MongoDB z [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="b8132-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="b8132-162">W tym przewodniku założono użycie domyślnej instalacji i serwera punktów końcowych dla bazy danych MongoDB, które w momencie pisania tego dokumentu jest mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="b8132-162">This walkthrough assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="b8132-163">Krok 5: Instalowanie modułów Restify w interfejsie API sieci web</span><span class="sxs-lookup"><span data-stu-id="b8132-163">Step 5: Install the Restify modules in your web API</span></span>
<span data-ttu-id="b8132-164">Restify jest używany do tworzenia interfejsie API REST.</span><span class="sxs-lookup"><span data-stu-id="b8132-164">We are using Restify to build our REST API.</span></span> <span data-ttu-id="b8132-165">Restify jest minimalną i elastyczną Node.js aplikacji platforma, która jest pochodną Express.</span><span class="sxs-lookup"><span data-stu-id="b8132-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="b8132-166">Oferuje rozbudowany zestaw funkcji do tworzenia interfejsów API REST na bazie usługi Connect.</span><span class="sxs-lookup"><span data-stu-id="b8132-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="b8132-167">Instalacja modułu Restify</span><span class="sxs-lookup"><span data-stu-id="b8132-167">Install Restify</span></span>
1. <span data-ttu-id="b8132-168">W wierszu polecenia przejdź do **azuread** katalogu.</span><span class="sxs-lookup"><span data-stu-id="b8132-168">From the command line, change directories to the **azuread** directory.</span></span> <span data-ttu-id="b8132-169">Jeśli **azuread** katalog nie istnieje, utwórz go.</span><span class="sxs-lookup"><span data-stu-id="b8132-169">If the **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="b8132-170">Wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b8132-170">Type the following command:</span></span>

    `npm install restify`

    <span data-ttu-id="b8132-171">To polecenie powoduje zainstalowanie modułu Restify.</span><span class="sxs-lookup"><span data-stu-id="b8132-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="b8132-172">Czy został wyświetlony komunikat o błędzie?</span><span class="sxs-lookup"><span data-stu-id="b8132-172">Did you get an error?</span></span>
<span data-ttu-id="b8132-173">Korzystając z programu NPM w niektórych systemach operacyjnych, zostanie zgłoszony błąd informujący o **błąd: EPERM, chmod "/ usr/lokalnej/bin /..."**</span><span class="sxs-lookup"><span data-stu-id="b8132-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="b8132-174">i sugestii, spróbuj konto uruchamiania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b8132-174">and a suggestion that you try running the account as an administrator.</span></span> <span data-ttu-id="b8132-175">W takim przypadku należy użyć polecenia sudo, aby uruchomić NPM na wyższym poziomie uprawnień.</span><span class="sxs-lookup"><span data-stu-id="b8132-175">If this occurs, use the sudo command to run NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="b8132-176">Czy został wyświetlony błąd dotyczący narzędzia DTRACE?</span><span class="sxs-lookup"><span data-stu-id="b8132-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="b8132-177">Podczas instalowania modułu Restify mogą pojawić następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="b8132-177">You might see an error like this when installing Restify:</span></span>

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
<span data-ttu-id="b8132-178">Moduł Restify zapewnia zaawansowany mechanizm śledzenia wywołań REST przy użyciu narzędzia DTrace.</span><span class="sxs-lookup"><span data-stu-id="b8132-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="b8132-179">Jednak wiele systemów operacyjnych bez narzędzia DTrace.</span><span class="sxs-lookup"><span data-stu-id="b8132-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="b8132-180">Można te błędy bezpiecznie zignorować.</span><span class="sxs-lookup"><span data-stu-id="b8132-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="b8132-181">Dane wyjściowe tego polecenia powinny wyglądać podobnie do następujących danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="b8132-181">The output of this command should look similar to the following output:</span></span>

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


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="b8132-182">Krok 6: Zainstaluj Passport.js w interfejsie API sieci web</span><span class="sxs-lookup"><span data-stu-id="b8132-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="b8132-183">[Passport](http://passportjs.org/) to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="b8132-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="b8132-184">Elastyczne i moduły, usługa Passport można dyskretnie usunięty każdym Express opartą na lub Restify aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b8132-184">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="b8132-185">Kompleksowy zestaw strategii obsługuje uwierzytelnianie za pomocą nazwy użytkownika i hasła, Facebook i Twitter.</span><span class="sxs-lookup"><span data-stu-id="b8132-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="b8132-186">Opracowaliśmy strategię dla usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8132-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="b8132-187">Firma Microsoft zainstalowaniu tego modułu, a następnie dodaj wtyczki usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8132-187">We install this module and then add the Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="b8132-188">W wierszu polecenia przejdź do **azuread** katalogu.</span><span class="sxs-lookup"><span data-stu-id="b8132-188">From the command line, change directories to the **azuread** directory.</span></span>

2. <span data-ttu-id="b8132-189">Aby zainstalować passport.js, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b8132-189">To install passport.js, enter the following command :</span></span>

    `npm install passport`

    <span data-ttu-id="b8132-190">Dane wyjściowe polecenia powinien wyglądać podobnie do następującego:</span><span class="sxs-lookup"><span data-stu-id="b8132-190">The output of the command should look similar to the following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="b8132-191">Krok 7: Dodawanie usługi Passport-Azure-AD do interfejsu API sieci web</span><span class="sxs-lookup"><span data-stu-id="b8132-191">Step 7: Add Passport-Azure-AD to your web API</span></span>
<span data-ttu-id="b8132-192">Następnie dodamy strategię OAuth przy użyciu `passport-azure-ad`, zestawu strategii łączących usługę Azure Active Directory do usługi Passport.</span><span class="sxs-lookup"><span data-stu-id="b8132-192">Next we add the OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory to Passport.</span></span> <span data-ttu-id="b8132-193">Używamy tej strategii do tokenów elementów nośnych w próbce tego interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b8132-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="b8132-194">Chociaż protokół OAuth2 zapewnia framework, w którym mogą być wystawiane dowolnego znanego typu tokenu, tylko niektóre typy tokenów są często używane.</span><span class="sxs-lookup"><span data-stu-id="b8132-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="b8132-195">Tokeny elementów nośnych są najczęściej używane tokeny zabezpieczające punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="b8132-195">Bearer tokens are the most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="b8132-196">Są one najczęściej wystawiany typ tokenu protokołu OAuth2.</span><span class="sxs-lookup"><span data-stu-id="b8132-196">They are the most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="b8132-197">W wielu wdrożeniach zakłada, że tokeny elementów nośnych są jedynym typem tokeny wystawione.</span><span class="sxs-lookup"><span data-stu-id="b8132-197">Many implementations assume that bearer tokens are the only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="b8132-198">W wierszu polecenia przejdź do **azuread** katalogu.</span><span class="sxs-lookup"><span data-stu-id="b8132-198">From the command line, change directories to the **azuread** directory.</span></span>

<span data-ttu-id="b8132-199">Wpisz następujące polecenie, aby zainstalować Passport.js `passport-azure-ad module`:</span><span class="sxs-lookup"><span data-stu-id="b8132-199">Type the following command to install the Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="b8132-200">Dane wyjściowe polecenia powinny wyglądać podobnie do następujących danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="b8132-200">The output of the command should look similar to the following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="b8132-201">Krok 8: Dodawanie modułów MongoDB do interfejsu API sieci web</span><span class="sxs-lookup"><span data-stu-id="b8132-201">Step 8: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="b8132-202">Korzystamy z bazy danych MongoDB jako naszego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="b8132-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="b8132-203">Z tego powodu należy zainstalować powszechnie używaną wtyczkę Mongoose o nazwie do zarządzania zabezpieczeniami.</span><span class="sxs-lookup"><span data-stu-id="b8132-203">For that reason, we need to install the widely used plug-in called Mongoose to manage models and schemas.</span></span> <span data-ttu-id="b8132-204">Musimy również zainstalować sterownik bazy danych dla bazy danych MongoDB (nazywane również bazy danych MongoDB).</span><span class="sxs-lookup"><span data-stu-id="b8132-204">We also need to install the database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="b8132-205">Krok 9: Instalowanie dodatkowych modułów</span><span class="sxs-lookup"><span data-stu-id="b8132-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="b8132-206">Następnie możemy Zainstaluj pozostałe wymagane moduły.</span><span class="sxs-lookup"><span data-stu-id="b8132-206">Next we install the remaining required modules.</span></span>

1. <span data-ttu-id="b8132-207">W wierszu polecenia przejdź do **azuread** folderu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="b8132-207">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="b8132-208">Wprowadź następujące polecenia, aby zainstalować te moduły w Twojej **node_modules** katalogu:</span><span class="sxs-lookup"><span data-stu-id="b8132-208">Enter the following commands to install these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="b8132-209">Krok 10: Tworzenie server.js własnymi zależnościami</span><span class="sxs-lookup"><span data-stu-id="b8132-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="b8132-210">Pliku server.js zapewnia większość funkcjonalności serwera interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="b8132-210">The server.js file provides most of the functionality for our web API server.</span></span> <span data-ttu-id="b8132-211">Możemy dodać większość naszego kodu do tego pliku.</span><span class="sxs-lookup"><span data-stu-id="b8132-211">We add most of our code to this file.</span></span> <span data-ttu-id="b8132-212">Do celów produkcyjnych zaleca się, że refaktoryzować funkcje na mniejsze pliki, np. odrębne trasy i kontrolery.</span><span class="sxs-lookup"><span data-stu-id="b8132-212">For production purposes, we recommend that you refactor the functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="b8132-213">Z tego pokazu używamy server.js dla tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b8132-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="b8132-214">W wierszu polecenia przejdź do **azuread** folderu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="b8132-214">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="b8132-215">Utwórz `server.js` plik w edytorze Ulubione, a następnie dodaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="b8132-215">Create a `server.js` file in your favorite editor, and then add the following information:</span></span>

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

3. <span data-ttu-id="b8132-216">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="b8132-216">Save the file.</span></span> <span data-ttu-id="b8132-217">Wrócimy do niego później.</span><span class="sxs-lookup"><span data-stu-id="b8132-217">We'll return to it shortly.</span></span>

## <a name="step-11-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="b8132-218">Krok 11: Utwórz plik konfiguracji do przechowywania ustawień usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8132-218">Step 11: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="b8132-219">Ten plik kodu przekazuje parametry konfiguracji z portalu usługi Azure Active Directory do Passport.js.</span><span class="sxs-lookup"><span data-stu-id="b8132-219">This code file passes the configuration parameters from your Azure Active Directory portal to Passport.js.</span></span> <span data-ttu-id="b8132-220">Te wartości konfiguracji są tworzone po dodaniu interfejsu API sieci web w portalu w pierwszej części tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="b8132-220">You created these configuration values when you added the web API to the portal in the first part of the walkthrough.</span></span> <span data-ttu-id="b8132-221">Wyjaśnijmy, co należy umieścić w wartościach tych parametrów, po skopiowaniu kodu.</span><span class="sxs-lookup"><span data-stu-id="b8132-221">We explain what to put in the values of these parameters after you copy the code.</span></span>

1. <span data-ttu-id="b8132-222">W wierszu polecenia przejdź do **azuread** folderu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="b8132-222">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="b8132-223">Utwórz `config.js` plik w edytorze Ulubione, a następnie dodaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="b8132-223">Create a `config.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in to your server unless you use the common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in to your server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes to stderr in Unix.

         };
    ```
3. <span data-ttu-id="b8132-224">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="b8132-224">Save the file.</span></span>

## <a name="step-12-add-configuration-values-to-your-serverjs-file"></a><span data-ttu-id="b8132-225">Krok 12: Wartości konfiguracji należy dodać do pliku server.js</span><span class="sxs-lookup"><span data-stu-id="b8132-225">Step 12: Add configuration values to your server.js file</span></span>
<span data-ttu-id="b8132-226">Należy odczytać wartości z pliku .config, który został utworzony w naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b8132-226">We need to read these values from the .config file that you created across our application.</span></span> <span data-ttu-id="b8132-227">Aby to zrobić, możemy dodać pliku .config jako wymagany zasób w naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b8132-227">To do this, we add the .config file as a required resource in our application.</span></span> <span data-ttu-id="b8132-228">Następnie ustaw zmienne globalne, aby dopasować zmiennych w dokumencie config.js.</span><span class="sxs-lookup"><span data-stu-id="b8132-228">Then we set the global variables to match the variables in the config.js document.</span></span>

1. <span data-ttu-id="b8132-229">W wierszu polecenia przejdź do **azuread** folderu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="b8132-229">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="b8132-230">Otwórz z `server.js` plik w edytorze Ulubione, a następnie dodaj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="b8132-230">Open your `server.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="b8132-231">Następnie dodaj nową sekcję dotyczącą `server.js` następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="b8132-231">Then add a new section to `server.js` with the following code:</span></span>

    ```Javascript
    var options = {
        // The URL of the metadata document for your app. We will put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array to hold logged in users and the current logged in user (owner).
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

      // If the logging level is specified, switch to it.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="b8132-232">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="b8132-232">Save the file.</span></span>

## <a name="step-13-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="b8132-233">Krok 13: Dodaj informacje o modelu bazy danych MongoDB i schematu przy użyciu wtyczki Mongoose</span><span class="sxs-lookup"><span data-stu-id="b8132-233">Step 13: Add The MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="b8132-234">Teraz tego przygotowania jest będzie można uruchomić płatności, ponieważ połączono tych trzech plików w ramach usługi interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b8132-234">Now all this preparation is going to start paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="b8132-235">W ramach tego przewodnika używamy bazy danych MongoDB do przechowywania nasze zadania zgodnie z opisem w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="b8132-235">For this walkthrough, we use MongoDB to store our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="b8132-236">W `config.js` pliku, że utworzyliśmy krok 11, dzwoniliśmy do naszej bazie danych `tasklist`, ponieważ został który testujemy na końcu naszych **mogoose_auth_local** adres URL połączenia.</span><span class="sxs-lookup"><span data-stu-id="b8132-236">In the `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at the end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="b8132-237">Nie trzeba tworzyć wcześniej tej bazy danych w module MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b8132-237">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="b8132-238">Zamiast tego bazy danych MongoDB tworzy to firmie Microsoft przy pierwszym uruchomieniu aplikacji serwera (przy założeniu, że baza danych już nie istnieje).</span><span class="sxs-lookup"><span data-stu-id="b8132-238">Instead, MongoDB creates this for us on the first run of our server application (assuming that the database doesn't already exist).</span></span>

<span data-ttu-id="b8132-239">Teraz, gdy firma Microsoft zostały informację serwera, które firma Microsoft ma być używana baza danych MongoDB, należy napisać dodatkowy kod w celu utworzenia modelu i schematu dla naszego serwera zadań.</span><span class="sxs-lookup"><span data-stu-id="b8132-239">Now that we've told the server which MongoDB database we'd like to use, we need to write some additional code to create the model and schema for our server's tasks.</span></span>

### <a name="discussion-of-the-model"></a><span data-ttu-id="b8132-240">Omówienie modelu</span><span class="sxs-lookup"><span data-stu-id="b8132-240">Discussion of the model</span></span>
<span data-ttu-id="b8132-241">Nasz model schematu jest proste.</span><span class="sxs-lookup"><span data-stu-id="b8132-241">Our schema model is simple.</span></span> <span data-ttu-id="b8132-242">Rozwiń go zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="b8132-242">You expand it as required.</span></span>

<span data-ttu-id="b8132-243">Nazwa: Nazwa osoby, która jest przypisana do zadania.</span><span class="sxs-lookup"><span data-stu-id="b8132-243">NAME: The name of the person who is assigned to the task.</span></span> <span data-ttu-id="b8132-244">A **ciąg**.</span><span class="sxs-lookup"><span data-stu-id="b8132-244">A **String**.</span></span>

<span data-ttu-id="b8132-245">ZADANIE: Samo zadanie.</span><span class="sxs-lookup"><span data-stu-id="b8132-245">TASK: The task itself.</span></span> <span data-ttu-id="b8132-246">A **ciąg**.</span><span class="sxs-lookup"><span data-stu-id="b8132-246">A **String**.</span></span>

<span data-ttu-id="b8132-247">Data: Data przypada zadania.</span><span class="sxs-lookup"><span data-stu-id="b8132-247">DATE: The date that the task is due.</span></span> <span data-ttu-id="b8132-248">A **DATETIME**.</span><span class="sxs-lookup"><span data-stu-id="b8132-248">A **DATETIME**.</span></span>

<span data-ttu-id="b8132-249">UKOŃCZONO: Jeśli zadanie zostało zakończone lub nie.</span><span class="sxs-lookup"><span data-stu-id="b8132-249">COMPLETED: If the task has been completed or not.</span></span> <span data-ttu-id="b8132-250">A **LOGICZNA**.</span><span class="sxs-lookup"><span data-stu-id="b8132-250">A **BOOLEAN**.</span></span>

### <a name="creating-the-schema-in-the-code"></a><span data-ttu-id="b8132-251">Tworzenie schematu w kodzie</span><span class="sxs-lookup"><span data-stu-id="b8132-251">Creating the schema in the code</span></span>
1. <span data-ttu-id="b8132-252">W wierszu polecenia przejdź do **azuread** folderu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="b8132-252">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="b8132-253">Otwórz z `server.js` plik w edytorze Ulubione, a następnie dodaj poniższe informacje poniżej pozycji konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="b8132-253">Open your `server.js` file in your favorite editor, and then add the following information below the configuration entry:</span></span>

    ```Javascript
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema to store our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="b8132-254">Jak stwierdzić, z kodu, utworzymy naszych schematu najpierw.</span><span class="sxs-lookup"><span data-stu-id="b8132-254">As you can tell from the code, we create our schema first.</span></span> <span data-ttu-id="b8132-255">Następnie utwórz obiekt modelu używanego do przechowywania danych w całym kodzie podczas definiujemy naszych **tras**.</span><span class="sxs-lookup"><span data-stu-id="b8132-255">Then we create a model object that we use to store our data throughout the code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="b8132-256">Krok 14: Dodawanie naszych tras do serwera zadań interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="b8132-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="b8132-257">Teraz, gdy mamy model bazy danych do pracy z Dodajmy tras, któremu zamierzamy korzystanie z naszego serwera interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b8132-257">Now that we have a database model to work with, let's add the routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="b8132-258">Informacje o trasach w module Restify</span><span class="sxs-lookup"><span data-stu-id="b8132-258">About routes in Restify</span></span>
<span data-ttu-id="b8132-259">Trasy działają w module Restify tak samo jak w stosie Express.</span><span class="sxs-lookup"><span data-stu-id="b8132-259">Routes work in Restify the same way they do in the Express stack.</span></span> <span data-ttu-id="b8132-260">Trasy są definiowane za pomocą identyfikatora URI, który ma być wywoływany przez aplikacje klienta.</span><span class="sxs-lookup"><span data-stu-id="b8132-260">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="b8132-261">Zazwyczaj należy zdefiniować trasy w oddzielnym pliku.</span><span class="sxs-lookup"><span data-stu-id="b8132-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="b8132-262">W celach naszych testujemy naszych trasy w pliku server.js.</span><span class="sxs-lookup"><span data-stu-id="b8132-262">For our purposes, we put our routes in the server.js file.</span></span> <span data-ttu-id="b8132-263">Firma Microsoft zaleca współczynnika te trasy do ich własnych plików do użytku produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b8132-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="b8132-264">Typowy wzorzec trasy modułu Restify jest następujący:</span><span class="sxs-lookup"><span data-stu-id="b8132-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep the server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="b8132-265">Jest to wzorzec na poziomie najbardziej podstawowym.</span><span class="sxs-lookup"><span data-stu-id="b8132-265">This is the pattern at its most basic level.</span></span> <span data-ttu-id="b8132-266">Moduły restify (i Express) podaj znacznie bardziej złożone funkcje, takie jak Definiowanie typów aplikacji i zapewnianie złożonego routingu przez różne punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="b8132-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="b8132-267">Dla naszych celów możemy utrzymują te trasy proste.</span><span class="sxs-lookup"><span data-stu-id="b8132-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-to-our-server"></a><span data-ttu-id="b8132-268">Dodawanie tras domyślnych do serwera</span><span class="sxs-lookup"><span data-stu-id="b8132-268">Add default routes to our server</span></span>
<span data-ttu-id="b8132-269">Teraz możemy dodać podstawowe trasy CRUD tworzenie, pobieranie, aktualizacji i usunąć.</span><span class="sxs-lookup"><span data-stu-id="b8132-269">We now add the basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="b8132-270">W wierszu polecenia przejdź do **azuread** folderu, jeśli nie masz już istnieje:</span><span class="sxs-lookup"><span data-stu-id="b8132-270">From the command line, change directories to the **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="b8132-271">Otwórz `server.js` plik w edytorze Ulubione, a następnie dodaj poniższe poprzednie wpisy w bazie danych, które należy podjąć następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="b8132-271">Open the `server.js` file in your favorite editor, and then add the following information below the previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it to Mongodb.
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

/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

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
            log.warn(err, "There is no tasks in the database. Did you initialize the database as stated in the README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="b8132-272">Dodawanie obsługi błędów w naszych interfejsów API</span><span class="sxs-lookup"><span data-stu-id="b8132-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back to the client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="b8132-273">Krok 15: Tworzenie serwera</span><span class="sxs-lookup"><span data-stu-id="b8132-273">Step 15: Create your server</span></span>
<span data-ttu-id="b8132-274">Zdefiniowanych naszej bazie danych i naszych tras na miejscu.</span><span class="sxs-lookup"><span data-stu-id="b8132-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="b8132-275">Ostatnim etapem jest dodanie wystąpienia serwera zarządzanego naszych wywołania.</span><span class="sxs-lookup"><span data-stu-id="b8132-275">The last thing to do is add the server instance that manages our calls.</span></span>

<span data-ttu-id="b8132-276">Restify (i Express) można zrobić dużo dostosowania do serwera interfejsu API REST, ale ponownie zamierzamy naszych służącej do najbardziej podstawowa konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="b8132-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going to use the most basic setup for our purposes.</span></span>

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

// Allow five requests per second by IP, and burst to 10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping to REST.
```

## <a name="step-16-add-the-routes-to-the-server-without-authentication-for-now"></a><span data-ttu-id="b8132-277">Krok 16: Dodawanie tras do serwera (bez uwierzytelniania obecnie)</span><span class="sxs-lookup"><span data-stu-id="b8132-277">Step 16: Add the routes to the server (without authentication for now)</span></span>
```Javascript
/// Now the real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In the pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need to maintain session state. You can experiment with removing API protection
/* by removing the passport.authenticate() method as follows:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-the-server-before-adding-oauth-support"></a><span data-ttu-id="b8132-278">Kroku 17: Uruchom serwer (przed dodaniem obsługi protokołu OAuth)</span><span class="sxs-lookup"><span data-stu-id="b8132-278">Step 17: Run the server (before adding OAuth support)</span></span>
<span data-ttu-id="b8132-279">Przetestowanie serwera przed dodamy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b8132-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="b8132-280">Najprostszym sposobem przetestować serwer jest przy użyciu programu curl w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="b8132-280">The easiest way to test your server is by using curl in a command line.</span></span> <span data-ttu-id="b8132-281">Zanim przejdziemy, potrzebujemy narzędzia, która umożliwia firmie Microsoft w celu analizy danych wyjściowych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="b8132-281">Before we do that, we need a utility that allows us to parse output as JSON.</span></span>

1. <span data-ttu-id="b8132-282">Zainstaluj narzędzie JSON następujące (następujące przykłady narzędzie to):</span><span class="sxs-lookup"><span data-stu-id="b8132-282">Install the following JSON tool (all the following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="b8132-283">Narzędzie JSON zostanie zainstalowane globalnie.</span><span class="sxs-lookup"><span data-stu-id="b8132-283">This installs the JSON tool globally.</span></span> <span data-ttu-id="b8132-284">Teraz, gdy firma Microsoft już osiągnąć, który, teraz odtworzyć na serwerze:</span><span class="sxs-lookup"><span data-stu-id="b8132-284">Now that we’ve accomplished that, let’s play with the server:</span></span>

2. <span data-ttu-id="b8132-285">Najpierw upewnij się, że wystąpienie bazy danych mongoDB jest uruchomione:</span><span class="sxs-lookup"><span data-stu-id="b8132-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="b8132-286">Następnie przejdź do katalogu i uruchom curling:</span><span class="sxs-lookup"><span data-stu-id="b8132-286">Then, change to the directory and start curling:</span></span>

    <span data-ttu-id="b8132-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="b8132-287">`$ cd azuread` `$ node server.js`</span></span>

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

4. <span data-ttu-id="b8132-288">Następnie można dodać zadania w ten sposób:</span><span class="sxs-lookup"><span data-stu-id="b8132-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="b8132-289">Odpowiedź powinna wyglądać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b8132-289">The response should be:</span></span>

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
    <span data-ttu-id="b8132-290">I można utworzyć listę zadań dla Brandon w ten sposób:</span><span class="sxs-lookup"><span data-stu-id="b8132-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="b8132-291">Jeśli wszystko to działa, jesteśmy gotowi dodać protokół OAuth do serwera interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b8132-291">If all this works, we're ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="b8132-292">Masz serwera interfejsu API REST z bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b8132-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-to-our-rest-api-server"></a><span data-ttu-id="b8132-293">Krok 18: Dodawanie uwierzytelniania do serwera interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="b8132-293">Step 18: Add authentication to our REST API server</span></span>
<span data-ttu-id="b8132-294">Teraz, gdy będziemy mieć uruchomiony interfejs API REST, Zacznijmy przydatne z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8132-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="b8132-295">W wierszu polecenia przejdź do **azuread** folderu, jeśli nie masz już istnieje.</span><span class="sxs-lookup"><span data-stu-id="b8132-295">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="b8132-296">Korzystanie ze strategii OIDCBearerStrategy dołączonej do modułu passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="b8132-296">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="b8132-297">Do tej pory nawiązaliśmy typowy serwer REST TODO bez żadnej autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="b8132-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="b8132-298">Jest to, gdzie Rozpoczniemy, który zestawienie.</span><span class="sxs-lookup"><span data-stu-id="b8132-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="b8132-299">Najpierw musimy wskazać chcemy korzystać z usługi Passport.</span><span class="sxs-lookup"><span data-stu-id="b8132-299">First, we need to indicate that we want to use Passport.</span></span> <span data-ttu-id="b8132-300">To prawo należy umieścić po konfiguracji serwera:</span><span class="sxs-lookup"><span data-stu-id="b8132-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="b8132-301">Podczas pisania interfejsów API, zaleca się, że możesz zawsze połączyć dane z unikatowym z tokenu, który użytkownik nie może się podszyć.</span><span class="sxs-lookup"><span data-stu-id="b8132-301">When you write APIs, we recommend that you always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="b8132-302">Gdy ten serwer przechowuje elementy przechowuje je na podstawie Identyfikatora obiektu użytkownika w tokenie (wywoływanym za pośrednictwem token.oid), który testujemy w polu "właściciela".</span><span class="sxs-lookup"><span data-stu-id="b8132-302">When this server stores TODO items, it stores them based on the object ID of the user in the token (called through token.oid), which we put in the “owner” field.</span></span> <span data-ttu-id="b8132-303">Daje to pewność, że tylko ten użytkownik ma dostęp do ich TODOs.</span><span class="sxs-lookup"><span data-stu-id="b8132-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="b8132-304">Nie ma ekspozycji w interfejsie API "właściciela", dlatego użytkownikowi zewnętrznemu zażądanie TODOs innych nawet po dokonaniu uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="b8132-304">There is no exposure in the API of “owner,” so an external user can request the TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="b8132-305">Następny Użyjmy strategii elementu nośnego dołączonej `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="b8132-305">Next let’s use the bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="b8132-306">Sprawdź kod teraz i wyjaśniamy pozostałe wkrótce.</span><span class="sxs-lookup"><span data-stu-id="b8132-306">Look at the code for now and we'll explain the rest shortly.</span></span> <span data-ttu-id="b8132-307">Umieścić po wkleić powyżej:</span><span class="sxs-lookup"><span data-stu-id="b8132-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling the OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides the need to manage users and info tokens
    /* with a FindorCreate() method that must be provided by the implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want to do something smarter.
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
            log.info('verifying the user');
            log.info(token, 'was the token retreived');
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

<span data-ttu-id="b8132-308">Usługa Passport używa podobnego wzorca do wszystkich swoich strategii (Twitter, Facebook itd.) zgodne ze wszyscy twórcy kodu strategii.</span><span class="sxs-lookup"><span data-stu-id="b8132-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="b8132-309">Spojrzenie na strategii, zobacz możemy przebiegu funkcję, która ma token i gotowe jako parametry.</span><span class="sxs-lookup"><span data-stu-id="b8132-309">Looking at the strategy, you see we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="b8132-310">Strategia zostanie zwrócona do nas po jego działa.</span><span class="sxs-lookup"><span data-stu-id="b8132-310">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="b8132-311">Po tak, możemy przechować dane użytkownika i Zapisz token, więc nie należy zażądać go ponownie.</span><span class="sxs-lookup"><span data-stu-id="b8132-311">After it does, we store the user and stash the token so we won’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8132-312">Poprzedni kod obejmuje wszystkich użytkowników, która do uwierzytelniania serwera.</span><span class="sxs-lookup"><span data-stu-id="b8132-312">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="b8132-313">Jest to nazywane rejestracji automatycznej.</span><span class="sxs-lookup"><span data-stu-id="b8132-313">This is known as auto-registration.</span></span> <span data-ttu-id="b8132-314">W przypadku serwerów produkcyjnych, firma Microsoft zaleca, aby nie zezwolić każda osoba, która bez konieczności ich przejściu przez proces rejestracji, który podjęciu decyzji o.</span><span class="sxs-lookup"><span data-stu-id="b8132-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="b8132-315">Jest to zwykle wzorzec, które są widoczne w aplikacjach komercyjnych, dzięki której można zarejestrować w usłudze Facebook, ale następnie wyświetli monit o podanie dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="b8132-315">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="b8132-316">Jeśli to nie programu wiersza polecenia, być może wyodrębniono wiadomość e-mail z obiektu tokena, który został zwrócony, a następnie monit użytkownika o podanie dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="b8132-316">If this wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="b8132-317">Ze względu na to, że jest to serwer testowy, informacje zostają po prostu dodane do bazy danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="b8132-317">Because this is a test server, we simply add them to the in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="b8132-318">Ochrona niektórych punktów końcowych</span><span class="sxs-lookup"><span data-stu-id="b8132-318">Protect some endpoints</span></span>
<span data-ttu-id="b8132-319">Ochrona punktów końcowych, określając `passport.authenticate()` wywołania z protokołem, którego chcesz używać.</span><span class="sxs-lookup"><span data-stu-id="b8132-319">You protect endpoints by specifying the `passport.authenticate()` call with the protocol that you want to use.</span></span>

<span data-ttu-id="b8132-320">Aby można było naszego kodu serwera wykonać ciekawsze, umożliwia edytowanie trasy.</span><span class="sxs-lookup"><span data-stu-id="b8132-320">To make our server code do something more interesting, let’s edit the route.</span></span>

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

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="b8132-321">Krok 19: Uruchom ponownie aplikację serwera i upewnij się, że użytkownik jest odrzucany</span><span class="sxs-lookup"><span data-stu-id="b8132-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="b8132-322">Użyjmy `curl` ponownie, aby zobaczyć, czy obecnie istnieją ochrony OAuth2 względem naszego punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="b8132-322">Let's use `curl` again to see if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="b8132-323">Możemy przeprowadzić ten test przed uruchomieniem żadnego z zestawów SDK klientów przed tym punktem końcowym.</span><span class="sxs-lookup"><span data-stu-id="b8132-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="b8132-324">Zwrócone nagłówki powinny wystarczyć Poinformuj nas, jeśli chcemy dół prawidłową ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="b8132-324">The headers that are returned should be enough to tell us if we're going down the right path.</span></span>

1. <span data-ttu-id="b8132-325">Najpierw upewnij się, że wystąpienie bazy danych mongoDB jest uruchomione:</span><span class="sxs-lookup"><span data-stu-id="b8132-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="b8132-326">Następnie przejdź do katalogu i uruchom curling.</span><span class="sxs-lookup"><span data-stu-id="b8132-326">Then, change to the directory and start curling.</span></span>

      <span data-ttu-id="b8132-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="b8132-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="b8132-328">Spróbuj podstawową procedurę testową POST.</span><span class="sxs-lookup"><span data-stu-id="b8132-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="b8132-329">401 jest odpowiedź, którego szukasz tutaj.</span><span class="sxs-lookup"><span data-stu-id="b8132-329">A 401 is the response you are looking for here.</span></span> <span data-ttu-id="b8132-330">Odpowiedź wskazuje, że warstwa oprogramowania Passport podejmuje próbę przekierowania do autoryzowanych punktu końcowego, który ma dokładnie.</span><span class="sxs-lookup"><span data-stu-id="b8132-330">This response indicates that the Passport layer is trying to redirect to the authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8132-331">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b8132-331">Next steps</span></span>
<span data-ttu-id="b8132-332">Został usunięty w zakresie, w jakim można z tego serwera bez użycia klienta zgodne OAuth2.</span><span class="sxs-lookup"><span data-stu-id="b8132-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="b8132-333">Należy przeprowadzić dodatkowe wskazówki.</span><span class="sxs-lookup"><span data-stu-id="b8132-333">You will need to go through an additional walkthrough.</span></span>

<span data-ttu-id="b8132-334">Teraz znasz implementowania interfejsu API REST przy użyciu modułu Restify i protokołu OAuth2.</span><span class="sxs-lookup"><span data-stu-id="b8132-334">You've now learned how to implement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="b8132-335">Masz również wystarczająco kod, aby zachować opracowywania usługi i poznanie kompilacji w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="b8132-335">You also have more than enough code to keep developing your service and learning how to build on this example.</span></span>

<span data-ttu-id="b8132-336">Jeśli interesuje Cię w następnych krokach w podróży ADAL, poniżej przedstawiono niektóre, firma Microsoft zaleca, aby kontynuować pracę z obsługiwanych klientów biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="b8132-336">If you are interested in the next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="b8132-337">Sklonuj dół komputerze dewelopera i skonfigurować zgodnie z opisem w tym przewodnikiem.</span><span class="sxs-lookup"><span data-stu-id="b8132-337">Clone down to your developer machine and configure as described in the walkthrough.</span></span>

[<span data-ttu-id="b8132-338">Biblioteka ADAL dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="b8132-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="b8132-339">ADAL dla systemu Android</span><span class="sxs-lookup"><span data-stu-id="b8132-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
