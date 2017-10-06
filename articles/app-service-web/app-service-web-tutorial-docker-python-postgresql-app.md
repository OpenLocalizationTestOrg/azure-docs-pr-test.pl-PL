---
title: aaaBuild Docker Python i PostgreSQL aplikacji sieci web na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooget aplikacji Docker Python działa na platformie Azure, z połączenia tooa PostgreSQL bazy danych."
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a>Tworzenie aplikacji sieci web Docker Python i PostgreSQL na platformie Azure

Aplikacje sieci Web platformy Azure oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web. Ten samouczek pokazuje, jak toocreate podstawowe Python Docker sieci web aplikacji na platformie Azure. Połączę się z tej bazy danych PostgreSQL tooa aplikacji. Gdy wszystko będzie gotowe, będziesz mieć aplikację platformy Python Flask uruchomione w kontenerze Docker na [Azure App Service Web Apps](app-service-web-overview.md).

![Docker Python Flask aplikacji w usłudze aplikacji Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

Można wykonać poniższe czynności hello na macOS. Instrukcje dotyczące systemu Linux i Windows są hello takie same, w większości przypadków, ale hello różnice nie są szczegółowo opisane w tym samouczku.
 
## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka:

1. [Zainstaluj oprogramowanie Git](https://git-scm.com/)
1. [Zainstaluj język Python](https://www.python.org/downloads/)
1. [Zainstaluj i uruchom PostgreSQL](https://www.postgresql.org/download/)
1. [Zainstaluj Docker Community Edition](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-postgresql-installation-and-create-a-database"></a>Testowanie instalacji lokalnej PostgreSQL i utworzyć bazę danych

Otwórz okno terminala hello i uruchom `psql postgres` tooconnect tooyour PostgreSQL serwera.

```bash
psql postgres
```

W przypadku pomyślnego nawiązania połączenia z bazą danych PostgreSQL jest uruchomiona. Jeśli nie, upewnij się, że lokalnej bazy danych PostgresQL została uruchomiona, wykonując kroki hello w [pobiera - dystrybucji Core PostgreSQL](https://www.postgresql.org/download/).

Utwórz bazę danych o nazwie *eventregistration* i Ustaw użytkownika oddzielnej bazy danych o nazwie *Menedżera* hasłem *supersecretpass*.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
Typ *\q* tooexit hello PostgreSQL klienta. 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a>Tworzenie aplikacji platformy Python Flask lokalnej

Ten krok umożliwia zdefiniowanie hello lokalnej platformy Python Flask projektu.

### <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Witaj Otwórz okno terminalu, i `CD` tooa katalog roboczy.  

Witaj uruchom następujące polecenia tooclone hello próbki repozytorium, a następnie przejść toohello *initialapp 0,1* wersji.

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

To repozytorium przykładowej zawiera [Flask](http://flask.pocoo.org/) aplikacji. 

### <a name="run-hello-application"></a>Uruchamianie aplikacji hello

> [!NOTE] 
> W kolejnym kroku można ułatwić ten proces przez utworzenie toouse kontenera Docker z hello w produkcyjnej bazie danych.

Instalowanie pakietów hello wymagane, a następnie uruchom aplikację hello.

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Po całkowitym załadowaniem aplikacji hello pojawić coś podobnego toohello następującego komunikatu:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Przejdź toohttp://127.0.0.1:5000 w przeglądarce. Kliknij przycisk **zarejestrować!** i tworzenie użytkownika testowego.

![Platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

Witaj Flask przykładowej aplikacji są przechowywane dane użytkownika w bazie danych hello. W przypadku pomyślnego na rejestrowanie użytkowników, aplikacja zapisuje toohello lokalnej PostgreSQL danych w bazie danych.

toostop hello Flask serwera w dowolnym momencie, wpisz hello terminali klawisze Ctrl + C. 

## <a name="create-a-production-postgresql-database"></a>Utwórz bazę danych PostgreSQL produkcji

W tym kroku utworzysz bazę danych PostgreSQL na platformie Azure. Aplikacja jest wdrożony tooAzure, zostanie użyty tej bazy danych w chmurze.

### <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Jesteś teraz będzie toouse hello Azure CLI 2.0 toocreate hello zasoby potrzebne toohost aplikacji Python w usłudze Azure App Service.  Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami. 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz [grupy zasobów](../azure-resource-manager/resource-group-overview.md) z hello [Tworzenie grupy az](/cli/azure/group#create). 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Witaj poniższy przykład tworzy grupę zasobów w regionu zachodnie stany USA hello:

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

Użyj hello [appservice az listy lokalizacje](/cli/azure/appservice#list-locations) toolist dostępne lokalizacje polecenia wiersza polecenia platformy Azure.

### <a name="create-an-azure-database-for-postgresql-server"></a>Tworzenie serwera usługi Azure Database for PostgreSQL

Utwórz serwer PostgreSQL z hello [utworzenie przez serwer postgres az](/cli/azure/documentdb#create) polecenia.

W hello następujące polecenia, należy zastąpić unikatową nazwą serwera na powitania  *\<postgresql_name >* symbolu zastępczego i nazwę użytkownika dla hello  *\<admin_username >* symbolu zastępczego . Nazwa serwera Hello jest używany w ramach punktu końcowego PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), więc nazwa hello musi toobe unikatowa na wszystkich serwerach w systemie Azure. Nazwa użytkownika Hello jest dla konta administratora hello początkowej bazy danych. Jesteś toopick zostanie wyświetlony monit o hasło dla tego użytkownika.

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

Po utworzeniu hello Azure bazy danych dla serwera PostgreSQL hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a>Tworzenie reguły zapory dla hello Azure bazy danych dla serwera PostgreSQL

Uruchom hello następującego wiersza polecenia platformy Azure polecenia tooallow toohello baz danych programu access ze wszystkich adresów IP.

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

Hello Azure CLI potwierdza tworzenie reguł zapory hello z danych wyjściowych toohello podobnie poniższy przykład:

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-toohello-database"></a>Połączenia bazy danych platformy Python Flask toohello aplikacji

W tym kroku Połącz się z platformy Python Flask przykładowej aplikacji toohello bazy danych Azure PostgreSQL serwera, który został utworzony.

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a>Utwórz pustą bazę danych i ustaw nowego użytkownika bazy danych aplikacji

Utwórz użytkownika bazy danych o dostęp tooa pojedynczej bazy danych tylko. Użyjesz tych tooavoid poświadczeń, co serwer toohello pełnego dostępu do aplikacji hello.

Połącz toohello bazy danych (zostanie wyświetlony monit o hasło administratora).

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

Utwórz hello bazy danych i użytkowników na podstawie hello PostgreSQL interfejsu wiersza polecenia.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

Typ *\q* tooexit hello PostgreSQL klienta.

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a>Testowanie aplikacji hello lokalnie w bazie danych hello Azure PostgreSQL 

Cofnięcie teraz toohello *aplikacji* folderu hello sklonować repozytorium Github, można uruchomić aplikacji platformy Python Flask hello aktualizując zmiennych środowiskowych hello bazy danych.

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Po całkowitym załadowaniem aplikacji hello pojawić coś podobnego toohello następującego komunikatu:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Przejdź toohttp://127.0.0.1:5000 w przeglądarce. Kliknij przycisk **zarejestrować!** i Utwórz rejestracji testu. Teraz pisania bazy danych toohello danych na platformie Azure.

![Platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a>Uruchomienie aplikacji hello z kontenera Docker

Utwórz obraz kontenera Docker hello.

```bash
cd ..
docker build -t flask-postgresql-sample .
```

Docker wyświetli potwierdzenie tego kontenera hello it pomyślnie utworzone.

```bash
Successfully built 7548f983a36b
```

Dodawanie bazy danych środowiska zmienne tooan środowiska zmiennej pliku *db.env*. Aplikacja Hello łączą toohello PostgreSQL w produkcyjnej bazie danych na platformie Azure.

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

Uruchom aplikację powitania od w kontenerze Docker hello. Witaj następujące polecenie Określa plik zmiennej środowiskowej hello i mapuje hello domyślny Flask port 5000 toolocal port 5000.

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

dane wyjściowe Hello są podobne toowhat, który został wcześniej wyświetlony. Jednak hello migracji wstępnej bazy danych nie będzie już potrzebował toobe wykonywane i w związku z tym jest pomijana.

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

Witaj baza danych zawiera już rejestracji hello, utworzonej wcześniej.

![Docker na podstawie kontenera platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a>Przekaż hello Docker kontenera tooa kontenera rejestru

W tym kroku możesz przekazać hello Docker kontenera tooa kontenera rejestru. Użyjesz rejestru kontenera platformy Azure, ale można również używać innych popularnych protokołów, takich jak Centrum Docker.

### <a name="create-an-azure-container-registry"></a>Tworzenie rejestru Azure Container Registry

W następujące polecenia toocreate rejestru kontenera hello Zastąp  *\<registry_name >* o nazwie rejestru unikatowy kontenera platformy Azure, wybranych przez użytkownika.

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

Dane wyjściowe
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a>Pobieranie poświadczeń rejestru hello wypychanie i ściąganie obrazy usługi Docker

poświadczenia rejestru tooshow, najpierw włączyć tryb administratora.

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

Możesz sprawdzić dwa hasła. Zwróć uwagę na powitania nazwy użytkownika i hasła pierwszy hello.

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-tooazure-container-registry"></a>Przekazywanie z tooAzure kontenera Docker rejestru kontenera

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a>Wdrażanie tooAzure aplikacji platformy Python Flask Docker hello

W tym kroku możesz wdrożyć programu Docker na podstawie kontenera platformy Python Flask aplikacji tooAzure usługi aplikacji.

### <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service

Tworzenie planu usługi aplikacji z hello [Tworzenie planu usług aplikacji az](/cli/azure/appservice/plan#create) polecenia. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Witaj poniższy przykład tworzy plan usługi aplikacji opartych na systemie Linux o nazwie *myAppServicePlan* przy użyciu hello S1 warstwa cenowa:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

Po utworzeniu planu usługi aplikacji hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web

Tworzenie aplikacji sieci web w hello *myAppServicePlan* planu usługi aplikacji z hello [tworzenie aplikacji sieci Web az](/cli/azure/webapp#create) polecenia. 

umożliwia aplikacji sieci web Hello możesz hosting miejsce toodeploy kodu i zawiera adres URL dla Ciebie tooview hello wdrożonych aplikacji. Użyj aplikacji sieci web hello toocreate. 

Witaj następujące polecenia, Zastąp hello  *\<nazwa_aplikacji >* symbol zastępczy unikatowej nazwy aplikacji. Ta nazwa jest częścią hello domyślny adres URL dla aplikacji sieci web hello, więc nazwa hello musi toobe unikatowy przez wszystkie aplikacje w usłudze Azure App Service. 

```azurecli
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

### <a name="configure-hello-database-environment-variables"></a>Skonfiguruj zmienne środowiskowe hello bazy danych

Wcześniej w samouczku hello zdefiniowano danych PostgreSQL tooyour tooconnect zmienne środowiskowe.

W usłudze App Service można ustawić zmienne środowiskowe jako _ustawień aplikacji_ przy użyciu hello [az aplikacji sieci Web config appsettings zestaw](/cli/azure/webapp/config#set) polecenia. 

Witaj poniższy przykład określa szczegóły połączenia z bazą danych hello jako ustawienia aplikacji. Używa również hello *portu* zmiennej toomap PORT 5000 z kontenera Docker ruchu tooreceive HTTP na porcie 80.

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a>Konfigurowanie wdrożenia kontenera Docker 

Usługi aplikacji może automatycznie Pobierz i uruchom kontener Docker.

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

Zawsze, gdy zaktualizować hello kontenera Docker lub zmienić ustawienia hello, należy ponownie uruchomić aplikacji hello. Ponowne uruchomienie gwarantuje, że wszystkie ustawienia są stosowane i kontener najnowsze hello są pobierane z rejestru hello.

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a>Przeglądaj toohello aplikacji sieci web Azure 

Przeglądaj toohello wdrożyć aplikację sieci web przy użyciu przeglądarki sieci web. 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> Hello aplikacji sieci web ma tooload dłużej, ponieważ kontener hello ma toobe pobieranie i uruchamianie po zmianie hello kontenera konfiguracji.

Widać wcześniej zarejestrowanego gości, zapisane w poprzednim kroku hello toohello Azure środowiska produkcyjnego w bazie danych.

![Docker na podstawie kontenera platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

**Gratulacje!** Używasz Docker aplikacji platformy Python Flask kontenera w usłudze Azure App Service.

## <a name="update-data-model-and-redeploy"></a>Aktualizacja modelu danych i utwórz je ponownie

W tym kroku możesz dodać hello numer rejestracji zdarzeń tooeach uczestników, aktualizując hello gościa modelu.

Zapoznaj się z hello *migracji 0,2* zlecenia przy użyciu następującego polecenia git hello:

```bash
git checkout tags/0.2-migration
```

Ta wersja jest już wykonane hello tooviews niezbędne zmiany, kontrolery i modelu. Obejmuje też migracja bazy danych, wygenerowane za pomocą *alembic* (`flask db migrate`). Można wyświetlić wszystkie zmiany dokonane za pomocą następującego polecenia git hello:

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a>Przetestuj zmiany lokalnie

Uruchamiając następujące polecenia tootest hello zmiany lokalnie uruchomiony serwer flask hello.

Mac / Linux:
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Przejdź toohttp://127.0.0.1:5000 zmiany hello tooview przeglądarki. Utwórz rejestracji testu.

![Docker na podstawie kontenera platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a>Publikowanie zmian tooAzure

Utwórz nowy obraz docker hello wypchnąć go toohello kontenera rejestru i ponownie uruchomić aplikacji hello.

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

Przejdź tooyour aplikacji sieci web platformy Azure i wypróbować nową funkcję hello ponownie. Utwórz inną rejestracja zdarzeń.

```bash 
http://<app_name>.azurewebsites.net 
```

![Docker Python Flask aplikacji w usłudze aplikacji Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a>Zarządzanie aplikacji sieci web platformy Azure

Przejdź toohello [portalu Azure](https://portal.azure.com) aplikacji sieci web hello toosee został utworzony.

W menu po lewej stronie powitania kliknij **usługi aplikacji**, następnie kliknij nazwę hello aplikacji sieci web platformy Azure.

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

Domyślnie hello portal przedstawiono aplikację sieci web **omówienie** strony. Ta strona udostępnia widok sposobu działania aplikacji. Tutaj możesz również wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie. Witaj w lewej części strony hello hello kartach hello innej konfiguracji stron, które można otworzyć.

![Strona usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a>Następne kroki

Przejść dalej toolearn samouczka toohello jak toomap DNS niestandardowej nazwy tooyour aplikacji sieci web.

> [!div class="nextstepaction"] 
> [Mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacji sieci Web](app-service-web-tutorial-custom-domain.md)
