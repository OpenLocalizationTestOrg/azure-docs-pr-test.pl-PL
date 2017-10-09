---
title: "Aplikacja aaaNode.js interfejsu API w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate interfejsu API RESTful środowiska Node.js i wdróż je tooan interfejsu API aplikacji w usłudze Azure App Service."
services: app-service\api
documentationcenter: node
author: bradygaster
manager: erikre
editor: 
ms.assetid: a820e400-06af-4852-8627-12b3db4a8e70
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: rachelap
ms.openlocfilehash: 3b3229c1453b6ca4d06bef26f476e92afda4e244
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a><span data-ttu-id="52607-103">Tworzenie interfejsu API RESTful środowiska Node.js i wdrażanie jej aplikacji tooan interfejsu API na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="52607-103">Build a Node.js RESTful API and deploy it tooan API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="52607-104">Ta opcja szybkiego startu przedstawia jak toocreate interfejsu API REST, napisanej dla platformy Node.js [Express](http://expressjs.com/)za pomocą [Swagger](http://swagger.io/) definicji i wdrażania go jako [aplikacji interfejsu API](app-service-api-apps-why-best-platform.md) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="52607-104">This quickstart shows how toocreate a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="52607-105">Tworzenie aplikacji hello za pomocą narzędzia wiersza polecenia, skonfiguruj zasoby z hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)i wdrażanie aplikacji hello przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="52607-105">You create hello app using command-line tools, configure resources with hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy hello app using Git.</span></span>  <span data-ttu-id="52607-106">Gdy wszystko będzie gotowe, uzyskasz funkcjonalny interfejs API REST działający na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="52607-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52607-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="52607-107">Prerequisites</span></span>

* [<span data-ttu-id="52607-108">Git</span><span class="sxs-lookup"><span data-stu-id="52607-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="52607-109">Node.js i NPM</span><span class="sxs-lookup"><span data-stu-id="52607-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="52607-110">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="52607-110">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="52607-111">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="52607-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="52607-112">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="52607-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="52607-113">Przygotowywanie środowiska</span><span class="sxs-lookup"><span data-stu-id="52607-113">Prepare your environment</span></span>

1. <span data-ttu-id="52607-114">W oknie terminalu Uruchom hello następujące polecenia tooclone hello próbki tooyour lokalnego komputera.</span><span class="sxs-lookup"><span data-stu-id="52607-114">In a terminal window, run hello following command tooclone hello sample tooyour local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="52607-115">Zmień katalog toohello, który zawiera hello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="52607-115">Change toohello directory that contains hello sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="52607-116">Zainstaluj [narzędzie Swaggerize](https://www.npmjs.com/package/swaggerize-express) na maszynie lokalnej.</span><span class="sxs-lookup"><span data-stu-id="52607-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="52607-117">Swaggerize to narzędzie generujące kod Node.js dla interfejsu API REST na podstawie definicji Swagger.</span><span class="sxs-lookup"><span data-stu-id="52607-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="52607-118">Generowanie kodu Node.js</span><span class="sxs-lookup"><span data-stu-id="52607-118">Generate Node.js code</span></span> 

<span data-ttu-id="52607-119">W tej części samouczka hello modele przepływu pracy programowania w którym najpierw utworzyć metadane programu Swagger i użyć tego tooscaffold (automatycznego generowania) kodu serwera na powitania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="52607-119">This section of hello tutorial models an API development workflow in which you create Swagger metadata first and use that tooscaffold (auto-generate) server code for hello API.</span></span> 

<span data-ttu-id="52607-120">Zmień katalog toohello *start* folderu, i uruchom `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="52607-120">Change directory toohello *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="52607-121">Narzędzie swaggerize tworzy projekt Node.js do interfejsu API z definicji struktury Swagger hello w *api.json*.</span><span class="sxs-lookup"><span data-stu-id="52607-121">Swaggerize creates a Node.js project for your API from hello Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="52607-122">Kiedy w narzędziu Swaggerize zostanie wyświetlony monit o podanie nazwy projektu, użyj nazwy *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="52607-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a><span data-ttu-id="52607-123">Dostosowywanie hello kodu projektu</span><span class="sxs-lookup"><span data-stu-id="52607-123">Customize hello project code</span></span>

1. <span data-ttu-id="52607-124">Kopiuj hello *lib* folderu do hello *ContactList* folder utworzony przez `yo swaggerize`, zmień katalog na *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="52607-124">Copy hello *lib* folder into hello *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="52607-125">Zainstaluj hello `jsonpath` i `swaggerize-ui` moduły NPM.</span><span class="sxs-lookup"><span data-stu-id="52607-125">Install hello `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="52607-126">Zastąp kod hello w hello *handlers/contacts.js* z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="52607-126">Replace hello code in hello *handlers/contacts.js* with hello following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="52607-127">Ten kod zawiera dane JSON hello przechowywane w *lib/contacts.json* obsługiwanej przez *lib/contactRepository.js*.</span><span class="sxs-lookup"><span data-stu-id="52607-127">This code uses hello JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="52607-128">nowe Hello *contacts.js* kod zwraca wszystkie kontakty w repozytorium hello jako ładunek JSON.</span><span class="sxs-lookup"><span data-stu-id="52607-128">hello new *contacts.js* code returns all contacts in hello repository as a JSON payload.</span></span> 

4. <span data-ttu-id="52607-129">Zastąp kod hello w hello **handlers/contacts/{id}.js** pliku z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="52607-129">Replace hello code in hello **handlers/contacts/{id}.js** file with hello following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="52607-130">Ten kod umożliwia używanie ścieżki tooreturn zmiennej tylko hello kontaktu z danym identyfikatorem.</span><span class="sxs-lookup"><span data-stu-id="52607-130">This code lets you use a path variable tooreturn only hello contact with a given ID.</span></span>

5. <span data-ttu-id="52607-131">Zastąp kod hello w **server.js** z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="52607-131">Replace hello code in **server.js** with hello following code:</span></span>

    ```javascript
    'use strict';

    var port = process.env.PORT || 8000; 

    var http = require('http');
    var express = require('express');
    var bodyParser = require('body-parser');
    var swaggerize = require('swaggerize-express');
    var swaggerUi = require('swaggerize-ui'); 
    var path = require('path');
    var fs = require("fs");
    
    fs.existsSync = fs.existsSync || require('path').existsSync;

    var app = express();

    var server = http.createServer(app);

    app.use(bodyParser.json());

    app.use(swaggerize({
        api: path.resolve('./config/swagger.json'),
        handlers: path.resolve('./handlers'),
        docspath: '/swagger' 
    }));

    // change four
    app.use('/docs', swaggerUi({
        docs: '/swagger'  
    }));

    server.listen(port, function () { 
    });
    ```   

    <span data-ttu-id="52607-132">Ten kod sprawia, że niektóre toolet niewielkich zmian, jego działania w usłudze Azure App Service i udostępnia interfejs sieci web interactive dla interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="52607-132">This code makes some small changes toolet it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-hello-api-locally"></a><span data-ttu-id="52607-133">Test hello interfejsu API lokalnie</span><span class="sxs-lookup"><span data-stu-id="52607-133">Test hello API locally</span></span>

1. <span data-ttu-id="52607-134">Uruchomić aplikację Node.js hello</span><span class="sxs-lookup"><span data-stu-id="52607-134">Start up hello Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="52607-135">Przeglądaj toohttp://localhost:8000 / kontaktuje tooview hello JSON dla hello całej listy kontaktów.</span><span class="sxs-lookup"><span data-stu-id="52607-135">Browse toohttp://localhost:8000/contacts tooview hello JSON for hello entire contact list.</span></span>
   
   ```json
    {
        "id": 1,
        "name": "Barney Poland",
        "email": "barney@contoso.com"
    },
    {
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    },
    {
        "id": 3,
        "name": "Lora Riggs",
        "email": "lora@contoso.com"
    }
   ```

3. <span data-ttu-id="52607-136">Przeglądaj toohttp://localhost:8000/kontakty/2 tooview hello kontaktować się z `id` liczby dwa.</span><span class="sxs-lookup"><span data-stu-id="52607-136">Browse toohttp://localhost:8000/contacts/2 tooview hello contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="52607-137">Za pomocą interfejsu sieci web struktury Swagger hello na http://localhost: 8000/docs API hello testu.</span><span class="sxs-lookup"><span data-stu-id="52607-137">Test hello API using hello Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Interfejs sieci web struktury Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="52607-139"><a id="createapiapp"></a> Tworzenie aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="52607-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="52607-140">W tej sekcji użyjesz hello Azure CLI 2.0 toocreate hello zasobów toohost hello interfejsu API w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="52607-140">In this section, you use hello Azure CLI 2.0 toocreate hello resources toohost hello API on Azure App Service.</span></span> 

1.  <span data-ttu-id="52607-141">Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="52607-141">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="52607-142">Jeśli masz wiele subskrypcji Azure, zmień hello domyślne subskrypcji toohello żądana jeden.</span><span class="sxs-lookup"><span data-stu-id="52607-142">If you have multiple Azure subscriptions, change hello default subscription toohello desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a><span data-ttu-id="52607-143">Wdrażanie hello API za pomocą narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="52607-143">Deploy hello API with Git</span></span>

<span data-ttu-id="52607-144">Wdrażanie aplikacji interfejsu API toohello kodu przez wypychanie zatwierdzeń z sieci lokalnej tooAzure repozytorium Git usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="52607-144">Deploy your code toohello API app by pushing commits from your local Git repository tooAzure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="52607-145">Inicjowanie nowego repozytorium w hello *ContactList* katalogu.</span><span class="sxs-lookup"><span data-stu-id="52607-145">Initialize a new repo in hello *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="52607-146">Wyklucz hello *node_modules* Katalog utworzony przez npm we wcześniejszym kroku w samouczku hello z repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="52607-146">Exclude hello *node_modules* directory created by npm in an earlier step in hello tutorial from Git.</span></span> <span data-ttu-id="52607-147">Utwórz nową `.gitignore` plików w bieżącym katalogu hello i Dodaj powitania po tekst na nowy wiersz w pliku hello w dowolnym miejscu.</span><span class="sxs-lookup"><span data-stu-id="52607-147">Create a new `.gitignore` file in hello current directory and add hello following text on a new line anywhere in hello file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="52607-148">Potwierdź hello `node_modules` folderu zostanie zignorowany z `git status`.</span><span class="sxs-lookup"><span data-stu-id="52607-148">Confirm hello `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="52607-149">Zatwierdź hello zmiany toohello repozytorium.</span><span class="sxs-lookup"><span data-stu-id="52607-149">Commit hello changes toohello repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a><span data-ttu-id="52607-150">Test hello interfejsu API na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="52607-150">Test hello API  in Azure</span></span>

1. <span data-ttu-id="52607-151">Otwórz toohttp://app_name.azurewebsites.net/contacts przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="52607-151">Open a browser toohttp://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="52607-152">Zostanie wyświetlony hello tego samego JSON zwracane jako podczas żądania hello lokalnie wcześniej w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="52607-152">You see hello same JSON returned as when you made hello request locally earlier in hello tutorial.</span></span>

   ```json
   {
       "id": 1,
       "name": "Barney Poland",
       "email": "barney@contoso.com"
   },
   {
       "id": 2,
       "name": "Lacy Barrera",
       "email": "lacy@contoso.com"
   },
   {
       "id": 3,
       "name": "Lora Riggs",
       "email": "lora@contoso.com"
   }
   ```

2. <span data-ttu-id="52607-153">W przeglądarce Przejdź toohello `http://app_name.azurewebsites.net/docs` tootry punktu końcowego limit hello interfejs użytkownika programu Swagger, działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="52607-153">In a browser, go toohello `http://app_name.azurewebsites.net/docs` endpoint tootry out hello Swagger UI running on Azure.</span></span>

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="52607-155">Teraz można wdrożyć aktualizacje toohello przykładowy interfejs API tooAzure po prostu wypychając repozytorium Azure Git toohello zatwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="52607-155">You can now deploy updates toohello sample API tooAzure simply by pushing commits toohello Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="52607-156">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="52607-156">Clean up</span></span>

<span data-ttu-id="52607-157">tooclean zasobów hello utworzone w tym Szybki Start, uruchom następujące polecenie z wiersza polecenia platformy Azure hello:</span><span class="sxs-lookup"><span data-stu-id="52607-157">tooclean up hello resources created in this quickstart, run hello following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="52607-158">Następny krok</span><span class="sxs-lookup"><span data-stu-id="52607-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="52607-159">Używanie aplikacji interfejsu API z klientów JavaScript za pomocą mechanizmu CORS</span><span class="sxs-lookup"><span data-stu-id="52607-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

