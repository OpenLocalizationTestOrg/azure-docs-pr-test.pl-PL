---
title: "Jak pracować z serwera wewnętrznej bazy danych Node.js SDK dla aplikacji mobilnych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak pracować z serwera wewnętrznej bazy danych Node.js SDK dla usługi Azure App Service Mobile Apps."
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
ms.openlocfilehash: 1d3aa7a0089279a8eafeb0ded951a5238e189eaa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="43a83-103">Jak używać zestawu SDK usługi Azure Mobile Apps Node.js</span><span class="sxs-lookup"><span data-stu-id="43a83-103">How to use the Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="43a83-104">Ten artykuł zawiera szczegółowe informacje i przykłady przedstawiający sposób pracy z zaplecza Node.js w usłudze Azure App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="43a83-104">This article provides detailed information and examples showing how to work with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="43a83-105"><a name="Introduction"></a>Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="43a83-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="43a83-106">Usługa Azure App Service Mobile Apps oferuje możliwość dodawania danych zoptymalizowanych pod kątem mobile dostępu do interfejsu API sieci Web do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="43a83-106">Azure App Service Mobile Apps provides the capability to add a mobile-optimized data access Web API to a web application.</span></span>  <span data-ttu-id="43a83-107">Zestaw SDK aplikacji mobilnych usługi aplikacji Azure jest dostępna dla aplikacji sieci web ASP.NET i Node.js.</span><span class="sxs-lookup"><span data-stu-id="43a83-107">The Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="43a83-108">Zestaw SDK udostępnia następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="43a83-108">The SDK provides the following operations:</span></span>

* <span data-ttu-id="43a83-109">Operacje tabeli (Odczyt, Insert, Update, Delete) dla dostępu do danych</span><span class="sxs-lookup"><span data-stu-id="43a83-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="43a83-110">Operacje niestandardowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="43a83-110">Custom API operations</span></span>

<span data-ttu-id="43a83-111">Obie operacje zapewnienia uwierzytelniania przez wszystkich dostawców tożsamości dozwolone w usłudze Azure App Service, w tym dostawców tożsamości społecznościowych, takich jak Facebook, Twitter, Google i Microsoft, jak również usługi Azure Active Directory dla tożsamości organizacji.</span><span class="sxs-lookup"><span data-stu-id="43a83-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="43a83-112">Przykłady można znaleźć do każdego przypadku użycia w [katalogu przykładów w witrynie GitHub].</span><span class="sxs-lookup"><span data-stu-id="43a83-112">You can find samples for each use case in the [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="43a83-113">Obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="43a83-113">Supported Platforms</span></span>
<span data-ttu-id="43a83-114">Zestaw SDK usługi Azure Mobile Apps węzła obsługuje bieżącej wersji LTS węzła i nowszych.</span><span class="sxs-lookup"><span data-stu-id="43a83-114">The Azure Mobile Apps Node SDK supports the current LTS release of Node and later.</span></span>  <span data-ttu-id="43a83-115">Począwszy od zapisu, najnowsza wersja LTS jest v4.5.0 węzła.</span><span class="sxs-lookup"><span data-stu-id="43a83-115">As of writing, the latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="43a83-116">Inne wersje węzeł może działać, ale nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="43a83-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="43a83-117">Zestaw SDK usługi Azure Mobile Apps węzła obsługuje dwa sterowniki bazy danych — sterownik mssql węzła obsługuje SQL Azure i lokalnego wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="43a83-117">The Azure Mobile Apps Node SDK supports two database drivers - the node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="43a83-118">Sterownik sqlite3 obsługuje tylko jedno wystąpienie bazy danych SQLite.</span><span class="sxs-lookup"><span data-stu-id="43a83-118">The sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="43a83-119"><a name="howto-cmdline-basicapp"></a>Porady: tworzenie zaplecza Node.js podstawowe przy użyciu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="43a83-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using the Command Line</span></span>
<span data-ttu-id="43a83-120">Jako aplikacja ExpressJS rozpoczyna się co wewnętrznej bazy danych usługi Azure App Service Mobile aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="43a83-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="43a83-121">ExpressJS jest dostępna dla środowiska Node.js struktury usługi najpopularniejszych sieci web.</span><span class="sxs-lookup"><span data-stu-id="43a83-121">ExpressJS is the most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="43a83-122">Można utworzyć basic [Express] aplikacji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="43a83-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="43a83-123">Polecenie lub oknie programu PowerShell należy utworzyć katalog w projekcie.</span><span class="sxs-lookup"><span data-stu-id="43a83-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="43a83-124">Uruchom npm inicjowania zainicjować struktury pakietu.</span><span class="sxs-lookup"><span data-stu-id="43a83-124">Run npm init to initialize the package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="43a83-125">Polecenie init npm zapyta zestaw pytań można zainicjować projektu.</span><span class="sxs-lookup"><span data-stu-id="43a83-125">The npm init command asks a set of questions to initialize the project.</span></span>  <span data-ttu-id="43a83-126">Zobacz przykład danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="43a83-126">See the example output:</span></span>

    ![Dane wyjściowe init npm][0]
3. <span data-ttu-id="43a83-128">Zainstaluj biblioteki express i aplikacje w przypadku mobilne platformy azure z repozytorium npm.</span><span class="sxs-lookup"><span data-stu-id="43a83-128">Install the express and azure-mobile-apps libraries from the npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="43a83-129">Tworzenie pliku app.js do zaimplementowania podstawowego serwera przenośnych.</span><span class="sxs-lookup"><span data-stu-id="43a83-129">Create an app.js file to implement the basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="43a83-130">Ta aplikacja tworzy zoptymalizowanych pod kątem mobile WebAPI z jednym punktem końcowym (`/tables/TodoItem`) który nieuwierzytelnionym udostępnia odpowiedni magazyn danych SQL przy użyciu dynamicznych schematu.</span><span class="sxs-lookup"><span data-stu-id="43a83-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access to an underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="43a83-131">Jest ona odpowiednia dla następującego Szybki Start biblioteki klienta:</span><span class="sxs-lookup"><span data-stu-id="43a83-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="43a83-132">[Szybki Start kliencką dla systemu android]</span><span class="sxs-lookup"><span data-stu-id="43a83-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="43a83-133">[Apache Cordova klienta — Szybki Start]</span><span class="sxs-lookup"><span data-stu-id="43a83-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="43a83-134">[iOS — Szybki Start klienta]</span><span class="sxs-lookup"><span data-stu-id="43a83-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="43a83-135">[Szybki Start klienta Sklepu Windows]</span><span class="sxs-lookup"><span data-stu-id="43a83-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="43a83-136">[Szybki Start klienta platformy Xamarin.iOS]</span><span class="sxs-lookup"><span data-stu-id="43a83-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="43a83-137">[Szybki Start klienta platformy Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="43a83-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="43a83-138">[Szybki Start klienta platformy Xamarin.Forms]</span><span class="sxs-lookup"><span data-stu-id="43a83-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="43a83-139">Możesz znaleźć kod dla tej aplikacji w warstwie podstawowa w [basicapp przykładem w witrynie GitHub].</span><span class="sxs-lookup"><span data-stu-id="43a83-139">You can find the code for this basic application in the [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="43a83-140"><a name="howto-vs2015-basicapp"></a>Porady: tworzenie zaplecza węzła z programem Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="43a83-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="43a83-141">Visual Studio 2015 wymaga rozszerzenia do tworzenia aplikacji Node.js w środowisku IDE.</span><span class="sxs-lookup"><span data-stu-id="43a83-141">Visual Studio 2015 requires an extension to develop Node.js applications within the IDE.</span></span>  <span data-ttu-id="43a83-142">Aby rozpocząć, zainstaluj [Node.js Tools 1.1 dla programu Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="43a83-142">To start, install the [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="43a83-143">Po zainstalowaniu narzędzia Node.js dla programu Visual Studio tworzy aplikację 4.x Express:</span><span class="sxs-lookup"><span data-stu-id="43a83-143">Once the Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="43a83-144">Otwórz **nowy projekt** okna dialogowego (z **pliku** > **nowy** > **projektu...** ).</span><span class="sxs-lookup"><span data-stu-id="43a83-144">Open the **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="43a83-145">Rozwiń węzeł **szablony** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="43a83-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="43a83-146">Wybierz **aplikacji podstawowe Azure Node.js Express 4**.</span><span class="sxs-lookup"><span data-stu-id="43a83-146">Select the **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="43a83-147">Wprowadź nazwę projektu.</span><span class="sxs-lookup"><span data-stu-id="43a83-147">Fill in the project name.</span></span>  <span data-ttu-id="43a83-148">Kliknij przycisk *OK*.</span><span class="sxs-lookup"><span data-stu-id="43a83-148">Click *OK*.</span></span>

    ![Nowy projekt programu Visual Studio 2015][1]
5. <span data-ttu-id="43a83-150">Kliknij prawym przyciskiem myszy **npm** a następnie wybierz węzeł **zainstalować nowych pakietów npm...** .</span><span class="sxs-lookup"><span data-stu-id="43a83-150">Right-click the **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="43a83-151">Należy odświeżyć katalog npm na tworzenie pierwszej aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="43a83-151">You may need to refresh the npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="43a83-152">Kliknij przycisk **Odśwież** w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="43a83-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="43a83-153">Wprowadź *apps w usłudze azure-mobile* w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="43a83-153">Enter *azure-mobile-apps* in the search box.</span></span>  <span data-ttu-id="43a83-154">Kliknij przycisk **usługi azure mobile apps 2.0.0** pakietu, a następnie kliknij przycisk **zainstaluj pakiet**.</span><span class="sxs-lookup"><span data-stu-id="43a83-154">Click the **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Zainstaluj nowych pakietów npm][2]
8. <span data-ttu-id="43a83-156">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="43a83-156">Click **Close**.</span></span>
9. <span data-ttu-id="43a83-157">Otwórz *app.js* plik, aby dodać obsługę zestaw SDK usługi Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="43a83-157">Open the *app.js* file to add support for the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="43a83-158">W wierszu 6 at dolnej części biblioteki wymagają instrukcje, Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="43a83-158">At line 6 at the bottom of the library require statements, add the following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="43a83-159">W wierszu około 27 po innych instrukcji app.use Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="43a83-159">At approximately line 27 after the other app.use statements, add the following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="43a83-160">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="43a83-160">Save the file.</span></span>
10. <span data-ttu-id="43a83-161">Uruchom aplikację lokalnie (interfejs API jest obsługiwana na http://localhost: 3000) lub publikowanie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="43a83-161">Either run the application locally (the API is served on http://localhost:3000) or publish to Azure.</span></span>

### <span data-ttu-id="43a83-162"><a name="create-node-backend-portal"></a>Porady: tworzenie zaplecza Node.js przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="43a83-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using the Azure portal</span></span>
<span data-ttu-id="43a83-163">Można tworzyć w prawej zaplecza aplikacji mobilnej [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="43a83-163">You can create a Mobile App backend right in the [Azure portal].</span></span> <span data-ttu-id="43a83-164">Można wykonać następujące czynności lub utworzyć klienta i serwera razem [tworzenie aplikacji mobilnej](app-service-mobile-ios-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="43a83-164">You can either follow the following steps or create a client and server together by following the [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="43a83-165">Samouczek zawiera uproszczonej wersji tych instrukcji i najlepiej stosować do weryfikacji koncepcji projektów.</span><span class="sxs-lookup"><span data-stu-id="43a83-165">The tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="43a83-166">W *wprowadzenie* bloku, w obszarze **Utwórz tabelę interfejsu API**, wybierz **Node.js** jako sieci **język wewnętrznej bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="43a83-166">Back in the *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="43a83-167">Pole wyboru dla "**potwierdzam, że spowoduje to zastąpienie wszystkich lokacji zawartości.**", następnie kliknij przycisk **Utwórz tabelę TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="43a83-167">Check the box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="43a83-168"><a name="download-quickstart"></a>Porady: pobieranie projekt kodu szybkiego startu zaplecza Node.js przy użyciu narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="43a83-168"><a name="download-quickstart"></a>How to: Download the Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="43a83-169">Po utworzeniu zaplecza aplikacji mobilnej Node.js przy użyciu portalu **szybki start** bloku projektu Node.js jest utworzony i wdrożone do tej witryny.</span><span class="sxs-lookup"><span data-stu-id="43a83-169">When you create a Node.js Mobile App backend by using the portal **Quick start** blade, a Node.js project is created for you and deployed to your site.</span></span> <span data-ttu-id="43a83-170">Można dodać tabele i interfejsów API i edytować pliki kodu dla zaplecza Node.js w portalu.</span><span class="sxs-lookup"><span data-stu-id="43a83-170">You can add tables and APIs and edit code files for the Node.js backend in the portal.</span></span> <span data-ttu-id="43a83-171">Aby pobrać projektu wewnętrznej bazy danych, dzięki czemu można dodać lub zmodyfikować tabele i interfejsów API, a następnie ponownie opublikować projekt umożliwia także różne narzędzia wdrażania.</span><span class="sxs-lookup"><span data-stu-id="43a83-171">You can also use various deployment tools to download the backend project so that you can add or modify tables and APIs, then republish the project.</span></span> <span data-ttu-id="43a83-172">Aby uzyskać więcej informacji, zobacz [Azure App Service Deployment Guide].</span><span class="sxs-lookup"><span data-stu-id="43a83-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="43a83-173">Poniższa procedura wykorzystuje repozytorium Git do pobierania kodu projektu Szybki Start.</span><span class="sxs-lookup"><span data-stu-id="43a83-173">the following procedure uses a Git repository to download the quickstart project code.</span></span>

1. <span data-ttu-id="43a83-174">Zainstaluj usługę Git, jeśli jeszcze tego nie zrobiono.</span><span class="sxs-lookup"><span data-stu-id="43a83-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="43a83-175">Kroki wymagane do zainstalowania Git się różnić między systemami operacyjnymi.</span><span class="sxs-lookup"><span data-stu-id="43a83-175">The steps required to install Git vary between operating systems.</span></span> <span data-ttu-id="43a83-176">Zobacz [instalowanie Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) dystrybucje systemu operacyjnego i instalacji.</span><span class="sxs-lookup"><span data-stu-id="43a83-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="43a83-177">Postępuj zgodnie z instrukcjami [włączyć repozytorium aplikacji usługi App Service](../app-service-web/app-service-deploy-local-git.md#Step3) umożliwiające repozytorium Git dla witryny sieci wewnętrznej bazy danych, co Uwaga wdrożenia nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="43a83-177">Follow the steps in [Enable the App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) to enable the Git repository for your backend site, making a note of the deployment username and password.</span></span>
3. <span data-ttu-id="43a83-178">W bloku dla zaplecza aplikacji mobilnej, zanotuj **adres URL klonowania Git** ustawienie.</span><span class="sxs-lookup"><span data-stu-id="43a83-178">In the blade for your Mobile App backend, make a note of the **Git clone URL** setting.</span></span>
4. <span data-ttu-id="43a83-179">Wykonanie `git clone` polecenia przy użyciu narzędzia Git clone adres URL, wprowadzania hasła, gdy jest to wymagane, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="43a83-179">Execute the `git clone` command using the Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="43a83-180">Przejdź do katalogu lokalnego, co w poprzednim przykładzie jest /todolist i zwróć uwagę, że pliki projektu zostały pobrane.</span><span class="sxs-lookup"><span data-stu-id="43a83-180">Browse to local directory, which in the preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="43a83-181">Zlokalizuj `todoitem.json` w pliku `/tables` katalogu.</span><span class="sxs-lookup"><span data-stu-id="43a83-181">Locate the `todoitem.json` file in the `/tables` directory.</span></span>  <span data-ttu-id="43a83-182">Ten plik definiuje uprawnienia w tabeli.</span><span class="sxs-lookup"><span data-stu-id="43a83-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="43a83-183">Jest także `todoitem.js` pliku w tym samym katalogu, który definiuje tej operacji CRUD skrypty dla tabeli.</span><span class="sxs-lookup"><span data-stu-id="43a83-183">Also find the `todoitem.js` file in the same directory, which defines that CRUD operation scripts for the table.</span></span>
6. <span data-ttu-id="43a83-184">Po wprowadzeniu zmian w plikach projektu, wykonaj następujące polecenia, aby dodać, zatwierdzić, a następnie przekazać zmiany do witryny:</span><span class="sxs-lookup"><span data-stu-id="43a83-184">After you have made changes to project files, execute the following commands to add, commit, then upload the changes to the site:</span></span>

        $ git commit -m "updated the table script"
        $ git push origin master

    <span data-ttu-id="43a83-185">Po dodaniu nowych plików do projektu, należy najpierw wykonać `git add .` polecenia.</span><span class="sxs-lookup"><span data-stu-id="43a83-185">When you add new files to the project, you first need to execute the `git add .` command.</span></span>

<span data-ttu-id="43a83-186">Opublikowaniu lokacji za każdym razem, gdy nowy zestaw zatwierdzeń zostanie przypisany do lokacji.</span><span class="sxs-lookup"><span data-stu-id="43a83-186">The site is republished every time a new set of commits is pushed to the site.</span></span>

### <span data-ttu-id="43a83-187"><a name="howto-publish-to-azure"></a>Porady: publikowanie zaplecza Node.js na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="43a83-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend to Azure</span></span>
<span data-ttu-id="43a83-188">Microsoft Azure udostępnia wiele mechanizmów publikowania z wewnętrzną bazą danych Azure App Service Mobile aplikacji Node.js w usłudze platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="43a83-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to the Azure service.</span></span>  <span data-ttu-id="43a83-189">Obejmują one przy użyciu narzędzia wdrażania zintegrowane w programie Visual Studio, narzędzia wiersza polecenia i opcje ciągłego wdrażania w oparciu o kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="43a83-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="43a83-190">Aby uzyskać więcej informacji na ten temat, zobacz [Azure App Service Deployment Guide].</span><span class="sxs-lookup"><span data-stu-id="43a83-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="43a83-191">Usługa aplikacji Azure ma poradę należy zapoznać się przed przystąpieniem do wdrażania aplikacji Node.js:</span><span class="sxs-lookup"><span data-stu-id="43a83-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="43a83-192">Jak [Określ wersję węzła]</span><span class="sxs-lookup"><span data-stu-id="43a83-192">How to [specify the Node Version]</span></span>
* <span data-ttu-id="43a83-193">Jak [Użyj modułów węzła]</span><span class="sxs-lookup"><span data-stu-id="43a83-193">How to [use Node modules]</span></span>

### <span data-ttu-id="43a83-194"><a name="howto-enable-homepage"></a>Porady: Włączanie strony głównej aplikacji</span><span class="sxs-lookup"><span data-stu-id="43a83-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="43a83-195">Wiele aplikacji są kombinacją sieci web i aplikacji mobilnych i ExpressJS framework pozwala na połączenie dwóch zestawów reguł.</span><span class="sxs-lookup"><span data-stu-id="43a83-195">Many applications are a combination of web and mobile apps and the ExpressJS framework allows you to combine the two facets.</span></span>  <span data-ttu-id="43a83-196">Czasami jednak warto tylko zaimplementować interfejs przenośnych.</span><span class="sxs-lookup"><span data-stu-id="43a83-196">Sometimes, however, you may wish to only implement a mobile interface.</span></span>  <span data-ttu-id="43a83-197">Należy zapewnić strony docelowej, aby upewnić się, usługi app service jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="43a83-197">It is useful to provide a landing page to ensure the app service is up and running.</span></span>  <span data-ttu-id="43a83-198">Można podać strony głównej lub włączyć tymczasowe strony głównej.</span><span class="sxs-lookup"><span data-stu-id="43a83-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="43a83-199">Aby włączyć tymczasowe strony głównej, należy użyć następującego można utworzyć wystąpienia usługi Azure Mobile Apps:</span><span class="sxs-lookup"><span data-stu-id="43a83-199">To enable a temporary home page, use the following to instantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="43a83-200">Jeśli mają tylko tej opcji, które są dostępne podczas tworzenia lokalnie, możesz dodać to ustawienie, aby Twoje `azureMobile.js` pliku.</span><span class="sxs-lookup"><span data-stu-id="43a83-200">If you only want this option available when developing locally, you can add this setting to your `azureMobile.js` file.</span></span>

## <span data-ttu-id="43a83-201"><a name="TableOperations"></a>Operacje tabeli</span><span class="sxs-lookup"><span data-stu-id="43a83-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="43a83-202">Aplikacje azure-mobile Node.js Server SDK zawiera mechanizmy do udostępnienia tabel danych przechowywanych w bazie danych SQL Azure jako WebAPI.</span><span class="sxs-lookup"><span data-stu-id="43a83-202">The azure-mobile-apps Node.js Server SDK provides mechanisms to expose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="43a83-203">Podano pięć operacji.</span><span class="sxs-lookup"><span data-stu-id="43a83-203">Five operations are provided.</span></span>

| <span data-ttu-id="43a83-204">Operacja</span><span class="sxs-lookup"><span data-stu-id="43a83-204">Operation</span></span> | <span data-ttu-id="43a83-205">Opis</span><span class="sxs-lookup"><span data-stu-id="43a83-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="43a83-206">GET /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="43a83-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="43a83-207">Pobierz wszystkie rekordy w tabeli</span><span class="sxs-lookup"><span data-stu-id="43a83-207">Get all records in the table</span></span> |
| <span data-ttu-id="43a83-208">GET /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="43a83-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="43a83-209">Pobierz określonego rekordu w tabeli</span><span class="sxs-lookup"><span data-stu-id="43a83-209">Get a specific record in the table</span></span> |
| <span data-ttu-id="43a83-210">POST /tables/*tablename*</span><span class="sxs-lookup"><span data-stu-id="43a83-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="43a83-211">Utwórz rekord w tabeli</span><span class="sxs-lookup"><span data-stu-id="43a83-211">Create a record in the table</span></span> |
| <span data-ttu-id="43a83-212">POPRAWKA /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="43a83-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="43a83-213">Aktualizacja rekordu w tabeli</span><span class="sxs-lookup"><span data-stu-id="43a83-213">Update a record in the table</span></span> |
| <span data-ttu-id="43a83-214">Usuń /tables/*tablename*/:id</span><span class="sxs-lookup"><span data-stu-id="43a83-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="43a83-215">Usuwanie rekordu w tabeli</span><span class="sxs-lookup"><span data-stu-id="43a83-215">Delete a record in the table</span></span> |

<span data-ttu-id="43a83-216">Obsługuje ten WebAPI [OData] i rozszerza schemat tabeli w celu obsługi [synchronizacji danych w trybie offline].</span><span class="sxs-lookup"><span data-stu-id="43a83-216">This WebAPI supports [OData] and extends the table schema to support [offline data sync].</span></span>

### <span data-ttu-id="43a83-217"><a name="howto-dynamicschema"></a>Porady: Definiowanie tabel za pomocą dynamicznej schematu</span><span class="sxs-lookup"><span data-stu-id="43a83-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="43a83-218">Przed użyciem tabeli musi być zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="43a83-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="43a83-219">Tabele mogą być definiowane ze schematem statyczne (gdzie dewelopera definiuje kolumn w schemacie) lub dynamicznie (gdzie zestawu SDK Określa schemat oparte na przychodzące żądania).</span><span class="sxs-lookup"><span data-stu-id="43a83-219">Tables can be defined with a static schema (where the developer defines the columns within the schema) or dynamically (where the SDK controls the schema based on incoming requests).</span></span> <span data-ttu-id="43a83-220">Ponadto deweloper może kontrolować określone aspekty WebAPI przez dodanie kodu Javascript do definicji.</span><span class="sxs-lookup"><span data-stu-id="43a83-220">In addition, the developer can control specific aspects of the WebAPI by adding Javascript code to the definition.</span></span>

<span data-ttu-id="43a83-221">Najlepszym rozwiązaniem można zdefiniować każdej tabeli w pliku Javascript w katalogu tabel, następnie użyj metody tables.import() Aby zaimportować tabele.</span><span class="sxs-lookup"><span data-stu-id="43a83-221">As a best practice, you should define each table in a Javascript file in the tables directory, then use the tables.import() method to import the tables.</span></span>  <span data-ttu-id="43a83-222">Rozszerzanie basic-app, będzie można dostosować pliku app.js:</span><span class="sxs-lookup"><span data-stu-id="43a83-222">Extending the basic-app, the app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define the database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="43a83-223">Zdefiniuj tabelę w. / tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="43a83-223">Define the table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for the table goes here

    module.exports = table;

<span data-ttu-id="43a83-224">Tabele domyślnie używają schematu dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="43a83-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="43a83-225">Aby wyłączyć funkcję dynamicznego schematu globalnie, określ dla ustawienia aplikacji **MS_DynamicSchema** o wartości false w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="43a83-225">To turn off dynamic schema globally, set the App Setting **MS_DynamicSchema** to false within the Azure portal.</span></span>

<span data-ttu-id="43a83-226">Znajduje się pełny przykład w [todo przykładem w witrynie GitHub].</span><span class="sxs-lookup"><span data-stu-id="43a83-226">You can find a complete example in the [todo sample on GitHub].</span></span>

### <span data-ttu-id="43a83-227"><a name="howto-staticschema"></a>Porady: Definiowanie tabel za pomocą statycznego schematu</span><span class="sxs-lookup"><span data-stu-id="43a83-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="43a83-228">Można jawnie definiować kolumn do ujawnienia za pomocą WebAPI.</span><span class="sxs-lookup"><span data-stu-id="43a83-228">You can explicitly define the columns to expose via the WebAPI.</span></span>  <span data-ttu-id="43a83-229">Zestaw Node.js SDK apps w usłudze azure-mobile automatycznie dodaje wszystkie dodatkowe kolumny są wymagane dla synchronizacji danych w trybie offline do listy, który podasz.</span><span class="sxs-lookup"><span data-stu-id="43a83-229">The azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync to the list that you provide.</span></span>  <span data-ttu-id="43a83-230">Na przykład wymagać tabeli z kolumnami przez aplikacje klienckie Szybki Start: tekst (ciąg) i ukończyć (wartość logiczna).</span><span class="sxs-lookup"><span data-stu-id="43a83-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="43a83-231">Tabeli można zdefiniować w tabeli JavaScript pliku definicji (znajduje się w katalogu tabele) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="43a83-231">The table can be defined in the table definition JavaScript file (located in the tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="43a83-232">Po zdefiniowaniu statycznie tabel, należy także wywołać metodę tables.initialize() utworzyć schemat bazy danych podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="43a83-232">If you define tables statically, then you must also call the tables.initialize() method to create the database schema on startup.</span></span>  <span data-ttu-id="43a83-233">Zwraca metodę tables.initialize() [Promise] tak, aby usługi sieci web nie obsługiwać żądań przed bazy danych został zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="43a83-233">The tables.initialize() method returns a [Promise] so that the web service does not serve requests before the database being initialized.</span></span>

### <span data-ttu-id="43a83-234"><a name="howto-sqlexpress-setup"></a>Porady: użycie programu SQL Express jako programowanie magazynu danych na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="43a83-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="43a83-235">Azure Mobile Apps AzureMobile aplikacji węzła SDK udostępnia trzy opcje do obsługi danych bez: zestaw SDK zawiera trzy opcje do obsługi danych poza pola:</span><span class="sxs-lookup"><span data-stu-id="43a83-235">The Azure Mobile Apps The AzureMobile Apps Node SDK provides three options for serving data out of the box: SDK provides three options for serving data out of the box:</span></span>

* <span data-ttu-id="43a83-236">Użyj **pamięci** sterownika do zapewnienia magazynu przykład nietrwałe</span><span class="sxs-lookup"><span data-stu-id="43a83-236">Use the **memory** driver to provide a non-persistent example store</span></span>
* <span data-ttu-id="43a83-237">Użyj **mssql** sterownik do zapewnienia magazynu danych programu SQL Express programowanie</span><span class="sxs-lookup"><span data-stu-id="43a83-237">Use the **mssql** driver to provide a SQL Express data store for development</span></span>
* <span data-ttu-id="43a83-238">Użyj **mssql** sterowników w celu zapewnienia magazynu danych bazy danych SQL Azure dla trybu produkcyjnego</span><span class="sxs-lookup"><span data-stu-id="43a83-238">Use the **mssql** driver to provide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="43a83-239">Zestaw SDK usługi Azure Mobile Apps Node.js używa [pakietu Node.js mssql] i użycia połączenia do bazy danych SQL i programu SQL Express.</span><span class="sxs-lookup"><span data-stu-id="43a83-239">The Azure Mobile Apps Node.js SDK uses the [mssql Node.js package] to establish and use a connection to both SQL Express and SQL Database.</span></span>  <span data-ttu-id="43a83-240">Ten pakiet wymaga włączenia połączeń TCP w wystąpieniu programu SQL Express.</span><span class="sxs-lookup"><span data-stu-id="43a83-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="43a83-241">Sterownik pamięci nie ma kompletnego zestawu urządzenia do testowania.</span><span class="sxs-lookup"><span data-stu-id="43a83-241">The memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="43a83-242">Jeśli chcesz przetestować zaplecza lokalnie, firma Microsoft zaleca korzystanie z magazynu danych programu SQL Express i sterownik mssql.</span><span class="sxs-lookup"><span data-stu-id="43a83-242">If you wish to test your backend locally, we recommend the use of a SQL Express data store and the mssql driver.</span></span>
>
>

1. <span data-ttu-id="43a83-243">Pobierz i zainstaluj [programu Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="43a83-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="43a83-244">Upewnij się, że instalowanie programu SQL Server 2014 Express Edition narzędzia.</span><span class="sxs-lookup"><span data-stu-id="43a83-244">Ensure you install the SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="43a83-245">Chyba że jawnie wymagana jest Obsługa 64-bitowy, 32-bitowej wersji zużywa mniej pamięci podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="43a83-245">Unless you explicitly require 64-bit support, the 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="43a83-246">Uruchom Menedżera konfiguracji programu SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="43a83-246">Run the SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="43a83-247">Rozwiń węzeł **konfigurację sieci programu SQL Server** węzła w menu po lewej stronie drzewa.</span><span class="sxs-lookup"><span data-stu-id="43a83-247">Expand the **SQL Server Network Configuration** node in the left-hand tree menu.</span></span>
   2. <span data-ttu-id="43a83-248">Kliknij przycisk **protokoły dla programu SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="43a83-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="43a83-249">Kliknij prawym przyciskiem myszy **TCP/IP** i wybierz **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="43a83-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="43a83-250">Kliknij przycisk **OK** w wyskakującym oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="43a83-250">Click **OK** in the pop-up dialog.</span></span>
   4. <span data-ttu-id="43a83-251">Kliknij prawym przyciskiem myszy **TCP/IP** i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="43a83-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="43a83-252">Kliknij przycisk **adresów IP** kartę.</span><span class="sxs-lookup"><span data-stu-id="43a83-252">Click the **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="43a83-253">Znajdź **IPWszystkie** węzła.</span><span class="sxs-lookup"><span data-stu-id="43a83-253">Find the **IPAll** node.</span></span>  <span data-ttu-id="43a83-254">W **TCP Port** wprowadź **1433**.</span><span class="sxs-lookup"><span data-stu-id="43a83-254">In the **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="43a83-255">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="43a83-255">Click **OK**.</span></span>  <span data-ttu-id="43a83-256">Kliknij przycisk **OK** w wyskakującym oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="43a83-256">Click **OK** in the pop-up dialog.</span></span>
   8. <span data-ttu-id="43a83-257">Kliknij przycisk **usług SQL Server** w menu po lewej stronie drzewa.</span><span class="sxs-lookup"><span data-stu-id="43a83-257">Click **SQL Server Services** in the left-hand tree menu.</span></span>
   9. <span data-ttu-id="43a83-258">Kliknij prawym przyciskiem myszy **programu SQL Server (SQLEXPRESS)** i wybierz **ponownego uruchomienia**</span><span class="sxs-lookup"><span data-stu-id="43a83-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="43a83-259">Zamknij Menedżera konfiguracji programu SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="43a83-259">Close the SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="43a83-260">Uruchom program SQL Server 2014 Management Studio i nawiąż połączenie lokalne wystąpienie programu SQL Express</span><span class="sxs-lookup"><span data-stu-id="43a83-260">Run the SQL Server 2014 Management Studio and connect to your local SQL Express instance</span></span>

   1. <span data-ttu-id="43a83-261">Kliknij prawym przyciskiem myszy wystąpienie w Eksploratorze obiektów i wybierz **właściwości**</span><span class="sxs-lookup"><span data-stu-id="43a83-261">Right-click your instance in the Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="43a83-262">Wybierz **zabezpieczeń** strony.</span><span class="sxs-lookup"><span data-stu-id="43a83-262">Select the **Security** page.</span></span>
   3. <span data-ttu-id="43a83-263">Upewnij się, **programu SQL Server i uwierzytelniania systemu Windows tryb** jest zaznaczone</span><span class="sxs-lookup"><span data-stu-id="43a83-263">Ensure the **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="43a83-264">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="43a83-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="43a83-265">Rozwiń węzeł **zabezpieczeń** > **logowania** w Eksploratorze obiektów</span><span class="sxs-lookup"><span data-stu-id="43a83-265">Expand **Security** > **Logins** in the Object Explorer</span></span>
   6. <span data-ttu-id="43a83-266">Kliknij prawym przyciskiem myszy **logowania** i wybierz **nowe dane logowania...**</span><span class="sxs-lookup"><span data-stu-id="43a83-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="43a83-267">Wprowadź nazwę logowania.</span><span class="sxs-lookup"><span data-stu-id="43a83-267">Enter a Login name.</span></span>  <span data-ttu-id="43a83-268">Wybierz pozycję **Uwierzytelnianie programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="43a83-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="43a83-269">Wprowadź hasło, a następnie wprowadź to samo hasło w **Potwierdź hasło**.</span><span class="sxs-lookup"><span data-stu-id="43a83-269">Enter a Password, then enter the same password in **Confirm password**.</span></span>  <span data-ttu-id="43a83-270">Hasło musi spełniać wymagania co do złożoności systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="43a83-270">The password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="43a83-271">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="43a83-271">Click **OK**</span></span>

          ![Add a new user to SQL Express][5]
   9. <span data-ttu-id="43a83-272">Kliknij prawym przyciskiem myszy nazwę nowego użytkownika, a następnie wybierz **właściwości**</span><span class="sxs-lookup"><span data-stu-id="43a83-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="43a83-273">Wybierz **ról serwera** strony</span><span class="sxs-lookup"><span data-stu-id="43a83-273">Select the **Server Roles** page</span></span>
   11. <span data-ttu-id="43a83-274">Zaznacz pole wyboru obok pozycji **dbcreator** roli serwera</span><span class="sxs-lookup"><span data-stu-id="43a83-274">Check the box next to the **dbcreator** server role</span></span>
   12. <span data-ttu-id="43a83-275">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="43a83-275">Click **OK**</span></span>
   13. <span data-ttu-id="43a83-276">Zamknij program SQL Server 2015 Management Studio</span><span class="sxs-lookup"><span data-stu-id="43a83-276">Close the SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="43a83-277">Upewnij się, że rekord nazwy użytkownika i hasła, które wybrano.</span><span class="sxs-lookup"><span data-stu-id="43a83-277">Ensure you record the username and password you selected.</span></span>  <span data-ttu-id="43a83-278">Może być konieczne do przypisywania dodatkowych ról serwera lub uprawnienia w zależności od wymagań określonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="43a83-278">You may need to assign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="43a83-279">Odczyty aplikacji Node.js **SQLCONNSTR_MS_TableConnectionString** zmiennej środowiskowej ciągu połączenia dla tej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="43a83-279">The Node.js application reads the **SQLCONNSTR_MS_TableConnectionString** environment variable for the connection string for this database.</span></span>  <span data-ttu-id="43a83-280">Można ustawić tę zmienną w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="43a83-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="43a83-281">Na przykład aby ustawić tej zmiennej środowiskowej można Użyj programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="43a83-281">For example, you can use PowerShell to set this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="43a83-282">Dostęp do bazy danych przy użyciu połączenia TCP/IP i podaj nazwę użytkownika i hasło dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="43a83-282">Access the database through a TCP/IP connection and provide a username and password for the connection.</span></span>

### <span data-ttu-id="43a83-283"><a name="howto-config-localdev"></a>Porady: Konfigurowanie projektu dla rozwoju lokalnych</span><span class="sxs-lookup"><span data-stu-id="43a83-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="43a83-284">Aplikacje mobilne platformy Azure odczytuje plik JavaScript o nazwie *azureMobile.js* z lokalnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="43a83-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from the local filesystem.</span></span>  <span data-ttu-id="43a83-285">Nie należy używać tego pliku można skonfigurować zestaw SDK usługi Azure Mobile Apps w środowisku produkcyjnym — za pomocą ustawień aplikacji w ramach [portalu Azure] zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="43a83-285">Do not use this file to configure the Azure Mobile Apps SDK in production - use App Settings within the [Azure portal] instead.</span></span>  <span data-ttu-id="43a83-286">*AzureMobile.js* plików należy wyeksportować obiekt konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="43a83-286">The *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="43a83-287">Najczęściej używane ustawienia to:</span><span class="sxs-lookup"><span data-stu-id="43a83-287">The most common settings are:</span></span>

* <span data-ttu-id="43a83-288">Ustawienia bazy danych</span><span class="sxs-lookup"><span data-stu-id="43a83-288">Database Settings</span></span>
* <span data-ttu-id="43a83-289">Ustawienia rejestrowania diagnostycznego</span><span class="sxs-lookup"><span data-stu-id="43a83-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="43a83-290">Alternatywne ustawienia mechanizmu CORS</span><span class="sxs-lookup"><span data-stu-id="43a83-290">Alternate CORS Settings</span></span>

<span data-ttu-id="43a83-291">Przykład *azureMobile.js* plik implementacji poprzedniego ustawienia bazy danych:</span><span class="sxs-lookup"><span data-stu-id="43a83-291">An example *azureMobile.js* file implementing the preceding database settings follows:</span></span>

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

<span data-ttu-id="43a83-292">Firma Microsoft zaleca dodanie *azureMobile.js* do Twojej *.gitignore* pliku (lub inne Ignoruj pliku kontroli kodu źródłowego) aby zapobiec hasła są przechowywane w chmurze.</span><span class="sxs-lookup"><span data-stu-id="43a83-292">We recommend that you add *azureMobile.js* to your *.gitignore* file (or other source code control ignore file) to prevent passwords from being stored in the cloud.</span></span>  <span data-ttu-id="43a83-293">Zawsze skonfigurować ustawienia produkcji w ustawieniach aplikacji w ramach [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="43a83-293">Always configure production settings in App Settings within the [Azure portal].</span></span>

### <span data-ttu-id="43a83-294"><a name="howto-appsettings"></a>Instrukcje: Konfigurowanie ustawień aplikacji dla aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="43a83-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="43a83-295">Większość ustawień w *azureMobile.js* plik ma odpowiednik ustawienia aplikacji [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="43a83-295">Most settings in the *azureMobile.js* file have an equivalent App Setting in the [Azure portal].</span></span>  <span data-ttu-id="43a83-296">Aby skonfigurować aplikację w ustawieniach aplikacji, należy użyć następującej listy:</span><span class="sxs-lookup"><span data-stu-id="43a83-296">Use the following list to configure your app in App Settings:</span></span>

| <span data-ttu-id="43a83-297">Ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="43a83-297">App Setting</span></span> | <span data-ttu-id="43a83-298">*azureMobile.js* ustawienie</span><span class="sxs-lookup"><span data-stu-id="43a83-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="43a83-299">Opis</span><span class="sxs-lookup"><span data-stu-id="43a83-299">Description</span></span> | <span data-ttu-id="43a83-300">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="43a83-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="43a83-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="43a83-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="43a83-302">name</span><span class="sxs-lookup"><span data-stu-id="43a83-302">name</span></span> |<span data-ttu-id="43a83-303">Nazwa aplikacji</span><span class="sxs-lookup"><span data-stu-id="43a83-303">The name of the app</span></span> |<span data-ttu-id="43a83-304">Ciąg</span><span class="sxs-lookup"><span data-stu-id="43a83-304">string</span></span> |
| <span data-ttu-id="43a83-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="43a83-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="43a83-306">Logging.level</span><span class="sxs-lookup"><span data-stu-id="43a83-306">logging.level</span></span> |<span data-ttu-id="43a83-307">Poziom minimalna dziennika komunikatów do zarejestrowania</span><span class="sxs-lookup"><span data-stu-id="43a83-307">Minimum log level of messages to log</span></span> |<span data-ttu-id="43a83-308">błąd, ostrzeżenie, informacje o verbose, debug, niemądre</span><span class="sxs-lookup"><span data-stu-id="43a83-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="43a83-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="43a83-309">**MS_DebugMode**</span></span> |<span data-ttu-id="43a83-310">Debugowania</span><span class="sxs-lookup"><span data-stu-id="43a83-310">debug</span></span> |<span data-ttu-id="43a83-311">Włącz lub wyłącz tryb debugowania</span><span class="sxs-lookup"><span data-stu-id="43a83-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="43a83-312">wartość true, false</span><span class="sxs-lookup"><span data-stu-id="43a83-312">true, false</span></span> |
| <span data-ttu-id="43a83-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="43a83-313">**MS_TableSchema**</span></span> |<span data-ttu-id="43a83-314">Data.Schema</span><span class="sxs-lookup"><span data-stu-id="43a83-314">data.schema</span></span> |<span data-ttu-id="43a83-315">Domyślna nazwa schematu dla tabel SQL</span><span class="sxs-lookup"><span data-stu-id="43a83-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="43a83-316">ciąg (domyślne: dbo)</span><span class="sxs-lookup"><span data-stu-id="43a83-316">string (default: dbo)</span></span> |
| <span data-ttu-id="43a83-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="43a83-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="43a83-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="43a83-318">data.dynamicSchema</span></span> |<span data-ttu-id="43a83-319">Włącz lub wyłącz tryb debugowania</span><span class="sxs-lookup"><span data-stu-id="43a83-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="43a83-320">wartość true, false</span><span class="sxs-lookup"><span data-stu-id="43a83-320">true, false</span></span> |
| <span data-ttu-id="43a83-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="43a83-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="43a83-322">Wersja (Ustaw do niezdefiniowanego)</span><span class="sxs-lookup"><span data-stu-id="43a83-322">version (set to undefined)</span></span> |<span data-ttu-id="43a83-323">Wyłącza nagłówka X-ZUMO-Server-Version</span><span class="sxs-lookup"><span data-stu-id="43a83-323">Disables the X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="43a83-324">wartość true, false</span><span class="sxs-lookup"><span data-stu-id="43a83-324">true, false</span></span> |
| <span data-ttu-id="43a83-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="43a83-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="43a83-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="43a83-326">skipversioncheck</span></span> |<span data-ttu-id="43a83-327">Wyłącza sprawdzanie wersji klienta interfejsu API</span><span class="sxs-lookup"><span data-stu-id="43a83-327">Disables the client API version check</span></span> |<span data-ttu-id="43a83-328">wartość true, false</span><span class="sxs-lookup"><span data-stu-id="43a83-328">true, false</span></span> |

<span data-ttu-id="43a83-329">Można skonfigurować ustawienie aplikacji:</span><span class="sxs-lookup"><span data-stu-id="43a83-329">To set an App Setting:</span></span>

1. <span data-ttu-id="43a83-330">Zaloguj się do witryny [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="43a83-330">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="43a83-331">Wybierz **wszystkie zasoby** lub **usługi aplikacji** następnie kliknij nazwę aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="43a83-331">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="43a83-332">Domyślnie zostanie otwarty blok ustawień.</span><span class="sxs-lookup"><span data-stu-id="43a83-332">The Settings blade opens by default.</span></span> <span data-ttu-id="43a83-333">Jeśli nie kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="43a83-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="43a83-334">Kliknij przycisk **ustawienia aplikacji** w menu Ogólne.</span><span class="sxs-lookup"><span data-stu-id="43a83-334">Click **Application settings** in the GENERAL menu.</span></span>
5. <span data-ttu-id="43a83-335">Przewiń do sekcji ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="43a83-335">Scroll to the App Settings section.</span></span>
6. <span data-ttu-id="43a83-336">Jeśli aplikacja, ustawienia już istnieje, kliknij wartość ustawienia aplikacji, aby edytować wartość.</span><span class="sxs-lookup"><span data-stu-id="43a83-336">If your app setting already exists, click the value of the app setting to edit the value.</span></span>
7. <span data-ttu-id="43a83-337">Jeśli ustawienia aplikacji nie istnieje, wprowadź ustawienie aplikacji w polu klucza i wartość w polu wartość.</span><span class="sxs-lookup"><span data-stu-id="43a83-337">If your app setting does not exist, enter the App Setting in the Key box and the value in the Value box.</span></span>
8. <span data-ttu-id="43a83-338">Po zakończeniu, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="43a83-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="43a83-339">Zmiana większość ustawień aplikacji wymaga ponownego uruchomienia usługi.</span><span class="sxs-lookup"><span data-stu-id="43a83-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="43a83-340"><a name="howto-use-sqlazure"></a>Porady: Użyj bazy danych SQL jako magazyn danych produkcyjnych</span><span class="sxs-lookup"><span data-stu-id="43a83-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="43a83-341">Przy użyciu bazy danych SQL Azure jako magazynu danych jest identyczne we wszystkich typów aplikacji w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="43a83-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="43a83-342">Jeśli jeszcze tego nie zrobiono, wykonaj następujące kroki, aby utworzyć zaplecze aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="43a83-342">If you have not done so already, follow these steps to create a Mobile App backend.</span></span>

1. <span data-ttu-id="43a83-343">Zaloguj się do witryny [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="43a83-343">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="43a83-344">W górnym lewym rogu okna, kliknij przycisk **+ nowy** przycisk > **sieci Web i mobilność** > **aplikacji mobilnej**, następnie podaj nazwę zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="43a83-344">In the top left of the window, click the **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="43a83-345">W **grupy zasobów** wprowadź takiej samej nazwie co aplikacja.</span><span class="sxs-lookup"><span data-stu-id="43a83-345">In the **Resource Group** box, enter the same name as your app.</span></span>
4. <span data-ttu-id="43a83-346">Plan usługi aplikacji domyślnie jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="43a83-346">The Default App Service plan is selected.</span></span>  <span data-ttu-id="43a83-347">Jeśli chcesz zmienić swój plan usługi aplikacji, możesz to zrobić, klikając Plan usługi aplikacji > **+ Utwórz nowe**.</span><span class="sxs-lookup"><span data-stu-id="43a83-347">If you wish to change your App Service plan, you can do so by clicking the App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="43a83-348">Podaj nazwę nowego planu usługi aplikacji i wybierz odpowiednią lokalizację.</span><span class="sxs-lookup"><span data-stu-id="43a83-348">Provide a name of the new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="43a83-349">Kliknij warstwa cenowa i wybierz odpowiednią warstwę cenową dla usługi.</span><span class="sxs-lookup"><span data-stu-id="43a83-349">Click the Pricing tier and select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="43a83-350">Wybierz **Wyświetl wszystkie** do widoku więcej cennik opcje, takie jak **wolne** i **Shared**.</span><span class="sxs-lookup"><span data-stu-id="43a83-350">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="43a83-351">Po wybraniu warstwy cenowej kliknij **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="43a83-351">Once you have selected the pricing tier, click the **Select** button.</span></span>  <span data-ttu-id="43a83-352">W **planu usługi aplikacji** bloku, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="43a83-352">Back in the **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="43a83-353">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="43a83-353">Click **Create**.</span></span> <span data-ttu-id="43a83-354">Inicjowanie obsługi administracyjnej zaplecza aplikacji mobilnej może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="43a83-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="43a83-355">Po zainicjowaniu obsługi zaplecza aplikacji mobilnej otwartego portalu **ustawienia** bloku dla zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="43a83-355">Once the Mobile App backend is provisioned, the portal opens the **Settings** blade for the Mobile App backend.</span></span>

<span data-ttu-id="43a83-356">Po utworzeniu zaplecza aplikacji mobilnej można połączyć z istniejącej bazy danych SQL do zaplecza aplikacji mobilnej albo utwórz nową bazę danych SQL.</span><span class="sxs-lookup"><span data-stu-id="43a83-356">Once the Mobile App backend is created, you can choose to either connect an existing SQL database to your Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="43a83-357">W tej sekcji utworzymy bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="43a83-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="43a83-358">Jeśli masz już bazę danych w tej samej lokalizacji co zaplecza aplikacji mobilnej, zamiast tego można wybrać **Użyj istniejącej bazy danych** , a następnie wybrać tę bazę danych.</span><span class="sxs-lookup"><span data-stu-id="43a83-358">If you already have a database in the same location as the mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="43a83-359">Bazy danych w innej lokalizacji nie jest zalecane z powodu większych opóźnień.</span><span class="sxs-lookup"><span data-stu-id="43a83-359">The use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="43a83-360">W zaplecze nowej aplikacji mobilnej kliknij **ustawienia** > **aplikacji mobilnej** > **danych** > **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="43a83-360">In the new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="43a83-361">W **Dodaj połączenie danych** bloku, kliknij przycisk **baza danych SQL — Skonfiguruj wymagane ustawienia** > **Utwórz nową bazę danych**.</span><span class="sxs-lookup"><span data-stu-id="43a83-361">In the **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="43a83-362">Wprowadź nazwę nowej bazy danych w **nazwa** pola.</span><span class="sxs-lookup"><span data-stu-id="43a83-362">Enter the name of the new database in the **Name** field.</span></span>
3. <span data-ttu-id="43a83-363">Kliknij przycisk **serwera**.</span><span class="sxs-lookup"><span data-stu-id="43a83-363">Click **Server**.</span></span>  <span data-ttu-id="43a83-364">W **nowy serwer** bloku, wprowadź unikatową nazwą serwera w **nazwy serwera** pól i zapewnienia odpowiedniej **identyfikator logowania administratora serwera** i **hasło**.</span><span class="sxs-lookup"><span data-stu-id="43a83-364">In the **New server** blade, enter a unique server name in the **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="43a83-365">Upewnij się, **Zezwalaj usługom platformy azure na dostęp do serwera** jest zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="43a83-365">Ensure **Allow azure services to access server** is checked.</span></span>  <span data-ttu-id="43a83-366">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="43a83-366">Click **OK**.</span></span>

    ![Utwórz bazę danych Azure SQL][6]
4. <span data-ttu-id="43a83-368">Na **nową bazę danych** bloku, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="43a83-368">On the **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="43a83-369">Ponownie **Dodaj połączenie danych** bloku, wybierz opcję **ciąg połączenia**, wprowadź identyfikator logowania i hasło, podane podczas tworzenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="43a83-369">Back on the **Add data connection** blade, select **Connection string**, enter the login and password that you provided when creating the database.</span></span>  <span data-ttu-id="43a83-370">Jeśli używasz istniejącej bazy danych, należy podać poświadczenia logowania dla tej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="43a83-370">If you use an existing database, provide the login credentials for that database.</span></span>  <span data-ttu-id="43a83-371">Po wpisaniu, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="43a83-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="43a83-372">Ponownie **Dodaj połączenie danych** bloku ponownie, kliknij przycisk **OK** utworzyć bazę danych.</span><span class="sxs-lookup"><span data-stu-id="43a83-372">Back on the **Add data connection** blade again, click **OK** to create the database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="43a83-373">Utworzenie bazy danych może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="43a83-373">Creation of the database can take a few minutes.</span></span>  <span data-ttu-id="43a83-374">Użyj **powiadomienia** obszaru do monitorowania postępu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="43a83-374">Use the **Notifications** area to monitor the progress of the deployment.</span></span>  <span data-ttu-id="43a83-375">Nie postępu aż do bazy danych został wdrożony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="43a83-375">Do not progress until the database has been deployed successfully.</span></span>  <span data-ttu-id="43a83-376">Po pomyślnym wdrożeniu, ciąg połączenia jest tworzony dla wystąpienia bazy danych SQL w zapleczu swojej przenośnych ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="43a83-376">Once successfully deployed, a Connection String is created for the SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="43a83-377">Można wyświetlić to ustawienie aplikacji w **ustawienia** > **ustawienia aplikacji** > **parametry połączenia**.</span><span class="sxs-lookup"><span data-stu-id="43a83-377">You can see this app setting in the **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="43a83-378"><a name="howto-tables-auth"></a>Porady: Wymagaj uwierzytelniania dostępu do tabel</span><span class="sxs-lookup"><span data-stu-id="43a83-378"><a name="howto-tables-auth"></a>How to: Require authentication for access to tables</span></span>
<span data-ttu-id="43a83-379">Jeśli chcesz użyć uwierzytelniania usługi aplikacji z punktem końcowym tabel, należy skonfigurować uwierzytelnianie usługi aplikacji w [portalu Azure] pierwszy.</span><span class="sxs-lookup"><span data-stu-id="43a83-379">If you wish to use App Service Authentication with the tables endpoint, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="43a83-380">Aby uzyskać więcej informacji na temat konfigurowania uwierzytelniania w usłudze Azure App Service Sprawdź w przewodniku konfiguracji dla dostawcy tożsamości, które mają być używane:</span><span class="sxs-lookup"><span data-stu-id="43a83-380">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="43a83-381">[Jak skonfigurować uwierzytelnianie usługi Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="43a83-381">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="43a83-382">[Jak skonfigurować uwierzytelnianie usługi Facebook]</span><span class="sxs-lookup"><span data-stu-id="43a83-382">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="43a83-383">[Jak skonfigurować uwierzytelnianie Google]</span><span class="sxs-lookup"><span data-stu-id="43a83-383">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="43a83-384">[Jak skonfigurować Authentication firmy Microsoft]</span><span class="sxs-lookup"><span data-stu-id="43a83-384">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="43a83-385">[Jak skonfigurować uwierzytelnianie w usłudze Twitter]</span><span class="sxs-lookup"><span data-stu-id="43a83-385">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="43a83-386">Każda tabela ma właściwość dostępu, który może służyć do kontrolowania dostępu do tabeli.</span><span class="sxs-lookup"><span data-stu-id="43a83-386">Each table has an access property that can be used to control access to the table.</span></span>  <span data-ttu-id="43a83-387">Poniższy przykład przedstawia statycznie zdefiniowanych tabeli z wymagane uwierzytelnienie.</span><span class="sxs-lookup"><span data-stu-id="43a83-387">The following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="43a83-388">Właściwość dostępu można wykonać jedną z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="43a83-388">The access property can take one of three values</span></span>

* <span data-ttu-id="43a83-389">*anonimowe* wskazuje, czy aplikacja kliencka może odczytać danych bez uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="43a83-389">*anonymous* indicates that the client application is allowed to read data without authentication</span></span>
* <span data-ttu-id="43a83-390">*uwierzytelniony* oznacza, że aplikacja kliencka musi wysłany token uwierzytelniania prawidłowe z żądaniem</span><span class="sxs-lookup"><span data-stu-id="43a83-390">*authenticated* indicates that the client application must send a valid authentication token with the request</span></span>
* <span data-ttu-id="43a83-391">*wyłączone* wskazuje, że ta tabela jest obecnie wyłączona</span><span class="sxs-lookup"><span data-stu-id="43a83-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="43a83-392">Jeśli zdefiniowano właściwość dostęp jest dozwolony dostęp nieuwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="43a83-392">If the access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="43a83-393"><a name="howto-tables-getidentity"></a>Porady: Użyj uwierzytelniania oświadczeń z tabel</span><span class="sxs-lookup"><span data-stu-id="43a83-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="43a83-394">Można skonfigurować różne oświadczenia, które są wymagane podczas konfigurowania uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="43a83-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="43a83-395">Te oświadczenia nie są zwykle dostępne za pośrednictwem `context.user` obiektu.</span><span class="sxs-lookup"><span data-stu-id="43a83-395">These claims are not normally available through the `context.user` object.</span></span>  <span data-ttu-id="43a83-396">Jednak mogą zostać pobrane za pomocą `context.user.getIdentity()` metody.</span><span class="sxs-lookup"><span data-stu-id="43a83-396">However, they can be retrieved using the `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="43a83-397">`getIdentity()` Metoda zwraca Promise, który jest rozpoznawany jako obiekt.</span><span class="sxs-lookup"><span data-stu-id="43a83-397">The `getIdentity()` method returns a Promise that resolves to an object.</span></span>  <span data-ttu-id="43a83-398">Obiekt jest wyznaczaną przez metodę uwierzytelniania (facebook, google, twitter, microsoftaccount lub aad).</span><span class="sxs-lookup"><span data-stu-id="43a83-398">The object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="43a83-399">Na przykład jeśli skonfigurowano uwierzytelnianie Microsoft Account i żądania oświadczeń adresów e-mail, można dodać adres e-mail do rekordu o następujący kontroler tabeli:</span><span class="sxs-lookup"><span data-stu-id="43a83-399">For example, if you set up Microsoft Account authentication and request the email addresses claim, you can add the email address to the record with the following table controller:</span></span>

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
    * Limit the context query to those records with the authenticated user email address
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds the email address from the claims to the context item - used for
    * insert operations
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when the client does a request
    // READ - only return records belonging to the authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite the userId based on the authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong to the authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong to the authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="43a83-400">Aby zobaczyć, jakie oświadczenia są dostępne, użyj przeglądarki sieci web, aby wyświetlić `/.auth/me` punktu końcowego witryny.</span><span class="sxs-lookup"><span data-stu-id="43a83-400">To see what claims are available, use a web browser to view the `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="43a83-401"><a name="howto-tables-disabled"></a>Porady: wyłączanie dostępu do określonej tabeli operacji</span><span class="sxs-lookup"><span data-stu-id="43a83-401"><a name="howto-tables-disabled"></a>How to: Disable access to specific table operations</span></span>
<span data-ttu-id="43a83-402">Oprócz wymienionych w tabeli, właściwości dostępu można można użyć do kontrolowania poszczególnych działań.</span><span class="sxs-lookup"><span data-stu-id="43a83-402">In addition to appearing on the table, the access property can be used to control individual operations.</span></span>  <span data-ttu-id="43a83-403">Istnieją cztery operacje:</span><span class="sxs-lookup"><span data-stu-id="43a83-403">There are four operations:</span></span>

* <span data-ttu-id="43a83-404">*Przeczytaj* jest operacji RESTful GET, w tabeli</span><span class="sxs-lookup"><span data-stu-id="43a83-404">*read* is the RESTful GET operation on the table</span></span>
* <span data-ttu-id="43a83-405">*Wstaw* jest operacji RESTful POST w tabeli</span><span class="sxs-lookup"><span data-stu-id="43a83-405">*insert* is the RESTful POST operation on the table</span></span>
* <span data-ttu-id="43a83-406">*Zaktualizuj* jest poprawka RESTful operacji w tabeli</span><span class="sxs-lookup"><span data-stu-id="43a83-406">*update* is the RESTful PATCH operation on the table</span></span>
* <span data-ttu-id="43a83-407">*Usuń* jest operacją RESTful usuwania w tabeli</span><span class="sxs-lookup"><span data-stu-id="43a83-407">*delete* is the RESTful DELETE operation on the table</span></span>

<span data-ttu-id="43a83-408">Na przykład możesz podać nieuwierzytelnione tabeli tylko do odczytu:</span><span class="sxs-lookup"><span data-stu-id="43a83-408">For example, you may wish to provide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="43a83-409"><a name="howto-tables-query"></a>Porady: dopasowywanie kwerendę, która jest używana z operacjami tabeli</span><span class="sxs-lookup"><span data-stu-id="43a83-409"><a name="howto-tables-query"></a>How to: Adjust the query that is used with table operations</span></span>
<span data-ttu-id="43a83-410">Typowe wymagania dotyczące operacji tabeli jest zapewnienie ograniczony widok danych.</span><span class="sxs-lookup"><span data-stu-id="43a83-410">A common requirement for table operations is to provide a restricted view of the data.</span></span>  <span data-ttu-id="43a83-411">Na przykład może udostępnić tabelę, która zostanie oznaczony przy użyciu Identyfikatora uwierzytelnionego użytkownika w taki sposób, że można tylko do odczytu lub aktualizacji własnych rekordów.</span><span class="sxs-lookup"><span data-stu-id="43a83-411">For example, you may provide a table that is tagged with the authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="43a83-412">Oferuje następujące definicji tabeli:</span><span class="sxs-lookup"><span data-stu-id="43a83-412">The following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for the table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for the authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite the userId with the authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="43a83-413">Operacje, które zwykle wykonać zapytania ma właściwość zapytania, który można dostosować, w której klauzuli.</span><span class="sxs-lookup"><span data-stu-id="43a83-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="43a83-414">Właściwość kwerendy jest [QueryJS] obiekt, który służy do konwertowania zapytania OData do zasobu, który może przetwarzać danych wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="43a83-414">The query property is a [QueryJS] object that is used to convert an OData query to something that the data backend can process.</span></span>  <span data-ttu-id="43a83-415">W przypadku prostego równości (na przykład mieszanego) można użyć mapy.</span><span class="sxs-lookup"><span data-stu-id="43a83-415">For simple equality cases (like the preceding one), a map can be used.</span></span> <span data-ttu-id="43a83-416">Możesz także dodać punkty SQL:</span><span class="sxs-lookup"><span data-stu-id="43a83-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="43a83-417"><a name="howto-tables-softdelete"></a>Porady: Konfigurowanie usuwania nietrwałego dla tabeli</span><span class="sxs-lookup"><span data-stu-id="43a83-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="43a83-418">Faktycznie usuwania nietrwałego nie powoduje usunięcia rekordów.</span><span class="sxs-lookup"><span data-stu-id="43a83-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="43a83-419">Zamiast tego oznacza je jako usunięte w bazie danych, ustawiając usuniętą kolumnę na wartość true.</span><span class="sxs-lookup"><span data-stu-id="43a83-419">Instead it marks them as deleted within the database by setting the deleted column to true.</span></span>  <span data-ttu-id="43a83-420">Zestaw SDK aplikacji usługi Azure Mobile automatycznie usuwa wszystkie usunięte nietrwale rekordy z wyników, chyba że IncludeDeleted() korzysta z zestawu SDK klienta Mobile.</span><span class="sxs-lookup"><span data-stu-id="43a83-420">The Azure Mobile Apps SDK automatically removes soft-deleted records from results unless the Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="43a83-421">Aby skonfigurować tabelę dla usuwania nietrwałego, ustaw `softDelete` właściwość w pliku definicji tabeli:</span><span class="sxs-lookup"><span data-stu-id="43a83-421">To configure a table for soft delete, set the `softDelete` property in the table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="43a83-422">Należy określić mechanizm przeczyszczanie rekordów — od aplikacji klienta, za pomocą zadania WebJob, funkcji platformy Azure lub za pomocą niestandardowego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="43a83-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="43a83-423"><a name="howto-tables-seeding"></a>Porady: inicjatora bazy danych z danymi</span><span class="sxs-lookup"><span data-stu-id="43a83-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="43a83-424">Podczas tworzenia nowej aplikacji, możesz inicjatora tabelę z danymi.</span><span class="sxs-lookup"><span data-stu-id="43a83-424">When creating a new application, you may wish to seed a table with data.</span></span>  <span data-ttu-id="43a83-425">Można to zrobić w pliku JavaScript definicji tabeli w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="43a83-425">This can be done within the table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
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

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="43a83-426">Wstępne wypełnianie danych jest wykonywane tylko, gdy tabela została utworzona przez zestaw SDK usługi Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="43a83-426">Seeding of data is only done when the table is created by the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="43a83-427">Jeśli tabela już istnieje w bazie danych, bez danych jest dodane do tabeli.</span><span class="sxs-lookup"><span data-stu-id="43a83-427">If the table already exists within the database, no data is injected into the table.</span></span>  <span data-ttu-id="43a83-428">Jeśli włączono dynamiczne schematu schematu jest wywnioskować na podstawie wprowadzonych danych.</span><span class="sxs-lookup"><span data-stu-id="43a83-428">If dynamic schema is turned on, then the schema is inferred from the seeded data.</span></span>

<span data-ttu-id="43a83-429">Zaleca się, że można jawnie wywołać `tables.initialize()` metodę w celu utworzenia tabeli, gdy usługa zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="43a83-429">We recommend that you explicitly call the `tables.initialize()` method to create the table when the service starts running.</span></span>

### <span data-ttu-id="43a83-430"><a name="Swagger"></a>Porady: Włączanie obsługi programu Swagger</span><span class="sxs-lookup"><span data-stu-id="43a83-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="43a83-431">Usługa Azure App Service Mobile Apps jest dostarczany z wbudowanych [Swagger] obsługuje.</span><span class="sxs-lookup"><span data-stu-id="43a83-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="43a83-432">Aby włączyć obsługę programu Swagger, należy najpierw zainstalować interfejsu użytkownika programu swagger jako zależność:</span><span class="sxs-lookup"><span data-stu-id="43a83-432">To enable Swagger support, first install the swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="43a83-433">Po zakończeniu instalacji można włączyć obsługę struktury Swagger w Konstruktorze Azure Mobile Apps:</span><span class="sxs-lookup"><span data-stu-id="43a83-433">Once installed, you can enable Swagger support in the Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="43a83-434">Możesz tylko prawdopodobnie chcesz włączyć obsługi struktury Swagger w wersjach programowanie.</span><span class="sxs-lookup"><span data-stu-id="43a83-434">You probably only want to enable Swagger support in development editions.</span></span>  <span data-ttu-id="43a83-435">Można to zrobić przy użyciu `NODE_ENV` ustawienie aplikacji:</span><span class="sxs-lookup"><span data-stu-id="43a83-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="43a83-436">Punktu końcowego struktury swagger znajduje się pod adresem http://*yoursite*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="43a83-436">The swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="43a83-437">Można uzyskać dostępu do interfejsu użytkownika programu Swagger za pomocą `/swagger/ui` punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="43a83-437">You can access the Swagger UI via the `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="43a83-438">Jeśli wybierzesz opcję Wymagaj uwierzytelniania na całej aplikacji, Swagger powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="43a83-438">if you choose to require authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="43a83-439">Aby uzyskać najlepsze wyniki, wybierz, aby zezwalać nieuwierzytelnione żądania za pośrednictwem w uwierzytelnianiu usługi aplikacji Azure / następnie kontrolować ustawienia autoryzacji uwierzytelnianie przy użyciu `table.access` właściwości.</span><span class="sxs-lookup"><span data-stu-id="43a83-439">For best results, choose to allow unauthenticated requests through in the Azure App Service Authentication / Authorization settings, then control authentication using the `table.access` property.</span></span>

<span data-ttu-id="43a83-440">Możesz także dodać opcję Swagger z `azureMobile.js` plik, jeśli mają tylko obsługę struktury Swagger podczas opracowywania lokalnie.</span><span class="sxs-lookup"><span data-stu-id="43a83-440">You can also add the Swagger option to your `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="43a83-441"><a name="push">Powiadomienia wypychane</span><span class="sxs-lookup"><span data-stu-id="43a83-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="43a83-442">Aplikacje mobilne integruje się z usługi Azure Notification Hubs umożliwia wysyłanie powiadomień wypychanych docelowe do milionów urządzeń we wszystkich głównych platform.</span><span class="sxs-lookup"><span data-stu-id="43a83-442">Mobile Apps integrates with Azure Notification Hubs to enable you to send targeted push notifications to millions of devices across all major platforms.</span></span> <span data-ttu-id="43a83-443">Przy użyciu usługi Notification Hubs, można wysyłać powiadomienia wypychane w systemach iOS, Android i Windows.</span><span class="sxs-lookup"><span data-stu-id="43a83-443">By using Notification Hubs, you can send push notifications to iOS, Android and Windows devices.</span></span> <span data-ttu-id="43a83-444">Aby dowiedzieć się więcej na temat wszystkich, które można wykonać przy użyciu usługi Notification Hubs, zobacz [omówienie centra powiadomień](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43a83-444">To learn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="43a83-445"></a><a name="send-push"></a>Porady: wysyłanie powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="43a83-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="43a83-446">Poniższy kod przedstawia sposób użycia obiektu wypychania do wysyłania powiadomień wypychanych emisji do urządzeń z systemem iOS zarejestrowanego:</span><span class="sxs-lookup"><span data-stu-id="43a83-446">The following code shows how to use the push object to send a broadcast push notification to registered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do the push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="43a83-447">Tworząc rejestracji wypychanych szablonu z klienta, można zamiast tego Wyślij wiadomość wypychania szablonu na urządzeniach, na wszystkich obsługiwanych platformach.</span><span class="sxs-lookup"><span data-stu-id="43a83-447">By creating a template push registration from the client, you can instead send a template push message to devices on all supported platforms.</span></span> <span data-ttu-id="43a83-448">Poniższy kod przedstawia sposób wysłania powiadomienia szablonu:</span><span class="sxs-lookup"><span data-stu-id="43a83-448">The following code shows how to send a template notification:</span></span>

    // Define the template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do the push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }


### <span data-ttu-id="43a83-449"><a name="push-user"></a>Porady: wysyłanie powiadomień wypychanych do uwierzytelnionego użytkownika przy użyciu tagów</span><span class="sxs-lookup"><span data-stu-id="43a83-449"><a name="push-user"></a>How to: Send push notifications to an authenticated user using tags</span></span>
<span data-ttu-id="43a83-450">Uwierzytelniony użytkownik rejestrujący dla powiadomień wypychanych, tag identyfikator użytkownika jest automatycznie dodawany do rejestracji.</span><span class="sxs-lookup"><span data-stu-id="43a83-450">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="43a83-451">Za pomocą tego tagu, można wysyłać powiadomienia wypychane do wszystkich urządzeń zarejestrowanych przez określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="43a83-451">By using this tag, you can send push notifications to all devices registered by a specific user.</span></span> <span data-ttu-id="43a83-452">Poniższy kod pobiera identyfikator SID użytkownika zgłaszającego żądanie i wyśle powiadomienie wypychane szablonu do rejestracji urządzeń dla tego użytkownika:</span><span class="sxs-lookup"><span data-stu-id="43a83-452">The following code gets the SID of user making the request and sends a template push notification to every device registration for that user:</span></span>

    // Only do the push if configured
    if (context.push) {
        // Send a notification to the current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="43a83-453">Podczas rejestrowania dla powiadomień wypychanych z uwierzytelnionego klienta, upewnij się, że przed podjęciem próby wykonania rejestracji zakończeniem uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="43a83-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="43a83-454"><a name="CustomAPI"></a>Niestandardowych interfejsów API</span><span class="sxs-lookup"><span data-stu-id="43a83-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="43a83-455"><a name="howto-customapi-basic"></a>Porady: Definiowanie niestandardowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="43a83-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="43a83-456">Oprócz dostępu do danych interfejsu API za pośrednictwem punktu końcowego /tables Azure Mobile Apps zapewniają niestandardowe pokrycia interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="43a83-456">In addition to the data access API via the /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="43a83-457">Niestandardowe interfejsy API są definiowane w sposób podobny do definicji tabeli i mogą uzyskiwać dostęp do tych samych urządzeń, włącznie z uwierzytelnianiem.</span><span class="sxs-lookup"><span data-stu-id="43a83-457">Custom APIs are defined in a similar way to the table definitions and can access all the same facilities, including authentication.</span></span>

<span data-ttu-id="43a83-458">Jeśli chcesz korzystać z API niestandardowych aplikacji usługi uwierzytelniania, należy skonfigurować uwierzytelnianie usługi aplikacji w [portalu Azure] pierwszy.</span><span class="sxs-lookup"><span data-stu-id="43a83-458">If you wish to use App Service Authentication with a Custom API, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="43a83-459">Aby uzyskać więcej informacji na temat konfigurowania uwierzytelniania w usłudze Azure App Service Sprawdź w przewodniku konfiguracji dla dostawcy tożsamości, które mają być używane:</span><span class="sxs-lookup"><span data-stu-id="43a83-459">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="43a83-460">[Jak skonfigurować uwierzytelnianie usługi Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="43a83-460">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="43a83-461">[Jak skonfigurować uwierzytelnianie usługi Facebook]</span><span class="sxs-lookup"><span data-stu-id="43a83-461">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="43a83-462">[Jak skonfigurować uwierzytelnianie Google]</span><span class="sxs-lookup"><span data-stu-id="43a83-462">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="43a83-463">[Jak skonfigurować Authentication firmy Microsoft]</span><span class="sxs-lookup"><span data-stu-id="43a83-463">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="43a83-464">[Jak skonfigurować uwierzytelnianie w usłudze Twitter]</span><span class="sxs-lookup"><span data-stu-id="43a83-464">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="43a83-465">Niestandardowych interfejsów API są definiowane w znacznie taki sam sposób jak tabele interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="43a83-465">Custom APIs are defined in much the same way as the Tables API.</span></span>

1. <span data-ttu-id="43a83-466">Utwórz **interfejsu api** katalogu</span><span class="sxs-lookup"><span data-stu-id="43a83-466">Create an **api** directory</span></span>
2. <span data-ttu-id="43a83-467">Utwórz plik JavaScript definicji interfejsu API w **interfejsu api** katalogu.</span><span class="sxs-lookup"><span data-stu-id="43a83-467">Create an API definition JavaScript file in the **api** directory.</span></span>
3. <span data-ttu-id="43a83-468">Metoda importu do zaimportowania **interfejsu api** katalogu.</span><span class="sxs-lookup"><span data-stu-id="43a83-468">Use the import method to import the **api** directory.</span></span>

<span data-ttu-id="43a83-469">W tym miejscu znajduje się definicja interfejsu api prototypu na podstawie próbki basic-app, do którego użyliśmy wcześniej.</span><span class="sxs-lookup"><span data-stu-id="43a83-469">Here is the prototype api definition based on the basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="43a83-470">Spójrzmy na przykład interfejsu API, która zwraca datę serwerze przy użyciu *Date.now()* metody.</span><span class="sxs-lookup"><span data-stu-id="43a83-470">Let's take an example API that returns the server date using the *Date.now()* method.</span></span>  <span data-ttu-id="43a83-471">Oto plik api/date.js:</span><span class="sxs-lookup"><span data-stu-id="43a83-471">Here is the api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="43a83-472">Każdy parametr jest jednym z zleceń standardowych RESTful - GET, POST, poprawki lub DELETE.</span><span class="sxs-lookup"><span data-stu-id="43a83-472">Each parameter is one of the standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="43a83-473">Metoda jest standardem [oprogramowanie pośredniczące ExpressJS] funkcja, która wysyła wymagane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="43a83-473">The method is a standard [ExpressJS Middleware] function that sends the required output.</span></span>

### <span data-ttu-id="43a83-474"><a name="howto-customapi-auth"></a>Porady: wymagają uwierzytelniania w celu uzyskania dostępu do niestandardowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="43a83-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access to a custom API</span></span>
<span data-ttu-id="43a83-475">Azure Mobile Apps SDK implementuje uwierzytelniania w taki sam sposób niestandardowych interfejsów API i tabele punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="43a83-475">Azure Mobile Apps SDK implements authentication in the same way for both the tables endpoint and custom APIs.</span></span>  <span data-ttu-id="43a83-476">Aby dodać uwierzytelniania interfejsu API w poprzedniej sekcji, Dodaj **dostępu** właściwości:</span><span class="sxs-lookup"><span data-stu-id="43a83-476">To add authentication to the API developed in the previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="43a83-477">Można również określić uwierzytelniania na określonych operacji:</span><span class="sxs-lookup"><span data-stu-id="43a83-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // The GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="43a83-478">Należy użyć tego samego tokenu, który jest używany dla punktu końcowego, tabelami dla niestandardowych interfejsów API wymaga uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="43a83-478">The same token that is used for the tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="43a83-479"><a name="howto-customapi-auth"></a>Porady: Obsługa wysyłania dużych plików</span><span class="sxs-lookup"><span data-stu-id="43a83-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="43a83-480">Azure Mobile Apps SDK używa [oprogramowanie pośredniczące treści analizator](https://github.com/expressjs/body-parser) do akceptowania i dekodowania zawartości w treści w Twoje zgłoszenie.</span><span class="sxs-lookup"><span data-stu-id="43a83-480">Azure Mobile Apps SDK uses the [body-parser middleware](https://github.com/expressjs/body-parser) to accept and decode body content in your submission.</span></span>  <span data-ttu-id="43a83-481">Można wstępnie skonfigurować analizator treści do przyjęcia przekazywania plików większych:</span><span class="sxs-lookup"><span data-stu-id="43a83-481">You can pre-configure body-parser to accept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="43a83-482">Plik jest algorytmem przed transmisją base-64.</span><span class="sxs-lookup"><span data-stu-id="43a83-482">The file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="43a83-483">To spowoduje zwiększenie rozmiaru rzeczywistego przekazywania (i dlatego rozmiar należy uwzględnić).</span><span class="sxs-lookup"><span data-stu-id="43a83-483">This increases the size of the actual upload (and hence the size you must account for).</span></span>

### <span data-ttu-id="43a83-484"><a name="howto-customapi-sql"></a>Porady: wykonanie niestandardowych instrukcje SQL</span><span class="sxs-lookup"><span data-stu-id="43a83-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="43a83-485">Zestaw SDK usługi Azure Mobile Apps umożliwia dostęp do całego kontekstu za pośrednictwem obiektu żądania, umożliwiając łatwe wykonywanie sparametryzowanych instrukcji SQL dla dostawcy danych:</span><span class="sxs-lookup"><span data-stu-id="43a83-485">The Azure Mobile Apps SDK allows access to the entire Context through the request object, allowing you to execute parameterized SQL statements to the defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on to a later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define the query - anything that can be handled by the mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute the query.  The context for Azure Mobile Apps is available through
            // request.azureMobile - the data object contains the configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="43a83-486"><a name="Debugging"></a>Debugowanie, łatwe tabel i łatwe interfejsów API</span><span class="sxs-lookup"><span data-stu-id="43a83-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="43a83-487"><a name="howto-diagnostic-logs"></a>Porady: debugowanie, diagnozowanie i rozwiązywanie problemów z usługi Azure Mobile apps</span><span class="sxs-lookup"><span data-stu-id="43a83-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="43a83-488">Usługi Azure App Service zapewnia kilka debugowania i rozwiązywanie problemów z techniki aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="43a83-488">The Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="43a83-489">Zobacz następujące artykuły, aby rozpocząć pracę z Rozwiązywanie problemów z poziomu zaplecza Node.js Mobile:</span><span class="sxs-lookup"><span data-stu-id="43a83-489">Refer to the following articles to get started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="43a83-490">[Monitorowanie usługi aplikacji Azure]</span><span class="sxs-lookup"><span data-stu-id="43a83-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="43a83-491">[Włączanie rejestrowania diagnostycznego w usłudze aplikacji Azure]</span><span class="sxs-lookup"><span data-stu-id="43a83-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="43a83-492">[Rozwiązywanie problemów z usługi aplikacji Azure w programie Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="43a83-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="43a83-493">Aplikacje środowiska node.js mają dostęp do szeroką gamę narzędzi diagnostycznych dziennika.</span><span class="sxs-lookup"><span data-stu-id="43a83-493">Node.js applications have access to a wide range of diagnostic log tools.</span></span>  <span data-ttu-id="43a83-494">Wewnętrznie, zestaw SDK usługi Azure Mobile Apps Node.js używa [Winston] dla rejestrowania diagnostycznego.</span><span class="sxs-lookup"><span data-stu-id="43a83-494">Internally, the Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="43a83-495">Rejestrowanie jest automatycznie włączone, należy włączyć tryb debugowania lub przez ustawienie **MS_DebugMode** ustawienia aplikacji na wartość true w [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="43a83-495">Logging is automatically enabled by enabling debug mode or by setting the **MS_DebugMode** app setting to true in the [Azure portal].</span></span> <span data-ttu-id="43a83-496">Dzienniki generowane są wyświetlane w dziennikach diagnostycznych na [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="43a83-496">Generated logs appear in the Diagnostic Logs on the [Azure portal].</span></span>

### <span data-ttu-id="43a83-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Porady: Praca z tabelami łatwy w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="43a83-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in the Azure portal</span></span>
<span data-ttu-id="43a83-498">Łatwe tabel w portalu umożliwiają tworzenie i Praca z tabelami bezpośrednio w portalu.</span><span class="sxs-lookup"><span data-stu-id="43a83-498">Easy Tables in the portal let you create and work with tables right in the portal.</span></span> <span data-ttu-id="43a83-499">Operacje tabeli za pomocą edytora usługi aplikacji nawet można edytować.</span><span class="sxs-lookup"><span data-stu-id="43a83-499">You can even edit table operations using the App Service Editor.</span></span>

<span data-ttu-id="43a83-500">Po kliknięciu **łatwe tabel** w ustawieniach wewnętrznej bazy danych lokacji można Dodawanie, modyfikowanie lub usuwanie tabeli.</span><span class="sxs-lookup"><span data-stu-id="43a83-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="43a83-501">Można również wyświetlić dane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="43a83-501">You can also see data in the table.</span></span>

![Praca z tabelami łatwe](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="43a83-503">Poniższe polecenia są dostępne na pasku poleceń dla tabeli:</span><span class="sxs-lookup"><span data-stu-id="43a83-503">The following commands are available on the command bar for a table:</span></span>

* <span data-ttu-id="43a83-504">**Zmienianie uprawnień** — modyfikować uprawnienia do odczytu, wstawianie, aktualizowanie i usuwanie operacji względem tabeli.</span><span class="sxs-lookup"><span data-stu-id="43a83-504">**Change permissions** - modify the permission for read, insert, update and delete operations on the table.</span></span>
  <span data-ttu-id="43a83-505">Aby zezwolić na dostęp anonimowy, aby wymagać uwierzytelniania lub wyłącz dostęp do operacji są opcje.</span><span class="sxs-lookup"><span data-stu-id="43a83-505">Options are to allow anonymous access, to require authentication, or to disable all access to the operation.</span></span>
* <span data-ttu-id="43a83-506">**Edytowanie skryptu** — plik skryptu dla tabeli jest otwarty w edytorze usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="43a83-506">**Edit script** - the script file for the table is opened in the App Service Editor.</span></span>
* <span data-ttu-id="43a83-507">**Zarządzanie schematem** — Dodawanie lub usuwanie kolumn lub zmiana indeksu tabeli.</span><span class="sxs-lookup"><span data-stu-id="43a83-507">**Manage schema** - add or delete columns or change the table index.</span></span>
* <span data-ttu-id="43a83-508">**Wyczyść tabeli** -obcina istniejącej tabeli jest usunięcie wszystkich wierszy danych, ale pozostawienie schematu bez zmian.</span><span class="sxs-lookup"><span data-stu-id="43a83-508">**Clear table** - truncates an existing table be deleting all data rows but leaving the schema unchanged.</span></span>
* <span data-ttu-id="43a83-509">**Usuwanie wierszy** -Usuń poszczególne wiersze danych.</span><span class="sxs-lookup"><span data-stu-id="43a83-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="43a83-510">**Wyświetl podgląd dzienników przesyłanych strumieniowo** -łączy do przesyłania strumieniowego usługi rejestrowania dla witryny.</span><span class="sxs-lookup"><span data-stu-id="43a83-510">**View streaming logs** - connects you to the streaming log service for your site.</span></span>

### <span data-ttu-id="43a83-511"><a name="work-easy-apis"></a>Porady: pracy z interfejsami API łatwy w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="43a83-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in the Azure portal</span></span>
<span data-ttu-id="43a83-512">Łatwe interfejsów API w portalu umożliwiają tworzenie i Praca z niestandardowych interfejsów API bezpośrednio w portalu.</span><span class="sxs-lookup"><span data-stu-id="43a83-512">Easy APIs in the portal let you create and work with custom APIs right in the portal.</span></span> <span data-ttu-id="43a83-513">Można edytować skrypty interfejsu API za pomocą edytora usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="43a83-513">You can edit API scripts using the App Service Editor.</span></span>

<span data-ttu-id="43a83-514">Po kliknięciu **łatwe interfejsów API** w ustawieniach wewnętrznej bazy danych lokacji można Dodawanie, modyfikowanie lub usuwanie niestandardowych punkt końcowy interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="43a83-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Praca z łatwe interfejsów API](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="43a83-516">W portalu można zmienić uprawnienia dostępu dla danej akcji HTTP, Edytuj plik skryptu interfejsu API w edytorze usługi aplikacji lub Wyświetl dzienniki przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="43a83-516">In the portal, you can change the access permissions for a given HTTP action, edit the API script file in the App Service Editor, or view the streaming logs.</span></span>

### <span data-ttu-id="43a83-517"><a name="online-editor"></a>Porady: edytowanie kodu w edytorze usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="43a83-517"><a name="online-editor"></a>How to: Edit code in the App Service Editor</span></span>
<span data-ttu-id="43a83-518">Azure portal umożliwia edytowanie plików skryptów zaplecza Node.js w edytorze usługi aplikacji bez konieczności pobierania projektu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="43a83-518">The Azure portal lets you edit your Node.js backend script files in the App Service Editor without having to download the project to your local computer.</span></span> <span data-ttu-id="43a83-519">Aby edytować pliki skryptów w edytorze online:</span><span class="sxs-lookup"><span data-stu-id="43a83-519">To edit script files in the online editor:</span></span>

1. <span data-ttu-id="43a83-520">W bloku zaplecza aplikacji mobilnej, kliknij **wszystkie ustawienia** > albo **łatwe tabel** lub **łatwe interfejsów API**, kliknij tabelę lub interfejsu API, a następnie kliknij przycisk **edytowanie skryptu**.</span><span class="sxs-lookup"><span data-stu-id="43a83-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="43a83-521">Plik skryptu jest otwarty w edytorze usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="43a83-521">The script file is opened in the App Service Editor.</span></span>

    ![Edytor usługi aplikacji](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="43a83-523">Wprowadź zmiany w pliku kodu w edytorze online.</span><span class="sxs-lookup"><span data-stu-id="43a83-523">Make your changes to the code file in the online editor.</span></span> <span data-ttu-id="43a83-524">Zmiany zostaną zapisane automatycznie podczas pisania.</span><span class="sxs-lookup"><span data-stu-id="43a83-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
<span data-ttu-id="43a83-525">[Szybki Start kliencką dla systemu android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="43a83-525">[Android Client QuickStart]: app-service-mobile-android-get-started.md</span></span>
<span data-ttu-id="43a83-526">[Apache Cordova klienta — Szybki Start]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="43a83-526">[Apache Cordova Client QuickStart]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="43a83-527">[iOS — Szybki Start klienta]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="43a83-527">[iOS Client QuickStart]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="43a83-528">[Szybki Start klienta platformy Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="43a83-528">[Xamarin.iOS Client QuickStart]: app-service-mobile-xamarin-ios-get-started.md</span></span>
<span data-ttu-id="43a83-529">[Szybki Start klienta platformy Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="43a83-529">[Xamarin.Android Client QuickStart]: app-service-mobile-xamarin-android-get-started.md</span></span>
<span data-ttu-id="43a83-530">[Szybki Start klienta platformy Xamarin.Forms]: app-service-mobile-xamarin-forms-get-started.md</span><span class="sxs-lookup"><span data-stu-id="43a83-530">[Xamarin.Forms Client QuickStart]: app-service-mobile-xamarin-forms-get-started.md</span></span>
<span data-ttu-id="43a83-531">[Szybki Start klienta Sklepu Windows]: app-service-mobile-windows-store-dotnet-get-started.md</span><span class="sxs-lookup"><span data-stu-id="43a83-531">[Windows Store Client QuickStart]: app-service-mobile-windows-store-dotnet-get-started.md</span></span>
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
<span data-ttu-id="43a83-532">[synchronizacji danych w trybie offline]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="43a83-532">[offline data sync]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="43a83-533">[Jak skonfigurować uwierzytelnianie usługi Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="43a83-533">[How to configure Azure Active Directory Authentication]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>
<span data-ttu-id="43a83-534">[Jak skonfigurować uwierzytelnianie usługi Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md</span><span class="sxs-lookup"><span data-stu-id="43a83-534">[How to configure Facebook Authentication]: app-service-mobile-how-to-configure-facebook-authentication.md</span></span>
<span data-ttu-id="43a83-535">[Jak skonfigurować uwierzytelnianie Google]: app-service-mobile-how-to-configure-google-authentication.md</span><span class="sxs-lookup"><span data-stu-id="43a83-535">[How to configure Google Authentication]: app-service-mobile-how-to-configure-google-authentication.md</span></span>
<span data-ttu-id="43a83-536">[Jak skonfigurować Authentication firmy Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="43a83-536">[How to configure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="43a83-537">[Jak skonfigurować uwierzytelnianie w usłudze Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md</span><span class="sxs-lookup"><span data-stu-id="43a83-537">[How to configure Twitter Authentication]: app-service-mobile-how-to-configure-twitter-authentication.md</span></span>
<span data-ttu-id="43a83-538">[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="43a83-538">[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md</span></span>
<span data-ttu-id="43a83-539">[Monitorowanie usługi aplikacji Azure]: ../app-service-web/web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="43a83-539">[Monitoring an Azure App Service]: ../app-service-web/web-sites-monitor.md</span></span>
<span data-ttu-id="43a83-540">[Włączanie rejestrowania diagnostycznego w usłudze aplikacji Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md</span><span class="sxs-lookup"><span data-stu-id="43a83-540">[Enable Diagnostic Logging in Azure App Service]: ../app-service-web/web-sites-enable-diagnostic-log.md</span></span>
<span data-ttu-id="43a83-541">[Rozwiązywanie problemów z usługi aplikacji Azure w programie Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span><span class="sxs-lookup"><span data-stu-id="43a83-541">[Troubleshoot an Azure App Service in Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span></span>
<span data-ttu-id="43a83-542">[Określ wersję węzła]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="43a83-542">[specify the Node Version]: ../nodejs-specify-node-version-azure-apps.md</span></span>
<span data-ttu-id="43a83-543">[Użyj modułów węzła]: ../nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="43a83-543">[use Node modules]: ../nodejs-use-node-modules-azure-apps.md</span></span>
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
<span data-ttu-id="43a83-544">[Express]: http://expressjs.com/</span><span class="sxs-lookup"><span data-stu-id="43a83-544">[Express]: http://expressjs.com/</span></span>
<span data-ttu-id="43a83-545">[Swagger]: http://swagger.io/</span><span class="sxs-lookup"><span data-stu-id="43a83-545">[Swagger]: http://swagger.io/</span></span>

<span data-ttu-id="43a83-546">[portalu Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="43a83-546">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="43a83-547">[OData]: http://www.odata.org</span><span class="sxs-lookup"><span data-stu-id="43a83-547">[OData]: http://www.odata.org</span></span>
<span data-ttu-id="43a83-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span><span class="sxs-lookup"><span data-stu-id="43a83-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span></span>
<span data-ttu-id="43a83-549">[basicapp przykładem w witrynie GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span><span class="sxs-lookup"><span data-stu-id="43a83-549">[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span></span>
<span data-ttu-id="43a83-550">[todo przykładem w witrynie GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span><span class="sxs-lookup"><span data-stu-id="43a83-550">[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span></span>
<span data-ttu-id="43a83-551">[katalogu przykładów w witrynie GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="43a83-551">[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span></span>
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
<span data-ttu-id="43a83-552">[QueryJS]: https://github.com/Azure/queryjs</span><span class="sxs-lookup"><span data-stu-id="43a83-552">[QueryJS]: https://github.com/Azure/queryjs</span></span>
<span data-ttu-id="43a83-553">[Node.js Tools 1.1 dla programu Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span><span class="sxs-lookup"><span data-stu-id="43a83-553">[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span></span>
<span data-ttu-id="43a83-554">[pakietu Node.js mssql]: https://www.npmjs.com/package/mssql</span><span class="sxs-lookup"><span data-stu-id="43a83-554">[mssql Node.js package]: https://www.npmjs.com/package/mssql</span></span>
<span data-ttu-id="43a83-555">[programu Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span><span class="sxs-lookup"><span data-stu-id="43a83-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span></span>
<span data-ttu-id="43a83-556">[oprogramowanie pośredniczące ExpressJS]: http://expressjs.com/guide/using-middleware.html</span><span class="sxs-lookup"><span data-stu-id="43a83-556">[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html</span></span>
<span data-ttu-id="43a83-557">[Winston]: https://github.com/winstonjs/winston</span><span class="sxs-lookup"><span data-stu-id="43a83-557">[Winston]: https://github.com/winstonjs/winston</span></span>
