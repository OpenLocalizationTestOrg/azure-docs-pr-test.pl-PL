---
title: "Wdrażanie aplikacji sieci web sails.js przy użyciu usługi Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrożyć aplikację Node.js usługi Azure App Service. Ten samouczek pokazuje, jak wdrożyć aplikację sieci web Sails.js."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: e36fc5f5273f98c3cca91973db9910f32443ec7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a><span data-ttu-id="79575-104">Wdrażanie aplikacji sieci Web Sails.js przy użyciu usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="79575-104">Deploy a Sails.js web app to Azure App Service</span></span>
<span data-ttu-id="79575-105">Ten samouczek przedstawia sposób wdrażania aplikacji Sails.js w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="79575-105">This tutorial shows you how to deploy a Sails.js app to Azure App Service.</span></span> <span data-ttu-id="79575-106">W procesie można zgromadzonych niektórych ogólnej wiedzy na temat konfigurowania aplikacji Node.js do uruchamiania w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="79575-106">In the process, you can glean some general knowledge on how to configure your Node.js app to run in App Service.</span></span>

<span data-ttu-id="79575-107">W tym miejscu dowiesz się, że przydatne umiejętności, takich jak:</span><span class="sxs-lookup"><span data-stu-id="79575-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="79575-108">Konfigurowanie aplikacji Sails.js, uruchom w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="79575-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="79575-109">Wdrażanie aplikacji w usłudze App Service z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="79575-109">Deploy an app to App Service from the command line.</span></span>
* <span data-ttu-id="79575-110">Przeczytaj dzienniki stderr i stdout rozwiązywać problemy z wdrażaniem.</span><span class="sxs-lookup"><span data-stu-id="79575-110">Read stderr and stdout logs to troubleshoot any deployment issues.</span></span>
* <span data-ttu-id="79575-111">Przechowywanie zmiennych środowiskowych poza kontrolą źródła.</span><span class="sxs-lookup"><span data-stu-id="79575-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="79575-112">Dostęp do zmiennych środowiskowych Azure z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="79575-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="79575-113">Połączenie z bazą danych (bazy danych MongoDB).</span><span class="sxs-lookup"><span data-stu-id="79575-113">Connect to a database (MongoDB).</span></span>

<span data-ttu-id="79575-114">Należy mieć praktyczną wiedzę o sails.js przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="79575-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="79575-115">W tym samouczku nie jest przeznaczona do pomocy w rozwiązaniu problemy związane z uruchamianiem Sail.js ogólnie.</span><span class="sxs-lookup"><span data-stu-id="79575-115">This tutorial is not intended to help you with issues related to running Sail.js in general.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="79575-116">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="79575-116">CLI versions to complete the task</span></span>

<span data-ttu-id="79575-117">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="79575-117">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="79575-118">[Interfejs wiersza polecenia platformy Azure w wersji 1.0](app-service-web-nodejs-sails-cli-nodejs.md) — nasz interfejs wiersza polecenia dla klasycznego modelu wdrażania i modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="79575-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="79575-119">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](app-service-web-nodejs-sails.md) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="79575-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79575-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="79575-120">Prerequisites</span></span>
* [<span data-ttu-id="79575-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="79575-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="79575-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="79575-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="79575-123">Git</span><span class="sxs-lookup"><span data-stu-id="79575-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="79575-124">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="79575-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="79575-125">Konto platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="79575-125">A Microsoft Azure account.</span></span> <span data-ttu-id="79575-126">Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="79575-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="79575-127">Usługę [App Service](https://azure.microsoft.com/try/app-service/) możesz wypróbować, nie mając konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="79575-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="79575-128">Utwórz aplikację startową i testuj ją nawet przez godzinę — bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="79575-128">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="79575-129">Krok 1: Tworzenie i konfigurowanie sails.js przy użyciu aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="79575-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="79575-130">Po pierwsze szybko utworzyć domyślna aplikacja Sails.js w środowisku projektowania wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="79575-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="79575-131">Otwórz wybrany terminal wiersza polecenia dowolnego i `CD` do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="79575-131">Open the command-line terminal of your choice and `CD` to a working directory.</span></span>
2. <span data-ttu-id="79575-132">Tworzenie aplikacji Sails.js i uruchom go:</span><span class="sxs-lookup"><span data-stu-id="79575-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="79575-133">Upewnij się, że można przejść do domyślnej strony głównej w http://localhost:1377.</span><span class="sxs-lookup"><span data-stu-id="79575-133">Make sure you can navigate to the default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="79575-134">Następnie należy włączyć rejestrowanie dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="79575-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="79575-135">W katalogu głównym, Utwórz plik o nazwie `iisnode.yml` i dodaj następujące dwa wiersze:</span><span class="sxs-lookup"><span data-stu-id="79575-135">In your root directory, create a file called `iisnode.yml` and add the following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="79575-136">Włączono rejestrowanie dla [iisnode](https://github.com/tjanczuk/iisnode) serwera, który używa usługi Azure App Service uruchamia aplikacje Node.js.</span><span class="sxs-lookup"><span data-stu-id="79575-136">Logging is now enabled for the [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses to run Node.js apps.</span></span> 
    <span data-ttu-id="79575-137">Aby uzyskać więcej informacji o jego działaniu, zobacz [debugowanie aplikacji sieci web Node.js w usłudze Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="79575-137">For more information on how this works, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="79575-138">Skonfiguruj aplikację Sails.js do używania zmiennych środowiskowych systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="79575-138">Next, configure the Sails.js app to use Azure environment variables.</span></span> <span data-ttu-id="79575-139">Otwórz config/env/production.js do skonfigurowania środowiska produkcyjnego i `port` i `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="79575-139">Open config/env/production.js to configure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="79575-140">Można znaleźć w dokumentacji tych ustawień konfiguracji w [dokumentacji Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="79575-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="79575-141">Następnie kodowania wersji środowiska Node.js, który ma być używany.</span><span class="sxs-lookup"><span data-stu-id="79575-141">Next, hardcode the Node.js version you want to use.</span></span> <span data-ttu-id="79575-142">W pliku package.json, Dodaj następujący `engines` właściwość umożliwiająca ustawienie wersji środowiska Node.js na taki, który chcemy.</span><span class="sxs-lookup"><span data-stu-id="79575-142">In package.json, add the following `engines` property to set the Node.js version to one that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="79575-143">Na koniec zainicjować repozytorium Git i przekazać pliki.</span><span class="sxs-lookup"><span data-stu-id="79575-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="79575-144">W katalogu głównym aplikacji (pliku package.json przypadku) uruchom następujące polecenia Git:</span><span class="sxs-lookup"><span data-stu-id="79575-144">In the application root (where package.json is), run the following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="79575-145">Kod jest gotowa do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="79575-145">Your code is ready to be deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="79575-146">Krok 2: Tworzenie aplikacji platformy Azure i wdrażanie Sails.js</span><span class="sxs-lookup"><span data-stu-id="79575-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="79575-147">Następnie utwórz zasób usługi aplikacji na platformie Azure i wdrażanie aplikacji Sails.js do niego.</span><span class="sxs-lookup"><span data-stu-id="79575-147">Next, create the App Service resource in Azure and deploy your Sails.js app to it.</span></span>

1. <span data-ttu-id="79575-148">Zaloguj się do platformy Azure w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="79575-148">log in to Azure like so:</span></span>

        az login

    <span data-ttu-id="79575-149">Postępuj zgodnie z wyświetlanymi instrukcjami, aby kontynuować logowanie w przeglądarce za pomocą konta Microsoft zawierającego subskrypcję Azure.</span><span class="sxs-lookup"><span data-stu-id="79575-149">Follow the prompt to continue the login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="79575-150">Ustaw użytkownika wdrożenia dla usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="79575-150">Set the deployment user for App Service.</span></span> <span data-ttu-id="79575-151">Kod zostanie później wdrożony przy użyciu tych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="79575-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="79575-152">Utwórz [grupy zasobów](../azure-resource-manager/resource-group-overview.md) o nazwie.</span><span class="sxs-lookup"><span data-stu-id="79575-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="79575-153">W tym samouczku środowiska Node.js nie naprawdę musisz wiedzieć, co to jest.</span><span class="sxs-lookup"><span data-stu-id="79575-153">For this Node.js tutorial, you don't really need to know what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="79575-154">Aby sprawdzić, jakich wartości można użyć dla lokalizacji `<location>`, użyj polecenia interfejsu wiersza polecenia `az appservice list-locations`.</span><span class="sxs-lookup"><span data-stu-id="79575-154">To see what possible values you can use for `<location>`, use the `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="79575-155">Tworzenie "Wolne" [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) o nazwie.</span><span class="sxs-lookup"><span data-stu-id="79575-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="79575-156">W tym samouczku środowiska Node.js wystarczy wiedzieć, że użytkownik nie zostanie obciążona dla aplikacji sieci web w tym planie.</span><span class="sxs-lookup"><span data-stu-id="79575-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="79575-157">Utwórz nową aplikację sieci Web o unikatowej nazwie wprowadzonej w tagu `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="79575-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="79575-158">Krok 3: Konfigurowanie i wdrażanie aplikacji Sails.js</span><span class="sxs-lookup"><span data-stu-id="79575-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="79575-159">Skonfiguruj lokalne wdrożenie narzędzia Git dla aplikacji sieci Web za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="79575-159">Configure local Git deployment for your new web app with the following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="79575-160">Otrzymasz dane wyjściowe JSON podobne do następujących, co oznacza, że skonfigurowano zdalne repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="79575-160">You will get a JSON output like this, which means that the remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="79575-161">Dodaj adres URL w formacie JSON jako zdalny obiekt narzędzia Git lokalnego repozytorium Git (nazywanego dla uproszczenia `azure`).</span><span class="sxs-lookup"><span data-stu-id="79575-161">Add the URL in the JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="79575-162">Wdróż przykładowy kod w zdalnym obiekcie narzędzia Git `azure`.</span><span class="sxs-lookup"><span data-stu-id="79575-162">Deploy your sample code to the `azure` Git remote.</span></span> <span data-ttu-id="79575-163">Gdy zostanie wyświetlony odpowiedni monit, użyj skonfigurowanych wcześniej poświadczeń wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="79575-163">When prompted, use the deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="79575-164">Na koniec można uruchomić działającą aplikację Azure w przeglądarce:</span><span class="sxs-lookup"><span data-stu-id="79575-164">Finally, just launch your live Azure app in the browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="79575-165">Powinna zostać wyświetlona strona główna sails.js przy użyciu tego samego.</span><span class="sxs-lookup"><span data-stu-id="79575-165">You should now see the same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="79575-166">Rozwiązywanie problemów z wdrożeniem</span><span class="sxs-lookup"><span data-stu-id="79575-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="79575-167">Jeśli zaistnieje w usłudze App Service sails.js przy użyciu aplikacji nie powiedzie się, Znajdź dzienniki stderr, aby ułatwić rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="79575-167">If your Sails.js application fails for some reason in App Service, find the stderr logs to help troubleshoot it.</span></span>
<span data-ttu-id="79575-168">Aby uzyskać więcej informacji, zobacz [debugowanie aplikacji sieci web Node.js w usłudze Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="79575-168">For more information, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="79575-169">Jeśli aplikacja została uruchomiona pomyślnie, dziennika stdout powinien być wyświetlony zostanie znanych komunikat:</span><span class="sxs-lookup"><span data-stu-id="79575-169">If the app has started successfully, the stdout log should show you the familiar message:</span></span>

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="79575-170">Można kontrolować poziom szczegółowości dzienniki stdout w [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) pliku.</span><span class="sxs-lookup"><span data-stu-id="79575-170">You can control granularity of the stdout logs in the [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-to-a-database-in-azure"></a><span data-ttu-id="79575-171">Połączenie z bazą danych na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="79575-171">Connect to a database in Azure</span></span>
<span data-ttu-id="79575-172">Do połączenia z bazą danych na platformie Azure, utworzyć bazę danych, wybranych przez użytkownika na platformie Azure, takich jak bazy danych SQL Azure, MySQL, bazy danych MongoDB, pamięć podręczna Azure (Redis), itp. i użyj odpowiadającego [karty magazyn danych](https://github.com/balderdashy/sails#compatibility) się z nią połączyć.</span><span class="sxs-lookup"><span data-stu-id="79575-172">To connect to a database in Azure, you create the database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use the corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) to connect to it.</span></span> <span data-ttu-id="79575-173">Kroki opisane w tej sekcji opisano sposób nawiązywania połączenia z bazy danych MongoDB przy użyciu [bazy danych Azure rozwiązania Cosmos](../documentdb/documentdb-protocol-mongodb.md) bazy danych, który może obsługiwać połączeń klienckich bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="79575-173">The steps in this section show you how to connect to MongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="79575-174">[Tworzenie konta bazy danych rozwiązania Cosmos z obsługą protokołu bazy danych MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="79575-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="79575-175">[Tworzenie kolekcji rozwiązania Cosmos bazy danych i bazy danych](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="79575-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="79575-176">Nazwa kolekcji nie ma znaczenia, ale potrzebna jest nazwa bazy danych podczas nawiązywania połączenia z Sails.js.</span><span class="sxs-lookup"><span data-stu-id="79575-176">The name of the collection doesn't matter, but you need the name of the database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="79575-177">[Znajdź informacje o połączeniu dla bazy danych DB rozwiązania Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="79575-177">[Find the connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="79575-178">Z wiersza polecenia terminalu należy zainstalować adapter bazy danych MongoDB:</span><span class="sxs-lookup"><span data-stu-id="79575-178">From your command-line terminal, install the MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="79575-179">Otwórz config/connections.js i Dodaj następujący obiekt połączenie do listy:</span><span class="sxs-lookup"><span data-stu-id="79575-179">Open config/connections.js and add the following connection object to the list:</span></span>

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > <span data-ttu-id="79575-180">`ssl: true` Ważne jest opcja, ponieważ [DB rozwiązania Cosmos wymaga](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="79575-180">The `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="79575-181">Dla każdej zmiennej środowiskowej (`process.env.*`), należy ustawić go w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="79575-181">For each environment variable (`process.env.*`), you need to set it in App Service.</span></span> <span data-ttu-id="79575-182">Aby to zrobić, uruchom następujące polecenia z terminala.</span><span class="sxs-lookup"><span data-stu-id="79575-182">To do this, run the following commands from your terminal.</span></span> <span data-ttu-id="79575-183">Użyj informacji o połączeniu dla Twojej bazy danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="79575-183">Use the connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="79575-184">Wprowadzanie ustawień w ustawieniach aplikacji Azure chroni poufne dane poza do kontroli źródła (Git).</span><span class="sxs-lookup"><span data-stu-id="79575-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="79575-185">Następnie należy skonfigurować środowiska deweloperskiego, aby użyć tego samego informacji o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="79575-185">Next, you will configure your development environment to use the same connection information.</span></span>
5. <span data-ttu-id="79575-186">Otwórz config/local.js i Dodaj następujący obiekt połączenia:</span><span class="sxs-lookup"><span data-stu-id="79575-186">Open config/local.js and add the following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="79575-187">Ta konfiguracja zastępuje ustawienia w pliku config/connections.js w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="79575-187">This configuration overrides the settings in your config/connections.js file for the local environment.</span></span> <span data-ttu-id="79575-188">Ten plik jest wykluczone przez domyślne .gitignore w projekcie, dlatego nie można zapisać w usłudze Git.</span><span class="sxs-lookup"><span data-stu-id="79575-188">This file is excluded by the default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="79575-189">Teraz jest możliwość połączenia z bazą danych rozwiązania Cosmos bazy danych (bazy danych MongoDB) zarówno z aplikacji sieci web platformy Azure i środowiska deweloperskiego lokalnego.</span><span class="sxs-lookup"><span data-stu-id="79575-189">Now, you are able to connect to your Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="79575-190">Otwórz config/env/production.js do konfigurowania środowiska produkcyjnego i dodaj następujące `models` obiektu:</span><span class="sxs-lookup"><span data-stu-id="79575-190">Open config/env/production.js to configure your production environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="79575-191">Otwórz config/env/development.js do konfigurowania środowiska deweloperskiego i dodaj następujące `models` obiektu:</span><span class="sxs-lookup"><span data-stu-id="79575-191">Open config/env/development.js to configure your development environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="79575-192">`migrate: 'alter'`Umożliwia tworzenie i aktualizowanie kolekcji bazy danych lub tabel łatwo przy użyciu funkcji migracji bazy danych.</span><span class="sxs-lookup"><span data-stu-id="79575-192">`migrate: 'alter'` lets you use database migration features to create and update database collections or tables easily.</span></span> <span data-ttu-id="79575-193">Jednak `migrate: 'safe'` służy do środowiska Azure (środowisko produkcyjne), ponieważ Sails.js nie będzie można korzystać `migrate: 'alter'` w środowisku produkcyjnym (zobacz [dokumentacji Sails.js](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="79575-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you to use `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="79575-194">Z poziomu terminala [Generowanie](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) Sails.js [plan interfejsu API](http://sailsjs.org/documentation/concepts/blueprints) tak jak zwykle następnie należy uruchomić `sails lift` utworzyć bazę danych z Sails.js migracja bazy danych.</span><span class="sxs-lookup"><span data-stu-id="79575-194">From the terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create the database with Sails.js database migration.</span></span> <span data-ttu-id="79575-195">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="79575-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="79575-196">`mywidget` Modelu wygenerowanym przez to polecenie jest pusty, ale możemy ich użyć do wyświetlenia, że istnieje łączność z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="79575-196">The `mywidget` model generated by this command is empty, but we can use it to show that we have database connectivity.</span></span>
    <span data-ttu-id="79575-197">Po uruchomieniu `sails lift`, tworzy Brak kolekcje i tabel dla modeli aplikacji używa.</span><span class="sxs-lookup"><span data-stu-id="79575-197">When you run `sails lift`, it creates the missing collections and tables for the models your app uses.</span></span>
9. <span data-ttu-id="79575-198">Dostęp do planu API właśnie utworzony w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="79575-198">Access the blueprint API you just created in the browser.</span></span> <span data-ttu-id="79575-199">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="79575-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="79575-200">Interfejs API należy wrócić utworzony wpis do w oknie przeglądarki, co oznacza, że pomyślnie utworzono kolekcję.</span><span class="sxs-lookup"><span data-stu-id="79575-200">The API should return the created entry back to you in the browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="79575-201">Teraz Wypchnij zmiany do platformy Azure i przejdź do aplikacji w taki sposób, aby upewnić się, że nadal działa.</span><span class="sxs-lookup"><span data-stu-id="79575-201">Now, push your changes to Azure, and browse to your app to make sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="79575-202">Dostęp do aplikacji sieci web platformy Azure plan interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="79575-202">Access the blueprint API of your Azure web app.</span></span> <span data-ttu-id="79575-203">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="79575-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="79575-204">Jeśli interfejs API zwraca nowy wpis innego, aplikacji sieci web platformy Azure jest rozmowie z bazy danych DB rozwiązania Cosmos (MongoDB).</span><span class="sxs-lookup"><span data-stu-id="79575-204">If the API returns another new entry, then your Azure web app is talking to your Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="79575-205">Więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="79575-205">More resources</span></span>
* [<span data-ttu-id="79575-206">Rozpoczynanie pracy z aplikacjami sieci web Node.js w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="79575-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="79575-207">Using Node.js Modules with Azure applications (Używanie modułów Node.js z aplikacjami platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="79575-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
