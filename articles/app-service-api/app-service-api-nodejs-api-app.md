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
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a>Tworzenie interfejsu API RESTful środowiska Node.js i wdrażanie jej aplikacji tooan interfejsu API na platformie Azure
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Ta opcja szybkiego startu przedstawia jak toocreate interfejsu API REST, napisanej dla platformy Node.js [Express](http://expressjs.com/)za pomocą [Swagger](http://swagger.io/) definicji i wdrażania go jako [aplikacji interfejsu API](app-service-api-apps-why-best-platform.md) na platformie Azure. Tworzenie aplikacji hello za pomocą narzędzia wiersza polecenia, skonfiguruj zasoby z hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)i wdrażanie aplikacji hello przy użyciu narzędzia Git.  Gdy wszystko będzie gotowe, uzyskasz funkcjonalny interfejs API REST działający na platformie Azure.

## <a name="prerequisites"></a>Wymagania wstępne

* [Git](https://git-scm.com/)
* [Node.js i NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-your-environment"></a>Przygotowywanie środowiska

1. W oknie terminalu Uruchom hello następujące polecenia tooclone hello próbki tooyour lokalnego komputera.

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. Zmień katalog toohello, który zawiera hello przykładowy kod.

    ```bash
    cd app-service-api-node-contact-list
    ```

3. Zainstaluj [narzędzie Swaggerize](https://www.npmjs.com/package/swaggerize-express) na maszynie lokalnej. Swaggerize to narzędzie generujące kod Node.js dla interfejsu API REST na podstawie definicji Swagger.

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a>Generowanie kodu Node.js 

W tej części samouczka hello modele przepływu pracy programowania w którym najpierw utworzyć metadane programu Swagger i użyć tego tooscaffold (automatycznego generowania) kodu serwera na powitania interfejsu API. 

Zmień katalog toohello *start* folderu, i uruchom `yo swaggerize`. Narzędzie swaggerize tworzy projekt Node.js do interfejsu API z definicji struktury Swagger hello w *api.json*.

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

Kiedy w narzędziu Swaggerize zostanie wyświetlony monit o podanie nazwy projektu, użyj nazwy *ContactList*.
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a>Dostosowywanie hello kodu projektu

1. Kopiuj hello *lib* folderu do hello *ContactList* folder utworzony przez `yo swaggerize`, zmień katalog na *ContactList*.

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. Zainstaluj hello `jsonpath` i `swaggerize-ui` moduły NPM. 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. Zastąp kod hello w hello *handlers/contacts.js* z hello następującego kodu: 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    Ten kod zawiera dane JSON hello przechowywane w *lib/contacts.json* obsługiwanej przez *lib/contactRepository.js*. nowe Hello *contacts.js* kod zwraca wszystkie kontakty w repozytorium hello jako ładunek JSON. 

4. Zastąp kod hello w hello **handlers/contacts/{id}.js** pliku z hello następującego kodu:

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    Ten kod umożliwia używanie ścieżki tooreturn zmiennej tylko hello kontaktu z danym identyfikatorem.

5. Zastąp kod hello w **server.js** z hello następującego kodu:

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

    Ten kod sprawia, że niektóre toolet niewielkich zmian, jego działania w usłudze Azure App Service i udostępnia interfejs sieci web interactive dla interfejsu API.

### <a name="test-hello-api-locally"></a>Test hello interfejsu API lokalnie

1. Uruchomić aplikację Node.js hello
    ```bash
    npm start
    ```
    
2. Przeglądaj toohttp://localhost:8000 / kontaktuje tooview hello JSON dla hello całej listy kontaktów.
   
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

3. Przeglądaj toohttp://localhost:8000/kontakty/2 tooview hello kontaktować się z `id` liczby dwa.
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. Za pomocą interfejsu sieci web struktury Swagger hello na http://localhost: 8000/docs API hello testu.
   
    ![Interfejs sieci web struktury Swagger](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <a id="createapiapp"></a> Tworzenie aplikacji interfejsu API

W tej sekcji użyjesz hello Azure CLI 2.0 toocreate hello zasobów toohost hello interfejsu API w usłudze Azure App Service. 

1.  Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami.

    ```azurecli-interactive
    az login
    ```

2. Jeśli masz wiele subskrypcji Azure, zmień hello domyślne subskrypcji toohello żądana jeden.

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a>Wdrażanie hello API za pomocą narzędzia Git

Wdrażanie aplikacji interfejsu API toohello kodu przez wypychanie zatwierdzeń z sieci lokalnej tooAzure repozytorium Git usługi aplikacji.

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. Inicjowanie nowego repozytorium w hello *ContactList* katalogu. 

    ```bash
    git init .
    ```

3. Wyklucz hello *node_modules* Katalog utworzony przez npm we wcześniejszym kroku w samouczku hello z repozytorium Git. Utwórz nową `.gitignore` plików w bieżącym katalogu hello i Dodaj powitania po tekst na nowy wiersz w pliku hello w dowolnym miejscu.

    ```
    node_modules/
    ```
    Potwierdź hello `node_modules` folderu zostanie zignorowany z `git status`.

4. Zatwierdź hello zmiany toohello repozytorium.
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a>Test hello interfejsu API na platformie Azure

1. Otwórz toohttp://app_name.azurewebsites.net/contacts przeglądarki. Zostanie wyświetlony hello tego samego JSON zwracane jako podczas żądania hello lokalnie wcześniej w samouczku hello.

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

2. W przeglądarce Przejdź toohello `http://app_name.azurewebsites.net/docs` tootry punktu końcowego limit hello interfejs użytkownika programu Swagger, działających na platformie Azure.

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    Teraz można wdrożyć aktualizacje toohello przykładowy interfejs API tooAzure po prostu wypychając repozytorium Azure Git toohello zatwierdzeń.

## <a name="clean-up"></a>Czyszczenie

tooclean zasobów hello utworzone w tym Szybki Start, uruchom następujące polecenie z wiersza polecenia platformy Azure hello:

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a>Następny krok 
> [!div class="nextstepaction"]
> [Używanie aplikacji interfejsu API z klientów JavaScript za pomocą mechanizmu CORS](app-service-api-cors-consume-javascript.md)

