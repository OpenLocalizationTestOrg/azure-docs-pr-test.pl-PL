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
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="a11d7-103">Tworzenie aplikacji sieci web Docker Python i PostgreSQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a11d7-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="a11d7-104">Aplikacje sieci Web platformy Azure oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web.</span><span class="sxs-lookup"><span data-stu-id="a11d7-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="a11d7-105">Ten samouczek pokazuje, jak toocreate podstawowe Python Docker sieci web aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a11d7-105">This tutorial shows how toocreate a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="a11d7-106">Połączę się z tej bazy danych PostgreSQL tooa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a11d7-106">You'll connect this app tooa PostgreSQL database.</span></span> <span data-ttu-id="a11d7-107">Gdy wszystko będzie gotowe, będziesz mieć aplikację platformy Python Flask uruchomione w kontenerze Docker na [Azure App Service Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a11d7-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Docker Python Flask aplikacji w usłudze aplikacji Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="a11d7-109">Można wykonać poniższe czynności hello na macOS.</span><span class="sxs-lookup"><span data-stu-id="a11d7-109">You can follow hello steps below on macOS.</span></span> <span data-ttu-id="a11d7-110">Instrukcje dotyczące systemu Linux i Windows są hello takie same, w większości przypadków, ale hello różnice nie są szczegółowo opisane w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="a11d7-110">Linux and Windows instructions are hello same in most cases, but hello differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="a11d7-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a11d7-111">Prerequisites</span></span>

<span data-ttu-id="a11d7-112">toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="a11d7-112">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="a11d7-113">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="a11d7-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="a11d7-114">Zainstaluj język Python</span><span class="sxs-lookup"><span data-stu-id="a11d7-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="a11d7-115">Zainstaluj i uruchom PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="a11d7-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="a11d7-116">Zainstaluj Docker Community Edition</span><span class="sxs-lookup"><span data-stu-id="a11d7-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a11d7-117">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="a11d7-117">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a11d7-118">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="a11d7-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a11d7-119">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a11d7-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="a11d7-120">Testowanie instalacji lokalnej PostgreSQL i utworzyć bazę danych</span><span class="sxs-lookup"><span data-stu-id="a11d7-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="a11d7-121">Otwórz okno terminala hello i uruchom `psql postgres` tooconnect tooyour PostgreSQL serwera.</span><span class="sxs-lookup"><span data-stu-id="a11d7-121">Open hello terminal window and run `psql postgres` tooconnect tooyour local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="a11d7-122">W przypadku pomyślnego nawiązania połączenia z bazą danych PostgreSQL jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="a11d7-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="a11d7-123">Jeśli nie, upewnij się, że lokalnej bazy danych PostgresQL została uruchomiona, wykonując kroki hello w [pobiera - dystrybucji Core PostgreSQL](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="a11d7-123">If not, make sure that your local PostgresQL database is started by following hello steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="a11d7-124">Utwórz bazę danych o nazwie *eventregistration* i Ustaw użytkownika oddzielnej bazy danych o nazwie *Menedżera* hasłem *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="a11d7-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
<span data-ttu-id="a11d7-125">Typ *\q* tooexit hello PostgreSQL klienta.</span><span class="sxs-lookup"><span data-stu-id="a11d7-125">Type *\q* tooexit hello PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="a11d7-126">Tworzenie aplikacji platformy Python Flask lokalnej</span><span class="sxs-lookup"><span data-stu-id="a11d7-126">Create local Python Flask application</span></span>

<span data-ttu-id="a11d7-127">Ten krok umożliwia zdefiniowanie hello lokalnej platformy Python Flask projektu.</span><span class="sxs-lookup"><span data-stu-id="a11d7-127">In this step, you set up hello local Python Flask project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="a11d7-128">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="a11d7-128">Clone hello sample application</span></span>

<span data-ttu-id="a11d7-129">Witaj Otwórz okno terminalu, i `CD` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="a11d7-129">Open hello terminal window, and `CD` tooa working directory.</span></span>  

<span data-ttu-id="a11d7-130">Witaj uruchom następujące polecenia tooclone hello próbki repozytorium, a następnie przejść toohello *initialapp 0,1* wersji.</span><span class="sxs-lookup"><span data-stu-id="a11d7-130">Run hello following commands tooclone hello sample repository and go toohello *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="a11d7-131">To repozytorium przykładowej zawiera [Flask](http://flask.pocoo.org/) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a11d7-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-hello-application"></a><span data-ttu-id="a11d7-132">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="a11d7-132">Run hello application</span></span>

> [!NOTE] 
> <span data-ttu-id="a11d7-133">W kolejnym kroku można ułatwić ten proces przez utworzenie toouse kontenera Docker z hello w produkcyjnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="a11d7-133">In a later step you simplify this process by building a Docker container toouse with hello production database.</span></span>

<span data-ttu-id="a11d7-134">Instalowanie pakietów hello wymagane, a następnie uruchom aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="a11d7-134">Install hello required packages and start hello application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="a11d7-135">Po całkowitym załadowaniem aplikacji hello pojawić coś podobnego toohello następującego komunikatu:</span><span class="sxs-lookup"><span data-stu-id="a11d7-135">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="a11d7-136">Przejdź toohttp://127.0.0.1:5000 w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="a11d7-136">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="a11d7-137">Kliknij przycisk **zarejestrować!**</span><span class="sxs-lookup"><span data-stu-id="a11d7-137">Click **Register!**</span></span> <span data-ttu-id="a11d7-138">i tworzenie użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="a11d7-138">and create a test user.</span></span>

![Platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="a11d7-140">Witaj Flask przykładowej aplikacji są przechowywane dane użytkownika w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="a11d7-140">hello Flask sample application stores user data in hello database.</span></span> <span data-ttu-id="a11d7-141">W przypadku pomyślnego na rejestrowanie użytkowników, aplikacja zapisuje toohello lokalnej PostgreSQL danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="a11d7-141">If you are successful at registering a user, your app is writing data toohello local PostgreSQL database.</span></span>

<span data-ttu-id="a11d7-142">toostop hello Flask serwera w dowolnym momencie, wpisz hello terminali klawisze Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="a11d7-142">toostop hello Flask server at anytime, type Ctrl+C in hello terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="a11d7-143">Utwórz bazę danych PostgreSQL produkcji</span><span class="sxs-lookup"><span data-stu-id="a11d7-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="a11d7-144">W tym kroku utworzysz bazę danych PostgreSQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a11d7-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="a11d7-145">Aplikacja jest wdrożony tooAzure, zostanie użyty tej bazy danych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a11d7-145">When your app is deployed tooAzure, it will use this cloud database.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="a11d7-146">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="a11d7-146">Log in tooAzure</span></span>

<span data-ttu-id="a11d7-147">Jesteś teraz będzie toouse hello Azure CLI 2.0 toocreate hello zasoby potrzebne toohost aplikacji Python w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a11d7-147">You are now going toouse hello Azure CLI 2.0 toocreate hello resources needed toohost your Python application in Azure App Service.</span></span>  <span data-ttu-id="a11d7-148">Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="a11d7-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="a11d7-149">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="a11d7-149">Create a resource group</span></span>

<span data-ttu-id="a11d7-150">Utwórz [grupy zasobów](../azure-resource-manager/resource-group-overview.md) z hello [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a11d7-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="a11d7-151">Witaj poniższy przykład tworzy grupę zasobów w regionu zachodnie stany USA hello:</span><span class="sxs-lookup"><span data-stu-id="a11d7-151">hello following example creates a resource group in hello West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="a11d7-152">Użyj hello [appservice az listy lokalizacje](/cli/azure/appservice#list-locations) toolist dostępne lokalizacje polecenia wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a11d7-152">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="a11d7-153">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="a11d7-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="a11d7-154">Utwórz serwer PostgreSQL z hello [utworzenie przez serwer postgres az](/cli/azure/documentdb#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="a11d7-154">Create a PostgreSQL server with hello [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="a11d7-155">W hello następujące polecenia, należy zastąpić unikatową nazwą serwera na powitania  *\<postgresql_name >* symbolu zastępczego i nazwę użytkownika dla hello  *\<admin_username >* symbolu zastępczego .</span><span class="sxs-lookup"><span data-stu-id="a11d7-155">In hello following command, substitute a unique server name for hello *\<postgresql_name>* placeholder and a user name for hello *\<admin_username>* placeholder.</span></span> <span data-ttu-id="a11d7-156">Nazwa serwera Hello jest używany w ramach punktu końcowego PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), więc nazwa hello musi toobe unikatowa na wszystkich serwerach w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="a11d7-156">hello server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so hello name needs toobe unique across all servers in Azure.</span></span> <span data-ttu-id="a11d7-157">Nazwa użytkownika Hello jest dla konta administratora hello początkowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a11d7-157">hello user name is for hello initial database admin user account.</span></span> <span data-ttu-id="a11d7-158">Jesteś toopick zostanie wyświetlony monit o hasło dla tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a11d7-158">You are prompted toopick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="a11d7-159">Po utworzeniu hello Azure bazy danych dla serwera PostgreSQL hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="a11d7-159">When hello Azure Database for PostgreSQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a><span data-ttu-id="a11d7-160">Tworzenie reguły zapory dla hello Azure bazy danych dla serwera PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="a11d7-160">Create a firewall rule for hello Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="a11d7-161">Uruchom hello następującego wiersza polecenia platformy Azure polecenia tooallow toohello baz danych programu access ze wszystkich adresów IP.</span><span class="sxs-lookup"><span data-stu-id="a11d7-161">Run hello following Azure CLI command tooallow access toohello database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="a11d7-162">Hello Azure CLI potwierdza tworzenie reguł zapory hello z danych wyjściowych toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="a11d7-162">hello Azure CLI confirms hello firewall rule creation with output similar toohello following example:</span></span>

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

## <a name="connect-your-python-flask-application-toohello-database"></a><span data-ttu-id="a11d7-163">Połączenia bazy danych platformy Python Flask toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="a11d7-163">Connect your Python Flask application toohello database</span></span>

<span data-ttu-id="a11d7-164">W tym kroku Połącz się z platformy Python Flask przykładowej aplikacji toohello bazy danych Azure PostgreSQL serwera, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="a11d7-164">In this step, you connect your Python Flask sample application toohello Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="a11d7-165">Utwórz pustą bazę danych i ustaw nowego użytkownika bazy danych aplikacji</span><span class="sxs-lookup"><span data-stu-id="a11d7-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="a11d7-166">Utwórz użytkownika bazy danych o dostęp tooa pojedynczej bazy danych tylko.</span><span class="sxs-lookup"><span data-stu-id="a11d7-166">Create a database user with access tooa single database only.</span></span> <span data-ttu-id="a11d7-167">Użyjesz tych tooavoid poświadczeń, co serwer toohello pełnego dostępu do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a11d7-167">You'll use these credentials tooavoid giving hello application full access toohello server.</span></span>

<span data-ttu-id="a11d7-168">Połącz toohello bazy danych (zostanie wyświetlony monit o hasło administratora).</span><span class="sxs-lookup"><span data-stu-id="a11d7-168">Connect toohello database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="a11d7-169">Utwórz hello bazy danych i użytkowników na podstawie hello PostgreSQL interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a11d7-169">Create hello database and user from hello PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

<span data-ttu-id="a11d7-170">Typ *\q* tooexit hello PostgreSQL klienta.</span><span class="sxs-lookup"><span data-stu-id="a11d7-170">Type *\q* tooexit hello PostgreSQL client.</span></span>

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a><span data-ttu-id="a11d7-171">Testowanie aplikacji hello lokalnie w bazie danych hello Azure PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="a11d7-171">Test hello application locally against hello Azure PostgreSQL database</span></span> 

<span data-ttu-id="a11d7-172">Cofnięcie teraz toohello *aplikacji* folderu hello sklonować repozytorium Github, można uruchomić aplikacji platformy Python Flask hello aktualizując zmiennych środowiskowych hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a11d7-172">Going back now toohello *app* folder of hello cloned Github repository, you can run hello Python Flask application by updating hello database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="a11d7-173">Po całkowitym załadowaniem aplikacji hello pojawić coś podobnego toohello następującego komunikatu:</span><span class="sxs-lookup"><span data-stu-id="a11d7-173">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="a11d7-174">Przejdź toohttp://127.0.0.1:5000 w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="a11d7-174">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="a11d7-175">Kliknij przycisk **zarejestrować!**</span><span class="sxs-lookup"><span data-stu-id="a11d7-175">Click **Register!**</span></span> <span data-ttu-id="a11d7-176">i Utwórz rejestracji testu.</span><span class="sxs-lookup"><span data-stu-id="a11d7-176">and create a test registration.</span></span> <span data-ttu-id="a11d7-177">Teraz pisania bazy danych toohello danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a11d7-177">You are now writing data toohello database in Azure.</span></span>

![Platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a><span data-ttu-id="a11d7-179">Uruchomienie aplikacji hello z kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="a11d7-179">Running hello application from a Docker Container</span></span>

<span data-ttu-id="a11d7-180">Utwórz obraz kontenera Docker hello.</span><span class="sxs-lookup"><span data-stu-id="a11d7-180">Build hello Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="a11d7-181">Docker wyświetli potwierdzenie tego kontenera hello it pomyślnie utworzone.</span><span class="sxs-lookup"><span data-stu-id="a11d7-181">Docker displays a confirmation that it successfully created hello container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="a11d7-182">Dodawanie bazy danych środowiska zmienne tooan środowiska zmiennej pliku *db.env*.</span><span class="sxs-lookup"><span data-stu-id="a11d7-182">Add database environment variables tooan environment variable file *db.env*.</span></span> <span data-ttu-id="a11d7-183">Aplikacja Hello łączą toohello PostgreSQL w produkcyjnej bazie danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a11d7-183">hello app will connect toohello PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="a11d7-184">Uruchom aplikację powitania od w kontenerze Docker hello.</span><span class="sxs-lookup"><span data-stu-id="a11d7-184">Run hello app from within hello Docker container.</span></span> <span data-ttu-id="a11d7-185">Witaj następujące polecenie Określa plik zmiennej środowiskowej hello i mapuje hello domyślny Flask port 5000 toolocal port 5000.</span><span class="sxs-lookup"><span data-stu-id="a11d7-185">hello following command specifies hello environment variable file and maps hello default Flask port 5000 toolocal port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="a11d7-186">dane wyjściowe Hello są podobne toowhat, który został wcześniej wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="a11d7-186">hello output is similar toowhat you saw earlier.</span></span> <span data-ttu-id="a11d7-187">Jednak hello migracji wstępnej bazy danych nie będzie już potrzebował toobe wykonywane i w związku z tym jest pomijana.</span><span class="sxs-lookup"><span data-stu-id="a11d7-187">However, hello initial database migration no longer needs toobe performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="a11d7-188">Witaj baza danych zawiera już rejestracji hello, utworzonej wcześniej.</span><span class="sxs-lookup"><span data-stu-id="a11d7-188">hello database already contains hello registration you created previously.</span></span>

![Docker na podstawie kontenera platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a><span data-ttu-id="a11d7-190">Przekaż hello Docker kontenera tooa kontenera rejestru</span><span class="sxs-lookup"><span data-stu-id="a11d7-190">Upload hello Docker container tooa container registry</span></span>

<span data-ttu-id="a11d7-191">W tym kroku możesz przekazać hello Docker kontenera tooa kontenera rejestru.</span><span class="sxs-lookup"><span data-stu-id="a11d7-191">In this step, you upload hello Docker container tooa container registry.</span></span> <span data-ttu-id="a11d7-192">Użyjesz rejestru kontenera platformy Azure, ale można również używać innych popularnych protokołów, takich jak Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="a11d7-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="a11d7-193">Tworzenie rejestru Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a11d7-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="a11d7-194">W następujące polecenia toocreate rejestru kontenera hello Zastąp  *\<registry_name >* o nazwie rejestru unikatowy kontenera platformy Azure, wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a11d7-194">In hello following command toocreate a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="a11d7-195">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="a11d7-195">Output</span></span>
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

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="a11d7-196">Pobieranie poświadczeń rejestru hello wypychanie i ściąganie obrazy usługi Docker</span><span class="sxs-lookup"><span data-stu-id="a11d7-196">Retrieve hello registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="a11d7-197">poświadczenia rejestru tooshow, najpierw włączyć tryb administratora.</span><span class="sxs-lookup"><span data-stu-id="a11d7-197">tooshow registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="a11d7-198">Możesz sprawdzić dwa hasła.</span><span class="sxs-lookup"><span data-stu-id="a11d7-198">You see two passwords.</span></span> <span data-ttu-id="a11d7-199">Zwróć uwagę na powitania nazwy użytkownika i hasła pierwszy hello.</span><span class="sxs-lookup"><span data-stu-id="a11d7-199">Make note of hello user name and hello first password.</span></span>

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

### <a name="upload-your-docker-container-tooazure-container-registry"></a><span data-ttu-id="a11d7-200">Przekazywanie z tooAzure kontenera Docker rejestru kontenera</span><span class="sxs-lookup"><span data-stu-id="a11d7-200">Upload your Docker container tooAzure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a><span data-ttu-id="a11d7-201">Wdrażanie tooAzure aplikacji platformy Python Flask Docker hello</span><span class="sxs-lookup"><span data-stu-id="a11d7-201">Deploy hello Docker Python Flask application tooAzure</span></span>

<span data-ttu-id="a11d7-202">W tym kroku możesz wdrożyć programu Docker na podstawie kontenera platformy Python Flask aplikacji tooAzure usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a11d7-202">In this step, you deploy your Docker container-based Python Flask application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="a11d7-203">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="a11d7-203">Create an App Service plan</span></span>

<span data-ttu-id="a11d7-204">Tworzenie planu usługi aplikacji z hello [Tworzenie planu usług aplikacji az](/cli/azure/appservice/plan#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="a11d7-204">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="a11d7-205">Witaj poniższy przykład tworzy plan usługi aplikacji opartych na systemie Linux o nazwie *myAppServicePlan* przy użyciu hello S1 warstwa cenowa:</span><span class="sxs-lookup"><span data-stu-id="a11d7-205">hello following example creates a Linux-based App Service plan named *myAppServicePlan* using hello S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="a11d7-206">Po utworzeniu planu usługi aplikacji hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="a11d7-206">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="a11d7-207">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="a11d7-207">Create a web app</span></span>

<span data-ttu-id="a11d7-208">Tworzenie aplikacji sieci web w hello *myAppServicePlan* planu usługi aplikacji z hello [tworzenie aplikacji sieci Web az](/cli/azure/webapp#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="a11d7-208">Create a web app in hello *myAppServicePlan* App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="a11d7-209">umożliwia aplikacji sieci web Hello możesz hosting miejsce toodeploy kodu i zawiera adres URL dla Ciebie tooview hello wdrożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a11d7-209">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="a11d7-210">Użyj aplikacji sieci web hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="a11d7-210">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="a11d7-211">Witaj następujące polecenia, Zastąp hello  *\<nazwa_aplikacji >* symbol zastępczy unikatowej nazwy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a11d7-211">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="a11d7-212">Ta nazwa jest częścią hello domyślny adres URL dla aplikacji sieci web hello, więc nazwa hello musi toobe unikatowy przez wszystkie aplikacje w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a11d7-212">This name is part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="a11d7-213">Podczas tworzenia aplikacji sieci web hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="a11d7-213">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-hello-database-environment-variables"></a><span data-ttu-id="a11d7-214">Skonfiguruj zmienne środowiskowe hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="a11d7-214">Configure hello database environment variables</span></span>

<span data-ttu-id="a11d7-215">Wcześniej w samouczku hello zdefiniowano danych PostgreSQL tooyour tooconnect zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="a11d7-215">Earlier in hello tutorial, you defined environment variables tooconnect tooyour PostgreSQL database.</span></span>

<span data-ttu-id="a11d7-216">W usłudze App Service można ustawić zmienne środowiskowe jako _ustawień aplikacji_ przy użyciu hello [az aplikacji sieci Web config appsettings zestaw](/cli/azure/webapp/config#set) polecenia.</span><span class="sxs-lookup"><span data-stu-id="a11d7-216">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="a11d7-217">Witaj poniższy przykład określa szczegóły połączenia z bazą danych hello jako ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a11d7-217">hello following example specifies hello database connection details as app settings.</span></span> <span data-ttu-id="a11d7-218">Używa również hello *portu* zmiennej toomap PORT 5000 z kontenera Docker ruchu tooreceive HTTP na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="a11d7-218">It also uses hello *PORT* variable toomap PORT 5000 from your Docker Container tooreceive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="a11d7-219">Konfigurowanie wdrożenia kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="a11d7-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="a11d7-220">Usługi aplikacji może automatycznie Pobierz i uruchom kontener Docker.</span><span class="sxs-lookup"><span data-stu-id="a11d7-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="a11d7-221">Zawsze, gdy zaktualizować hello kontenera Docker lub zmienić ustawienia hello, należy ponownie uruchomić aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a11d7-221">Whenever you update hello Docker container or change hello settings, restart hello app.</span></span> <span data-ttu-id="a11d7-222">Ponowne uruchomienie gwarantuje, że wszystkie ustawienia są stosowane i kontener najnowsze hello są pobierane z rejestru hello.</span><span class="sxs-lookup"><span data-stu-id="a11d7-222">Restarting ensures that all settings are applied and hello latest container is pulled from hello registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="a11d7-223">Przeglądaj toohello aplikacji sieci web Azure</span><span class="sxs-lookup"><span data-stu-id="a11d7-223">Browse toohello Azure web app</span></span> 

<span data-ttu-id="a11d7-224">Przeglądaj toohello wdrożyć aplikację sieci web przy użyciu przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="a11d7-224">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="a11d7-225">Hello aplikacji sieci web ma tooload dłużej, ponieważ kontener hello ma toobe pobieranie i uruchamianie po zmianie hello kontenera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a11d7-225">hello web app takes longer tooload because hello container has toobe downloaded and started after hello container configuration is changed.</span></span>

<span data-ttu-id="a11d7-226">Widać wcześniej zarejestrowanego gości, zapisane w poprzednim kroku hello toohello Azure środowiska produkcyjnego w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="a11d7-226">You see previously registered guests that were saved toohello Azure production database in hello previous step.</span></span>

![Docker na podstawie kontenera platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="a11d7-228">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="a11d7-228">**Congratulations!**</span></span> <span data-ttu-id="a11d7-229">Używasz Docker aplikacji platformy Python Flask kontenera w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a11d7-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="a11d7-230">Aktualizacja modelu danych i utwórz je ponownie</span><span class="sxs-lookup"><span data-stu-id="a11d7-230">Update data model and redeploy</span></span>

<span data-ttu-id="a11d7-231">W tym kroku możesz dodać hello numer rejestracji zdarzeń tooeach uczestników, aktualizując hello gościa modelu.</span><span class="sxs-lookup"><span data-stu-id="a11d7-231">In this step, you add hello number of attendees tooeach event registration by updating hello Guest model.</span></span>

<span data-ttu-id="a11d7-232">Zapoznaj się z hello *migracji 0,2* zlecenia przy użyciu następującego polecenia git hello:</span><span class="sxs-lookup"><span data-stu-id="a11d7-232">Check out hello *0.2-migration* release with hello following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="a11d7-233">Ta wersja jest już wykonane hello tooviews niezbędne zmiany, kontrolery i modelu.</span><span class="sxs-lookup"><span data-stu-id="a11d7-233">This release already made hello necessary changes tooviews, controllers, and model.</span></span> <span data-ttu-id="a11d7-234">Obejmuje też migracja bazy danych, wygenerowane za pomocą *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="a11d7-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="a11d7-235">Można wyświetlić wszystkie zmiany dokonane za pomocą następującego polecenia git hello:</span><span class="sxs-lookup"><span data-stu-id="a11d7-235">You can see all changes made via hello following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="a11d7-236">Przetestuj zmiany lokalnie</span><span class="sxs-lookup"><span data-stu-id="a11d7-236">Test your changes locally</span></span>

<span data-ttu-id="a11d7-237">Uruchamiając następujące polecenia tootest hello zmiany lokalnie uruchomiony serwer flask hello.</span><span class="sxs-lookup"><span data-stu-id="a11d7-237">Run hello following commands tootest your changes locally by running hello flask server.</span></span>

<span data-ttu-id="a11d7-238">Mac / Linux:</span><span class="sxs-lookup"><span data-stu-id="a11d7-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="a11d7-239">Przejdź toohttp://127.0.0.1:5000 zmiany hello tooview przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="a11d7-239">Navigate toohttp://127.0.0.1:5000 in your browser tooview hello changes.</span></span> <span data-ttu-id="a11d7-240">Utwórz rejestracji testu.</span><span class="sxs-lookup"><span data-stu-id="a11d7-240">Create a test registration.</span></span>

![Docker na podstawie kontenera platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a><span data-ttu-id="a11d7-242">Publikowanie zmian tooAzure</span><span class="sxs-lookup"><span data-stu-id="a11d7-242">Publish changes tooAzure</span></span>

<span data-ttu-id="a11d7-243">Utwórz nowy obraz docker hello wypchnąć go toohello kontenera rejestru i ponownie uruchomić aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a11d7-243">Build hello new docker image, push it toohello container registry, and restart hello app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="a11d7-244">Przejdź tooyour aplikacji sieci web platformy Azure i wypróbować nową funkcję hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="a11d7-244">Navigate tooyour Azure web app and try out hello new functionality again.</span></span> <span data-ttu-id="a11d7-245">Utwórz inną rejestracja zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="a11d7-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Docker Python Flask aplikacji w usłudze aplikacji Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="a11d7-247">Zarządzanie aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a11d7-247">Manage your Azure web app</span></span>

<span data-ttu-id="a11d7-248">Przejdź toohello [portalu Azure](https://portal.azure.com) aplikacji sieci web hello toosee został utworzony.</span><span class="sxs-lookup"><span data-stu-id="a11d7-248">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="a11d7-249">W menu po lewej stronie powitania kliknij **usługi aplikacji**, następnie kliknij nazwę hello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a11d7-249">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="a11d7-251">Domyślnie hello portal przedstawiono aplikację sieci web **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="a11d7-251">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="a11d7-252">Ta strona udostępnia widok sposobu działania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a11d7-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="a11d7-253">Tutaj możesz również wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="a11d7-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="a11d7-254">Witaj w lewej części strony hello hello kartach hello innej konfiguracji stron, które można otworzyć.</span><span class="sxs-lookup"><span data-stu-id="a11d7-254">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Strona usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="a11d7-256">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a11d7-256">Next steps</span></span>

<span data-ttu-id="a11d7-257">Przejść dalej toolearn samouczka toohello jak toomap DNS niestandardowej nazwy tooyour aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a11d7-257">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="a11d7-258">Mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="a11d7-258">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
