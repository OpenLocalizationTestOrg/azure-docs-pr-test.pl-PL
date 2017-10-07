---
title: aaaBuild Node.js i bazy danych MongoDB aplikacji sieci web na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooget aplikacji Node.js działa na platformie Azure, z połączenia tooa rozwiązania Cosmos DB bazy danych przy użyciu parametrów połączenia bazy danych MongoDB."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a>Tworzenie aplikacji sieci web Node.js i bazy danych MongoDB na platformie Azure

Aplikacje sieci Web platformy Azure oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web. Ten samouczek pokazuje, jak toocreate Node.js sieci web aplikacji na platformie Azure i podłącz go tooa baza danych MongoDB. Gdy wszystko będzie gotowe, będziesz mieć uruchomionej aplikacji średniej (bazy danych MongoDB, Express AngularJS i Node.js) w [usłudze Azure App Service](app-service-web-overview.md). Dla uproszczenia hello Przykładowa aplikacja korzysta hello [platforma sieci web MEAN.js](http://meanjs.org/).

![Aplikacja MEAN.js uruchomiona w usłudze Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Zawartość:

> [!div class="checklist"]
> * Tworzenie bazy danych MongoDB na platformie Azure
> * Połącz tooMongoDB aplikacji Node.js
> * Wdrażanie tooAzure aplikacji hello
> * Aktualizacja modelu danych hello i wdrożenie aplikacji hello
> * Strumieniowe przesyłanie dzienników diagnostycznych z platformy Azure
> * Zarządzanie aplikacją hello w hello portalu Azure

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka:

1. [Zainstaluj oprogramowanie Git](https://git-scm.com/)
1. [Zainstaluj środowisko Node.js i menedżer NPM](https://nodejs.org/)
1. [Zainstaluj Gulp.js](http://gulpjs.com/) (wymagany przez [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))
1. [Zainstaluj i uruchom MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-mongodb"></a>Test lokalnej bazy danych MongoDB

Witaj Otwórz okno terminala i `cd` toohello `bin` katalogu instalacji bazy danych MongoDB. Wszystkie polecenia hello toorun to okno terminalu można użyć w tym samouczku.

Uruchom `mongo` w hello terminali tooconnect tooyour MongoDB serwera lokalnego.

```bash
mongo
```

Jeśli połączenie zostanie nawiązane, bazy danych MongoDB już jest uruchomiony. Jeśli nie, upewnij się, że lokalnej bazy danych MongoDB została uruchomiona, wykonując kroki hello na [zainstalować bazy danych MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/). Często jest zainstalowana baza danych MongoDB, ale nadal potrzebujesz toostart ją, uruchamiając `mongod`. 

Po zakończeniu testowania bazy danych MongoDB, wpisz `Ctrl+C` w hello terminala. 

## <a name="create-local-nodejs-app"></a>Tworzenie lokalnych aplikacji Node.js

Ten krok umożliwia zdefiniowanie hello lokalnego Node.js projektu.

### <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Okno terminalu hello `cd` tooa katalog roboczy.  

Hello uruchom następujące polecenie tooclone hello próbki repozytorium. 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

To repozytorium przykładowej zawiera kopię hello [repozytorium MEAN.js](https://github.com/meanjs/mean). Jest zmodyfikowany toorun w usłudze aplikacji (Aby uzyskać więcej informacji, zobacz repozytorium MEAN.js hello [Plik README](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).

### <a name="run-hello-application"></a>Uruchamianie aplikacji hello

Uruchom następujące polecenia tooinstall hello wymaganych pakietów hello i uruchomienia aplikacji hello.

```bash
cd meanjs
npm install
npm start
```

Po całkowitym załadowaniem aplikacji hello pojawić coś podobnego toohello następującego komunikatu:

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

Przejdź toohttp://localhost:3000 w przeglądarce. Kliknij przycisk **Utwórz konto** w menu u góry hello i tworzenie użytkownika testowego. 

Witaj MEAN.js Przykładowa aplikacja przechowuje dane użytkownika w bazie danych hello. W przypadku pomyślnego tworzenia użytkownika i logowanie, aplikację zapisywania danych toohello lokalnej bazy danych MongoDB.

![MEAN.js pomyślnie łączy tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

Wybierz **Admin > Zarządzaj artykuły** tooadd niektórych artykułach.

toostop Node.js w dowolnym momencie, naciśnij klawisz `Ctrl+C` w hello terminala. 

## <a name="create-production-mongodb"></a>Utwórz produkcyjnej bazy danych MongoDB

W tym kroku utworzysz bazę danych MongoDB na platformie Azure. Gdy aplikacji jest wdrożony tooAzure, używa tej bazy danych w chmurze.

Bazy danych mongodb, w tym samouczku używana [bazy danych Azure rozwiązania Cosmos](/azure/documentdb/). Rozwiązania cosmos bazy danych obsługuje połączenia klienta bazy danych MongoDB.

### <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Użyjesz hello Azure CLI 2.0 toocreate hello zasobów niezbędnych toohost aplikacji na platformie Azure. Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami.

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Witaj poniższy przykład tworzy grupę zasobów w regionie Europy Zachodniej hello.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

Użyj hello [appservice az listy lokalizacje](/cli/azure/appservice#list-locations) toolist dostępne lokalizacje polecenia wiersza polecenia platformy Azure. 

### <a name="create-a-cosmos-db-account"></a>Tworzenie konta bazy danych rozwiązania Cosmos

Tworzenie konta bazy danych rozwiązania Cosmos z hello [az cosmosdb utworzyć](/cli/azure/cosmosdb#create) polecenia.

W hello następujące polecenia, należy zastąpić unikatową nazwę bazy danych rozwiązania Cosmos hello  *\<cosmosdb_name >* symbolu zastępczego. Ta nazwa jest używana jako część hello hello DB rozwiązania Cosmos punktu końcowego, `https://<cosmosdb_name>.documents.azure.com/`, więc nazwa hello musi toobe unikatowy wszystkich kont rozwiązania Cosmos bazy danych na platformie Azure. Nazwa Hello musi zawierać tylko małe litery, cyfry i znaki łącznika (-) hello i musi mieć długość od 3 do 50 znaków.

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

Witaj *--rodzaju bazy danych MongoDB* parametru zapewnia połączeń klienckich bazy danych MongoDB.

Po utworzeniu hello konto bazy danych rozwiązania Cosmos hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-tooproduction-mongodb"></a>Łączenie aplikacji tooproduction bazy danych MongoDB

W tym kroku połączenie MEAN.js przykładowej bazy danych aplikacji toohello DB rozwiązania Cosmos utworzony, przy użyciu parametrów połączenia bazy danych MongoDB. 

### <a name="retrieve-hello-database-key"></a>Pobrać hello klucza bazy danych

bazy danych DB rozwiązania Cosmos toohello tooconnect, należy hello klucza bazy danych. Użyj hello [az cosmosdb listy kluczy](/cli/azure/cosmosdb#list-keys) klucz podstawowy hello tooretrieve polecenia.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

Hello interfejsu wiersza polecenia Azure zawiera informacje o toohello podobnie poniższy przykład:

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Skopiuj wartość hello `primaryMasterKey`. Należy te informacje w hello następnego kroku.

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Konfigurowanie parametrów połączenia hello w aplikacji Node.js

Otwórz w repozytorium MEAN.js _config/env/production.js_.

W hello `db` obiektów, zaktualizuj wartość hello `uri`:

* Zastąp hello dwa  *\<cosmosdb_name >* symbole zastępcze nazwą bazy danych DB rozwiązania Cosmos.
* Zastąp hello  *\<primary_master_key >* symbol zastępczy hello klucza skopiowany w poprzednim kroku hello.

Witaj poniższy kod przedstawia hello `db` obiektu:

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

Witaj `ssl=true` opcja jest wymagana, ponieważ [DB rozwiązania Cosmos wymaga protokołu SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 

Zapisz zmiany.

### <a name="test-hello-application-in-production-mode"></a>Testowanie aplikacji hello w trybie produkcyjnym 

Uruchom następujące polecenie toominify i pakietu skryptów w środowisku produkcyjnym hello hello. Ten proces generuje hello pliki wymagane przez hello środowiska produkcyjnego.

```bash
gulp prod
```

Hello uruchom następujące polecenie toouse hello ciąg połączenia został skonfigurowany w _config/env/production.js_.

```bash
NODE_ENV=production node server.js
```

`NODE_ENV=production`Ustawia zmienną środowiskową hello informujący o Node.js toorun w środowisku produkcyjnym hello.  `node server.js`Uruchamia hello Node.js server z `server.js` w katalogu głównym repozytorium. Jest to, jak załadowano aplikację Node.js na platformie Azure. 

Podczas ładowania aplikacji hello Sprawdź toomake się, że jest uruchomiony w środowisku produkcyjnym hello:

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

Przejdź toohttp://localhost:8443 w przeglądarce. Kliknij przycisk **Utwórz konto** w menu u góry hello i tworzenie użytkownika testowego. Jeśli tworzenie użytkownika i logowanie powiodło się, aplikacja jest zapisywanie bazy danych DB rozwiązania Cosmos toohello danych na platformie Azure. 

W terminalu hello, Zatrzymaj Node.js, wpisując `Ctrl+C`. 

## <a name="deploy-app-tooazure"></a>Wdrażanie aplikacji tooAzure

W tym kroku możesz wdrożyć tooAzure aplikacji programu Node.js połączenia bazy danych MongoDB usługi aplikacji.

### <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service

Tworzenie planu usługi aplikacji z hello [Tworzenie planu usług aplikacji az](/cli/azure/appservice/plan#create) polecenia. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Witaj poniższy przykład tworzy plan usługi aplikacji o nazwie _myAppServicePlan_ przy użyciu hello **wolne** warstwa cenowa:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Po utworzeniu planu usługi aplikacji hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web

Tworzenie aplikacji sieci web w hello `myAppServicePlan` planu usługi aplikacji z hello [tworzenie aplikacji sieci Web az](/cli/azure/webapp#create) polecenia. 

umożliwia aplikacji sieci web Hello możesz hosting miejsce toodeploy kodu i zawiera adres URL dla Ciebie tooview hello wdrożonych aplikacji. Użyj aplikacji sieci web hello toocreate. 

Witaj następujące polecenia, Zastąp hello  *\<nazwa_aplikacji >* symbol zastępczy unikatowej nazwy aplikacji. Ta nazwa jest używana jako część hello hello domyślny adres URL dla aplikacji sieci web hello, więc nazwa hello musi toobe unikatowy przez wszystkie aplikacje w usłudze Azure App Service. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Podczas tworzenia aplikacji sieci web hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-an-environment-variable"></a>Skonfigurować zmienną środowiskową

Wcześniej w hello samouczek, zostanie zapisane na stałe hello parametry połączenia bazy danych w _config/env/production.js_. Zgodnie z zaleceniami dotyczącymi zabezpieczeń ma tookeep danych poufnych poza repozytorium Git. Dla aplikacji działających na platformie Azure będzie zamiast tego użyć zmiennej środowiskowej.

W usłudze App Service można ustawić zmienne środowiskowe jako _ustawień aplikacji_ przy użyciu hello [zaktualizować appsettings konfiguracji aplikacji sieci Web az](/cli/azure/webapp/config/appsettings#update) polecenia. 

Witaj poniższy przykład konfiguruje `MONGODB_URI` ustawienie aplikacji w aplikacji sieci web platformy Azure. Zastąp hello  *\<nazwa_aplikacji >*,  *\<cosmosdb_name >*, i  *\<primary_master_key >* symbole zastępcze.

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

W kodzie Node.js dostępu to ustawienie aplikacji o `process.env.MONGODB_URI`, tak jak będzie dostęp do wszelkich zmiennej środowiskowej. 

Teraz Cofnij too_config/env/production.js_ Twoje zmiany z hello następujące polecenie:

```bash
git checkout -- .
```

Otwórz _config/env/production.js_ ponownie. Należy pamiętać, aplikacja hello domyślnego MEAN.js jest już skonfigurowany toouse hello `MONGODB_URI` zmienną środowiskową, który został utworzony.

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a>Konfigurowanie lokalnego wdrożenia narzędzia Git 

Użyj hello [ustawiono użytkownika wdrożenia aplikacji sieci Web az](/cli/azure/webapp/deployment/user#set) polecenia toocreate poświadczeń do wdrożenia.

Można wdrożyć tooAzure Twojej aplikacji usługi App Service na różne sposoby, w tym FTP, Git lokalnego GitHub, Visual Studio Team Services i BitBucket. FTP i lokalne Git, konieczne jest toohave użytkownika wdrożenia skonfigurowane na powitania serwera tooauthenticate wdrożenia. Ten użytkownik wdrożenia poziomie konta i różni się od konta subskrypcji platformy Azure. Wystarczy tooconfigure tego użytkownika wdrożenia raz.

Zastąp następujące polecenie, w hello  *\<nazwa użytkownika >* i  *\<hasło >* nową nazwę użytkownika i hasło. Witaj, nazwa użytkownika musi być unikatowa. Witaj hasło musi mieć co najmniej ośmiu znaków, przy użyciu dwóch hello następujące trzy elementy: liter, cyfr, symboli. Jeśli otrzymasz ` 'Conflict'. Details: 409` błąd, username hello zmiany. Jeśli wystąpił błąd ` 'Bad Request'. Details: 400`, użyj silniejszego hasła.

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

Nazwa użytkownika hello rekordu i hasło do użycia w kolejnych krokach podczas wdrażania aplikacji hello.

Użyj hello [źródło wdrożenia az aplikacji sieci Web — config lokalnych git](/cli/azure/webapp/deployment/source#config-local-git) polecenia tooconfigure lokalnego Git dostępu toohello aplikacji sieci web Azure. 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

Po skonfigurowaniu użytkownika wdrażania hello hello Azure CLI zawiera hello adres URL wdrożenia dla aplikacji sieci web platformy Azure w hello następującego formatu:

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

Skopiować hello dane wyjściowe z hello terminal, będzie on używany w hello następnego kroku. 

### <a name="push-tooazure-from-git"></a>Wypychać tooAzure za pomocą narzędzia Git

Dodaj Azure tooyour zdalnego lokalnego repozytorium Git. 

```bash
git remote add azure <paste_copied_url_here> 
```

Wypchnij toohello Azure toodeploy zdalnego aplikacji Node.js. Pojawi się monit dla hello hasło wcześniej w ramach tworzenia hello hello wdrożenia użytkownika. 

```bash
git push azure master
```

Podczas wdrażania usługi Azure App Service komunikuje się postęp za pomocą narzędzia Git.

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

Można zauważyć, że proces wdrażania hello uruchamia [system Gulp](http://gulpjs.com/) po `npm install`. Usługi aplikacji Gulp lub Grunt zadań nie jest uruchamiane podczas wdrażania, więc to repozytorium przykładowej ma dwa dodatkowe pliki w jego tooenable katalogu głównego go: 

- _.Deployment_ -toorun usługi aplikacji określa, że ten plik `bash deploy.sh` jako hello niestandardowe wdrożenie skryptu.
- _Deploy.sh_ — Witaj niestandardowe wdrożenie skryptu. Jeśli możesz przejrzeć plik hello, zobaczysz, że działa `gulp prod` po `npm install` i `bower install`. 

Tooadd tej metody można użyć dowolnego kroku tooyour wdrożenia na podstawie Git. W przypadku ponownego uruchomienia aplikacji sieci web platformy Azure w dowolnym momencie, usługi aplikacji nie ponownie te zadania automatyzacji.

### <a name="browse-toohello-azure-web-app"></a>Przeglądaj toohello aplikacji sieci web Azure 

Przeglądaj toohello wdrożyć aplikację sieci web przy użyciu przeglądarki sieci web. 

```bash 
http://<app_name>.azurewebsites.net 
``` 

Kliknij przycisk **Utwórz konto** w menu u góry hello i Utwórz użytkownika zastępczego. 

Jeśli pomyślnie i automatycznie loguje aplikacji hello toohello utworzyć użytkownika, a następnie MEAN.js aplikacji na platformie Azure ma bazy danych MongoDB (DB rozwiązania Cosmos) toohello łączności. 

![Aplikacja MEAN.js uruchomiona w usłudze Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Wybierz **Admin > Zarządzaj artykuły** tooadd niektórych artykułach. 

**Gratulacje!** Używasz aplikacji Node.js opartych na danych w usłudze Azure App Service.

## <a name="update-data-model-and-redeploy"></a>Aktualizacja modelu danych i utwórz je ponownie

W tym kroku, możesz zmienić hello `article` danych model i opublikuj tooAzure Twoje zmiany.

### <a name="update-hello-data-model"></a>Model danych hello aktualizacji

Otwórz _modules/articles/server/models/article.server.model.js_.

W `ArticleSchema`, Dodaj `String` typu o nazwie `comment`. Gdy wszystko będzie gotowe, schemat kod powinien wyglądać następująco:

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-hello-articles-code"></a>Zaktualizuj kod artykuły hello

Zaktualizuj hello reszty Twojej `articles` kodu toouse `comment`.

Jest pięć plików należy toomodify: hello serwera kontrolera i hello cztery widoki klientów. 

Otwórz _modules/articles/server/controllers/articles.server.controller.js_.

W hello `update` funkcji, należy dodać przydziału `article.comment`. Witaj poniższy kod przedstawia ukończyć powitalnych `update` funkcji:

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

Otwórz _modules/articles/client/views/view-article.client.view.html_.

Powyżej zamknięcia hello `</section>` tagów, Dodaj powitania po wierszu toodisplay `comment` wraz z hello pozostałe dane artykułu hello:

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

Otwórz _modules/articles/client/views/list-articles.client.view.html_.

Powyżej zamknięcia hello `</a>` tagów, Dodaj powitania po wierszu toodisplay `comment` wraz z hello pozostałe dane artykułu hello:

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

Otwórz _modules/articles/client/views/admin/list-articles.client.view.html_.

Wewnątrz hello `<div class="list-group">` element i nad zamknięciem hello `</a>` tagów, Dodaj powitania po wierszu toodisplay `comment` wraz z hello pozostałe dane artykułu hello:

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

Otwórz _modules/articles/client/views/admin/form-article.client.view.html_.

Znajdź hello `<div class="form-group">` element, który zawiera przycisk Prześlij hello, która wygląda podobnie do następującej:

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

Powyżej tego tagu, dodać kolejne `<div class="form-group">` elementu można edytować hello `comment` pola. Nazwę nowego elementu powinna wyglądać następująco:

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a>Przetestuj zmiany lokalnie

Zapisz wszystkie zmiany.

Ponownie przetestuj zmiany w trybie produkcyjnym.

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> Należy pamiętać, że Twoje _config/env/production.js_ została wycofana i hello `MONGODB_URI` zmiennej środowiskowej ustawiono tylko w aplikacji sieci web platformy Azure, a nie na komputerze lokalnym. Podczas przeglądania w pliku konfiguracyjnym hello okaże się, że hello toouse ustawienia domyślne konfiguracji produkcji lokalnej bazy danych MongoDB. Dzięki temu nie ruszaj danych produkcyjnych podczas testowania zmiany kodu lokalnie.

Przejdź do zbyt`http://localhost:8443` w przeglądarce i upewnij się, że użytkownik jest zalogowany.

Wybierz **Admin > Zarządzaj artykuły**, następnie dodać artykułu, wybierając hello  **+**  przycisku.

Witaj Zobacz nowe `Comment` teraz pola tekstowego.

![Komentarz dodany tooArticles pola](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

W terminalu hello, Zatrzymaj Node.js, wpisując `Ctrl+C`. 

### <a name="publish-changes-tooazure"></a>Publikowanie zmian tooAzure

Zatwierdź zmiany w usłudze Git, a następnie Wypchnij tooAzure zmiany kodu hello.

```bash
git commit -am "added article comment"
git push azure master
```

Raz hello `git push` jest zakończenie, przejdź tooyour aplikacji sieci web platformy Azure i wypróbować hello nowych funkcji.

![Zmiany modelu i bazy danych publikowanych tooAzure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

Jeśli wcześniej dodane artykułów, nadal widać je. Istniejące dane w bazie danych z rozwiązania Cosmos nie zostaną utracone. Ponadto schemat danych toohello aktualizacji i pozostawienie bez zmian do istniejących danych.

## <a name="stream-diagnostic-logs"></a>Dzienniki diagnostyczne strumienia 

Podczas wykonywania aplikacji Node.js w usłudze Azure App Service można uzyskać tooyour gazociągami dzienniki konsoli hello terminala. W ten sposób można uzyskać hello tego samego komunikaty diagnostyczne toohelp Debugowanie błędów aplikacji.

Dziennik toostart przesyłania strumieniowego, użyj hello [końcowego fragmentu dziennika aplikacji sieci Web az](/cli/azure/webapp/log#tail) polecenia.

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

Po rozpoczęciu przesyłania strumieniowego dzienników odświeżanie aplikacji sieci web platformy Azure w tooget przeglądarki hello część ruchu w sieci web. Pojawi się dzienniki konsoli przetwarzana potokowo tooyour terminala.

Dziennik zatrzymania przesyłania strumieniowego w dowolnym momencie, wpisując `Ctrl+C`. 

## <a name="manage-your-azure-web-app"></a>Zarządzanie aplikacji sieci web platformy Azure

Przejdź toohello [portalu Azure](https://portal.azure.com) aplikacji sieci web hello toosee został utworzony.

W menu po lewej stronie powitania kliknij **usługi aplikacji**, następnie kliknij nazwę hello aplikacji sieci web platformy Azure.

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

Domyślnie hello portal przedstawiono aplikację sieci web **omówienie** strony. Ta strona udostępnia widok sposobu działania aplikacji. Tutaj możesz również wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie. Witaj w lewej części strony hello hello kartach hello innej konfiguracji stron, które można otworzyć.

![Strona usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a>Następne kroki

Wiadomości:

> [!div class="checklist"]
> * Tworzenie bazy danych MongoDB na platformie Azure
> * Połącz tooMongoDB aplikacji Node.js
> * Wdrażanie tooAzure aplikacji hello
> * Aktualizacja modelu danych hello i wdrożenie aplikacji hello
> * Strumieniowe przesyłanie dzienników z Azure tooyour terminali
> * Zarządzanie aplikacją hello w hello portalu Azure

Przejść dalej toolearn samouczka toohello jak toomap DNS niestandardowej nazwy tooyour aplikacji sieci web.

> [!div class="nextstepaction"] 
> [Mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacji sieci Web](app-service-web-tutorial-custom-domain.md)
