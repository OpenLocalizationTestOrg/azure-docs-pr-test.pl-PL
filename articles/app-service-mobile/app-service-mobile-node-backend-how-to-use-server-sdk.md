---
title: "toowork aaaHow z serwera wewnętrznej bazy danych hello Node.js SDK for Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toowork z hello serwera zaplecza Node.js SDK dla usługi Azure App Service Mobile Apps."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="a5e12-103">Jak toouse hello Azure Mobile Apps Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="a5e12-103">How toouse hello Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="a5e12-104">Ten artykuł zawiera szczegółowe informacje i przykłady przedstawiający sposób toowork z zaplecza Node.js w usłudze Azure App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="a5e12-104">This article provides detailed information and examples showing how toowork with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="a5e12-105"><a name="Introduction"></a>Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="a5e12-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="a5e12-106">Usługa Azure App Service Mobile Apps udostępnia hello możliwości tooadd mobile zoptymalizowane danych aplikacji sieci web tooa interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a5e12-106">Azure App Service Mobile Apps provides hello capability tooadd a mobile-optimized data access Web API tooa web application.</span></span>  <span data-ttu-id="a5e12-107">Witaj zestaw SDK aplikacji mobilnych usługi aplikacji Azure jest dostępna dla aplikacji sieci web ASP.NET i Node.js.</span><span class="sxs-lookup"><span data-stu-id="a5e12-107">hello Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="a5e12-108">Witaj SDK udostępnia hello następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="a5e12-108">hello SDK provides hello following operations:</span></span>

* <span data-ttu-id="a5e12-109">Operacje tabeli (Odczyt, Insert, Update, Delete) dla dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="a5e12-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="a5e12-110">Operacje niestandardowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a5e12-110">Custom API operations</span></span>

<span data-ttu-id="a5e12-111">Obie operacje zapewnienia uwierzytelniania przez wszystkich dostawców tożsamości dozwolone w usłudze Azure App Service, w tym dostawców tożsamości społecznościowych, takich jak Facebook, Twitter, Google i Microsoft, jak również usługi Azure Active Directory dla tożsamości organizacji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="a5e12-112">Można znaleźć przykłady dla każdego przypadku użycia w hello [katalogu przykładów w witrynie GitHub].</span><span class="sxs-lookup"><span data-stu-id="a5e12-112">You can find samples for each use case in hello [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="a5e12-113">Obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="a5e12-113">Supported Platforms</span></span>
<span data-ttu-id="a5e12-114">Witaj zestaw SDK usługi Azure Mobile Apps węzła obsługuje powitalne wersji LTS bieżącego węzła i nowszych.</span><span class="sxs-lookup"><span data-stu-id="a5e12-114">hello Azure Mobile Apps Node SDK supports hello current LTS release of Node and later.</span></span>  <span data-ttu-id="a5e12-115">Począwszy od zapisu, najnowsza wersja LTS hello jest v4.5.0 węzła.</span><span class="sxs-lookup"><span data-stu-id="a5e12-115">As of writing, hello latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="a5e12-116">Inne wersje węzeł może działać, ale nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a5e12-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="a5e12-117">zestaw SDK usługi Azure Mobile Apps węzła Hello obsługuje dwa sterowniki bazy danych — hello mssql węzła sterownik obsługuje SQL Azure i lokalnego wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a5e12-117">hello Azure Mobile Apps Node SDK supports two database drivers - hello node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="a5e12-118">Sterownik sqlite3 Hello obsługuje bazy danych SQLite na tylko jedno wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="a5e12-118">hello sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="a5e12-119"><a name="howto-cmdline-basicapp"></a>Porady: tworzenie przy użyciu wiersza polecenia hello zaplecza Node.js podstawowe</span><span class="sxs-lookup"><span data-stu-id="a5e12-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using hello Command Line</span></span>
<span data-ttu-id="a5e12-120">Jako aplikacja ExpressJS rozpoczyna się co wewnętrznej bazy danych usługi Azure App Service Mobile aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="a5e12-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="a5e12-121">ExpressJS jest hello najpopularniejszych platforma sieci web usługi dostępne dla środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="a5e12-121">ExpressJS is hello most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="a5e12-122">Można utworzyć basic [Express] aplikacji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a5e12-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="a5e12-123">Polecenie lub oknie programu PowerShell należy utworzyć katalog w projekcie.</span><span class="sxs-lookup"><span data-stu-id="a5e12-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="a5e12-124">Uruchom npm init tooinitialize hello pakietu struktury.</span><span class="sxs-lookup"><span data-stu-id="a5e12-124">Run npm init tooinitialize hello package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="a5e12-125">polecenie init npm Hello zapyta zestaw pytań tooinitialize hello projektu.</span><span class="sxs-lookup"><span data-stu-id="a5e12-125">hello npm init command asks a set of questions tooinitialize hello project.</span></span>  <span data-ttu-id="a5e12-126">Zobacz hello przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="a5e12-126">See hello example output:</span></span>

    ![Witaj npm init w danych wyjściowych][0]
3. <span data-ttu-id="a5e12-128">Zainstaluj biblioteki hello express i aplikacje w przypadku mobilne platformy azure z repozytorium npm hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-128">Install hello express and azure-mobile-apps libraries from hello npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="a5e12-129">Tworzenie app.js tooimplement hello podstawowe przenośnych serwera plików.</span><span class="sxs-lookup"><span data-stu-id="a5e12-129">Create an app.js file tooimplement hello basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="a5e12-130">Ta aplikacja tworzy zoptymalizowanych pod kątem mobile WebAPI z jednym punktem końcowym (`/tables/TodoItem`) zapewnia tooan nieuwierzytelnionym dostępem jest podstawowy magazyn danych SQL przy użyciu dynamicznych schematu.</span><span class="sxs-lookup"><span data-stu-id="a5e12-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access tooan underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="a5e12-131">Jest ona odpowiednia dla następującego Szybki Start biblioteki klienta:</span><span class="sxs-lookup"><span data-stu-id="a5e12-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="a5e12-132">[Szybki Start kliencką dla systemu android]</span><span class="sxs-lookup"><span data-stu-id="a5e12-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="a5e12-133">[Apache Cordova klienta — Szybki Start]</span><span class="sxs-lookup"><span data-stu-id="a5e12-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="a5e12-134">[iOS — Szybki Start klienta]</span><span class="sxs-lookup"><span data-stu-id="a5e12-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="a5e12-135">[Szybki Start klienta Sklepu Windows]</span><span class="sxs-lookup"><span data-stu-id="a5e12-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="a5e12-136">[Szybki Start klienta platformy Xamarin.iOS]</span><span class="sxs-lookup"><span data-stu-id="a5e12-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="a5e12-137">[Szybki Start klienta platformy Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="a5e12-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="a5e12-138">[Szybki Start klienta platformy Xamarin.Forms]</span><span class="sxs-lookup"><span data-stu-id="a5e12-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="a5e12-139">Dla tej aplikacji w warstwie podstawowa w hello można znaleźć kod hello [basicapp przykładem w witrynie GitHub].</span><span class="sxs-lookup"><span data-stu-id="a5e12-139">You can find hello code for this basic application in hello [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="a5e12-140"><a name="howto-vs2015-basicapp"></a>Porady: tworzenie zaplecza węzła z programem Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="a5e12-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="a5e12-141">Visual Studio 2015 wymaga rozszerzenia toodevelop Node.js aplikacji w obrębie hello IDE.</span><span class="sxs-lookup"><span data-stu-id="a5e12-141">Visual Studio 2015 requires an extension toodevelop Node.js applications within hello IDE.</span></span>  <span data-ttu-id="a5e12-142">toostart, zainstaluj hello [Node.js Tools 1.1 dla programu Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="a5e12-142">toostart, install hello [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="a5e12-143">Po zainstalowaniu hello Node.js Tools for Visual Studio tworzy aplikację 4.x Express:</span><span class="sxs-lookup"><span data-stu-id="a5e12-143">Once hello Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="a5e12-144">Otwórz hello **nowy projekt** okna dialogowego (z **pliku** > **nowy** > **projektu...** ).</span><span class="sxs-lookup"><span data-stu-id="a5e12-144">Open hello **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="a5e12-145">Rozwiń węzeł **szablony** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="a5e12-146">Wybierz hello **Azure Node.js Express 4 aplikacji w warstwie podstawowa**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-146">Select hello **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="a5e12-147">Wprowadź nazwę projektu hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-147">Fill in hello project name.</span></span>  <span data-ttu-id="a5e12-148">Kliknij przycisk *OK*.</span><span class="sxs-lookup"><span data-stu-id="a5e12-148">Click *OK*.</span></span>

    ![Nowy projekt programu Visual Studio 2015][1]
5. <span data-ttu-id="a5e12-150">Kliknij prawym przyciskiem myszy hello **npm** a następnie wybierz węzeł **zainstalować nowych pakietów npm...** .</span><span class="sxs-lookup"><span data-stu-id="a5e12-150">Right-click hello **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="a5e12-151">Może być konieczne toorefresh hello npm katalogu na tworzenie pierwszej aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="a5e12-151">You may need toorefresh hello npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="a5e12-152">Kliknij przycisk **Odśwież** w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="a5e12-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="a5e12-153">Wprowadź *apps w usłudze azure-mobile* hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a5e12-153">Enter *azure-mobile-apps* in hello search box.</span></span>  <span data-ttu-id="a5e12-154">Kliknij przycisk hello **usługi azure mobile apps 2.0.0** pakietu, a następnie kliknij przycisk **zainstaluj pakiet**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-154">Click hello **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Zainstaluj nowych pakietów npm][2]
8. <span data-ttu-id="a5e12-156">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-156">Click **Close**.</span></span>
9. <span data-ttu-id="a5e12-157">Otwórz hello *app.js* pliku tooadd obsługę hello Azure Mobile Apps SDK.</span><span class="sxs-lookup"><span data-stu-id="a5e12-157">Open hello *app.js* file tooadd support for hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="a5e12-158">U dołu hello 6 at wiersza biblioteki hello wymagają instrukcje, Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="a5e12-158">At line 6 at hello bottom of hello library require statements, add hello following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="a5e12-159">W wierszu około 27 po hello inne instrukcje app.use Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="a5e12-159">At approximately line 27 after hello other app.use statements, add hello following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="a5e12-160">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-160">Save hello file.</span></span>
10. <span data-ttu-id="a5e12-161">Uruchom lokalnie aplikacji hello (powitalne interfejsu API jest obsługiwana na http://localhost: 3000) lub opublikować tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a5e12-161">Either run hello application locally (hello API is served on http://localhost:3000) or publish tooAzure.</span></span>

### <span data-ttu-id="a5e12-162"><a name="create-node-backend-portal"></a>Porady: tworzenie zaplecza Node.js przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a5e12-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using hello Azure portal</span></span>
<span data-ttu-id="a5e12-163">Możesz utworzyć prawo zaplecza aplikacji mobilnej w hello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="a5e12-163">You can create a Mobile App backend right in hello [Azure portal].</span></span> <span data-ttu-id="a5e12-164">Można albo wykonaj hello następujące kroki albo utwórz klienta i serwera razem po hello [tworzenie aplikacji mobilnej](app-service-mobile-ios-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="a5e12-164">You can either follow hello following steps or create a client and server together by following hello [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="a5e12-165">Samouczek Hello zawiera uproszczonej wersji tych instrukcji i najlepiej stosować do weryfikacji koncepcji projektów.</span><span class="sxs-lookup"><span data-stu-id="a5e12-165">hello tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="a5e12-166">Po powrocie do hello *wprowadzenie* bloku, w obszarze **Utwórz tabelę interfejsu API**, wybierz **Node.js** jako z **język wewnętrznej bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-166">Back in hello *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="a5e12-167">Sprawdź pola hello "**potwierdzam, że spowoduje to zastąpienie wszystkich lokacji zawartości.**", następnie kliknij przycisk **Utwórz tabelę TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-167">Check hello box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="a5e12-168"><a name="download-quickstart"></a>Porady: pobieranie hello Node.js zaplecza projekt szybkiego startu kodu przy użyciu narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="a5e12-168"><a name="download-quickstart"></a>How to: Download hello Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="a5e12-169">Po utworzeniu zaplecza aplikacji mobilnej Node.js przy użyciu portalu hello **szybki start** bloku, tworzony jest projekt środowiska Node.js i wdrożone tooyour lokacji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-169">When you create a Node.js Mobile App backend by using hello portal **Quick start** blade, a Node.js project is created for you and deployed tooyour site.</span></span> <span data-ttu-id="a5e12-170">Można dodać tabele i interfejsów API i edytować pliki kodu dla zaplecza Node.js hello w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-170">You can add tables and APIs and edit code files for hello Node.js backend in hello portal.</span></span> <span data-ttu-id="a5e12-171">Umożliwia także różne wdrażania narzędzia toodownload hello wewnętrznej bazy danych projektu tak, aby można dodać lub zmodyfikować tabele i interfejsów API, a następnie ponownie opublikować hello projektu.</span><span class="sxs-lookup"><span data-stu-id="a5e12-171">You can also use various deployment tools toodownload hello backend project so that you can add or modify tables and APIs, then republish hello project.</span></span> <span data-ttu-id="a5e12-172">Aby uzyskać więcej informacji, zobacz [Azure App Service Deployment Guide].</span><span class="sxs-lookup"><span data-stu-id="a5e12-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="a5e12-173">Witaj poniższej procedurze używana jest kod projektu szybkiego startu hello toodownload Git repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a5e12-173">hello following procedure uses a Git repository toodownload hello quickstart project code.</span></span>

1. <span data-ttu-id="a5e12-174">Zainstaluj usługę Git, jeśli jeszcze tego nie zrobiono.</span><span class="sxs-lookup"><span data-stu-id="a5e12-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="a5e12-175">tooinstall wymagane kroki Hello Git różnią się między systemami operacyjnymi.</span><span class="sxs-lookup"><span data-stu-id="a5e12-175">hello steps required tooinstall Git vary between operating systems.</span></span> <span data-ttu-id="a5e12-176">Zobacz [instalowanie Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) dystrybucje systemu operacyjnego i instalacji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="a5e12-177">Wykonaj kroki hello w [hello Włącz repozytorium aplikacji usługi App Service](../app-service-web/app-service-deploy-local-git.md#Step3) repozytorium Git hello tooenable dla witryny sieci wewnętrznej bazy danych, co wiadomości powitania wdrożenia użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="a5e12-177">Follow hello steps in [Enable hello App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello Git repository for your backend site, making a note of hello deployment username and password.</span></span>
3. <span data-ttu-id="a5e12-178">W bloku hello zaplecza aplikacji mobilnej, zanotuj hello **adres URL klonowania Git** ustawienie.</span><span class="sxs-lookup"><span data-stu-id="a5e12-178">In hello blade for your Mobile App backend, make a note of hello **Git clone URL** setting.</span></span>
4. <span data-ttu-id="a5e12-179">Wykonanie hello `git clone` polecenia przy użyciu hello adres URL klonowania Git, wprowadzania hasła, gdy jest to wymagane, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="a5e12-179">Execute hello `git clone` command using hello Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="a5e12-180">Przeglądaj toolocal w hello poprzedzających przykładzie jest to katalog /todolist i zwróć uwagę, że pliki projektu zostały pobrane.</span><span class="sxs-lookup"><span data-stu-id="a5e12-180">Browse toolocal directory, which in hello preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="a5e12-181">Zlokalizuj hello `todoitem.json` pliku w hello `/tables` katalogu.</span><span class="sxs-lookup"><span data-stu-id="a5e12-181">Locate hello `todoitem.json` file in hello `/tables` directory.</span></span>  <span data-ttu-id="a5e12-182">Ten plik definiuje uprawnienia w tabeli.</span><span class="sxs-lookup"><span data-stu-id="a5e12-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="a5e12-183">Również znaleźć hello `todoitem.js` w pliku hello sam katalog, który określa, że operacji CRUD skrypty hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="a5e12-183">Also find hello `todoitem.js` file in hello same directory, which defines that CRUD operation scripts for hello table.</span></span>
6. <span data-ttu-id="a5e12-184">Po dokonaniu zmiany tooproject pliki, wykonaj hello następujące polecenia tooadd, zatwierdzić, a następnie przekaż lokacji toohello zmiany:</span><span class="sxs-lookup"><span data-stu-id="a5e12-184">After you have made changes tooproject files, execute hello following commands tooadd, commit, then upload the changes toohello site:</span></span>

        $ git commit -m "updated hello table script"
        $ git push origin master

    <span data-ttu-id="a5e12-185">Po dodaniu nowego projektu toohello plików, należy najpierw tooexecute hello `git add .` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a5e12-185">When you add new files toohello project, you first need tooexecute hello `git add .` command.</span></span>

<span data-ttu-id="a5e12-186">opublikowaniu lokacji Hello za każdym razem, gdy nowy zestaw zatwierdzeń spoczywa toohello lokacji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-186">hello site is republished every time a new set of commits is pushed toohello site.</span></span>

### <span data-ttu-id="a5e12-187"><a name="howto-publish-to-azure"></a>Porady: publikowanie programu tooAzure zaplecza Node.js</span><span class="sxs-lookup"><span data-stu-id="a5e12-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend tooAzure</span></span>
<span data-ttu-id="a5e12-188">Microsoft Azure udostępnia wiele mechanizmów publikowania zaplecza Azure App Service Mobile aplikacji Node.js do hello usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e12-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to hello Azure service.</span></span>  <span data-ttu-id="a5e12-189">Obejmują one przy użyciu narzędzia wdrażania zintegrowane w programie Visual Studio, narzędzia wiersza polecenia i opcje ciągłego wdrażania w oparciu o kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="a5e12-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="a5e12-190">Aby uzyskać więcej informacji na ten temat, zobacz [Azure App Service Deployment Guide].</span><span class="sxs-lookup"><span data-stu-id="a5e12-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="a5e12-191">Usługa aplikacji Azure ma poradę należy zapoznać się przed przystąpieniem do wdrażania aplikacji Node.js:</span><span class="sxs-lookup"><span data-stu-id="a5e12-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="a5e12-192">Jak zbyt[Określ hello wersji węzła]</span><span class="sxs-lookup"><span data-stu-id="a5e12-192">How too[specify hello Node Version]</span></span>
* <span data-ttu-id="a5e12-193">Jak zbyt[Użyj modułów węzła]</span><span class="sxs-lookup"><span data-stu-id="a5e12-193">How too[use Node modules]</span></span>

### <span data-ttu-id="a5e12-194"><a name="howto-enable-homepage"></a>Porady: Włączanie strony głównej aplikacji</span><span class="sxs-lookup"><span data-stu-id="a5e12-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="a5e12-195">Wiele aplikacji są kombinacją sieci web i aplikacji mobilnych i hello ExpressJS framework umożliwia toocombine dwa aspekty.</span><span class="sxs-lookup"><span data-stu-id="a5e12-195">Many applications are a combination of web and mobile apps and hello ExpressJS framework allows you toocombine the two facets.</span></span>  <span data-ttu-id="a5e12-196">Czasami jednak warto zapoznać się z tooonly implementacji interfejsu dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="a5e12-196">Sometimes, however, you may wish tooonly implement a mobile interface.</span></span>  <span data-ttu-id="a5e12-197">Jest przydatne tooprovide, którą usługą aplikacji docelowej strony tooensure hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="a5e12-197">It is useful tooprovide a landing page tooensure hello app service is up and running.</span></span>  <span data-ttu-id="a5e12-198">Można podać strony głównej lub włączyć tymczasowe strony głównej.</span><span class="sxs-lookup"><span data-stu-id="a5e12-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="a5e12-199">tooenable tymczasowe strony głównej, użyj powitania po tooinstantiate Azure Mobile Apps:</span><span class="sxs-lookup"><span data-stu-id="a5e12-199">tooenable a temporary home page, use hello following tooinstantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="a5e12-200">Jeśli mają tylko tej opcji, które są dostępne podczas tworzenia lokalnie, możesz dodać tooyour to ustawienie `azureMobile.js` pliku.</span><span class="sxs-lookup"><span data-stu-id="a5e12-200">If you only want this option available when developing locally, you can add this setting tooyour `azureMobile.js` file.</span></span>

## <span data-ttu-id="a5e12-201"><a name="TableOperations"></a>Operacje tabeli</span><span class="sxs-lookup"><span data-stu-id="a5e12-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="a5e12-202">Hello azure-mobile aplikacji Node.js Server SDK udostępnia mechanizmy tooexpose dane przechowywane w bazie danych SQL Azure jako WebAPI tabel.</span><span class="sxs-lookup"><span data-stu-id="a5e12-202">hello azure-mobile-apps Node.js Server SDK provides mechanisms tooexpose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="a5e12-203">Podano pięć operacji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-203">Five operations are provided.</span></span>

| <span data-ttu-id="a5e12-204">Operacja</span><span class="sxs-lookup"><span data-stu-id="a5e12-204">Operation</span></span> | <span data-ttu-id="a5e12-205">Opis</span><span class="sxs-lookup"><span data-stu-id="a5e12-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5e12-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="a5e12-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="a5e12-207">Pobierz wszystkie rekordy w tabeli hello</span><span class="sxs-lookup"><span data-stu-id="a5e12-207">Get all records in hello table</span></span> |
| <span data-ttu-id="a5e12-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="a5e12-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="a5e12-209">Pobierz określonego rekordu w tabeli hello</span><span class="sxs-lookup"><span data-stu-id="a5e12-209">Get a specific record in hello table</span></span> |
| <span data-ttu-id="a5e12-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="a5e12-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="a5e12-211">Utwórz rekord tabeli hello</span><span class="sxs-lookup"><span data-stu-id="a5e12-211">Create a record in hello table</span></span> |
| <span data-ttu-id="a5e12-212">POPRAWKA /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="a5e12-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="a5e12-213">Aktualizacja rekordu w tabeli hello</span><span class="sxs-lookup"><span data-stu-id="a5e12-213">Update a record in hello table</span></span> |
| <span data-ttu-id="a5e12-214">Usuń /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="a5e12-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="a5e12-215">Usuwanie rekordu w tabeli hello</span><span class="sxs-lookup"><span data-stu-id="a5e12-215">Delete a record in hello table</span></span> |

<span data-ttu-id="a5e12-216">Obsługuje ten WebAPI [OData] i rozszerza toosupport schematu tabeli hello [synchronizacji danych w trybie offline].</span><span class="sxs-lookup"><span data-stu-id="a5e12-216">This WebAPI supports [OData] and extends hello table schema toosupport [offline data sync].</span></span>

### <span data-ttu-id="a5e12-217"><a name="howto-dynamicschema"></a>Porady: Definiowanie tabel za pomocą dynamicznej schematu</span><span class="sxs-lookup"><span data-stu-id="a5e12-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="a5e12-218">Przed użyciem tabeli musi być zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="a5e12-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="a5e12-219">Tabele mogą być definiowane ze schematem statyczne (gdzie hello developer definiuje hello kolumn w schemacie hello) lub dynamicznie (gdzie hello SDK Określa schemat hello oparty na przychodzące żądania).</span><span class="sxs-lookup"><span data-stu-id="a5e12-219">Tables can be defined with a static schema (where hello developer defines hello columns within hello schema) or dynamically (where hello SDK controls hello schema based on incoming requests).</span></span> <span data-ttu-id="a5e12-220">Ponadto hello deweloper może kontrolować określonych aspekty hello WebAPI przez dodanie definicji toohello kodu Javascript.</span><span class="sxs-lookup"><span data-stu-id="a5e12-220">In addition, hello developer can control specific aspects of hello WebAPI by adding Javascript code toohello definition.</span></span>

<span data-ttu-id="a5e12-221">Najlepszym rozwiązaniem należy zdefiniować każdej tabeli w pliku Javascript w katalogu tabel hello następnie tabele hello tooimport tables.import() — metoda.</span><span class="sxs-lookup"><span data-stu-id="a5e12-221">As a best practice, you should define each table in a Javascript file in hello tables directory, then use the tables.import() method tooimport hello tables.</span></span>  <span data-ttu-id="a5e12-222">Rozszerzanie hello basic-app, będzie można dostosować pliku app.js hello:</span><span class="sxs-lookup"><span data-stu-id="a5e12-222">Extending hello basic-app, hello app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="a5e12-223">Definiowanie tabeli hello. / tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="a5e12-223">Define hello table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

<span data-ttu-id="a5e12-224">Tabele domyślnie używają schematu dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="a5e12-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="a5e12-225">tooturn poza dynamiczne schematu globalnie, ustawić ustawienia aplikacji hello **MS_DynamicSchema** toofalse w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e12-225">tooturn off dynamic schema globally, set hello App Setting **MS_DynamicSchema** toofalse within hello Azure portal.</span></span>

<span data-ttu-id="a5e12-226">Pełny przykład można znaleźć w hello [todo przykładem w witrynie GitHub].</span><span class="sxs-lookup"><span data-stu-id="a5e12-226">You can find a complete example in hello [todo sample on GitHub].</span></span>

### <span data-ttu-id="a5e12-227"><a name="howto-staticschema"></a>Porady: Definiowanie tabel za pomocą statycznego schematu</span><span class="sxs-lookup"><span data-stu-id="a5e12-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="a5e12-228">Można jawnie definiować hello tooexpose kolumn za pomocą hello WebAPI.</span><span class="sxs-lookup"><span data-stu-id="a5e12-228">You can explicitly define hello columns tooexpose via hello WebAPI.</span></span>  <span data-ttu-id="a5e12-229">Hello azure-mobile aplikacji Node.js SDK automatycznie dodaje wszystkie dodatkowe kolumny są wymagane dla listy toohello synchronizacji danych w trybie offline, który podasz.</span><span class="sxs-lookup"><span data-stu-id="a5e12-229">hello azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync toohello list that you provide.</span></span>  <span data-ttu-id="a5e12-230">Na przykład wymagać tabeli z kolumnami przez aplikacje klienckie Szybki Start: tekst (ciąg) i ukończyć (wartość logiczna).</span><span class="sxs-lookup"><span data-stu-id="a5e12-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="a5e12-231">Hello tabeli można zdefiniować w hello tabeli JavaScript pliku definicji (znajdujący się w katalogu tabel hello) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a5e12-231">hello table can be defined in hello table definition JavaScript file (located in hello tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="a5e12-232">Tabel w przypadku definiowania statycznie, następnie należy także wywołać schematu bazy danych hello toocreate hello tables.initialize() — metoda podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="a5e12-232">If you define tables statically, then you must also call hello tables.initialize() method toocreate hello database schema on startup.</span></span>  <span data-ttu-id="a5e12-233">Zwraca metodę tables.initialize() Hello [Promise] tak, aby usługi sieci web hello nie obsługiwać żądań przed hello bazy danych został zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="a5e12-233">hello tables.initialize() method returns a [Promise] so that hello web service does not serve requests before hello database being initialized.</span></span>

### <span data-ttu-id="a5e12-234"><a name="howto-sqlexpress-setup"></a>Porady: użycie programu SQL Express jako programowanie magazynu danych na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="a5e12-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="a5e12-235">Witaj hello Azure Mobile Apps SDK węzła aplikacje AzureMobile zawiera trzy opcje do obsługi danych fabrycznej hello: zestaw SDK zawiera trzy opcje do obsługi danych fabrycznej hello:</span><span class="sxs-lookup"><span data-stu-id="a5e12-235">hello Azure Mobile Apps hello AzureMobile Apps Node SDK provides three options for serving data out of hello box: SDK provides three options for serving data out of hello box:</span></span>

* <span data-ttu-id="a5e12-236">Użyj hello **pamięci** magazynu przykład tooprovide nietrwałe sterowników</span><span class="sxs-lookup"><span data-stu-id="a5e12-236">Use hello **memory** driver tooprovide a non-persistent example store</span></span>
* <span data-ttu-id="a5e12-237">Użyj hello **mssql** tooprovide sterowników magazynu danych programu SQL Express dla rozwoju</span><span class="sxs-lookup"><span data-stu-id="a5e12-237">Use hello **mssql** driver tooprovide a SQL Express data store for development</span></span>
* <span data-ttu-id="a5e12-238">Użyj hello **mssql** tooprovide sterowników magazynu danych bazy danych SQL Azure dla trybu produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="a5e12-238">Use hello **mssql** driver tooprovide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="a5e12-239">zestaw SDK usługi Azure Mobile Apps Node.js Hello używa hello [mssql Node.js pakietu] tooestablish i użyj programu SQL Express tooboth połączenia i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="a5e12-239">hello Azure Mobile Apps Node.js SDK uses hello [mssql Node.js package] tooestablish and use a connection tooboth SQL Express and SQL Database.</span></span>  <span data-ttu-id="a5e12-240">Ten pakiet wymaga włączenia połączeń TCP w wystąpieniu programu SQL Express.</span><span class="sxs-lookup"><span data-stu-id="a5e12-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="a5e12-241">Sterownik pamięci Hello nie ma kompletnego zestawu urządzenia do testowania.</span><span class="sxs-lookup"><span data-stu-id="a5e12-241">hello memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="a5e12-242">W razie potrzeby tootest zaplecza lokalnie zaleca użycie hello magazyn danych SQL Express i hello mssql sterownika.</span><span class="sxs-lookup"><span data-stu-id="a5e12-242">If you wish tootest your backend locally, we recommend hello use of a SQL Express data store and hello mssql driver.</span></span>
>
>

1. <span data-ttu-id="a5e12-243">Pobierz i zainstaluj [programu Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="a5e12-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="a5e12-244">Upewnij się, że hello programu SQL Server 2014 Express jest instalowany z wersji narzędzia.</span><span class="sxs-lookup"><span data-stu-id="a5e12-244">Ensure you install hello SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="a5e12-245">Chyba że jawnie wymagana jest Obsługa 64-bitowych, hello 32-bitowej wersji zużywa mniej pamięci podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="a5e12-245">Unless you explicitly require 64-bit support, hello 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="a5e12-246">Uruchom Menedżera konfiguracji programu SQL Server 2014 hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-246">Run hello SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="a5e12-247">Rozwiń węzeł hello **konfigurację sieci programu SQL Server** węzła w menu drzewa po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="a5e12-247">Expand hello **SQL Server Network Configuration** node in hello left-hand tree menu.</span></span>
   2. <span data-ttu-id="a5e12-248">Kliknij przycisk **protokoły dla programu SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="a5e12-249">Kliknij prawym przyciskiem myszy **TCP/IP** i wybierz **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="a5e12-250">Kliknij przycisk **OK** w wyskakującym oknie dialogowym hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-250">Click **OK** in hello pop-up dialog.</span></span>
   4. <span data-ttu-id="a5e12-251">Kliknij prawym przyciskiem myszy **TCP/IP** i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="a5e12-252">Kliknij przycisk hello **adresów IP** kartę.</span><span class="sxs-lookup"><span data-stu-id="a5e12-252">Click hello **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="a5e12-253">Znajdź hello **IPWszystkie** węzła.</span><span class="sxs-lookup"><span data-stu-id="a5e12-253">Find hello **IPAll** node.</span></span>  <span data-ttu-id="a5e12-254">W hello **TCP Port** wprowadź **1433**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-254">In hello **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="a5e12-255">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-255">Click **OK**.</span></span>  <span data-ttu-id="a5e12-256">Kliknij przycisk **OK** w wyskakującym oknie dialogowym hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-256">Click **OK** in hello pop-up dialog.</span></span>
   8. <span data-ttu-id="a5e12-257">Kliknij przycisk **usług SQL Server** w menu drzewa po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="a5e12-257">Click **SQL Server Services** in hello left-hand tree menu.</span></span>
   9. <span data-ttu-id="a5e12-258">Kliknij prawym przyciskiem myszy **programu SQL Server (SQLEXPRESS)** i wybierz **ponownego uruchomienia**</span><span class="sxs-lookup"><span data-stu-id="a5e12-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="a5e12-259">Zamknij hello Menedżera konfiguracji programu SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="a5e12-259">Close hello SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="a5e12-260">Uruchom hello SQL Server 2014 Management Studio i połącz tooyour lokalne wystąpienie programu SQL Express</span><span class="sxs-lookup"><span data-stu-id="a5e12-260">Run hello SQL Server 2014 Management Studio and connect tooyour local SQL Express instance</span></span>

   1. <span data-ttu-id="a5e12-261">Kliknij prawym przyciskiem myszy wystąpienie w hello Eksplorator obiektów i wybierz **właściwości**</span><span class="sxs-lookup"><span data-stu-id="a5e12-261">Right-click your instance in hello Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="a5e12-262">Wybierz hello **zabezpieczeń** strony.</span><span class="sxs-lookup"><span data-stu-id="a5e12-262">Select hello **Security** page.</span></span>
   3. <span data-ttu-id="a5e12-263">Upewnij się, hello **tryb programu SQL Server i uwierzytelniania systemu Windows** jest zaznaczone</span><span class="sxs-lookup"><span data-stu-id="a5e12-263">Ensure hello **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="a5e12-264">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="a5e12-265">Rozwiń węzeł **zabezpieczeń** > **logowania** w hello Eksplorator obiektów</span><span class="sxs-lookup"><span data-stu-id="a5e12-265">Expand **Security** > **Logins** in hello Object Explorer</span></span>
   6. <span data-ttu-id="a5e12-266">Kliknij prawym przyciskiem myszy **logowania** i wybierz **nowe dane logowania...**</span><span class="sxs-lookup"><span data-stu-id="a5e12-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="a5e12-267">Wprowadź nazwę logowania.</span><span class="sxs-lookup"><span data-stu-id="a5e12-267">Enter a Login name.</span></span>  <span data-ttu-id="a5e12-268">Wybierz pozycję **Uwierzytelnianie programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="a5e12-269">Wprowadź hasło, a następnie wprowadź hello tego samego hasła w **Potwierdź hasło**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-269">Enter a Password, then enter hello same password in **Confirm password**.</span></span>  <span data-ttu-id="a5e12-270">Witaj hasło musi spełniać wymagania co do złożoności systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a5e12-270">hello password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="a5e12-271">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-271">Click **OK**</span></span>

          ![Add a new user tooSQL Express][5]
   9. <span data-ttu-id="a5e12-272">Kliknij prawym przyciskiem myszy nazwę nowego użytkownika, a następnie wybierz **właściwości**</span><span class="sxs-lookup"><span data-stu-id="a5e12-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="a5e12-273">Wybierz hello **ról serwera** strony</span><span class="sxs-lookup"><span data-stu-id="a5e12-273">Select hello **Server Roles** page</span></span>
   11. <span data-ttu-id="a5e12-274">Sprawdź hello pole dalej toohello **dbcreator** roli serwera</span><span class="sxs-lookup"><span data-stu-id="a5e12-274">Check hello box next toohello **dbcreator** server role</span></span>
   12. <span data-ttu-id="a5e12-275">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-275">Click **OK**</span></span>
   13. <span data-ttu-id="a5e12-276">Zamknij hello SQL Server 2015 Management Studio</span><span class="sxs-lookup"><span data-stu-id="a5e12-276">Close hello SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="a5e12-277">Zapewnić, że hello rekordu nazwy użytkownika i hasła, wybrane.</span><span class="sxs-lookup"><span data-stu-id="a5e12-277">Ensure you record hello username and password you selected.</span></span>  <span data-ttu-id="a5e12-278">W zależności od wymagań określonej bazy danych może być konieczne tooassign dodatkowych ról serwera lub uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="a5e12-278">You may need tooassign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="a5e12-279">Witaj aplikacji Node.js odczytuje hello **SQLCONNSTR_MS_TableConnectionString** zmiennej środowiskowej hello ciągu połączenia dla tej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a5e12-279">hello Node.js application reads hello **SQLCONNSTR_MS_TableConnectionString** environment variable for hello connection string for this database.</span></span>  <span data-ttu-id="a5e12-280">Można ustawić tę zmienną w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="a5e12-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="a5e12-281">Na przykład można użyć PowerShell tooset tej zmiennej środowiskowej:</span><span class="sxs-lookup"><span data-stu-id="a5e12-281">For example, you can use PowerShell tooset this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="a5e12-282">Hello dostępu do bazy danych przy użyciu połączenia TCP/IP i podaj nazwę użytkownika i hasło dla połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-282">Access hello database through a TCP/IP connection and provide a username and password for hello connection.</span></span>

### <span data-ttu-id="a5e12-283"><a name="howto-config-localdev"></a>Porady: Konfigurowanie projektu dla rozwoju lokalnych</span><span class="sxs-lookup"><span data-stu-id="a5e12-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="a5e12-284">Aplikacje mobilne platformy Azure odczytuje plik JavaScript o nazwie *azureMobile.js* z hello lokalnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="a5e12-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from hello local filesystem.</span></span>  <span data-ttu-id="a5e12-285">Nie używać tego pliku tooconfigure hello zestaw SDK usługi Azure Mobile Apps w środowisku produkcyjnym — Użyj ustawień aplikacji w ramach hello [portalu Azure] zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="a5e12-285">Do not use this file tooconfigure hello Azure Mobile Apps SDK in production - use App Settings within hello [Azure portal] instead.</span></span>  <span data-ttu-id="a5e12-286">Witaj *azureMobile.js* plików należy wyeksportować obiekt konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-286">hello *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="a5e12-287">Witaj najczęściej używane ustawienia to:</span><span class="sxs-lookup"><span data-stu-id="a5e12-287">hello most common settings are:</span></span>

* <span data-ttu-id="a5e12-288">Ustawienia bazy danych</span><span class="sxs-lookup"><span data-stu-id="a5e12-288">Database Settings</span></span>
* <span data-ttu-id="a5e12-289">Ustawienia rejestrowania diagnostycznego</span><span class="sxs-lookup"><span data-stu-id="a5e12-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="a5e12-290">Alternatywne ustawienia mechanizmu CORS</span><span class="sxs-lookup"><span data-stu-id="a5e12-290">Alternate CORS Settings</span></span>

<span data-ttu-id="a5e12-291">Przykład *azureMobile.js* pliku implementacji hello poprzedzających następujące ustawienia bazy danych:</span><span class="sxs-lookup"><span data-stu-id="a5e12-291">An example *azureMobile.js* file implementing hello preceding database settings follows:</span></span>

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

<span data-ttu-id="a5e12-292">Firma Microsoft zaleca dodanie *azureMobile.js* tooyour *.gitignore* pliku (lub inne Ignoruj pliku kontroli kodu źródłowego) hasła tooprevent znajdują się w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-292">We recommend that you add *azureMobile.js* tooyour *.gitignore* file (or other source code control ignore file) tooprevent passwords from being stored in hello cloud.</span></span>  <span data-ttu-id="a5e12-293">Zawsze skonfigurować ustawienia produkcji w ustawieniach aplikacji w ramach hello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="a5e12-293">Always configure production settings in App Settings within hello [Azure portal].</span></span>

### <span data-ttu-id="a5e12-294"><a name="howto-appsettings"></a>Instrukcje: Konfigurowanie ustawień aplikacji dla aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="a5e12-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="a5e12-295">Większość ustawień w hello *azureMobile.js* plik ma odpowiednik ustawienia aplikacji w hello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="a5e12-295">Most settings in hello *azureMobile.js* file have an equivalent App Setting in hello [Azure portal].</span></span>  <span data-ttu-id="a5e12-296">W ustawieniach aplikacji, należy użyć powitania po tooconfigure listy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a5e12-296">Use hello following list tooconfigure your app in App Settings:</span></span>

| <span data-ttu-id="a5e12-297">Ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="a5e12-297">App Setting</span></span> | <span data-ttu-id="a5e12-298">*azureMobile.js* ustawienie</span><span class="sxs-lookup"><span data-stu-id="a5e12-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="a5e12-299">Opis</span><span class="sxs-lookup"><span data-stu-id="a5e12-299">Description</span></span> | <span data-ttu-id="a5e12-300">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a5e12-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a5e12-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="a5e12-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="a5e12-302">name</span><span class="sxs-lookup"><span data-stu-id="a5e12-302">name</span></span> |<span data-ttu-id="a5e12-303">Nazwa aplikacji hello Hello</span><span class="sxs-lookup"><span data-stu-id="a5e12-303">hello name of hello app</span></span> |<span data-ttu-id="a5e12-304">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a5e12-304">string</span></span> |
| <span data-ttu-id="a5e12-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="a5e12-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="a5e12-306">Logging.level</span><span class="sxs-lookup"><span data-stu-id="a5e12-306">logging.level</span></span> |<span data-ttu-id="a5e12-307">Poziom dziennika minimalna toolog wiadomości</span><span class="sxs-lookup"><span data-stu-id="a5e12-307">Minimum log level of messages toolog</span></span> |<span data-ttu-id="a5e12-308">błąd, ostrzeżenie, informacje o verbose, debug, niemądre</span><span class="sxs-lookup"><span data-stu-id="a5e12-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="a5e12-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="a5e12-309">**MS_DebugMode**</span></span> |<span data-ttu-id="a5e12-310">Debugowania</span><span class="sxs-lookup"><span data-stu-id="a5e12-310">debug</span></span> |<span data-ttu-id="a5e12-311">Włącz lub wyłącz tryb debugowania</span><span class="sxs-lookup"><span data-stu-id="a5e12-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="a5e12-312">wartość true, false</span><span class="sxs-lookup"><span data-stu-id="a5e12-312">true, false</span></span> |
| <span data-ttu-id="a5e12-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="a5e12-313">**MS_TableSchema**</span></span> |<span data-ttu-id="a5e12-314">Data.Schema</span><span class="sxs-lookup"><span data-stu-id="a5e12-314">data.schema</span></span> |<span data-ttu-id="a5e12-315">Domyślna nazwa schematu dla tabel SQL</span><span class="sxs-lookup"><span data-stu-id="a5e12-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="a5e12-316">ciąg (domyślne: dbo)</span><span class="sxs-lookup"><span data-stu-id="a5e12-316">string (default: dbo)</span></span> |
| <span data-ttu-id="a5e12-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="a5e12-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="a5e12-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="a5e12-318">data.dynamicSchema</span></span> |<span data-ttu-id="a5e12-319">Włącz lub wyłącz tryb debugowania</span><span class="sxs-lookup"><span data-stu-id="a5e12-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="a5e12-320">wartość true, false</span><span class="sxs-lookup"><span data-stu-id="a5e12-320">true, false</span></span> |
| <span data-ttu-id="a5e12-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="a5e12-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="a5e12-322">Wersja (tooundefined zestaw)</span><span class="sxs-lookup"><span data-stu-id="a5e12-322">version (set tooundefined)</span></span> |<span data-ttu-id="a5e12-323">Wyłącza nagłówka X-ZUMO-Server-Version hello</span><span class="sxs-lookup"><span data-stu-id="a5e12-323">Disables hello X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="a5e12-324">wartość true, false</span><span class="sxs-lookup"><span data-stu-id="a5e12-324">true, false</span></span> |
| <span data-ttu-id="a5e12-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="a5e12-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="a5e12-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="a5e12-326">skipversioncheck</span></span> |<span data-ttu-id="a5e12-327">Wyłącza sprawdzanie wersji powitania klienta interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a5e12-327">Disables hello client API version check</span></span> |<span data-ttu-id="a5e12-328">wartość true, false</span><span class="sxs-lookup"><span data-stu-id="a5e12-328">true, false</span></span> |

<span data-ttu-id="a5e12-329">tooset ustawienie aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a5e12-329">tooset an App Setting:</span></span>

1. <span data-ttu-id="a5e12-330">Zaloguj się za toohello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="a5e12-330">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="a5e12-331">Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę hello aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="a5e12-331">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="a5e12-332">Domyślnie zostanie otwarty blok ustawień Hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-332">hello Settings blade opens by default.</span></span> <span data-ttu-id="a5e12-333">Jeśli nie kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="a5e12-334">Kliknij przycisk **ustawienia aplikacji** hello ogólne menu.</span><span class="sxs-lookup"><span data-stu-id="a5e12-334">Click **Application settings** in hello GENERAL menu.</span></span>
5. <span data-ttu-id="a5e12-335">Przewiń toohello w sekcji Ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-335">Scroll toohello App Settings section.</span></span>
6. <span data-ttu-id="a5e12-336">Jeśli aplikacja, ustawienia już istnieje, kliknij wartość hello hello aplikacji ustawienie tooedit hello wartości.</span><span class="sxs-lookup"><span data-stu-id="a5e12-336">If your app setting already exists, click hello value of hello app setting tooedit hello value.</span></span>
7. <span data-ttu-id="a5e12-337">Jeśli ustawienia aplikacji nie istnieje, wprowadź hello ustawienie aplikacji w polu klucza hello a hello wartość w polu wartość hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-337">If your app setting does not exist, enter hello App Setting in hello Key box and hello value in hello Value box.</span></span>
8. <span data-ttu-id="a5e12-338">Po zakończeniu, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="a5e12-339">Zmiana większość ustawień aplikacji wymaga ponownego uruchomienia usługi.</span><span class="sxs-lookup"><span data-stu-id="a5e12-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="a5e12-340"><a name="howto-use-sqlazure"></a>Porady: Użyj bazy danych SQL jako magazyn danych produkcyjnych</span><span class="sxs-lookup"><span data-stu-id="a5e12-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="a5e12-341">Przy użyciu bazy danych SQL Azure jako magazynu danych jest identyczne we wszystkich typów aplikacji w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a5e12-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="a5e12-342">Jeśli jeszcze tego nie zrobiono, wykonaj te kroki toocreate zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="a5e12-342">If you have not done so already, follow these steps toocreate a Mobile App backend.</span></span>

1. <span data-ttu-id="a5e12-343">Zaloguj się za toohello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="a5e12-343">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="a5e12-344">W hello lewym górnym rogu okna hello, kliknij przycisk hello **+ nowy** przycisk > **sieci Web i mobilność** > **aplikacji mobilnej**, następnie podaj nazwę zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="a5e12-344">In hello top left of hello window, click hello **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="a5e12-345">W hello **grupy zasobów** wprowadź hello takie same nazwy co aplikacja.</span><span class="sxs-lookup"><span data-stu-id="a5e12-345">In hello **Resource Group** box, enter hello same name as your app.</span></span>
4. <span data-ttu-id="a5e12-346">plan usługi aplikacji — domyślna Hello jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="a5e12-346">hello Default App Service plan is selected.</span></span>  <span data-ttu-id="a5e12-347">Jeśli chcesz toochange planu usługi aplikacji, możesz to zrobić, klikając hello Plan usługi aplikacji > **+ Utwórz nowe**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-347">If you wish toochange your App Service plan, you can do so by clicking hello App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="a5e12-348">Podaj nazwę nowego planu usługi aplikacji hello i wybierz odpowiednią lokalizację.</span><span class="sxs-lookup"><span data-stu-id="a5e12-348">Provide a name of hello new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="a5e12-349">Kliknij hello warstwa cenowa i wybierz odpowiednią warstwę cenową dla usługi hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-349">Click hello Pricing tier and select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="a5e12-350">Wybierz **Wyświetl wszystkie** tooview więcej cennik opcje, takie jak **wolne** i **Shared**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-350">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="a5e12-351">Po wybraniu warstwy cenowej kliknij hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a5e12-351">Once you have selected the pricing tier, click hello **Select** button.</span></span>  <span data-ttu-id="a5e12-352">Po powrocie do hello **planu usługi aplikacji** bloku, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-352">Back in hello **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="a5e12-353">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-353">Click **Create**.</span></span> <span data-ttu-id="a5e12-354">Inicjowanie obsługi administracyjnej zaplecza aplikacji mobilnej może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="a5e12-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="a5e12-355">Po zainicjowaniu obsługi zaplecza aplikacji mobilnej hello portalu hello otwiera hello **ustawienia** bloku hello zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="a5e12-355">Once hello Mobile App backend is provisioned, hello portal opens hello **Settings** blade for hello Mobile App backend.</span></span>

<span data-ttu-id="a5e12-356">Po utworzeniu hello zaplecza aplikacji mobilnej, można wybrać tooeither Połącz istniejące zaplecza aplikacji mobilnej tooyour bazy danych SQL lub Utwórz nową bazę danych SQL.</span><span class="sxs-lookup"><span data-stu-id="a5e12-356">Once hello Mobile App backend is created, you can choose tooeither connect an existing SQL database tooyour Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="a5e12-357">W tej sekcji utworzymy bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="a5e12-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="a5e12-358">Jeśli masz już bazę danych w hello tej samej lokalizacji co hello zaplecza aplikacji mobilnej, zamiast tego możesz **Użyj istniejącej bazy danych** , a następnie wybrać tę bazę danych.</span><span class="sxs-lookup"><span data-stu-id="a5e12-358">If you already have a database in hello same location as hello mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="a5e12-359">Użycie Hello bazy danych w innej lokalizacji nie jest zalecane z powodu większych opóźnień.</span><span class="sxs-lookup"><span data-stu-id="a5e12-359">hello use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="a5e12-360">W zaplecze nowej aplikacji mobilnej powitania kliknij **ustawienia** > **aplikacji mobilnej** > **danych** > **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-360">In hello new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="a5e12-361">W hello **Dodaj połączenie danych** bloku, kliknij przycisk **baza danych SQL — Skonfiguruj wymagane ustawienia** > **Utwórz nową bazę danych**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-361">In hello **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="a5e12-362">Wprowadź nazwę nowej bazy danych hello hello w hello **nazwa** pola.</span><span class="sxs-lookup"><span data-stu-id="a5e12-362">Enter hello name of hello new database in hello **Name** field.</span></span>
3. <span data-ttu-id="a5e12-363">Kliknij przycisk **serwera**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-363">Click **Server**.</span></span>  <span data-ttu-id="a5e12-364">W hello **nowy serwer** bloku, wprowadź unikatową nazwą serwera w hello **nazwy serwera** pól i zapewnienia odpowiedniej **identyfikator logowania administratora serwera** i **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-364">In hello **New server** blade, enter a unique server name in hello **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="a5e12-365">Upewnij się, **Zezwalaj usługom platformy azure tooaccess serwera** jest zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="a5e12-365">Ensure **Allow azure services tooaccess server** is checked.</span></span>  <span data-ttu-id="a5e12-366">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-366">Click **OK**.</span></span>

    ![Utwórz bazę danych Azure SQL][6]
4. <span data-ttu-id="a5e12-368">Na powitania **nową bazę danych** bloku, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-368">On hello **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="a5e12-369">Powrót na powitania **Dodaj połączenie danych** bloku, wybierz opcję **ciąg połączenia**, wprowadź hello logowania i hasło podane podczas tworzenia hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a5e12-369">Back on hello **Add data connection** blade, select **Connection string**, enter hello login and password that you provided when creating hello database.</span></span>  <span data-ttu-id="a5e12-370">Jeśli używasz istniejącej bazy danych, należy podać poświadczenia logowania powitania dla tej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a5e12-370">If you use an existing database, provide hello login credentials for that database.</span></span>  <span data-ttu-id="a5e12-371">Po wpisaniu, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="a5e12-372">Wróć na powitania **Dodaj połączenie danych** bloku ponownie, kliknij przycisk **OK** toocreate hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="a5e12-372">Back on hello **Add data connection** blade again, click **OK** toocreate hello database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="a5e12-373">Tworzenie bazy danych hello może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="a5e12-373">Creation of hello database can take a few minutes.</span></span>  <span data-ttu-id="a5e12-374">Użyj hello **powiadomienia** obszaru toomonitor hello postęp wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-374">Use hello **Notifications** area toomonitor hello progress of hello deployment.</span></span>  <span data-ttu-id="a5e12-375">Nie postępu aż hello bazy danych został wdrożony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a5e12-375">Do not progress until hello database has been deployed successfully.</span></span>  <span data-ttu-id="a5e12-376">Po pomyślnym wdrożeniu, ciąg połączenia jest tworzony dla wystąpienia bazy danych SQL hello w zapleczu swojej przenośnych ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-376">Once successfully deployed, a Connection String is created for hello SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="a5e12-377">Można wyświetlić to ustawienie aplikacji hello **ustawienia** > **ustawienia aplikacji** > **parametry połączenia**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-377">You can see this app setting in hello **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="a5e12-378"><a name="howto-tables-auth"></a>Porady: Wymagaj uwierzytelniania tootables dostępu</span><span class="sxs-lookup"><span data-stu-id="a5e12-378"><a name="howto-tables-auth"></a>How to: Require authentication for access tootables</span></span>
<span data-ttu-id="a5e12-379">Jeśli chcesz toouse uwierzytelniania usługi aplikacji z punktem końcowym tabel hello, należy skonfigurować uwierzytelnianie usługi aplikacji w hello [portalu Azure] pierwszy.</span><span class="sxs-lookup"><span data-stu-id="a5e12-379">If you wish toouse App Service Authentication with hello tables endpoint, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="a5e12-380">Dla więcej szczegółów na temat konfigurowania uwierzytelniania w usłudze Azure App Service, przejrzyj hello przewodnik konfiguracji dla dostawcy tożsamości hello mają toouse:</span><span class="sxs-lookup"><span data-stu-id="a5e12-380">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="a5e12-381">[Jak tooconfigure uwierzytelniania usługi Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="a5e12-381">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="a5e12-382">[Jak tooconfigure uwierzytelniania serwisu Facebook]</span><span class="sxs-lookup"><span data-stu-id="a5e12-382">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="a5e12-383">[Jak tooconfigure uwierzytelniania serwisu Google]</span><span class="sxs-lookup"><span data-stu-id="a5e12-383">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="a5e12-384">[Jak tooconfigure Authentication firmy Microsoft]</span><span class="sxs-lookup"><span data-stu-id="a5e12-384">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="a5e12-385">[Jak tooconfigure uwierzytelniania w usłudze Twitter]</span><span class="sxs-lookup"><span data-stu-id="a5e12-385">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="a5e12-386">Każda tabela ma właściwość dostępu, które mogą być używane toocontrol dostępu toohello tabeli.</span><span class="sxs-lookup"><span data-stu-id="a5e12-386">Each table has an access property that can be used toocontrol access toohello table.</span></span>  <span data-ttu-id="a5e12-387">następujące przykładowe Hello jest wyświetlana tabela statycznie zdefiniowanych wymagane uwierzytelnienie.</span><span class="sxs-lookup"><span data-stu-id="a5e12-387">hello following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="a5e12-388">Hello dostępu do właściwości można wykonać jedną z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="a5e12-388">hello access property can take one of three values</span></span>

* <span data-ttu-id="a5e12-389">*anonimowe* wskazuje, czy aplikacja kliencka hello może tooread danych bez uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="a5e12-389">*anonymous* indicates that hello client application is allowed tooread data without authentication</span></span>
* <span data-ttu-id="a5e12-390">*uwierzytelniony* oznacza, że aplikacja kliencka hello musi wysłany token uwierzytelniania prawidłowe z żądaniem hello</span><span class="sxs-lookup"><span data-stu-id="a5e12-390">*authenticated* indicates that hello client application must send a valid authentication token with hello request</span></span>
* <span data-ttu-id="a5e12-391">*wyłączone* wskazuje, że ta tabela jest obecnie wyłączona</span><span class="sxs-lookup"><span data-stu-id="a5e12-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="a5e12-392">Jeśli zdefiniowano właściwość dostępu hello nieuwierzytelnionym dostępem jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="a5e12-392">If hello access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="a5e12-393"><a name="howto-tables-getidentity"></a>Porady: Użyj uwierzytelniania oświadczeń z tabel</span><span class="sxs-lookup"><span data-stu-id="a5e12-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="a5e12-394">Można skonfigurować różne oświadczenia, które są wymagane podczas konfigurowania uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a5e12-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="a5e12-395">Te oświadczenia nie są zwykle dostępne za pośrednictwem hello `context.user` obiektu.</span><span class="sxs-lookup"><span data-stu-id="a5e12-395">These claims are not normally available through hello `context.user` object.</span></span>  <span data-ttu-id="a5e12-396">Jednak mogą zostać pobrane za pomocą hello `context.user.getIdentity()` metody.</span><span class="sxs-lookup"><span data-stu-id="a5e12-396">However, they can be retrieved using hello `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="a5e12-397">Witaj `getIdentity()` metoda zwraca Promise, który jest rozpoznawany jako obiekt tooan.</span><span class="sxs-lookup"><span data-stu-id="a5e12-397">hello `getIdentity()` method returns a Promise that resolves tooan object.</span></span>  <span data-ttu-id="a5e12-398">Obiekt Hello jest wyznaczaną przez metodę uwierzytelniania (facebook, google, twitter, microsoftaccount lub aad).</span><span class="sxs-lookup"><span data-stu-id="a5e12-398">hello object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="a5e12-399">Na przykład skonfigurować uwierzytelnianie Microsoft Account i oświadczeń adresów e-mail hello żądania, można dodać rekordu toohello adresu e-mail hello z powitania po kontrolera tabeli:</span><span class="sxs-lookup"><span data-stu-id="a5e12-399">For example, if you set up Microsoft Account authentication and request hello email addresses claim, you can add hello email address toohello record with hello following table controller:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="a5e12-400">toosee jakie oświadczenia są dostępne, użyj hello tooview przeglądarki sieci web `/.auth/me` punktu końcowego witryny.</span><span class="sxs-lookup"><span data-stu-id="a5e12-400">toosee what claims are available, use a web browser tooview hello `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="a5e12-401"><a name="howto-tables-disabled"></a>Porady: wyłączanie dostępu toospecific tabeli operacji</span><span class="sxs-lookup"><span data-stu-id="a5e12-401"><a name="howto-tables-disabled"></a>How to: Disable access toospecific table operations</span></span>
<span data-ttu-id="a5e12-402">W tooappearing dodawania tabeli hello hello dostępu do właściwości mogą być używane toocontrol poszczególnych działań.</span><span class="sxs-lookup"><span data-stu-id="a5e12-402">In addition tooappearing on hello table, hello access property can be used toocontrol individual operations.</span></span>  <span data-ttu-id="a5e12-403">Istnieją cztery operacje:</span><span class="sxs-lookup"><span data-stu-id="a5e12-403">There are four operations:</span></span>

* <span data-ttu-id="a5e12-404">*Przeczytaj* jest hello operacji RESTful GET, w tabeli hello</span><span class="sxs-lookup"><span data-stu-id="a5e12-404">*read* is hello RESTful GET operation on hello table</span></span>
* <span data-ttu-id="a5e12-405">*Wstaw* jest operację RESTful POST hello na powitania tabeli</span><span class="sxs-lookup"><span data-stu-id="a5e12-405">*insert* is hello RESTful POST operation on hello table</span></span>
* <span data-ttu-id="a5e12-406">*Zaktualizuj* hello poprawka RESTful operacja jest w tabeli hello</span><span class="sxs-lookup"><span data-stu-id="a5e12-406">*update* is hello RESTful PATCH operation on hello table</span></span>
* <span data-ttu-id="a5e12-407">*Usuń* hello RESTful usunąć operacja jest w tabeli hello</span><span class="sxs-lookup"><span data-stu-id="a5e12-407">*delete* is hello RESTful DELETE operation on hello table</span></span>

<span data-ttu-id="a5e12-408">Na przykład możesz tooprovide nieuwierzytelnione tabeli tylko do odczytu:</span><span class="sxs-lookup"><span data-stu-id="a5e12-408">For example, you may wish tooprovide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="a5e12-409"><a name="howto-tables-query"></a>Porady: dopasowywanie hello kwerendę, która jest używana z operacjami tabeli</span><span class="sxs-lookup"><span data-stu-id="a5e12-409"><a name="howto-tables-query"></a>How to: Adjust hello query that is used with table operations</span></span>
<span data-ttu-id="a5e12-410">Typowe wymagania dotyczące operacji tabeli jest tooprovide ograniczony widok hello danych.</span><span class="sxs-lookup"><span data-stu-id="a5e12-410">A common requirement for table operations is tooprovide a restricted view of hello data.</span></span>  <span data-ttu-id="a5e12-411">Na przykład musisz podać tabelę, która jest oznaczane hello uwierzytelnianego identyfikator użytkownika w taki sposób, że można tylko do odczytu lub aktualizacji własnych.</span><span class="sxs-lookup"><span data-stu-id="a5e12-411">For example, you may provide a table that is tagged with hello authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="a5e12-412">oferuje powitania po definicji tabeli:</span><span class="sxs-lookup"><span data-stu-id="a5e12-412">hello following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="a5e12-413">Operacje, które zwykle wykonać zapytania ma właściwość zapytania, który można dostosować, w której klauzuli.</span><span class="sxs-lookup"><span data-stu-id="a5e12-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="a5e12-414">Właściwość kwerendy Hello jest [QueryJS] obiekt może przetwarzać używane tooconvert toosomething zapytania OData, która hello danych zaplecza.</span><span class="sxs-lookup"><span data-stu-id="a5e12-414">hello query property is a [QueryJS] object that is used tooconvert an OData query toosomething that hello data backend can process.</span></span>  <span data-ttu-id="a5e12-415">W przypadku prostego równości (na przykład hello poprzedzających jeden) można użyć mapy.</span><span class="sxs-lookup"><span data-stu-id="a5e12-415">For simple equality cases (like hello preceding one), a map can be used.</span></span> <span data-ttu-id="a5e12-416">Możesz także dodać punkty SQL:</span><span class="sxs-lookup"><span data-stu-id="a5e12-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="a5e12-417"><a name="howto-tables-softdelete"></a>Porady: Konfigurowanie usuwania nietrwałego dla tabeli</span><span class="sxs-lookup"><span data-stu-id="a5e12-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="a5e12-418">Faktycznie usuwania nietrwałego nie powoduje usunięcia rekordów.</span><span class="sxs-lookup"><span data-stu-id="a5e12-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="a5e12-419">Zamiast tego oznacza je jako usunięte w bazie danych hello przez ustawienie tootrue kolumna usunąć hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-419">Instead it marks them as deleted within hello database by setting hello deleted column tootrue.</span></span>  <span data-ttu-id="a5e12-420">Hello Azure Mobile Apps SDK automatycznie usuwa wszystkie usunięte nietrwale rekordy z wyników, chyba że IncludeDeleted() używa hello zestawu SDK klienta usługi Mobile.</span><span class="sxs-lookup"><span data-stu-id="a5e12-420">hello Azure Mobile Apps SDK automatically removes soft-deleted records from results unless hello Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="a5e12-421">tooconfigure Usuń tabelę dla elastyczne, ustaw hello `softDelete` właściwość w pliku definicji tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="a5e12-421">tooconfigure a table for soft delete, set hello `softDelete` property in hello table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="a5e12-422">Należy określić mechanizm przeczyszczanie rekordów — od aplikacji klienta, za pomocą zadania WebJob, funkcji platformy Azure lub za pomocą niestandardowego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a5e12-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="a5e12-423"><a name="howto-tables-seeding"></a>Porady: inicjatora bazy danych z danymi</span><span class="sxs-lookup"><span data-stu-id="a5e12-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="a5e12-424">Podczas tworzenia nowej aplikacji, warto zapoznać się z tooseed tabelę z danymi.</span><span class="sxs-lookup"><span data-stu-id="a5e12-424">When creating a new application, you may wish tooseed a table with data.</span></span>  <span data-ttu-id="a5e12-425">Można to zrobić w pliku JavaScript w definicji tabeli hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a5e12-425">This can be done within hello table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="a5e12-426">Wstępne wypełnianie danych jest wykonywane tylko po utworzeniu tabeli hello przez hello Azure Mobile Apps SDK.</span><span class="sxs-lookup"><span data-stu-id="a5e12-426">Seeding of data is only done when hello table is created by hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="a5e12-427">Jeśli hello tabela już istnieje w bazie danych hello, żadne dane nie jest dodane do tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-427">If hello table already exists within hello database, no data is injected into hello table.</span></span>  <span data-ttu-id="a5e12-428">Jeśli włączono dynamiczne schematu schematu jest wywnioskować na podstawie danych hello rozpoczęta.</span><span class="sxs-lookup"><span data-stu-id="a5e12-428">If dynamic schema is turned on, then the schema is inferred from hello seeded data.</span></span>

<span data-ttu-id="a5e12-429">Firma Microsoft zaleca jawnie wywołać hello `tables.initialize()` metody toocreate hello tabeli, gdy usługa hello zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="a5e12-429">We recommend that you explicitly call hello `tables.initialize()` method toocreate hello table when hello service starts running.</span></span>

### <span data-ttu-id="a5e12-430"><a name="Swagger"></a>Porady: Włączanie obsługi programu Swagger</span><span class="sxs-lookup"><span data-stu-id="a5e12-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="a5e12-431">Usługa Azure App Service Mobile Apps jest dostarczany z wbudowanych [Swagger] obsługuje.</span><span class="sxs-lookup"><span data-stu-id="a5e12-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="a5e12-432">tooenable pomocy technicznej programu Swagger, najpierw zainstalować hello interfejsu użytkownika programu swagger jako zależność:</span><span class="sxs-lookup"><span data-stu-id="a5e12-432">tooenable Swagger support, first install hello swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="a5e12-433">Po zakończeniu instalacji można włączyć obsługę struktury Swagger w Konstruktorze Azure Mobile Apps hello:</span><span class="sxs-lookup"><span data-stu-id="a5e12-433">Once installed, you can enable Swagger support in hello Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="a5e12-434">Możesz tylko prawdopodobnie chcesz tooenable obsługi struktury Swagger w wersjach programowanie.</span><span class="sxs-lookup"><span data-stu-id="a5e12-434">You probably only want tooenable Swagger support in development editions.</span></span>  <span data-ttu-id="a5e12-435">Można to zrobić przy użyciu `NODE_ENV` ustawienie aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a5e12-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="a5e12-436">Witaj punktu końcowego struktury swagger znajduje się pod adresem http://*yoursite*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="a5e12-436">hello swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="a5e12-437">Dostęp można uzyskać hello interfejs użytkownika programu Swagger za pośrednictwem hello `/swagger/ui` punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="a5e12-437">You can access hello Swagger UI via hello `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="a5e12-438">Jeśli zostanie wybrana opcja uwierzytelniania toorequire w całej aplikacji, struktury Swagger powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="a5e12-438">if you choose toorequire authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="a5e12-439">Aby uzyskać najlepsze wyniki, wybierz tooallow nieuwierzytelniony żądań za pośrednictwem hello uwierzytelniania usługi aplikacji Azure / ustawienia autoryzacji, następnie kontrolować uwierzytelnianie przy użyciu hello `table.access` właściwości.</span><span class="sxs-lookup"><span data-stu-id="a5e12-439">For best results, choose tooallow unauthenticated requests through in hello Azure App Service Authentication / Authorization settings, then control authentication using hello `table.access` property.</span></span>

<span data-ttu-id="a5e12-440">Możesz także dodać hello Swagger opcji tooyour `azureMobile.js` plik, jeśli mają tylko obsługę struktury Swagger podczas opracowywania lokalnie.</span><span class="sxs-lookup"><span data-stu-id="a5e12-440">You can also add hello Swagger option tooyour `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="a5e12-441"><a name="push">Powiadomienia wypychane</span><span class="sxs-lookup"><span data-stu-id="a5e12-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="a5e12-442">Aplikacje mobilne integruje się z tooenable usługi Azure Notification Hubs można toomillions powiadomień wypychanych toosend docelowych urządzeń we wszystkich głównych platform.</span><span class="sxs-lookup"><span data-stu-id="a5e12-442">Mobile Apps integrates with Azure Notification Hubs tooenable you toosend targeted push notifications toomillions of devices across all major platforms.</span></span> <span data-ttu-id="a5e12-443">Przy użyciu usługi Notification Hubs, możesz wysłać wypychania tooiOS powiadomienia, Android i Windows.</span><span class="sxs-lookup"><span data-stu-id="a5e12-443">By using Notification Hubs, you can send push notifications tooiOS, Android and Windows devices.</span></span> <span data-ttu-id="a5e12-444">toolearn więcej informacji na temat wszystkie opcje, które można wykonać przy użyciu usługi Notification Hubs, zobacz [omówienie centra powiadomień](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5e12-444">toolearn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="a5e12-445"></a><a name="send-push"></a>Porady: wysyłanie powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="a5e12-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="a5e12-446">Witaj następującego kodu pokazano, jak toouse hello wypychania obiektu toosend emisji push urządzeń z systemem iOS tooregistered powiadomień:</span><span class="sxs-lookup"><span data-stu-id="a5e12-446">hello following code shows how toouse hello push object toosend a broadcast push notification tooregistered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="a5e12-447">Tworząc rejestracji wypychanych szablonu z powitania klienta, możesz zamiast tego wysłać toodevices wiadomości wypychanych szablonu, na wszystkich obsługiwanych platformach.</span><span class="sxs-lookup"><span data-stu-id="a5e12-447">By creating a template push registration from hello client, you can instead send a template push message toodevices on all supported platforms.</span></span> <span data-ttu-id="a5e12-448">Witaj następującego kodu pokazuje sposób toosend powiadomienie o szablonie:</span><span class="sxs-lookup"><span data-stu-id="a5e12-448">hello following code shows how toosend a template notification:</span></span>

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <span data-ttu-id="a5e12-449"><a name="push-user"></a>Porady: tooan powiadomień wypychanych wysyłania uwierzytelnić użytkownika przy użyciu tagów</span><span class="sxs-lookup"><span data-stu-id="a5e12-449"><a name="push-user"></a>How to: Send push notifications tooan authenticated user using tags</span></span>
<span data-ttu-id="a5e12-450">Uwierzytelniony użytkownik rejestruje dla powiadomień wypychanych, tag identyfikator użytkownika jest automatycznie dodawany toohello rejestracji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-450">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="a5e12-451">Za pomocą tego tagu, możesz wysłać wypychania powiadomień tooall urządzeń zarejestrowanych przez określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a5e12-451">By using this tag, you can send push notifications tooall devices registered by a specific user.</span></span> <span data-ttu-id="a5e12-452">Hello poniższy kod pobiera identyfikator SID użytkownika zgłaszającego żądanie hello hello i wysyła rejestracji urządzenia tooevery powiadomień wypychanych szablon dla tego użytkownika:</span><span class="sxs-lookup"><span data-stu-id="a5e12-452">hello following code gets hello SID of user making hello request and sends a template push notification tooevery device registration for that user:</span></span>

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="a5e12-453">Podczas rejestrowania dla powiadomień wypychanych z uwierzytelnionego klienta, upewnij się, że przed podjęciem próby wykonania rejestracji zakończeniem uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a5e12-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="a5e12-454"><a name="CustomAPI"></a>Niestandardowych interfejsów API</span><span class="sxs-lookup"><span data-stu-id="a5e12-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="a5e12-455"><a name="howto-customapi-basic"></a>Porady: Definiowanie niestandardowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a5e12-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="a5e12-456">Ponadto toohello dostępu do danych interfejsu API za pośrednictwem punktu końcowego /tables hello, Azure Mobile Apps zapewniają niestandardowe pokrycia interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a5e12-456">In addition toohello data access API via hello /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="a5e12-457">Niestandardowych interfejsów API są zdefiniowane w podobne definicji tabeli toohello sposób i uzyskać dostęp do wszystkich hello tego samego urządzenia, włącznie z uwierzytelnianiem.</span><span class="sxs-lookup"><span data-stu-id="a5e12-457">Custom APIs are defined in a similar way toohello table definitions and can access all hello same facilities, including authentication.</span></span>

<span data-ttu-id="a5e12-458">W razie potrzeby toouse aplikacji usługa uwierzytelniania za pomocą API niestandardowe, należy skonfigurować uwierzytelnianie usługi aplikacji w hello [portalu Azure] pierwszy.</span><span class="sxs-lookup"><span data-stu-id="a5e12-458">If you wish toouse App Service Authentication with a Custom API, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="a5e12-459">Dla więcej szczegółów na temat konfigurowania uwierzytelniania w usłudze Azure App Service, przejrzyj hello przewodnik konfiguracji dla dostawcy tożsamości hello mają toouse:</span><span class="sxs-lookup"><span data-stu-id="a5e12-459">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="a5e12-460">[Jak tooconfigure uwierzytelniania usługi Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="a5e12-460">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="a5e12-461">[Jak tooconfigure uwierzytelniania serwisu Facebook]</span><span class="sxs-lookup"><span data-stu-id="a5e12-461">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="a5e12-462">[Jak tooconfigure uwierzytelniania serwisu Google]</span><span class="sxs-lookup"><span data-stu-id="a5e12-462">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="a5e12-463">[Jak tooconfigure Authentication firmy Microsoft]</span><span class="sxs-lookup"><span data-stu-id="a5e12-463">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="a5e12-464">[Jak tooconfigure uwierzytelniania w usłudze Twitter]</span><span class="sxs-lookup"><span data-stu-id="a5e12-464">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="a5e12-465">Niestandardowych interfejsów API są zdefiniowane w taki sam sposób jak hello API tabel hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-465">Custom APIs are defined in much hello same way as hello Tables API.</span></span>

1. <span data-ttu-id="a5e12-466">Utwórz **interfejsu api** katalogu</span><span class="sxs-lookup"><span data-stu-id="a5e12-466">Create an **api** directory</span></span>
2. <span data-ttu-id="a5e12-467">Utwórz plik JavaScript definicji interfejsu API w hello **interfejsu api** katalogu.</span><span class="sxs-lookup"><span data-stu-id="a5e12-467">Create an API definition JavaScript file in hello **api** directory.</span></span>
3. <span data-ttu-id="a5e12-468">Użyj hello importu metody tooimport hello **interfejsu api** katalogu.</span><span class="sxs-lookup"><span data-stu-id="a5e12-468">Use hello import method tooimport hello **api** directory.</span></span>

<span data-ttu-id="a5e12-469">Oto definicji interfejsu api prototypu hello na podstawie próbki basic aplikacji hello, którego użyliśmy wcześniej.</span><span class="sxs-lookup"><span data-stu-id="a5e12-469">Here is hello prototype api definition based on hello basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="a5e12-470">Spójrzmy na przykład interfejs API, który zwraca datę serwera hello przy użyciu hello *Date.now()* metody.</span><span class="sxs-lookup"><span data-stu-id="a5e12-470">Let's take an example API that returns hello server date using hello *Date.now()* method.</span></span>  <span data-ttu-id="a5e12-471">Oto hello api/date.js pliku:</span><span class="sxs-lookup"><span data-stu-id="a5e12-471">Here is hello api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="a5e12-472">Każdy parametr jest jednym z hello RESTful zleceń standardowych - GET, POST, poprawki lub DELETE.</span><span class="sxs-lookup"><span data-stu-id="a5e12-472">Each parameter is one of hello standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="a5e12-473">Metoda Hello jest standardem [oprogramowanie pośredniczące ExpressJS] funkcji, który wysyła dane wyjściowe hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="a5e12-473">hello method is a standard [ExpressJS Middleware] function that sends hello required output.</span></span>

### <span data-ttu-id="a5e12-474"><a name="howto-customapi-auth"></a>Porady: Wymagaj uwierzytelniania niestandardowego interfejsu API tooa dostępu</span><span class="sxs-lookup"><span data-stu-id="a5e12-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access tooa custom API</span></span>
<span data-ttu-id="a5e12-475">Azure Mobile Apps SDK implementuje uwierzytelnianie w hello tak samo dla punktu końcowego tabel hello i niestandardowych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a5e12-475">Azure Mobile Apps SDK implements authentication in hello same way for both hello tables endpoint and custom APIs.</span></span>  <span data-ttu-id="a5e12-476">Aby dodać utworzonych w poprzedniej sekcji hello API toohello uwierzytelnianie, Dodaj **dostępu** właściwości:</span><span class="sxs-lookup"><span data-stu-id="a5e12-476">To add authentication toohello API developed in hello previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="a5e12-477">Można również określić uwierzytelniania na określonych operacji:</span><span class="sxs-lookup"><span data-stu-id="a5e12-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="a5e12-478">Witaj tego samego tokenu, który jest używany dla punktu końcowego tabel hello należy użyć dla niestandardowych interfejsów API wymaga uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a5e12-478">hello same token that is used for hello tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="a5e12-479"><a name="howto-customapi-auth"></a>Porady: Obsługa wysyłania dużych plików</span><span class="sxs-lookup"><span data-stu-id="a5e12-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="a5e12-480">Azure Mobile Apps SDK używa hello [oprogramowanie pośredniczące analizator treści](https://github.com/expressjs/body-parser) tooaccept i dekodowania zawartości w treści w Twoje zgłoszenie.</span><span class="sxs-lookup"><span data-stu-id="a5e12-480">Azure Mobile Apps SDK uses hello [body-parser middleware](https://github.com/expressjs/body-parser) tooaccept and decode body content in your submission.</span></span>  <span data-ttu-id="a5e12-481">Można wstępnie skonfigurować przekazywania plików większych tooaccept analizator treści:</span><span class="sxs-lookup"><span data-stu-id="a5e12-481">You can pre-configure body-parser tooaccept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="a5e12-482">Plik Hello jest algorytmem przed transmisją base-64.</span><span class="sxs-lookup"><span data-stu-id="a5e12-482">hello file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="a5e12-483">Zwiększa to hello rozmiar rzeczywisty przekazywania hello (i dlatego hello rozmiar, które należy uwzględnić).</span><span class="sxs-lookup"><span data-stu-id="a5e12-483">This increases hello size of hello actual upload (and hence hello size you must account for).</span></span>

### <span data-ttu-id="a5e12-484"><a name="howto-customapi-sql"></a>Porady: wykonanie niestandardowych instrukcje SQL</span><span class="sxs-lookup"><span data-stu-id="a5e12-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="a5e12-485">Hello zestaw SDK usługi Azure Mobile Apps umożliwia toohello dostęp do całego kontekstu za pośrednictwem obiektu żądania hello, dzięki czemu tooexecute sparametryzowana łatwo dostawcy danych toohello instrukcji SQL:</span><span class="sxs-lookup"><span data-stu-id="a5e12-485">hello Azure Mobile Apps SDK allows access toohello entire Context through hello request object, allowing you tooexecute parameterized SQL statements toohello defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="a5e12-486"><a name="Debugging"></a>Debugowanie, łatwe tabel i łatwe interfejsów API</span><span class="sxs-lookup"><span data-stu-id="a5e12-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="a5e12-487"><a name="howto-diagnostic-logs"></a>Porady: debugowanie, diagnozowanie i rozwiązywanie problemów z usługi Azure Mobile apps</span><span class="sxs-lookup"><span data-stu-id="a5e12-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="a5e12-488">Hello Azure App Service zapewnia kilka debugowania i rozwiązywanie problemów z techniki aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="a5e12-488">hello Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="a5e12-489">Można znaleźć toohello następujące artykuły tooget uruchomione przy rozwiązywaniu problemów z poziomu zaplecza Node.js Mobile:</span><span class="sxs-lookup"><span data-stu-id="a5e12-489">Refer toohello following articles tooget started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="a5e12-490">[Monitorowanie usługi aplikacji Azure]</span><span class="sxs-lookup"><span data-stu-id="a5e12-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="a5e12-491">[Włączanie rejestrowania diagnostycznego w usłudze aplikacji Azure]</span><span class="sxs-lookup"><span data-stu-id="a5e12-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="a5e12-492">[Rozwiązywanie problemów z usługi aplikacji Azure w programie Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a5e12-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="a5e12-493">Aplikacje środowiska node.js mają dostęp tooa szeroką gamę narzędzi diagnostycznych dziennika.</span><span class="sxs-lookup"><span data-stu-id="a5e12-493">Node.js applications have access tooa wide range of diagnostic log tools.</span></span>  <span data-ttu-id="a5e12-494">Wewnętrznie hello korzysta z zestawu SDK usługi Azure Mobile Apps Node.js [Winston] dla rejestrowania diagnostycznego.</span><span class="sxs-lookup"><span data-stu-id="a5e12-494">Internally, hello Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="a5e12-495">Rejestrowanie jest automatycznie włączone, należy włączyć tryb debugowania lub przez ustawienie hello **MS_DebugMode** tootrue ustawienie aplikacji w hello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="a5e12-495">Logging is automatically enabled by enabling debug mode or by setting hello **MS_DebugMode** app setting tootrue in hello [Azure portal].</span></span> <span data-ttu-id="a5e12-496">Dzienniki generowane są wyświetlane w hello dzienników diagnostycznych na powitania [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="a5e12-496">Generated logs appear in hello Diagnostic Logs on hello [Azure portal].</span></span>

### <span data-ttu-id="a5e12-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Porady: Praca z tabelami łatwy w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a5e12-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in hello Azure portal</span></span>
<span data-ttu-id="a5e12-498">Łatwe tabel w portalu hello umożliwiają tworzenie i Praca z tabelami bezpośrednio w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-498">Easy Tables in hello portal let you create and work with tables right in hello portal.</span></span> <span data-ttu-id="a5e12-499">Operacje tabeli za pomocą edytora usługi aplikacji hello nawet można edytować.</span><span class="sxs-lookup"><span data-stu-id="a5e12-499">You can even edit table operations using hello App Service Editor.</span></span>

<span data-ttu-id="a5e12-500">Po kliknięciu **łatwe tabel** w ustawieniach wewnętrznej bazy danych lokacji można Dodawanie, modyfikowanie lub usuwanie tabeli.</span><span class="sxs-lookup"><span data-stu-id="a5e12-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="a5e12-501">Można również sprawdzić dane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-501">You can also see data in hello table.</span></span>

![Praca z tabelami łatwe](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="a5e12-503">Hello są dostępne na pasku poleceń hello tabeli następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="a5e12-503">hello following commands are available on hello command bar for a table:</span></span>

* <span data-ttu-id="a5e12-504">**Zmienianie uprawnień** — zmodyfikować hello uprawnienie do odczytu, wstawianie, aktualizowanie i usuwanie operacji względem tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-504">**Change permissions** - modify hello permission for read, insert, update and delete operations on hello table.</span></span>
  <span data-ttu-id="a5e12-505">Dostępne są opcje tooallow dostępu anonimowego, uwierzytelniania toorequire lub toodisable wszystkie dostępu toohello operacji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-505">Options are tooallow anonymous access, toorequire authentication, or toodisable all access toohello operation.</span></span>
* <span data-ttu-id="a5e12-506">**Edytowanie skryptu** -hello pliku skryptu tabeli hello jest otwarty w hello Edytor usług aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-506">**Edit script** - hello script file for hello table is opened in hello App Service Editor.</span></span>
* <span data-ttu-id="a5e12-507">**Zarządzanie schematem** — Dodawanie lub usuwanie kolumn lub zmienianie hello indeksu tabeli.</span><span class="sxs-lookup"><span data-stu-id="a5e12-507">**Manage schema** - add or delete columns or change hello table index.</span></span>
* <span data-ttu-id="a5e12-508">**Wyczyść tabeli** -obcina istniejącej tabeli jest usunięcie wszystkich wierszy danych, ale pozostawienie schematu hello bez zmian.</span><span class="sxs-lookup"><span data-stu-id="a5e12-508">**Clear table** - truncates an existing table be deleting all data rows but leaving hello schema unchanged.</span></span>
* <span data-ttu-id="a5e12-509">**Usuwanie wierszy** -Usuń poszczególne wiersze danych.</span><span class="sxs-lookup"><span data-stu-id="a5e12-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="a5e12-510">**Wyświetl podgląd dzienników przesyłanych strumieniowo** -łączy toohello przesyłania strumieniowego usługi rejestrowania dla witryny.</span><span class="sxs-lookup"><span data-stu-id="a5e12-510">**View streaming logs** - connects you toohello streaming log service for your site.</span></span>

### <span data-ttu-id="a5e12-511"><a name="work-easy-apis"></a>Porady: pracy z interfejsami API łatwy w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a5e12-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in hello Azure portal</span></span>
<span data-ttu-id="a5e12-512">Łatwe interfejsów API w portalu hello umożliwiają tworzenie i Praca z niestandardowych bezpośrednio interfejsy API w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-512">Easy APIs in hello portal let you create and work with custom APIs right in hello portal.</span></span> <span data-ttu-id="a5e12-513">Można edytować skrypty interfejsu API przy użyciu hello Edytor usług aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-513">You can edit API scripts using hello App Service Editor.</span></span>

<span data-ttu-id="a5e12-514">Po kliknięciu **łatwe interfejsów API** w ustawieniach wewnętrznej bazy danych lokacji można Dodawanie, modyfikowanie lub usuwanie niestandardowych punkt końcowy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a5e12-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Praca z łatwe interfejsów API](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="a5e12-516">W portalu hello można zmienić hello uprawnienia dostępu dla danej akcji HTTP, Edytuj plik skryptu interfejsu API hello w edytorze usługi aplikacji lub Wyświetl dzienniki przesyłania strumieniowego hello.</span><span class="sxs-lookup"><span data-stu-id="a5e12-516">In hello portal, you can change hello access permissions for a given HTTP action, edit hello API script file in the App Service Editor, or view hello streaming logs.</span></span>

### <span data-ttu-id="a5e12-517"><a name="online-editor"></a>Porady: edytowanie kodu hello Edytor usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="a5e12-517"><a name="online-editor"></a>How to: Edit code in hello App Service Editor</span></span>
<span data-ttu-id="a5e12-518">Hello portalu Azure umożliwia edytowanie plików skryptów zaplecza Node.js w hello Edytor usług aplikacji bez konieczności pobierania hello komputera lokalnego tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="a5e12-518">hello Azure portal lets you edit your Node.js backend script files in hello App Service Editor without having to download hello project tooyour local computer.</span></span> <span data-ttu-id="a5e12-519">pliki skryptów tooedit hello edytora online:</span><span class="sxs-lookup"><span data-stu-id="a5e12-519">tooedit script files in hello online editor:</span></span>

1. <span data-ttu-id="a5e12-520">W bloku zaplecza aplikacji mobilnej, kliknij **wszystkie ustawienia** > albo **łatwe tabel** lub **łatwe interfejsów API**, kliknij tabelę lub interfejsu API, a następnie kliknij przycisk **edytowanie skryptu**.</span><span class="sxs-lookup"><span data-stu-id="a5e12-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="a5e12-521">plik skryptu Hello jest otwarty w hello Edytor usług aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a5e12-521">hello script file is opened in hello App Service Editor.</span></span>

    ![Edytor usługi aplikacji](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="a5e12-523">Tworzenie pliku kodu toohello zmiany w hello edytora online.</span><span class="sxs-lookup"><span data-stu-id="a5e12-523">Make your changes toohello code file in hello online editor.</span></span> <span data-ttu-id="a5e12-524">Zmiany zostaną zapisane automatycznie podczas pisania.</span><span class="sxs-lookup"><span data-stu-id="a5e12-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Szybki Start kliencką dla systemu android]: app-service-mobile-android-get-started.md
[Apache Cordova klienta — Szybki Start]: app-service-mobile-cordova-get-started.md
[iOS — Szybki Start klienta]: app-service-mobile-ios-get-started.md
[Szybki Start klienta platformy Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md
[Szybki Start klienta platformy Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md
[Szybki Start klienta platformy Xamarin.Forms]: app-service-mobile-xamarin-forms-get-started.md
[Szybki Start klienta Sklepu Windows]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[synchronizacji danych w trybie offline]: app-service-mobile-offline-data-sync.md
[Jak tooconfigure uwierzytelniania usługi Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Jak tooconfigure uwierzytelniania serwisu Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md
[Jak tooconfigure uwierzytelniania serwisu Google]: app-service-mobile-how-to-configure-google-authentication.md
[Jak tooconfigure Authentication firmy Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Jak tooconfigure uwierzytelniania w usłudze Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md
[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md
[Monitorowanie usługi aplikacji Azure]: ../app-service-web/web-sites-monitor.md
[Włączanie rejestrowania diagnostycznego w usłudze aplikacji Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Rozwiązywanie problemów z usługi aplikacji Azure w programie Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[Określ hello wersji węzła]: ../nodejs-specify-node-version-azure-apps.md
[Użyj modułów węzła]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[portalu Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp przykładem w witrynie GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo przykładem w witrynie GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[katalogu przykładów w witrynie GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 dla programu Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js pakietu]: https://www.npmjs.com/package/mssql
[programu Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[oprogramowanie pośredniczące ExpressJS]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
