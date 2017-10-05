---
title: Tworzenie aplikacji sieci web Node.js i bazy danych MongoDB na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak pobrać aplikację Node.js, praca na platformie Azure z połączenia z bazą danych rozwiązania Cosmos bazy danych przy użyciu parametrów połączenia bazy danych MongoDB."
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
ms.openlocfilehash: 3b309382be8cdf8d48b396207fd482a5dc5ed934
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a>Tworzenie aplikacji sieci web Node.js i bazy danych MongoDB na platformie Azure

Aplikacje sieci Web platformy Azure oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web. W tym samouczku przedstawiono sposób tworzenia aplikacji sieci web Node.js na platformie Azure i podłącz go do bazy danych MongoDB. Gdy wszystko będzie gotowe, będziesz mieć uruchomionej aplikacji średniej (bazy danych MongoDB, Express AngularJS i Node.js) w [usłudze Azure App Service](app-service-web-overview.md). Dla uproszczenia Przykładowa aplikacja korzysta z [platforma sieci web MEAN.js](http://meanjs.org/).

![Aplikacja MEAN.js uruchomiona w usłudze Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Zawartość:

> [!div class="checklist"]
> * Tworzenie bazy danych MongoDB na platformie Azure
> * Łączenie aplikacji Node.js z bazy danych MongoDB
> * Wdrażanie aplikacji na platformie Azure
> * Aktualizacja modelu danych i ponownie wdrożyć aplikację
> * Strumieniowe przesyłanie dzienników diagnostycznych z platformy Azure
> * Zarządzanie aplikacją w portalu Azure

## <a name="prerequisites"></a>Wymagania wstępne

W celu ukończenia tego samouczka:

1. [Zainstaluj oprogramowanie Git](https://git-scm.com/)
1. [Zainstaluj środowisko Node.js i menedżer NPM](https://nodejs.org/)
1. [Zainstaluj Gulp.js](http://gulpjs.com/) (wymagany przez [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))
1. [Zainstaluj i uruchom MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej. Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-mongodb"></a>Test lokalnej bazy danych MongoDB

Otwórz okno terminala i `cd` do `bin` katalogu instalacji bazy danych MongoDB. To okno terminalu służy do uruchamiania wszystkich poleceń w tym samouczku.

Uruchom `mongo` w terminalu, aby połączyć się z lokalnym serwerem bazy danych MongoDB.

```bash
mongo
```

Jeśli połączenie zostanie nawiązane, bazy danych MongoDB już jest uruchomiony. Jeśli nie, upewnij się, że lokalnej bazy danych MongoDB została uruchomiona, wykonując kroki opisane w temacie [zainstalować bazy danych MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/). Często jest zainstalowana baza danych MongoDB, ale nadal należy ją uruchomić, uruchamiając `mongod`. 

Po zakończeniu testowania bazy danych MongoDB, wpisz `Ctrl+C` w terminalu. 

## <a name="create-local-nodejs-app"></a>Tworzenie lokalnych aplikacji Node.js

Ten krok służy do konfigurowania lokalnego projektu Node.js.

### <a name="clone-the-sample-application"></a>Klonowanie przykładowej aplikacji

W oknie terminalu `cd` do katalogu roboczego.  

Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium. 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

To repozytorium przykładowej zawiera kopię [repozytorium MEAN.js](https://github.com/meanjs/mean). Są modyfikowane w celu uruchomienia w usłudze aplikacji (Aby uzyskać więcej informacji, zobacz repozytorium MEAN.js [Plik README](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).

### <a name="run-the-application"></a>Uruchamianie aplikacji

Uruchom następujące polecenia, aby zainstalować wymagane pakiety i uruchom aplikację.

```bash
cd meanjs
npm install
npm start
```

Gdy aplikacja zostanie całkowicie załadowany, zobacz podobny do następującego:

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

Przejdź do http://localhost: 3000 w przeglądarce. Kliknij przycisk **Utwórz konto** w menu u góry i tworzenie użytkownika testowego. 

Przykładowa aplikacja MEAN.js przechowuje dane użytkowników w bazie danych. W przypadku pomyślnego tworzenia użytkownika i logowanie, aplikacja jest zapisywania danych do lokalnej bazy danych MongoDB.

![Pomyślne połączenie MEAN.js z MongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

Wybierz **Admin > Zarządzaj artykuły** można dodać niektórych artykułach.

Aby zatrzymać Node.js w dowolnym momencie, naciśnij klawisz `Ctrl+C` w terminalu. 

## <a name="create-production-mongodb"></a>Utwórz produkcyjnej bazy danych MongoDB

W tym kroku utworzysz bazę danych MongoDB na platformie Azure. Po wdrożeniu aplikacji na platformie Azure wykorzystuje tę bazę danych w chmurze.

Bazy danych mongodb, w tym samouczku używana [bazy danych Azure rozwiązania Cosmos](/azure/documentdb/). Rozwiązania cosmos bazy danych obsługuje połączenia klienta bazy danych MongoDB.

### <a name="log-in-to-azure"></a>Zaloguj się do platformy Azure.

Użyj interfejsu wiersza polecenia platformy Azure w wersji 2.0, aby utworzyć zasoby potrzebne do hostowania Twojej aplikacji na platformie Azure. Zaloguj się do subskrypcji platformy Azure za pomocą polecenia [az login](/cli/azure/#login) i postępuj zgodnie z instrukcjami wyświetlanymi na ekranie.

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Poniższy przykład obejmuje tworzenie grupy zasobów w regionie Europa Zachodnia.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

Użyj [appservice az listy lokalizacje](/cli/azure/appservice#list-locations) polecenia wiersza polecenia platformy Azure do listy dostępnych lokalizacji. 

### <a name="create-a-cosmos-db-account"></a>Tworzenie konta bazy danych rozwiązania Cosmos

Tworzenie konta bazy danych rozwiązania Cosmos z [az cosmosdb utworzyć](/cli/azure/cosmosdb#create) polecenia.

W poniższym poleceniu zastąp unikatową nazwę bazy danych rozwiązania Cosmos  *\<cosmosdb_name >* symbolu zastępczego. Ta nazwa jest używana jako część rozwiązania Cosmos DB punkt końcowy, `https://<cosmosdb_name>.documents.azure.com/`, więc nazwa musi być unikatowa na wszystkich kontach DB rozwiązania Cosmos w programie Azure. Nazwa musi zawierać tylko małe litery, cyfry i znaki łącznika (-) i musi mieć długość od 3 do 50 znaków.

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

*--Rodzaju bazy danych MongoDB* parametru zapewnia połączeń klienckich bazy danych MongoDB.

Po utworzeniu konta DB rozwiązania Cosmos interfejsu wiersza polecenia Azure zawiera informacje podobne do poniższego przykładu:

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

## <a name="connect-app-to-production-mongodb"></a>Łączenie aplikacji produkcyjnej bazy danych MongoDB

W tym kroku połączenie aplikacji przykładowej MEAN.js do bazy danych DB rozwiązania Cosmos utworzony, przy użyciu parametrów połączenia bazy danych MongoDB. 

### <a name="retrieve-the-database-key"></a>Pobierz klucz bazy danych

Do połączenia z bazą danych rozwiązania Cosmos bazy danych, należy klucza bazy danych. Aby pobrać klucz podstawowy, użyj polecenia [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys).

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

Interfejsu wiersza polecenia Azure zawiera informacje podobne do poniższego przykładu:

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Skopiuj wartość `primaryMasterKey`. Ta informacja będzie potrzebna w następnym kroku.

<a name="devconfig"></a>
### <a name="configure-the-connection-string-in-your-nodejs-application"></a>Konfigurowanie parametrów połączenia w aplikacji Node.js

Otwórz w repozytorium MEAN.js _config/env/production.js_.

W `db` obiektów, zaktualizuj wartość `uri`:

* Zastąp dwa  *\<cosmosdb_name >* symbole zastępcze nazwą bazy danych DB rozwiązania Cosmos.
* Zastąp  *\<primary_master_key >* symbol zastępczy klucz został skopiowany w poprzednim kroku.

Poniższy kod przedstawia `db` obiektu:

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

`ssl=true` Opcja jest wymagana, ponieważ [DB rozwiązania Cosmos wymaga protokołu SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 

Zapisz zmiany.

### <a name="test-the-application-in-production-mode"></a>Testowanie aplikacji w trybie produkcyjnym 

Uruchom następujące polecenie w celu zminimalizowania i pakietów skryptów w środowisku produkcyjnym. Ten proces generuje pliki wymagane przez środowisko produkcyjne.

```bash
gulp prod
```

Uruchom następujące polecenie, aby użyć skonfigurowane w ciągu połączenia _config/env/production.js_.

```bash
NODE_ENV=production node server.js
```

`NODE_ENV=production`Ustawia zmienną środowiskową, informujący o Node.js do uruchamiania w środowisku produkcyjnym.  `node server.js`Uruchamia serwer Node.js z `server.js` w katalogu głównym repozytorium. Jest to, jak załadowano aplikację Node.js na platformie Azure. 

Podczas ładowania aplikacji, należy sprawdzić, czy działa w środowisku produkcyjnym:

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

Przejdź do http://localhost:8443 w przeglądarce. Kliknij przycisk **Utwórz konto** w menu u góry i tworzenie użytkownika testowego. W przypadku pomyślnego tworzenia użytkownika i zaloguj się, aplikacja jest zapisywania danych do bazy danych DB rozwiązania Cosmos na platformie Azure. 

W terminalu, Zatrzymaj Node.js, wpisując `Ctrl+C`. 

## <a name="deploy-app-to-azure"></a>Wdrażanie aplikacji na platformie Azure

W tym kroku możesz wdrożyć aplikację Node.js połączenia bazy danych MongoDB w usłudze Azure App Service.

### <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service

Utwórz plan usługi App Service za pomocą polecenia [az appservice plan create](/cli/azure/appservice/plan#create). 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Poniższy przykład tworzy plan usługi aplikacji o nazwie _myAppServicePlan_ przy użyciu **wolne** warstwa cenowa:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Po utworzeniu planu usługi aplikacji Azure CLI pokazuje informacje podobne do poniższego przykładu:

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

Tworzenie aplikacji sieci web w `myAppServicePlan` planu usługi aplikacji z [tworzenie aplikacji sieci Web az](/cli/azure/webapp#create) polecenia. 

Aplikacja sieci web udostępnia hostingu miejsca, aby wdrożyć kod i zawiera adres URL do wyświetlania wdrożonej aplikacji. Służy do tworzenia aplikacji sieci web. 

W poniższym poleceniu zastąp  *\<nazwa_aplikacji >* symbol zastępczy unikatowej nazwy aplikacji. Ta nazwa jest używana jako część domyślnego adresu URL dla aplikacji sieci web, więc nazwa musi być unikatowy w obrębie wszystkich aplikacji w usłudze Azure App Service. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Po utworzeniu aplikacji internetowej w interfejsie wiersza polecenia platformy Azure zostaną wyświetlone informacje podobne do następujących: 

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

Wcześniej w samouczku, zostanie zapisane na stałe połączenie z bazą danych ciąg w _config/env/production.js_. Zgodnie ze względów bezpieczeństwa chcesz zachować poufne dane poza repozytorium Git. Dla aplikacji działających na platformie Azure będzie zamiast tego użyć zmiennej środowiskowej.

W usłudze App Service można ustawić zmienne środowiskowe jako _ustawień aplikacji_ za pomocą [zaktualizować appsettings konfiguracji aplikacji sieci Web az](/cli/azure/webapp/config/appsettings#update) polecenia. 

Poniższy przykład konfiguruje `MONGODB_URI` ustawienie aplikacji w aplikacji sieci web platformy Azure. Zastąp  *\<nazwa_aplikacji >*,  *\<cosmosdb_name >*, i  *\<primary_master_key >* symbole zastępcze.

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

W kodzie Node.js dostępu to ustawienie aplikacji o `process.env.MONGODB_URI`, tak jak będzie dostęp do wszelkich zmiennej środowiskowej. 

Teraz, Cofnij zmiany _config/env/production.js_ przy użyciu następującego polecenia:

```bash
git checkout -- .
```

Otwórz _config/env/production.js_ ponownie. Należy pamiętać, że domyślna aplikacja MEAN.js jest już skonfigurowana do używania `MONGODB_URI` zmienną środowiskową, który został utworzony.

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a>Konfigurowanie lokalnego wdrożenia narzędzia Git 

Użyj [ustawiono użytkownika wdrożenia aplikacji sieci Web az](/cli/azure/webapp/deployment/user#set) polecenie, aby utworzyć poświadczenia dla wdrożenia.

Można wdrożyć aplikację w usłudze Azure App Service na różne sposoby, w tym FTP, Git lokalnego GitHub, Visual Studio Team Services i BitBucket. FTP i lokalne Git jest konieczne użytkownika wdrożenia skonfigurowane na serwerze do uwierzytelniania wdrożenia. Ten użytkownik wdrożenia poziomie konta i różni się od konta subskrypcji platformy Azure. Wystarczy raz skonfigurować ten użytkownik wdrożenia.

W poniższym poleceniu zastąp ciągi *\<user-name>* i *\<password>* nową nazwą użytkownika i hasłem. Nazwa użytkownika musi być unikatowa. Hasło musi mieć długość co najmniej ośmiu znaków i zawierać dwa z następujących trzech elementów: litery, cyfry, symbole. Jeśli wystąpił błąd ` 'Conflict'. Details: 409`, zmień nazwę użytkownika. Jeśli wystąpił błąd ` 'Bad Request'. Details: 400`, użyj silniejszego hasła.

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

Zapisz nazwę użytkownika i hasło do użycia w kolejnych krokach podczas wdrażania aplikacji.

Użyj [źródło wdrożenia az aplikacji sieci Web — config lokalnych git](/cli/azure/webapp/deployment/source#config-local-git) polecenie, aby skonfigurować dostęp lokalny Git do aplikacji sieci web platformy Azure. 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

Po skonfigurowaniu użytkownika wdrażania interfejsu wiersza polecenia Azure zawiera adres URL wdrożenia dla aplikacji sieci web platformy Azure w następującym formacie:

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

Skopiuj dane wyjściowe z terminala, ponieważ będzie on używany w następnym kroku. 

### <a name="push-to-azure-from-git"></a>Wypychanie z narzędzia Git na platformę Azure

Dodaj zdalną platformę Azure do lokalnego repozytorium Git. 

```bash
git remote add azure <paste_copied_url_here> 
```

Wypychanie do platformy Azure zdalnego wdrażania aplikacji Node.js. Zostanie wyświetlony monit o podanie hasła określonego wcześniej w ramach tworzenia użytkownika wdrożenia. 

```bash
git push azure master
```

Podczas wdrażania usługi Azure App Service komunikuje się postęp za pomocą narzędzia Git.

```bash
Counting objects: 5, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

Można zauważyć, że proces wdrażania uruchamia [system Gulp](http://gulpjs.com/) po `npm install`. Usługi aplikacji nie działa Gulp lub Grunt zadań podczas wdrażania, dzięki czemu to repozytorium przykładowej mają dwa dodatkowe pliki w katalogu głównym ją włączyć: 

- _.Deployment_ — ten plik zawiera usługę aplikacji w celu uruchomienia `bash deploy.sh` jako niestandardowe wdrożenie skryptu.
- _Deploy.sh_ -niestandardowe wdrożenie skryptu. Jeśli przejrzenie pliku, zobaczysz, że działa `gulp prod` po `npm install` i `bower install`. 

Ta metoda służy do dodawania każdy krok do wdrożenia na podstawie Git. W przypadku ponownego uruchomienia aplikacji sieci web platformy Azure w dowolnym momencie, usługi aplikacji nie ponownie te zadania automatyzacji.

### <a name="browse-to-the-azure-web-app"></a>Przejdź do aplikacji sieci web platformy Azure 

Przejdź do wdrożonej aplikacji sieci web za pomocą przeglądarki sieci web. 

```bash 
http://<app_name>.azurewebsites.net 
``` 

Kliknij przycisk **Utwórz konto** w menu u góry i utworzyć fikcyjny użytkownika. 

Jeśli aplikacja automatycznie loguje się do utworzonego użytkownika powiodą się, aplikacja MEAN.js na platformie Azure ma łączność z bazą danych MongoDB (DB rozwiązania Cosmos). 

![Aplikacja MEAN.js uruchomiona w usłudze Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Wybierz **Admin > Zarządzaj artykuły** można dodać niektórych artykułach. 

**Gratulacje!** Używasz aplikacji Node.js opartych na danych w usłudze Azure App Service.

## <a name="update-data-model-and-redeploy"></a>Aktualizacja modelu danych i utwórz je ponownie

W tym kroku, możesz zmienić `article` danych model i opublikuj zmiany na platformie Azure.

### <a name="update-the-data-model"></a>Aktualizacja modelu danych

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

### <a name="update-the-articles-code"></a>Zaktualizuj kod artykułów

Zaktualizuj reszty Twojej `articles` kod, aby używał `comment`.

Jest pięć plików, należy zmodyfikować: kontroler serwera i klienta cztery widoki. 

Otwórz _modules/articles/server/controllers/articles.server.controller.js_.

W `update` funkcji, należy dodać przydziału `article.comment`. Poniższy kod przedstawia ukończonej `update` funkcji:

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

Powyżej zamknięcia `</section>` tagów, Dodaj następujący wiersz do wyświetlenia `comment` wraz z resztą dane artykułu:

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

Otwórz _modules/articles/client/views/list-articles.client.view.html_.

Powyżej zamknięcia `</a>` tagów, Dodaj następujący wiersz do wyświetlenia `comment` wraz z resztą dane artykułu:

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

Otwórz _modules/articles/client/views/admin/list-articles.client.view.html_.

Wewnątrz `<div class="list-group">` element i powyżej zamknięcia `</a>` tagów, Dodaj następujący wiersz do wyświetlenia `comment` wraz z resztą dane artykułu:

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

Otwórz _modules/articles/client/views/admin/form-article.client.view.html_.

Znajdź `<div class="form-group">` element, który zawiera przycisk Prześlij, która wygląda podobnie do następującej:

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

Powyżej tego tagu, dodać kolejne `<div class="form-group">` elementu można edytować `comment` pola. Nazwę nowego elementu powinna wyglądać następująco:

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
> Należy pamiętać, że Twoje _config/env/production.js_ została wycofana i `MONGODB_URI` zmiennej środowiskowej ustawiono tylko w aplikacji sieci web platformy Azure, a nie na komputerze lokalnym. Należy sprawdzić plik konfiguracji, można znaleźć konfiguracji produkcji domyślnie korzystania z lokalnej bazy danych MongoDB. Dzięki temu nie ruszaj danych produkcyjnych podczas testowania zmiany kodu lokalnie.

Przejdź do `http://localhost:8443` w przeglądarce i upewnij się, że użytkownik jest zalogowany.

Wybierz **Admin > Zarządzaj artykuły**, następnie dodać artykułu, wybierając  **+**  przycisku.

Zostanie wyświetlony nowy `Comment` teraz pola tekstowego.

![Pole komentarz dodany do artykułów](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

W terminalu, Zatrzymaj Node.js, wpisując `Ctrl+C`. 

### <a name="publish-changes-to-azure"></a>Publikowanie zmian na platformie Azure

Zatwierdź zmiany w usłudze Git, a następnie Wypchnij zmiany kodu na platformie Azure.

```bash
git commit -am "added article comment"
git push azure master
```

Raz `git push` jest zakończenie, przejdź do aplikacji sieci web platformy Azure i wypróbowanie nowych funkcji.

![Zmiany modelu i bazy danych publikowanych w systemie Azure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

Jeśli wcześniej dodane artykułów, nadal widać je. Istniejące dane w bazie danych z rozwiązania Cosmos nie zostaną utracone. Ponadto aktualizacje schematu danych i pozostawienie bez zmian do istniejących danych.

## <a name="stream-diagnostic-logs"></a>Dzienniki diagnostyczne strumienia 

Podczas wykonywania aplikacji Node.js w usłudze Azure App Service można uzyskać dzienniki konsoli w potoku do terminalu. W ten sposób można uzyskać tego samego komunikaty diagnostyczne w celu ułatwienia debugowania błędów aplikacji.

Aby rozpocząć przesyłanie strumieniowe dziennika, użyj [końcowego fragmentu dziennika aplikacji sieci Web az](/cli/azure/webapp/log#tail) polecenia.

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

Po rozpoczęciu przesyłania strumieniowego dzienników odświeżanie aplikacji sieci web platformy Azure w przeglądarce, aby uzyskać pewne ruchu w sieci web. Pojawi się w potoku do terminalu dzienniki konsoli.

Dziennik zatrzymania przesyłania strumieniowego w dowolnym momencie, wpisując `Ctrl+C`. 

## <a name="manage-your-azure-web-app"></a>Zarządzanie aplikacji sieci web platformy Azure

Przejdź do [portalu Azure](https://portal.azure.com) zobaczyć aplikacji sieci web został utworzony.

W lewym menu kliknij pozycję **App Services**, a następnie kliknij nazwę swojej aplikacji sieci Web platformy Azure.

![Nawigacja w portalu do aplikacji sieci Web platformy Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

Domyślnie portalu zawiera aplikację sieci web **omówienie** strony. Ta strona udostępnia widok sposobu działania aplikacji. Tutaj możesz również wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie. W lewej części strony kartach stron innej konfiguracji może być otwarty.

![Strona usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a>Następne kroki

Wiadomości:

> [!div class="checklist"]
> * Tworzenie bazy danych MongoDB na platformie Azure
> * Łączenie aplikacji Node.js z bazy danych MongoDB
> * Wdrażanie aplikacji na platformie Azure
> * Aktualizacja modelu danych i ponownie wdrożyć aplikację
> * Strumieniowe przesyłanie dzienników z platformy Azure na terminalu
> * Zarządzanie aplikacją w portalu Azure

Przejdź do następnego samouczek, aby dowiedzieć się, jak zamapować niestandardową nazwę DNS na aplikację sieci web.

> [!div class="nextstepaction"] 
> [Map an existing custom DNS name to Azure Web Apps (Mapowanie istniejącej niestandardowej nazwy DNS na aplikacje internetowe platformy Azure)](app-service-web-tutorial-custom-domain.md)
