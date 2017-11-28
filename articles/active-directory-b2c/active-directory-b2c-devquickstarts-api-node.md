---
title: "Usługa Azure AD B2C: zabezpieczanie interfejsu API sieci Web przy użyciu środowiska Node.js | Microsoft Docs"
description: "W jaki sposób toobuild Node.js interfejs API sieci web, która akceptuje tokeny od dzierżawcy usługi B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="cdea8-103">Usługa Azure AD B2C: zabezpieczanie interfejsu API sieci Web przy użyciu środowiska Node.js</span><span class="sxs-lookup"><span data-stu-id="cdea8-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="cdea8-104">Usługa Azure Active Directory (Azure AD) B2C umożliwia zabezpieczanie interfejsu API sieci Web za pomocą tokenów dostępu protokołu OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="cdea8-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="cdea8-105">Tokeny te aplikacjom klienckim korzystających z interfejsu API toohello tooauthenticate usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="cdea8-105">These tokens allow your client apps that use Azure AD B2C tooauthenticate toohello API.</span></span> <span data-ttu-id="cdea8-106">W tym artykule opisano, jak toocreate interfejs API "Lista zadań do wykonania" umożliwiająca użytkownikom tooadd i listy zadań.</span><span class="sxs-lookup"><span data-stu-id="cdea8-106">This article shows you how toocreate a "to-do list" API that allows users tooadd and list tasks.</span></span> <span data-ttu-id="cdea8-107">Interfejs API sieci web Hello jest zabezpieczone przy użyciu usługi Azure AD B2C i tylko umożliwia toomanage uwierzytelnionym użytkownikom ich listy zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="cdea8-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="cdea8-108">Ta próbka została zapisana przy użyciu tooby toobe połączone naszych [B2C systemu iOS Przykładowa aplikacja](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="cdea8-108">This sample was written toobe connected tooby using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="cdea8-109">Najpierw hello bieżący samouczek, a następnie kontynuować pracę z próbką.</span><span class="sxs-lookup"><span data-stu-id="cdea8-109">Do hello current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="cdea8-110">**Passport** to uwierzytelniające oprogramowanie pośredniczące dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="cdea8-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="cdea8-111">Jest to elastyczne i modułowe oprogramowanie, które można dyskretnie zainstalować w dowolnej aplikacji sieci Web opartej na module Express lub Restify.</span><span class="sxs-lookup"><span data-stu-id="cdea8-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="cdea8-112">Kompleksowy zestaw strategii obsługuje uwierzytelnianie przy użyciu m.in. nazwy użytkownika i hasła lub kont w serwisach Facebook i Twitter.</span><span class="sxs-lookup"><span data-stu-id="cdea8-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="cdea8-113">Opracowaliśmy strategię dla usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cdea8-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="cdea8-114">Zainstaluj ten moduł, a następnie dodaj hello Azure AD `passport-azure-ad` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="cdea8-114">You install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="cdea8-115">toodo tej próbki, należy:</span><span class="sxs-lookup"><span data-stu-id="cdea8-115">toodo this sample, you need to:</span></span>

1. <span data-ttu-id="cdea8-116">Zarejestrować aplikację w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cdea8-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="cdea8-117">Konfigurowanie Twojej aplikacji toouse Passport w `azure-ad-passport` wtyczki.</span><span class="sxs-lookup"><span data-stu-id="cdea8-117">Set up your application toouse Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="cdea8-118">Konfigurowanie klienta aplikacji toocall hello "Lista zadań do wykonania" składnika web API.</span><span class="sxs-lookup"><span data-stu-id="cdea8-118">Configure a client application toocall hello "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="cdea8-119">Tworzenie katalogu usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="cdea8-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="cdea8-120">Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.</span><span class="sxs-lookup"><span data-stu-id="cdea8-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="cdea8-121">Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów.</span><span class="sxs-lookup"><span data-stu-id="cdea8-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="cdea8-122">Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.</span><span class="sxs-lookup"><span data-stu-id="cdea8-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="cdea8-123">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="cdea8-123">Create an application</span></span>
<span data-ttu-id="cdea8-124">Następnie należy toocreate aplikację w katalogu B2C, która zapewnia usługi Azure AD pewne informacje, że wymaga ona toosecurely komunikacji z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="cdea8-124">Next, you need toocreate an app in your B2C directory that gives Azure AD some information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="cdea8-125">W takim przypadku zarówno aplikacja kliencka hello, jak i interfejs API sieci web są reprezentowane przez jeden **identyfikator aplikacji**, ponieważ stanowią jedną aplikację logiczną.</span><span class="sxs-lookup"><span data-stu-id="cdea8-125">In this case, both hello client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="cdea8-126">toocreate usługi aplikacji, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="cdea8-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="cdea8-127">Należy pamiętać o wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="cdea8-127">Be sure to:</span></span>

* <span data-ttu-id="cdea8-128">Obejmują **sieci web w sieci web i aplikacji interfejsu api** w aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="cdea8-128">Include a **web app/web api** in hello application</span></span>
* <span data-ttu-id="cdea8-129">Wprowadź `http://localhost/TodoListService` w polu **Adres URL odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="cdea8-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="cdea8-130">Jest hello domyślny adres URL dla tego przykładu kodu.</span><span class="sxs-lookup"><span data-stu-id="cdea8-130">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="cdea8-131">Utwórz **klucz tajny aplikacji** i skopiuj go.</span><span class="sxs-lookup"><span data-stu-id="cdea8-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="cdea8-132">Te dane będą potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="cdea8-132">You need this data later.</span></span> <span data-ttu-id="cdea8-133">Należy pamiętać, że ta wartość musi toobe [XML w znaki ucieczki](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) przed jego użyciem.</span><span class="sxs-lookup"><span data-stu-id="cdea8-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="cdea8-134">Kopiuj hello **identyfikator aplikacji** czyli przypisanej tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdea8-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="cdea8-135">Te dane będą potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="cdea8-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="cdea8-136">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="cdea8-136">Create your policies</span></span>
<span data-ttu-id="cdea8-137">W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="cdea8-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="cdea8-138">Ta aplikacja zawiera dwa elementy dotyczące tożsamości: rejestracja i logowanie.</span><span class="sxs-lookup"><span data-stu-id="cdea8-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="cdea8-139">Należy jedna zasada toocreate każdego typu zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="cdea8-139">You need toocreate one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="cdea8-140">Podczas tworzenia trzech zbiorów zasad należy koniecznie:</span><span class="sxs-lookup"><span data-stu-id="cdea8-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="cdea8-141">Wybierz hello **Nazwa wyświetlana** i inne atrybuty rejestracji w ramach zasad rejestracji.</span><span class="sxs-lookup"><span data-stu-id="cdea8-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="cdea8-142">Wybierz hello **Nazwa wyświetlana** i **obiektu o identyfikatorze** oświadczenia aplikacji we wszystkich zasadach.</span><span class="sxs-lookup"><span data-stu-id="cdea8-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="cdea8-143">Można również wybrać inne oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="cdea8-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="cdea8-144">Skopiuj hello **nazwa** poszczególnych zasad po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="cdea8-144">Copy down hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="cdea8-145">Powinien on mieć prefiks hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="cdea8-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="cdea8-146">Te nazwy zasad będą potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="cdea8-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="cdea8-147">Po utworzeniu trzech zbiorów zasad, wszystko jest gotowe toobuild aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdea8-147">After you have created your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="cdea8-148">toolearn o sposób działania zasad w usłudze Azure AD B2C, rozpoczynać hello [.NET sieci web aplikacji Wprowadzenie — samouczek](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="cdea8-148">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="cdea8-149">Pobierz kod hello</span><span class="sxs-lookup"><span data-stu-id="cdea8-149">Download hello code</span></span>
<span data-ttu-id="cdea8-150">Witaj kodu w tym samouczku [jest przechowywany w serwisie GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="cdea8-150">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="cdea8-151">Przykładowe hello toobuild podczas przejść, możesz [pobrać szkielet projektu jako plik .zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="cdea8-151">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="cdea8-152">Można również sklonować szkielet hello:</span><span class="sxs-lookup"><span data-stu-id="cdea8-152">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="cdea8-153">Aplikacja Hello ukończone jest również [dostępny jako plik zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) lub na powitania `complete` gałęzi hello tego samego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="cdea8-153">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="cdea8-154">Pobieranie środowiska Node.js dla platformy</span><span class="sxs-lookup"><span data-stu-id="cdea8-154">Download Node.js for your platform</span></span>
<span data-ttu-id="cdea8-155">toosuccessfully korzystać z tej próbki, należy działającą instalacją środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="cdea8-155">toosuccessfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="cdea8-156">Zainstaluj środowisko Node.js z witryny [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="cdea8-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="cdea8-157">Instalowanie bazy danych MongoDB dla platformy</span><span class="sxs-lookup"><span data-stu-id="cdea8-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="cdea8-158">toosuccessfully korzystać z tej próbki, należy działającą instalacją bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cdea8-158">toosuccessfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="cdea8-159">Korzystamy z bazy danych MongoDB toomake trwałego interfejsu API REST w wystąpieniach serwera.</span><span class="sxs-lookup"><span data-stu-id="cdea8-159">We use MongoDB toomake your REST API persistent across server instances.</span></span>

<span data-ttu-id="cdea8-160">Zainstaluj bazę danych MongoDB z witryny [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="cdea8-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="cdea8-161">W tym przewodniku zakłada, użyj hello domyślnej instalacji serwera punktów końcowych i bazy danych mongodb, który w czasie hello pisania tego dokumentu jest `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="cdea8-161">This walk-through assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="cdea8-162">Instalowanie modułów Restify hello w interfejsie API sieci web</span><span class="sxs-lookup"><span data-stu-id="cdea8-162">Install hello Restify modules in your web API</span></span>
<span data-ttu-id="cdea8-163">Używamy Restify toobuild interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="cdea8-163">We use Restify toobuild your REST API.</span></span> <span data-ttu-id="cdea8-164">Restify jest minimalną i elastyczną strukturą aplikacji w środowisku Node.js, która pochodzi z modułu Express.</span><span class="sxs-lookup"><span data-stu-id="cdea8-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="cdea8-165">Oferuje rozbudowany zestaw funkcji do tworzenia interfejsów API REST na bazie usługi Connect.</span><span class="sxs-lookup"><span data-stu-id="cdea8-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="cdea8-166">Instalacja modułu Restify</span><span class="sxs-lookup"><span data-stu-id="cdea8-166">Install Restify</span></span>
<span data-ttu-id="cdea8-167">W wierszu polecenia hello, zmień katalog zbyt`azuread`.</span><span class="sxs-lookup"><span data-stu-id="cdea8-167">From hello command line, change your directory too`azuread`.</span></span> <span data-ttu-id="cdea8-168">Jeśli hello `azuread` katalog nie istnieje, utwórz go.</span><span class="sxs-lookup"><span data-stu-id="cdea8-168">If hello `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="cdea8-169">`cd azuread` lub `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="cdea8-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="cdea8-170">Wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="cdea8-170">Enter hello following command:</span></span>

`npm install restify`

<span data-ttu-id="cdea8-171">To polecenie powoduje zainstalowanie modułu Restify.</span><span class="sxs-lookup"><span data-stu-id="cdea8-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="cdea8-172">Czy został wyświetlony komunikat o błędzie?</span><span class="sxs-lookup"><span data-stu-id="cdea8-172">Did you get an error?</span></span>
<span data-ttu-id="cdea8-173">W niektórych systemach operacyjnych, korzystając z `npm`, może zostać wyświetlony błąd hello `Error: EPERM, chmod '/usr/local/bin/..'` i żądania uruchomienia hello konta z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="cdea8-173">In some operating systems, when you use `npm`, you may receive hello error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run hello account as an administrator.</span></span> <span data-ttu-id="cdea8-174">Jeśli wystąpi ten problem, użyj hello `sudo` toorun polecenia `npm` na wyższym poziomie uprawnień.</span><span class="sxs-lookup"><span data-stu-id="cdea8-174">If this problem occurs, use hello `sudo` command toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="cdea8-175">Czy został wyświetlony błąd narzędzia DTrace?</span><span class="sxs-lookup"><span data-stu-id="cdea8-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="cdea8-176">Po zainstalowaniu modułu Restify może zostać wyświetlony następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="cdea8-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="cdea8-177">Moduł Restify zapewnia zaawansowany mechanizm śledzenia wywołań REST przy użyciu narzędzia DTrace.</span><span class="sxs-lookup"><span data-stu-id="cdea8-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="cdea8-178">Jednak w wielu systemach operacyjnych narzędzie DTrace jest niedostępne.</span><span class="sxs-lookup"><span data-stu-id="cdea8-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="cdea8-179">Można te błędy bezpiecznie zignorować.</span><span class="sxs-lookup"><span data-stu-id="cdea8-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="cdea8-180">Hello dane wyjściowe polecenia hello powinna wyglądać podobnie tekst toothis:</span><span class="sxs-lookup"><span data-stu-id="cdea8-180">hello output of hello command should appear similar toothis text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="cdea8-181">Instalacja oprogramowania Passport w interfejsie API sieci Web</span><span class="sxs-lookup"><span data-stu-id="cdea8-181">Install Passport in your web API</span></span>
<span data-ttu-id="cdea8-182">W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje.</span><span class="sxs-lookup"><span data-stu-id="cdea8-182">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="cdea8-183">Instalacja oprogramowania Passport przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="cdea8-183">Install Passport using hello following command:</span></span>

`npm install passport`

<span data-ttu-id="cdea8-184">dane wyjściowe polecenia hello Hello powinny być podobne toothis tekst:</span><span class="sxs-lookup"><span data-stu-id="cdea8-184">hello output of hello command should be similar toothis text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a><span data-ttu-id="cdea8-185">Dodawanie biblioteki passport-azuread tooyour — interfejs API sieci web</span><span class="sxs-lookup"><span data-stu-id="cdea8-185">Add passport-azuread tooyour web API</span></span>
<span data-ttu-id="cdea8-186">Następnie dodaj strategię OAuth hello przy użyciu `passport-azuread`, zestawu strategii łączących usługę Azure AD z usługą Passport.</span><span class="sxs-lookup"><span data-stu-id="cdea8-186">Next, add hello OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="cdea8-187">Użyj tej strategii do tokenów elementów nośnych w próbce interfejsu API REST hello.</span><span class="sxs-lookup"><span data-stu-id="cdea8-187">Use this strategy for bearer tokens in hello REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="cdea8-188">Chociaż protokół OAuth2 zapewnia platformę umożliwiającą wystawienie dowolnego znanego typu tokenu, tylko niektóre typy tokenów weszły do powszechnego użycia.</span><span class="sxs-lookup"><span data-stu-id="cdea8-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="cdea8-189">tokeny Hello punkty końcowe są tokenami elementów nośnych.</span><span class="sxs-lookup"><span data-stu-id="cdea8-189">hello tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="cdea8-190">Te typy tokenów są hello najczęściej wystawiony protokołu oauth2.</span><span class="sxs-lookup"><span data-stu-id="cdea8-190">These types of tokens are hello most widely issued in OAuth2.</span></span> <span data-ttu-id="cdea8-191">W wielu wdrożeniach zakłada, że tokeny elementów nośnych są jedynym typem wystawianych tokenów hello.</span><span class="sxs-lookup"><span data-stu-id="cdea8-191">Many implementations assume that bearer tokens are hello only type of token issued.</span></span>
>
>

<span data-ttu-id="cdea8-192">W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje.</span><span class="sxs-lookup"><span data-stu-id="cdea8-192">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="cdea8-193">Zainstaluj hello Passport `passport-azure-ad` modułu przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="cdea8-193">Install hello Passport `passport-azure-ad` module using hello following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="cdea8-194">dane wyjściowe polecenia hello Hello powinny być podobne toothis tekst:</span><span class="sxs-lookup"><span data-stu-id="cdea8-194">hello output of hello command should be similar toothis text:</span></span>

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="cdea8-195">Dodawanie bazy danych MongoDB modułów tooyour — interfejs API sieci web</span><span class="sxs-lookup"><span data-stu-id="cdea8-195">Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="cdea8-196">W tej próbce moduł MongoDB będzie używany jako magazyn danych.</span><span class="sxs-lookup"><span data-stu-id="cdea8-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="cdea8-197">W tym celu zainstaluj oprogramowanie Mongoose — powszechnie używaną wtyczkę do zarządzania modelami i schematami.</span><span class="sxs-lookup"><span data-stu-id="cdea8-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="cdea8-198">Instalowanie dodatkowych modułów</span><span class="sxs-lookup"><span data-stu-id="cdea8-198">Install additional modules</span></span>
<span data-ttu-id="cdea8-199">Następnie zainstaluj pozostałe wymagane moduły hello.</span><span class="sxs-lookup"><span data-stu-id="cdea8-199">Next, install hello remaining required modules.</span></span>

<span data-ttu-id="cdea8-200">W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:</span><span class="sxs-lookup"><span data-stu-id="cdea8-200">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="cdea8-201">Instalowanie modułów hello w Twojej `node_modules` katalogu:</span><span class="sxs-lookup"><span data-stu-id="cdea8-201">Install hello modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="cdea8-202">Tworzenie pliku server.js z własnymi zależnościami</span><span class="sxs-lookup"><span data-stu-id="cdea8-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="cdea8-203">Witaj `server.js` plik zawiera większość hello hello funkcji serwera interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cdea8-203">hello `server.js` file provides hello majority of hello functionality for your Web API server.</span></span>

<span data-ttu-id="cdea8-204">W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:</span><span class="sxs-lookup"><span data-stu-id="cdea8-204">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="cdea8-205">Utwórz plik `server.js` w edytorze.</span><span class="sxs-lookup"><span data-stu-id="cdea8-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="cdea8-206">Dodaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="cdea8-206">Add hello following information:</span></span>

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

<span data-ttu-id="cdea8-207">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="cdea8-207">Save hello file.</span></span> <span data-ttu-id="cdea8-208">Tooit wróć później.</span><span class="sxs-lookup"><span data-stu-id="cdea8-208">You return tooit later.</span></span>

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="cdea8-209">Utwórz toostore pliku config.js ustawienia usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cdea8-209">Create a config.js file toostore your Azure AD settings</span></span>
<span data-ttu-id="cdea8-210">Ten plik kodu przekazuje parametry konfiguracji hello z toohello z portalu Azure AD `Passport.js` pliku.</span><span class="sxs-lookup"><span data-stu-id="cdea8-210">This code file passes hello configuration parameters from your Azure AD Portal toohello `Passport.js` file.</span></span> <span data-ttu-id="cdea8-211">Te wartości konfiguracji są tworzone po dodaniu portalu toohello interfejsu API sieci web hello w pierwszej części przewodnika hello hello.</span><span class="sxs-lookup"><span data-stu-id="cdea8-211">You created these configuration values when you added hello web API toohello portal in hello first part of hello walk-through.</span></span> <span data-ttu-id="cdea8-212">Po skopiowaniu kodu hello prezentujemy zasady jakie tooput hello wartości tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="cdea8-212">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

<span data-ttu-id="cdea8-213">W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:</span><span class="sxs-lookup"><span data-stu-id="cdea8-213">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="cdea8-214">Utwórz plik `config.js` w edytorze.</span><span class="sxs-lookup"><span data-stu-id="cdea8-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="cdea8-215">Dodaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="cdea8-215">Add hello following information:</span></span>

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="cdea8-216">Wymagane wartości</span><span class="sxs-lookup"><span data-stu-id="cdea8-216">Required values</span></span>
<span data-ttu-id="cdea8-217">`clientID`: hello identyfikator klienta aplikacji interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cdea8-217">`clientID`: hello client ID of your Web API application.</span></span>

<span data-ttu-id="cdea8-218">`IdentityMetadata`: To jest where `passport-azure-ad` sprawdza dane konfiguracyjne dla hello dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="cdea8-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for hello identity provider.</span></span> <span data-ttu-id="cdea8-219">Wyszukuje również toovalidate klucze hello hello tokenów sieci web JSON.</span><span class="sxs-lookup"><span data-stu-id="cdea8-219">It also looks for hello keys toovalidate hello JSON web tokens.</span></span>

<span data-ttu-id="cdea8-220">`audience`: hello identyfikator uniform resource identifier (URI) z portalu hello, który identyfikuje wywoływania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdea8-220">`audience`: hello uniform resource identifier (URI) from hello portal that identifies your calling application.</span></span>

<span data-ttu-id="cdea8-221">`tenantName`: nazwa dzierżawy (na przykład **contoso.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="cdea8-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="cdea8-222">`policyName`: hello zasady, które chcesz toovalidate hello tokenów przychodzących tooyour serwera.</span><span class="sxs-lookup"><span data-stu-id="cdea8-222">`policyName`: hello policy that you want toovalidate hello tokens coming in tooyour server.</span></span> <span data-ttu-id="cdea8-223">Ta zasada powinna być hello te same zasady używanego na powitania klienta aplikacji do logowania.</span><span class="sxs-lookup"><span data-stu-id="cdea8-223">This policy should be hello same policy that you use on hello client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="cdea8-224">Na razie użyj hello takie same zasady przez klienta i serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cdea8-224">For now, use hello same policies across both client and server setup.</span></span> <span data-ttu-id="cdea8-225">Jeśli zostały już wykonane w ramach tego przewodnika i utworzyć zasady, nie potrzebujesz toodo więc ponownie.</span><span class="sxs-lookup"><span data-stu-id="cdea8-225">If you have already completed a walk-through and created these policies, you don't need toodo so again.</span></span> <span data-ttu-id="cdea8-226">Ponieważ ukończono przewodnik hello, nie ma potrzeby tooset się nowych zasad dla przewodników klienta na powitania lokacji.</span><span class="sxs-lookup"><span data-stu-id="cdea8-226">Because you completed hello walk-through, you shouldn't need tooset up new policies for client walk-throughs on hello site.</span></span>
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a><span data-ttu-id="cdea8-227">Dodawanie pliku server.js tooyour konfiguracji</span><span class="sxs-lookup"><span data-stu-id="cdea8-227">Add configuration tooyour server.js file</span></span>
<span data-ttu-id="cdea8-228">wartości hello tooread z hello `config.js` utworzonego pliku, Dodaj hello `.config` pliku jako wymagany zasób w aplikacji, a następnie ustaw toothose zmienne globalne hello w hello `config.js` dokumentu.</span><span class="sxs-lookup"><span data-stu-id="cdea8-228">tooread hello values from hello `config.js` file you created, add hello `.config` file as a required resource in your application, and then set hello global variables toothose in hello `config.js` document.</span></span>

<span data-ttu-id="cdea8-229">W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:</span><span class="sxs-lookup"><span data-stu-id="cdea8-229">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="cdea8-230">Otwórz hello `server.js` plik w edytorze.</span><span class="sxs-lookup"><span data-stu-id="cdea8-230">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="cdea8-231">Dodaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="cdea8-231">Add hello following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="cdea8-232">Dodaj nową sekcję zbyt`server.js` zawierającą hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="cdea8-232">Add a new section too`server.js` that includes hello following code:</span></span>

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="cdea8-233">Następnie możemy dodać niektóre symbole zastępcze dla użytkowników hello otrzymane od naszych wywoływania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cdea8-233">Next, let's add some placeholders for hello users we receive from our calling applications.</span></span>

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="cdea8-234">Utwórzmy także naszego rejestratora.</span><span class="sxs-lookup"><span data-stu-id="cdea8-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="cdea8-235">Dodawanie informacji modelu i schemacie modułu MongoDB hello przy użyciu wtyczki Mongoose</span><span class="sxs-lookup"><span data-stu-id="cdea8-235">Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="cdea8-236">Witaj wcześniejsze przygotowania pozwoli zaoszczędzić czas podczas łączenia tych trzech plików w usłudze interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="cdea8-236">hello earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="cdea8-237">Na potrzeby tego przewodnika Użyj bazy danych MongoDB toostore zadań, zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="cdea8-237">For this walk-through, use MongoDB toostore your tasks, as discussed earlier.</span></span>

<span data-ttu-id="cdea8-238">W hello `config.js` plik, nazwę bazy danych **tasklist**.</span><span class="sxs-lookup"><span data-stu-id="cdea8-238">In hello `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="cdea8-239">Ta nazwa została ona również umieszczona na końcu hello hello `mongoose_auth_local` adres URL połączenia.</span><span class="sxs-lookup"><span data-stu-id="cdea8-239">That name was also what you put at hello end of hello `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="cdea8-240">Nie trzeba toocreate tej bazy danych wcześniej w module MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cdea8-240">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="cdea8-241">Tworzy hello bazy danych dla Ciebie na powitania pierwszym uruchomieniu aplikacji serwera.</span><span class="sxs-lookup"><span data-stu-id="cdea8-241">It creates hello database for you on hello first run of your server application.</span></span>

<span data-ttu-id="cdea8-242">Po przekazaniu powitania serwera które toouse bazy danych MongoDB należy toowrite niektóre dodatkowy kod toocreate hello modelu i schematu dla zadań serwera.</span><span class="sxs-lookup"><span data-stu-id="cdea8-242">After you tell hello server which MongoDB database toouse, you need toowrite some additional code toocreate hello model and schema for your server tasks.</span></span>

### <a name="expand-hello-model"></a><span data-ttu-id="cdea8-243">Rozwiń węzeł hello modelu</span><span class="sxs-lookup"><span data-stu-id="cdea8-243">Expand hello model</span></span>
<span data-ttu-id="cdea8-244">Ten model schematu jest prosty.</span><span class="sxs-lookup"><span data-stu-id="cdea8-244">This schema model is simple.</span></span> <span data-ttu-id="cdea8-245">Można go rozszerzyć w zależności od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="cdea8-245">You can expand it as required.</span></span>

<span data-ttu-id="cdea8-246">`owner`: Kto jest przydzielony toohello zadań.</span><span class="sxs-lookup"><span data-stu-id="cdea8-246">`owner`: Who is assigned toohello task.</span></span> <span data-ttu-id="cdea8-247">Ten obiekt to **ciąg**.</span><span class="sxs-lookup"><span data-stu-id="cdea8-247">This object is a **string**.</span></span>  

<span data-ttu-id="cdea8-248">`Text`: samo zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="cdea8-248">`Text`: hello task itself.</span></span> <span data-ttu-id="cdea8-249">Ten obiekt to **ciąg**.</span><span class="sxs-lookup"><span data-stu-id="cdea8-249">This object is a **string**.</span></span>

<span data-ttu-id="cdea8-250">`date`: hello Data przypada hello zadania.</span><span class="sxs-lookup"><span data-stu-id="cdea8-250">`date`: hello date that hello task is due.</span></span> <span data-ttu-id="cdea8-251">Ten obiekt to **data i godzina**.</span><span class="sxs-lookup"><span data-stu-id="cdea8-251">This object is a **datetime**.</span></span>

<span data-ttu-id="cdea8-252">`completed`: Jeśli hello zadanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="cdea8-252">`completed`: If hello task is complete.</span></span> <span data-ttu-id="cdea8-253">Ten obiekt to **dane logiczne**.</span><span class="sxs-lookup"><span data-stu-id="cdea8-253">This object is a **Boolean**.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="cdea8-254">Tworzenie schematu hello w kodzie hello</span><span class="sxs-lookup"><span data-stu-id="cdea8-254">Create hello schema in hello code</span></span>
<span data-ttu-id="cdea8-255">W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:</span><span class="sxs-lookup"><span data-stu-id="cdea8-255">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="cdea8-256">Otwórz hello `server.js` plik w edytorze.</span><span class="sxs-lookup"><span data-stu-id="cdea8-256">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="cdea8-257">Dodaj następujące informacje poniżej pozycji konfiguracji hello hello:</span><span class="sxs-lookup"><span data-stu-id="cdea8-257">Add hello following information below hello configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="cdea8-258">Najpierw utworzyć hello schematu, a następnie utwórz obiekt modelu używanego danych w całym hello kodu podczas definiowania toostore Twojego **tras**.</span><span class="sxs-lookup"><span data-stu-id="cdea8-258">You first create hello schema, and then you create a model object that you use toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="cdea8-259">Dodawanie tras do serwera zadań interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="cdea8-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="cdea8-260">Teraz, gdy masz toowork modelu bazy danych, z Dodaj hello trasy, używanego serwera interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="cdea8-260">Now that you have a database model toowork with, add hello routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="cdea8-261">Informacje o trasach w module Restify</span><span class="sxs-lookup"><span data-stu-id="cdea8-261">About routes in Restify</span></span>
<span data-ttu-id="cdea8-262">Trasy działają w module Restify w hello sam sposób, jak przy korzystaniu z hello Express stosu.</span><span class="sxs-lookup"><span data-stu-id="cdea8-262">Routes work in Restify in hello same way that they work when they use hello Express stack.</span></span> <span data-ttu-id="cdea8-263">Trasy są definiowane za pomocą hello spodziewać się powitania klienta aplikacji toocall identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="cdea8-263">You define routes by using hello URI that you expect hello client applications toocall.</span></span>

<span data-ttu-id="cdea8-264">Oto typowy wzorzec trasy modułu Restify:</span><span class="sxs-lookup"><span data-stu-id="cdea8-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="cdea8-265">Moduły Restify i Express mogą zapewniać o wiele bardziej złożone funkcje, takie jak definiowanie typów aplikacji i wykonywanie złożonego routingu przez różne punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="cdea8-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="cdea8-266">Do celów tego samouczka hello możemy proste trasy.</span><span class="sxs-lookup"><span data-stu-id="cdea8-266">For hello purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="cdea8-267">Dodaj serwer tooyour trasy domyślnej</span><span class="sxs-lookup"><span data-stu-id="cdea8-267">Add default routes tooyour server</span></span>
<span data-ttu-id="cdea8-268">Teraz Dodaj hello podstawowe trasy CRUD **utworzyć** i **listy** na interfejsie API REST.</span><span class="sxs-lookup"><span data-stu-id="cdea8-268">You now add hello basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="cdea8-269">Innych tras znajdują się w hello `complete` gałęzi hello próbki.</span><span class="sxs-lookup"><span data-stu-id="cdea8-269">Other routes can be found in hello `complete` branch of hello sample.</span></span>

<span data-ttu-id="cdea8-270">W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:</span><span class="sxs-lookup"><span data-stu-id="cdea8-270">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="cdea8-271">Otwórz hello `server.js` plik w edytorze.</span><span class="sxs-lookup"><span data-stu-id="cdea8-271">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="cdea8-272">Poniżej wpisy w bazie danych hello wprowadzone powyżej Dodaj hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="cdea8-272">Below hello database entries you made above add hello following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="cdea8-273">Dodawanie obsługi błędów dla tras hello</span><span class="sxs-lookup"><span data-stu-id="cdea8-273">Add error handling for hello routes</span></span>
<span data-ttu-id="cdea8-274">Dodać niektóre Obsługa błędów i może komunikować się wszelkie problemy wystąpią klienta toohello Wstecz w taki sposób, który może zrozumieć.</span><span class="sxs-lookup"><span data-stu-id="cdea8-274">Add some error handling so that you can communicate any problems you encounter back toohello client in a way that it can understand.</span></span>

<span data-ttu-id="cdea8-275">Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="cdea8-275">Add hello following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a><span data-ttu-id="cdea8-276">Tworzenie serwera</span><span class="sxs-lookup"><span data-stu-id="cdea8-276">Create your server</span></span>
<span data-ttu-id="cdea8-277">Baza danych została zdefiniowana, a trasy — określone.</span><span class="sxs-lookup"><span data-stu-id="cdea8-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="cdea8-278">ostatnim zadaniem Hello toodo możesz jest wystąpienie serwera hello tooadd, która zarządza wywołania.</span><span class="sxs-lookup"><span data-stu-id="cdea8-278">hello last thing for you toodo is tooadd hello server instance that manages your calls.</span></span>

<span data-ttu-id="cdea8-279">Moduły restify i Express oferują możliwość głębokiego dostosowania do serwera interfejsu API REST, ale używana hello najbardziej podstawowa konfiguracja tutaj.</span><span class="sxs-lookup"><span data-stu-id="cdea8-279">Restify and Express provide deep customization for a REST API server, but we use hello most basic setup here.</span></span>

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a><span data-ttu-id="cdea8-280">Dodaj serwer toohello trasy hello (bez uwierzytelniania)</span><span class="sxs-lookup"><span data-stu-id="cdea8-280">Add hello routes toohello server (without authentication)</span></span>
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="cdea8-281">Dodawanie serwera interfejsu API REST tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="cdea8-281">Add authentication tooyour REST API server</span></span>
<span data-ttu-id="cdea8-282">Działający serwer interfejsu API REST można wykorzystać do celów usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cdea8-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="cdea8-283">W wierszu polecenia hello, zmień katalog zbyt`azuread`, jeśli nie jest już istnieje:</span><span class="sxs-lookup"><span data-stu-id="cdea8-283">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="cdea8-284">Użyj hello OIDCBearerStrategy dołączonej usługi passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="cdea8-284">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="cdea8-285">Podczas pisania interfejsów API, należy zawsze połączyć toosomething danych hello unikatowy z tokenu hello hello użytkownika nie może się podszyć.</span><span class="sxs-lookup"><span data-stu-id="cdea8-285">When you write APIs, you should always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="cdea8-286">Gdy serwer hello przechowuje elementy, tak więc na powitania podstawie **oid** użytkownika hello w hello tokenie (wywoływanym za pośrednictwem token.oid), który znajduje się w polu "hello"właściciela".</span><span class="sxs-lookup"><span data-stu-id="cdea8-286">When hello server stores ToDo items, it does so based on hello **oid** of hello user in hello token (called through token.oid), which goes in hello “owner” field.</span></span> <span data-ttu-id="cdea8-287">Ta wartość zapewnia, że tylko ten użytkownik może uzyskać dostęp do własnych zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="cdea8-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="cdea8-288">Nie ma ekspozycji w hello interfejsu API "właściciela", dlatego użytkownikowi zewnętrznemu zażądanie innych zadań do wykonania nawet po dokonaniu uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="cdea8-288">There is no exposure in hello API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="cdea8-289">Następnie użyj strategii elementu nośnego hello dołączoną `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="cdea8-289">Next, use hello bearer strategy that comes with `passport-azure-ad`.</span></span>

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

<span data-ttu-id="cdea8-290">Passport używa hello wzorca takie same dla wszystkich swoich strategii.</span><span class="sxs-lookup"><span data-stu-id="cdea8-290">Passport uses hello same pattern for all its strategies.</span></span> <span data-ttu-id="cdea8-291">Zawiera on polecenie `function()` z parametrami `token` i `done`.</span><span class="sxs-lookup"><span data-stu-id="cdea8-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="cdea8-292">Strategia Hello wróci tooyou po wykonaniu całego zadania.</span><span class="sxs-lookup"><span data-stu-id="cdea8-292">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="cdea8-293">A następnie należy przechowywać hello użytkownika i zapisać hello token, tak aby nie trzeba tooask go ponownie.</span><span class="sxs-lookup"><span data-stu-id="cdea8-293">You should then store hello user and save hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cdea8-294">Powyższy kod Hello obejmuje żadnych użytkowników, którzy tooauthenticate tooyour serwera.</span><span class="sxs-lookup"><span data-stu-id="cdea8-294">hello code above takes any user who happens tooauthenticate tooyour server.</span></span> <span data-ttu-id="cdea8-295">Ten proces jest nazywany autorejestracją.</span><span class="sxs-lookup"><span data-stu-id="cdea8-295">This process is known as autoregistration.</span></span> <span data-ttu-id="cdea8-296">W przypadku serwerów produkcyjnych nie umożliwiają w interfejsie API hello żadnych użytkowników dostęp bez konieczności ich przechodzą przez proces rejestracji.</span><span class="sxs-lookup"><span data-stu-id="cdea8-296">In production servers, don't let in any users access hello API without first having them go through a registration process.</span></span> <span data-ttu-id="cdea8-297">Ten proces jest zwykle wzorzec hello, które są widoczne w aplikacjach komercyjnych, który pozwala tooregister za pomocą usługi Facebook, ale następnie poprosić toofill dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="cdea8-297">This process is usually hello pattern you see in consumer apps that allow you tooregister by using Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="cdea8-298">Jeśli ten program nie programu wiersza polecenia, być może wyodrębniono hello wiadomości e-mail z hello obiektu tokena, który został zwrócony, a następnie zadawane toofill użytkowników dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="cdea8-298">If this program wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked users toofill out additional information.</span></span> <span data-ttu-id="cdea8-299">Ponieważ to jest przykład możemy dodać je tooan bazy danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="cdea8-299">Because this is a sample, we add them tooan in-memory database.</span></span>
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a><span data-ttu-id="cdea8-300">Uruchom tooverify aplikacji z serwera jego odrzuca możesz</span><span class="sxs-lookup"><span data-stu-id="cdea8-300">Run your server application tooverify that it rejects you</span></span>
<span data-ttu-id="cdea8-301">Można użyć `curl` toosee, jeśli masz teraz OAuth2 ochrony punktów końcowych przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="cdea8-301">You can use `curl` toosee if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="cdea8-302">Hello zwrócone nagłówki powinny być za mało tootell że znajdują się na powitania prawidłową ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="cdea8-302">hello headers returned should be enough tootell you that you are on hello right path.</span></span>

<span data-ttu-id="cdea8-303">Upewnij się, że wystąpienie bazy danych MongoDB zostało uruchomione:</span><span class="sxs-lookup"><span data-stu-id="cdea8-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="cdea8-304">Zmień katalog toohello i hello uruchomienia serwera:</span><span class="sxs-lookup"><span data-stu-id="cdea8-304">Change toohello directory and run hello server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="cdea8-305">W nowym oknie terminala uruchom polecenie `curl`</span><span class="sxs-lookup"><span data-stu-id="cdea8-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="cdea8-306">Wypróbuj podstawową procedurę testową POST:</span><span class="sxs-lookup"><span data-stu-id="cdea8-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="cdea8-307">Odpowiedzi na powitania jest błąd 401.</span><span class="sxs-lookup"><span data-stu-id="cdea8-307">A 401 error is hello response you want.</span></span> <span data-ttu-id="cdea8-308">Wskazuje, że warstwa oprogramowania Passport hello próbuje tooredirect toohello punktu końcowego autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="cdea8-308">It indicates that hello Passport layer is trying tooredirect toohello authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="cdea8-309">Efektem jest usługa interfejsu API REST korzystająca z protokołu OAuth2</span><span class="sxs-lookup"><span data-stu-id="cdea8-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="cdea8-310">Udało Ci się wdrożyć interfejs API REST przy użyciu modułu Restify i strategii OAuth!</span><span class="sxs-lookup"><span data-stu-id="cdea8-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="cdea8-311">Teraz masz kod wystarczające, dzięki czemu można kontynuować toodevelop usługi i kompilacji w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="cdea8-311">You now have sufficient code so that you can continue toodevelop your service and build on this example.</span></span> <span data-ttu-id="cdea8-312">W przypadku tego serwera nie można wykonać żadnych dalszych czynności bez użycia klienta zgodnego z protokołem OAuth2.</span><span class="sxs-lookup"><span data-stu-id="cdea8-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="cdea8-313">Dla tego kroku dalej używać jest dodatkowy przewodnik, takich jak naszym [połączyć tooa interfejsu API sieci web przy użyciu systemu iOS z usługi B2C](active-directory-b2c-devquickstarts-ios.md) wskazówki.</span><span class="sxs-lookup"><span data-stu-id="cdea8-313">For that next step use an additional walk-through like our [Connect tooa web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdea8-314">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cdea8-314">Next steps</span></span>
<span data-ttu-id="cdea8-315">Możesz teraz przejść toomore zaawansowanych tematów, takich jak:</span><span class="sxs-lookup"><span data-stu-id="cdea8-315">You can now move toomore advanced topics, such as:</span></span>

[<span data-ttu-id="cdea8-316">Połącz tooa interfejsu API sieci web przy użyciu systemu iOS z usługi B2C</span><span class="sxs-lookup"><span data-stu-id="cdea8-316">Connect tooa web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
