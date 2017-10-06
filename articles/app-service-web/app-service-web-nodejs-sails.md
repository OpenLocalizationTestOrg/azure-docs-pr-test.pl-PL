---
title: "aaaDeploy Sails.js tooAzure aplikacji sieci web usługi App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy aplikacji Node.js usługi Azure App Service. Ten samouczek pokazuje, jak jest toodeploy sails.js przy użyciu aplikacji sieci web."
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
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a><span data-ttu-id="054c2-104">Wdrażanie Sails.js tooAzure aplikacji sieci web usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="054c2-104">Deploy a Sails.js web app tooAzure App Service</span></span>
<span data-ttu-id="054c2-105">W tym samouczku przedstawiono sposób toodeploy Sails.js tooAzure aplikację usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="054c2-105">This tutorial shows you how toodeploy a Sails.js app tooAzure App Service.</span></span> <span data-ttu-id="054c2-106">W procesie hello można zgromadzonych niektórych ogólnej wiedzy na temat tooconfigure Twojego toorun aplikacji Node.js w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="054c2-106">In hello process, you can glean some general knowledge on how tooconfigure your Node.js app toorun in App Service.</span></span>

<span data-ttu-id="054c2-107">W tym miejscu dowiesz się, że przydatne umiejętności, takich jak:</span><span class="sxs-lookup"><span data-stu-id="054c2-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="054c2-108">Konfigurowanie aplikacji Sails.js, uruchom w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="054c2-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="054c2-109">Wdróż tooApp aplikacji usługi z wiersza polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="054c2-109">Deploy an app tooApp Service from hello command line.</span></span>
* <span data-ttu-id="054c2-110">Przeczytaj stderr i stdout tootroubleshoot dzienniki wszelkich problemów dotyczących wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="054c2-110">Read stderr and stdout logs tootroubleshoot any deployment issues.</span></span>
* <span data-ttu-id="054c2-111">Przechowywanie zmiennych środowiskowych poza kontrolą źródła.</span><span class="sxs-lookup"><span data-stu-id="054c2-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="054c2-112">Dostęp do zmiennych środowiskowych Azure z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="054c2-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="054c2-113">Połącz tooa bazy danych (bazy danych MongoDB).</span><span class="sxs-lookup"><span data-stu-id="054c2-113">Connect tooa database (MongoDB).</span></span>

<span data-ttu-id="054c2-114">Należy mieć praktyczną wiedzę o sails.js przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="054c2-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="054c2-115">W tym samouczku nie jest zamierzone toohelp toorunning Sail.js z problemów powiązanych ogólnie.</span><span class="sxs-lookup"><span data-stu-id="054c2-115">This tutorial is not intended toohelp you with issues related toorunning Sail.js in general.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="054c2-116">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="054c2-116">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="054c2-117">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="054c2-117">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="054c2-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modelami wdrażania</span><span class="sxs-lookup"><span data-stu-id="054c2-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="054c2-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="054c2-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="054c2-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="054c2-120">Prerequisites</span></span>
* [<span data-ttu-id="054c2-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="054c2-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="054c2-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="054c2-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="054c2-123">Git</span><span class="sxs-lookup"><span data-stu-id="054c2-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="054c2-124">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="054c2-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="054c2-125">Konto platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="054c2-125">A Microsoft Azure account.</span></span> <span data-ttu-id="054c2-126">Jeśli nie masz konta, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="054c2-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="054c2-127">Usługę [App Service](https://azure.microsoft.com/try/app-service/) możesz wypróbować, nie mając konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="054c2-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="054c2-128">Utwórz początkową aplikację i odtworzyć na temat godzinę tooan — bez karty kredytowej i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="054c2-128">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="054c2-129">Krok 1: Tworzenie i konfigurowanie sails.js przy użyciu aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="054c2-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="054c2-130">Po pierwsze szybko utworzyć domyślna aplikacja Sails.js w środowisku projektowania wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="054c2-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="054c2-131">Witaj Otwórz terminal wiersza polecenia dowolnego i `CD` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="054c2-131">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span>
2. <span data-ttu-id="054c2-132">Tworzenie aplikacji Sails.js i uruchom go:</span><span class="sxs-lookup"><span data-stu-id="054c2-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="054c2-133">Upewnij się, że można przechodzić toohello domyślną stronę główną w http://localhost:1377.</span><span class="sxs-lookup"><span data-stu-id="054c2-133">Make sure you can navigate toohello default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="054c2-134">Następnie należy włączyć rejestrowanie dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="054c2-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="054c2-135">W katalogu głównym, Utwórz plik o nazwie `iisnode.yml` i Dodaj hello następujące dwa wiersze:</span><span class="sxs-lookup"><span data-stu-id="054c2-135">In your root directory, create a file called `iisnode.yml` and add hello following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="054c2-136">Włączono rejestrowanie dla hello [iisnode](https://github.com/tjanczuk/iisnode) serwera używany toorun aplikacji Node.js w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="054c2-136">Logging is now enabled for hello [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses toorun Node.js apps.</span></span> 
    <span data-ttu-id="054c2-137">Aby uzyskać więcej informacji o jego działaniu, zobacz [jak toodebug Node.js sieci web aplikacji w usłudze Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="054c2-137">For more information on how this works, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="054c2-138">Skonfiguruj hello sails.js przy użyciu aplikacji toouse środowiska platformy Azure zmiennych.</span><span class="sxs-lookup"><span data-stu-id="054c2-138">Next, configure hello Sails.js app toouse Azure environment variables.</span></span> <span data-ttu-id="054c2-139">Otwórz config/env/production.js tooconfigure środowiska produkcyjnego i ustaw `port` i `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="054c2-139">Open config/env/production.js tooconfigure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="054c2-140">Można znaleźć w dokumentacji tych ustawień konfiguracji w [dokumentacji Sails.js](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="054c2-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="054c2-141">Następnie kodowania hello Node.js w wersji ma toouse.</span><span class="sxs-lookup"><span data-stu-id="054c2-141">Next, hardcode hello Node.js version you want toouse.</span></span> <span data-ttu-id="054c2-142">W pliku package.json, należy dodać następujące hello `engines` systemu właściwość tooset hello Node.js wersji tooone który chcemy.</span><span class="sxs-lookup"><span data-stu-id="054c2-142">In package.json, add hello following `engines` property tooset hello Node.js version tooone that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="054c2-143">Na koniec zainicjować repozytorium Git i przekazać pliki.</span><span class="sxs-lookup"><span data-stu-id="054c2-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="054c2-144">W hello katalog główny aplikacji (pliku package.json przypadku), uruchom następujące polecenia usługi Git hello:</span><span class="sxs-lookup"><span data-stu-id="054c2-144">In hello application root (where package.json is), run hello following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="054c2-145">Kod jest gotowy toobe wdrożone.</span><span class="sxs-lookup"><span data-stu-id="054c2-145">Your code is ready toobe deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="054c2-146">Krok 2: Tworzenie aplikacji platformy Azure i wdrażanie Sails.js</span><span class="sxs-lookup"><span data-stu-id="054c2-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="054c2-147">Następnie utwórz hello zasobów usługi aplikacji na platformie Azure i wdrażanie Twojego Sails.js tooit aplikacji.</span><span class="sxs-lookup"><span data-stu-id="054c2-147">Next, create hello App Service resource in Azure and deploy your Sails.js app tooit.</span></span>

1. <span data-ttu-id="054c2-148">dziennik w tooAzure w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="054c2-148">log in tooAzure like so:</span></span>

        az login

    <span data-ttu-id="054c2-149">Wykonaj hello monitu toocontinue hello logowania w przeglądarce za pomocą konta Microsoft, które ma subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="054c2-149">Follow hello prompt toocontinue hello login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="054c2-150">Ustaw hello użytkownika wdrożenia dla aplikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="054c2-150">Set hello deployment user for App Service.</span></span> <span data-ttu-id="054c2-151">Kod zostanie później wdrożony przy użyciu tych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="054c2-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="054c2-152">Utwórz [grupy zasobów](../azure-resource-manager/resource-group-overview.md) o nazwie.</span><span class="sxs-lookup"><span data-stu-id="054c2-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="054c2-153">W tym samouczku środowiska Node.js nie naprawdę potrzebny tooknow co to jest.</span><span class="sxs-lookup"><span data-stu-id="054c2-153">For this Node.js tutorial, you don't really need tooknow what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="054c2-154">toosee jakie możliwe wartości można użyć dla `<location>`, użyj hello `az appservice list-locations` polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="054c2-154">toosee what possible values you can use for `<location>`, use hello `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="054c2-155">Tworzenie "Wolne" [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) o nazwie.</span><span class="sxs-lookup"><span data-stu-id="054c2-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="054c2-156">W tym samouczku środowiska Node.js wystarczy wiedzieć, że użytkownik nie zostanie obciążona dla aplikacji sieci web w tym planie.</span><span class="sxs-lookup"><span data-stu-id="054c2-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="054c2-157">Utwórz nową aplikację sieci Web o unikatowej nazwie wprowadzonej w tagu `<app_name>`.</span><span class="sxs-lookup"><span data-stu-id="054c2-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="054c2-158">Krok 3: Konfigurowanie i wdrażanie aplikacji Sails.js</span><span class="sxs-lookup"><span data-stu-id="054c2-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="054c2-159">Skonfigurować lokalne wdrożenie Git dla nowej aplikacji sieci web z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="054c2-159">Configure local Git deployment for your new web app with hello following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="054c2-160">Otrzymasz dane wyjściowe JSON podobny do tego, co oznacza, że skonfigurowano tego hello zdalnego repozytorium Git:</span><span class="sxs-lookup"><span data-stu-id="054c2-160">You will get a JSON output like this, which means that hello remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="054c2-161">Dodaj adres URL hello w hello JSON jako zdalnego dla lokalnego repozytorium Git (nazywane `azure` dla uproszczenia).</span><span class="sxs-lookup"><span data-stu-id="054c2-161">Add hello URL in hello JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="054c2-162">Wdrażanie programu przykładowy kod toohello `azure` zdalnego Git.</span><span class="sxs-lookup"><span data-stu-id="054c2-162">Deploy your sample code toohello `azure` Git remote.</span></span> <span data-ttu-id="054c2-163">Po wyświetleniu monitu użyj poświadczeń wdrożenia hello przez skonfigurowane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="054c2-163">When prompted, use hello deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="054c2-164">Na koniec można uruchomić w przeglądarce hello działającą aplikację Azure:</span><span class="sxs-lookup"><span data-stu-id="054c2-164">Finally, just launch your live Azure app in hello browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="054c2-165">Powinien zostać wyświetlony hello tej samej stronie głównej Sails.js.</span><span class="sxs-lookup"><span data-stu-id="054c2-165">You should now see hello same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="054c2-166">Rozwiązywanie problemów z wdrożeniem</span><span class="sxs-lookup"><span data-stu-id="054c2-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="054c2-167">Jeśli zaistnieje w usłudze App Service sails.js przy użyciu aplikacji nie powiedzie się, Znajdź dzienniki stderr hello toohelp Rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="054c2-167">If your Sails.js application fails for some reason in App Service, find hello stderr logs toohelp troubleshoot it.</span></span>
<span data-ttu-id="054c2-168">Aby uzyskać więcej informacji, zobacz [jak toodebug Node.js sieci web aplikacji w usłudze Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="054c2-168">For more information, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="054c2-169">Jeśli pomyślnie uruchomił aplikacji hello dziennika stdout hello powinny być widoczne należy zapoznać się wiadomość hello:</span><span class="sxs-lookup"><span data-stu-id="054c2-169">If hello app has started successfully, hello stdout log should show you hello familiar message:</span></span>

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
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="054c2-170">Można kontrolować poziom szczegółowości dzienniki stdout hello w hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) pliku.</span><span class="sxs-lookup"><span data-stu-id="054c2-170">You can control granularity of hello stdout logs in hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-tooa-database-in-azure"></a><span data-ttu-id="054c2-171">Połączenia bazy danych tooa na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="054c2-171">Connect tooa database in Azure</span></span>
<span data-ttu-id="054c2-172">Baza danych tooa tooconnect na platformie Azure, Utwórz bazę danych hello wybranym na platformie Azure, takich jak bazy danych SQL Azure, MySQL, bazy danych MongoDB, pamięć podręczna Azure (Redis), itp. i użyj odpowiadającego hello [karty magazyn danych](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="054c2-172">tooconnect tooa database in Azure, you create hello database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use hello corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span></span> <span data-ttu-id="054c2-173">Witaj kroki opisane w tej sekcji opisano sposób tooMongoDB tooconnect za pomocą [bazy danych Azure rozwiązania Cosmos](../documentdb/documentdb-protocol-mongodb.md) bazy danych, który może obsługiwać połączeń klienckich bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="054c2-173">hello steps in this section show you how tooconnect tooMongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="054c2-174">[Tworzenie konta bazy danych rozwiązania Cosmos z obsługą protokołu bazy danych MongoDB](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="054c2-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="054c2-175">[Tworzenie kolekcji rozwiązania Cosmos bazy danych i bazy danych](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="054c2-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="054c2-176">Nazwa Hello hello kolekcji nie ma znaczenia, ale należy hello nazwa hello bazy danych, podczas łączenia z Sails.js.</span><span class="sxs-lookup"><span data-stu-id="054c2-176">hello name of hello collection doesn't matter, but you need hello name of hello database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="054c2-177">[Znajdź informacje o połączeniu hello bazy danych DB rozwiązania Cosmos](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="054c2-177">[Find hello connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="054c2-178">Z wiersza polecenia terminalu Zainstaluj hello bazy danych MongoDB karty:</span><span class="sxs-lookup"><span data-stu-id="054c2-178">From your command-line terminal, install hello MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="054c2-179">Otwórz config/connections.js i Dodaj powitania po liście toohello obiektu połączenia:</span><span class="sxs-lookup"><span data-stu-id="054c2-179">Open config/connections.js and add hello following connection object toohello list:</span></span>

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
    > <span data-ttu-id="054c2-180">Witaj `ssl: true` opcji ważne jest, ponieważ [DB rozwiązania Cosmos wymaga](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="054c2-180">hello `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="054c2-181">Dla każdej zmiennej środowiskowej (`process.env.*`), należy tooset go w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="054c2-181">For each environment variable (`process.env.*`), you need tooset it in App Service.</span></span> <span data-ttu-id="054c2-182">toodo tego hello uruchom następujące polecenia z terminala.</span><span class="sxs-lookup"><span data-stu-id="054c2-182">toodo this, run hello following commands from your terminal.</span></span> <span data-ttu-id="054c2-183">Użyj informacji o połączeniu hello Twojego rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="054c2-183">Use hello connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="054c2-184">Wprowadzanie ustawień w ustawieniach aplikacji Azure chroni poufne dane poza do kontroli źródła (Git).</span><span class="sxs-lookup"><span data-stu-id="054c2-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="054c2-185">Następnie należy skonfigurować programowania toouse środowiska hello tych samych informacji połączenia.</span><span class="sxs-lookup"><span data-stu-id="054c2-185">Next, you will configure your development environment toouse hello same connection information.</span></span>
5. <span data-ttu-id="054c2-186">Otwórz config/local.js i Dodaj powitania od obiektu połączenia:</span><span class="sxs-lookup"><span data-stu-id="054c2-186">Open config/local.js and add hello following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="054c2-187">Ta konfiguracja zastępuje ustawienia hello w pliku config/connections.js hello środowiska lokalnego.</span><span class="sxs-lookup"><span data-stu-id="054c2-187">This configuration overrides hello settings in your config/connections.js file for hello local environment.</span></span> <span data-ttu-id="054c2-188">Ten plik jest wykluczone przez hello domyślne .gitignore w projekcie, dlatego nie można zapisać w usłudze Git.</span><span class="sxs-lookup"><span data-stu-id="054c2-188">This file is excluded by hello default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="054c2-189">Teraz jesteś stanie tooconnect tooyour rozwiązania Cosmos bazy danych (bazy danych MongoDB) w bazie danych zarówno z aplikacji sieci web platformy Azure i środowiska deweloperskiego lokalnego.</span><span class="sxs-lookup"><span data-stu-id="054c2-189">Now, you are able tooconnect tooyour Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="054c2-190">Otwórz config/env/production.js tooconfigure środowiska produkcyjnego i dodaj następujące hello `models` obiektu:</span><span class="sxs-lookup"><span data-stu-id="054c2-190">Open config/env/production.js tooconfigure your production environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="054c2-191">Otwórz config/env/development.js tooconfigure środowiska projektowego i dodaj następujące hello `models` obiektu:</span><span class="sxs-lookup"><span data-stu-id="054c2-191">Open config/env/development.js tooconfigure your development environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="054c2-192">`migrate: 'alter'`pozwala używać toocreate funkcji migracji bazy danych i łatwo aktualizować kolekcje bazy danych lub tabel.</span><span class="sxs-lookup"><span data-stu-id="054c2-192">`migrate: 'alter'` lets you use database migration features toocreate and update database collections or tables easily.</span></span> <span data-ttu-id="054c2-193">Jednak `migrate: 'safe'` służy do środowiska Azure (środowisko produkcyjne), ponieważ Sails.js pozwalają toouse `migrate: 'alter'` w środowisku produkcyjnym (zobacz [dokumentacji Sails.js](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="054c2-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you toouse `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="054c2-194">Z hello terminali [Generowanie](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) Sails.js [plan interfejsu API](http://sailsjs.org/documentation/concepts/blueprints) tak jak zwykle następnie należy uruchomić `sails lift` do tworzenia bazy danych hello sails.js przy użyciu bazy danych migracji.</span><span class="sxs-lookup"><span data-stu-id="054c2-194">From hello terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create hello database with Sails.js database migration.</span></span> <span data-ttu-id="054c2-195">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="054c2-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="054c2-196">Witaj `mywidget` modelu wygenerowanym przez to polecenie jest pusty, ale firma Microsoft może być używany tooshow, że istnieje łączność z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="054c2-196">hello `mywidget` model generated by this command is empty, but we can use it tooshow that we have database connectivity.</span></span>
    <span data-ttu-id="054c2-197">Po uruchomieniu `sails lift`, tworzy hello Brak kolekcje i tabel dla hello modele używany przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="054c2-197">When you run `sails lift`, it creates hello missing collections and tables for hello models your app uses.</span></span>
9. <span data-ttu-id="054c2-198">Interfejs API hello plan utworzony w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="054c2-198">Access hello blueprint API you just created in hello browser.</span></span> <span data-ttu-id="054c2-199">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="054c2-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="054c2-200">Witaj interfejsu API powinien zwrócić tooyou wstecz hello utworzony wpis w oknie przeglądarki hello, co oznacza, że pomyślnie utworzono kolekcję.</span><span class="sxs-lookup"><span data-stu-id="054c2-200">hello API should return hello created entry back tooyou in hello browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="054c2-201">Teraz push tooAzure Twoje zmiany i Przeglądaj toomake aplikacji tooyour się, że nadal działa.</span><span class="sxs-lookup"><span data-stu-id="054c2-201">Now, push your changes tooAzure, and browse tooyour app toomake sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="054c2-202">Hello plan interfejsu API dostępu do aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="054c2-202">Access hello blueprint API of your Azure web app.</span></span> <span data-ttu-id="054c2-203">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="054c2-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="054c2-204">Jeśli hello interfejsu API zwraca nowy wpis innego, aplikacji sieci web platformy Azure rozmawia tooyour rozwiązania Cosmos bazy danych (bazy danych MongoDB) w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="054c2-204">If hello API returns another new entry, then your Azure web app is talking tooyour Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="054c2-205">Więcej zasobów</span><span class="sxs-lookup"><span data-stu-id="054c2-205">More resources</span></span>
* [<span data-ttu-id="054c2-206">Rozpoczynanie pracy z aplikacjami sieci web Node.js w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="054c2-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="054c2-207">Using Node.js Modules with Azure applications (Używanie modułów Node.js z aplikacjami platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="054c2-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
