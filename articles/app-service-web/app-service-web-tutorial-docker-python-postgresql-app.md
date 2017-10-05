---
title: Tworzenie aplikacji sieci web Docker Python i PostgreSQL na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak pobrać aplikację Docker Python, działa na platformie Azure z połączeniem z bazą danych PostgreSQL."
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
ms.openlocfilehash: e70f85a1eb4a6e1a81e0ca4fae228ca97deca6fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="81089-103">Tworzenie aplikacji sieci web Docker Python i PostgreSQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="81089-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="81089-104">Aplikacje sieci Web platformy Azure oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web.</span><span class="sxs-lookup"><span data-stu-id="81089-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="81089-105">W tym samouczku przedstawiono sposób tworzenia podstawowej aplikacji sieci web Docker Python na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="81089-105">This tutorial shows how to create a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="81089-106">Będzie połączyć tę aplikację z bazy danych programu PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="81089-106">You'll connect this app to a PostgreSQL database.</span></span> <span data-ttu-id="81089-107">Gdy wszystko będzie gotowe, będziesz mieć aplikację platformy Python Flask uruchomione w kontenerze Docker na [Azure App Service Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="81089-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Docker Python Flask aplikacji w usłudze aplikacji Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="81089-109">Na macOS można wykonać poniższe czynności.</span><span class="sxs-lookup"><span data-stu-id="81089-109">You can follow the steps below on macOS.</span></span> <span data-ttu-id="81089-110">Instrukcje dotyczące systemu Linux i Windows są takie same, w większości przypadków, ale różnice nie są szczegółowo opisane w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="81089-110">Linux and Windows instructions are the same in most cases, but the differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="81089-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="81089-111">Prerequisites</span></span>

<span data-ttu-id="81089-112">W celu ukończenia tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="81089-112">To complete this tutorial:</span></span>

1. [<span data-ttu-id="81089-113">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="81089-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="81089-114">Zainstaluj język Python</span><span class="sxs-lookup"><span data-stu-id="81089-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="81089-115">Zainstaluj i uruchom PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="81089-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="81089-116">Zainstaluj Docker Community Edition</span><span class="sxs-lookup"><span data-stu-id="81089-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="81089-117">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="81089-117">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="81089-118">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="81089-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="81089-119">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="81089-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="81089-120">Testowanie instalacji lokalnej PostgreSQL i utworzyć bazę danych</span><span class="sxs-lookup"><span data-stu-id="81089-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="81089-121">Otwórz okno terminalu i uruchom `psql postgres` nawiązać połączenia z serwerem lokalnym PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="81089-121">Open the terminal window and run `psql postgres` to connect to your local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="81089-122">W przypadku pomyślnego nawiązania połączenia z bazą danych PostgreSQL jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="81089-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="81089-123">Jeśli nie, upewnij się, że lokalnej bazy danych PostgresQL została uruchomiona, wykonując kroki opisane w temacie [pobiera - dystrybucji Core PostgreSQL](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="81089-123">If not, make sure that your local PostgresQL database is started by following the steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="81089-124">Utwórz bazę danych o nazwie *eventregistration* i Ustaw użytkownika oddzielnej bazy danych o nazwie *Menedżera* hasłem *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="81089-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```
<span data-ttu-id="81089-125">Typ *\q* aby zamknąć klienta programu PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="81089-125">Type *\q* to exit the PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="81089-126">Tworzenie aplikacji platformy Python Flask lokalnej</span><span class="sxs-lookup"><span data-stu-id="81089-126">Create local Python Flask application</span></span>

<span data-ttu-id="81089-127">Ten krok służy do konfigurowania lokalnego projektu platformy Python Flask.</span><span class="sxs-lookup"><span data-stu-id="81089-127">In this step, you set up the local Python Flask project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="81089-128">Klonowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="81089-128">Clone the sample application</span></span>

<span data-ttu-id="81089-129">Otwórz okno terminala i `CD` do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="81089-129">Open the terminal window, and `CD` to a working directory.</span></span>  

<span data-ttu-id="81089-130">Uruchom następujące polecenia w klonowania repozytorium przykładowej i przejdź do *initialapp 0,1* wersji.</span><span class="sxs-lookup"><span data-stu-id="81089-130">Run the following commands to clone the sample repository and go to the *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="81089-131">To repozytorium przykładowej zawiera [Flask](http://flask.pocoo.org/) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81089-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-the-application"></a><span data-ttu-id="81089-132">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="81089-132">Run the application</span></span>

> [!NOTE] 
> <span data-ttu-id="81089-133">W kolejnym kroku można ułatwić ten proces przez utworzenie kontenera Docker można używać z produkcyjną bazę danych.</span><span class="sxs-lookup"><span data-stu-id="81089-133">In a later step you simplify this process by building a Docker container to use with the production database.</span></span>

<span data-ttu-id="81089-134">Zainstaluj wymagane pakiety i uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="81089-134">Install the required packages and start the application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="81089-135">Gdy aplikacja zostanie całkowicie załadowany, zobacz podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="81089-135">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="81089-136">Przejdź do http://127.0.0.1:5000 w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="81089-136">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="81089-137">Kliknij przycisk **zarejestrować!**</span><span class="sxs-lookup"><span data-stu-id="81089-137">Click **Register!**</span></span> <span data-ttu-id="81089-138">i tworzenie użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="81089-138">and create a test user.</span></span>

![Platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="81089-140">Przykładowa aplikacja platformy Flask przechowuje dane użytkownika w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="81089-140">The Flask sample application stores user data in the database.</span></span> <span data-ttu-id="81089-141">W przypadku pomyślnego na rejestrowanie użytkowników, aplikacja zapisuje dane w lokalnej bazie danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="81089-141">If you are successful at registering a user, your app is writing data to the local PostgreSQL database.</span></span>

<span data-ttu-id="81089-142">Aby zatrzymać serwer platformy Flask, w dowolnym momencie, wpisz klawisze Ctrl + C w terminalu.</span><span class="sxs-lookup"><span data-stu-id="81089-142">To stop the Flask server at anytime, type Ctrl+C in the terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="81089-143">Utwórz bazę danych PostgreSQL produkcji</span><span class="sxs-lookup"><span data-stu-id="81089-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="81089-144">W tym kroku utworzysz bazę danych PostgreSQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="81089-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="81089-145">Gdy aplikacja jest wdrażana na platformie Azure, będzie on używać tej bazy danych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="81089-145">When your app is deployed to Azure, it will use this cloud database.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="81089-146">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="81089-146">Log in to Azure</span></span>

<span data-ttu-id="81089-147">Teraz ma Azure CLI 2.0 umożliwia tworzenie zasobów niezbędnych do hostowania aplikacji języka Python w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="81089-147">You are now going to use the Azure CLI 2.0 to create the resources needed to host your Python application in Azure App Service.</span></span>  <span data-ttu-id="81089-148">Zaloguj się do subskrypcji platformy Azure za pomocą polecenia [az login](/cli/azure/#login) i postępuj zgodnie z instrukcjami wyświetlanymi na ekranie.</span><span class="sxs-lookup"><span data-stu-id="81089-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="81089-149">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="81089-149">Create a resource group</span></span>

<span data-ttu-id="81089-150">Utwórz [grupę zasobów](../azure-resource-manager/resource-group-overview.md) za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="81089-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="81089-151">Poniższy przykład tworzy grupę zasobów regionu zachodnie stany USA:</span><span class="sxs-lookup"><span data-stu-id="81089-151">The following example creates a resource group in the West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="81089-152">Użyj [appservice az listy lokalizacje](/cli/azure/appservice#list-locations) polecenia wiersza polecenia platformy Azure do listy dostępnych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="81089-152">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="81089-153">Tworzenie serwera usługi Azure Database for PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="81089-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="81089-154">Utwórz serwer PostgreSQL z [utworzenie przez serwer postgres az](/cli/azure/documentdb#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="81089-154">Create a PostgreSQL server with the [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="81089-155">W poniższym poleceniu zastąp unikatową nazwą serwera dla  *\<postgresql_name >* nazw dla symbolu zastępczego i użytkownik  *\<admin_username >* symbolu zastępczego.</span><span class="sxs-lookup"><span data-stu-id="81089-155">In the following command, substitute a unique server name for the *\<postgresql_name>* placeholder and a user name for the *\<admin_username>* placeholder.</span></span> <span data-ttu-id="81089-156">Nazwa serwera jest używana jako część PostgreSQL punktu końcowego (`https://<postgresql_name>.postgres.database.azure.com`), więc nazwa musi być unikatowa na wszystkich serwerach w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="81089-156">The server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so the name needs to be unique across all servers in Azure.</span></span> <span data-ttu-id="81089-157">Nazwa użytkownika jest dla konta użytkownika administracyjnego początkowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="81089-157">The user name is for the initial database admin user account.</span></span> <span data-ttu-id="81089-158">Zostanie wyświetlony monit wybierz hasło dla tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="81089-158">You are prompted to pick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="81089-159">Po utworzeniu bazy danych Azure dla serwera PostgreSQL interfejsu wiersza polecenia Azure zawiera informacje podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="81089-159">When the Azure Database for PostgreSQL server is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="create-a-firewall-rule-for-the-azure-database-for-postgresql-server"></a><span data-ttu-id="81089-160">Tworzenie reguły zapory bazy danych Azure PostgreSQL serwera</span><span class="sxs-lookup"><span data-stu-id="81089-160">Create a firewall rule for the Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="81089-161">Uruchom następujące polecenie wiersza polecenia platformy Azure, aby zezwolić na dostęp do bazy danych ze wszystkich adresów IP.</span><span class="sxs-lookup"><span data-stu-id="81089-161">Run the following Azure CLI command to allow access to the database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="81089-162">Azure CLI potwierdza tworzenia reguły zapory, przy czym dane wyjściowe podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="81089-162">The Azure CLI confirms the firewall rule creation with output similar to the following example:</span></span>

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

## <a name="connect-your-python-flask-application-to-the-database"></a><span data-ttu-id="81089-163">Połączyć aplikację platformy Python Flask do bazy danych</span><span class="sxs-lookup"><span data-stu-id="81089-163">Connect your Python Flask application to the database</span></span>

<span data-ttu-id="81089-164">W tym kroku łączysz przykładowej aplikacji platformy Python Flask do bazy danych Azure PostgreSQL serwera, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="81089-164">In this step, you connect your Python Flask sample application to the Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="81089-165">Utwórz pustą bazę danych i ustaw nowego użytkownika bazy danych aplikacji</span><span class="sxs-lookup"><span data-stu-id="81089-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="81089-166">Utwórz użytkownika bazy danych z dostępem do tylko jednej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="81089-166">Create a database user with access to a single database only.</span></span> <span data-ttu-id="81089-167">Te poświadczenia będą używane w celu uniknięcia nadanie pełny dostęp do aplikacji na serwerze.</span><span class="sxs-lookup"><span data-stu-id="81089-167">You'll use these credentials to avoid giving the application full access to the server.</span></span>

<span data-ttu-id="81089-168">Połączenia z bazą danych (zostanie wyświetlony monit o hasło administratora).</span><span class="sxs-lookup"><span data-stu-id="81089-168">Connect to the database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="81089-169">Utwórz bazę danych i użytkownika z interfejsu wiersza polecenia PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="81089-169">Create the database and user from the PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```

<span data-ttu-id="81089-170">Typ *\q* aby zamknąć klienta programu PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="81089-170">Type *\q* to exit the PostgreSQL client.</span></span>

### <a name="test-the-application-locally-against-the-azure-postgresql-database"></a><span data-ttu-id="81089-171">Testowanie aplikacji lokalnie w bazie danych Azure PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="81089-171">Test the application locally against the Azure PostgreSQL database</span></span> 

<span data-ttu-id="81089-172">Po powrocie teraz do *aplikacji* folderu sklonowanego repozytorium Github, można uruchomić aplikacji platformy Python Flask, aktualizując bazy danych zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="81089-172">Going back now to the *app* folder of the cloned Github repository, you can run the Python Flask application by updating the database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="81089-173">Gdy aplikacja zostanie całkowicie załadowany, zobacz podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="81089-173">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="81089-174">Przejdź do http://127.0.0.1:5000 w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="81089-174">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="81089-175">Kliknij przycisk **zarejestrować!**</span><span class="sxs-lookup"><span data-stu-id="81089-175">Click **Register!**</span></span> <span data-ttu-id="81089-176">i Utwórz rejestracji testu.</span><span class="sxs-lookup"><span data-stu-id="81089-176">and create a test registration.</span></span> <span data-ttu-id="81089-177">Dane są teraz zapisywania do bazy danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="81089-177">You are now writing data to the database in Azure.</span></span>

![Platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-the-application-from-a-docker-container"></a><span data-ttu-id="81089-179">Uruchamianie aplikacji z kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="81089-179">Running the application from a Docker Container</span></span>

<span data-ttu-id="81089-180">Tworzenie obrazu kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="81089-180">Build the Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="81089-181">Docker wyświetla potwierdzenie, że pomyślnie utworzono kontener.</span><span class="sxs-lookup"><span data-stu-id="81089-181">Docker displays a confirmation that it successfully created the container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="81089-182">Dodaj zmiennych środowiskowych bazy danych do pliku zmiennej środowiskowej *db.env*.</span><span class="sxs-lookup"><span data-stu-id="81089-182">Add database environment variables to an environment variable file *db.env*.</span></span> <span data-ttu-id="81089-183">Aplikacja będzie łączyć się PostgreSQL produkcyjną bazę danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="81089-183">The app will connect to the PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="81089-184">Uruchamianie aplikacji z w kontenerze Docker.</span><span class="sxs-lookup"><span data-stu-id="81089-184">Run the app from within the Docker container.</span></span> <span data-ttu-id="81089-185">Polecenie Określa plik zmiennej środowiskowej i mapuje Flask domyślny port 5000 na port lokalny 5000.</span><span class="sxs-lookup"><span data-stu-id="81089-185">The following command specifies the environment variable file and maps the default Flask port 5000 to local port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="81089-186">Wynik jest podobny do wcześniej przedstawiono.</span><span class="sxs-lookup"><span data-stu-id="81089-186">The output is similar to what you saw earlier.</span></span> <span data-ttu-id="81089-187">Jednak migracji wstępnej bazy danych nie jest już musi zostać wykonana i w związku z tym jest pomijana.</span><span class="sxs-lookup"><span data-stu-id="81089-187">However, the initial database migration no longer needs to be performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="81089-188">Baza danych zawiera już utworzonego wcześniej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="81089-188">The database already contains the registration you created previously.</span></span>

![Docker na podstawie kontenera platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-the-docker-container-to-a-container-registry"></a><span data-ttu-id="81089-190">Przekaż kontenera Docker w rejestrze kontenera</span><span class="sxs-lookup"><span data-stu-id="81089-190">Upload the Docker container to a container registry</span></span>

<span data-ttu-id="81089-191">W tym kroku możesz przekazać kontenera Docker rejestru kontenera.</span><span class="sxs-lookup"><span data-stu-id="81089-191">In this step, you upload the Docker container to a container registry.</span></span> <span data-ttu-id="81089-192">Użyjesz rejestru kontenera platformy Azure, ale można również używać innych popularnych protokołów, takich jak Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="81089-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="81089-193">Tworzenie rejestru Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="81089-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="81089-194">W następujące polecenie, aby utworzyć rejestru kontenera Zastąp  *\<registry_name >* o nazwie rejestru unikatowy kontenera platformy Azure, wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="81089-194">In the following command to create a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="81089-195">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="81089-195">Output</span></span>
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

### <a name="retrieve-the-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="81089-196">Pobieranie poświadczeń rejestru dla wypychanie i ściąganie obrazy usługi Docker</span><span class="sxs-lookup"><span data-stu-id="81089-196">Retrieve the registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="81089-197">Aby pokazać rejestru poświadczeń, Włącz tryb administratora najpierw.</span><span class="sxs-lookup"><span data-stu-id="81089-197">To show registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="81089-198">Możesz sprawdzić dwa hasła.</span><span class="sxs-lookup"><span data-stu-id="81089-198">You see two passwords.</span></span> <span data-ttu-id="81089-199">Zanotuj nazwę użytkownika i hasło pierwszy.</span><span class="sxs-lookup"><span data-stu-id="81089-199">Make note of the user name and the first password.</span></span>

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

### <a name="upload-your-docker-container-to-azure-container-registry"></a><span data-ttu-id="81089-200">Przekazywanie z kontenera Docker w rejestrze kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="81089-200">Upload your Docker container to Azure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-the-docker-python-flask-application-to-azure"></a><span data-ttu-id="81089-201">Wdrażanie aplikacji platformy Python Flask Docker na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="81089-201">Deploy the Docker Python Flask application to Azure</span></span>

<span data-ttu-id="81089-202">W tym kroku, w przypadku wdrażania rozwiązania Docker na podstawie kontenera platformy Python Flask aplikacji do usługi Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="81089-202">In this step, you deploy your Docker container-based Python Flask application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="81089-203">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="81089-203">Create an App Service plan</span></span>

<span data-ttu-id="81089-204">Utwórz plan usługi App Service za pomocą polecenia [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="81089-204">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="81089-205">Poniższy przykład tworzy plan usługi aplikacji opartych na systemie Linux o nazwie *myAppServicePlan* przy użyciu cennik S1 warstwy:</span><span class="sxs-lookup"><span data-stu-id="81089-205">The following example creates a Linux-based App Service plan named *myAppServicePlan* using the S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="81089-206">Po utworzeniu planu usługi aplikacji Azure CLI pokazuje informacje podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="81089-206">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="81089-207">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="81089-207">Create a web app</span></span>

<span data-ttu-id="81089-208">Tworzenie aplikacji sieci web w *myAppServicePlan* planu usługi aplikacji z [tworzenie aplikacji sieci Web az](/cli/azure/webapp#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="81089-208">Create a web app in the *myAppServicePlan* App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="81089-209">Aplikacja sieci web udostępnia hostingu miejsca, aby wdrożyć kod i zawiera adres URL do wyświetlania wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81089-209">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="81089-210">Służy do tworzenia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="81089-210">Use  to create the web app.</span></span> 

<span data-ttu-id="81089-211">W poniższym poleceniu zastąp  *\<nazwa_aplikacji >* symbol zastępczy unikatowej nazwy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81089-211">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="81089-212">Ta nazwa jest częścią domyślny adres URL aplikacji sieci web, więc nazwa musi być unikatowy w obrębie wszystkich aplikacji w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="81089-212">This name is part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="81089-213">Po utworzeniu aplikacji internetowej w interfejsie wiersza polecenia platformy Azure zostaną wyświetlone informacje podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="81089-213">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-the-database-environment-variables"></a><span data-ttu-id="81089-214">Skonfiguruj zmienne środowiskowe bazy danych</span><span class="sxs-lookup"><span data-stu-id="81089-214">Configure the database environment variables</span></span>

<span data-ttu-id="81089-215">Wcześniej w samouczku zdefiniowano zmiennych środowiskowych w celu połączenia z bazą danych PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="81089-215">Earlier in the tutorial, you defined environment variables to connect to your PostgreSQL database.</span></span>

<span data-ttu-id="81089-216">W usłudze App Service można ustawić zmienne środowiskowe jako _ustawień aplikacji_ za pomocą [az aplikacji sieci Web config appsettings zestaw](/cli/azure/webapp/config#set) polecenia.</span><span class="sxs-lookup"><span data-stu-id="81089-216">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="81089-217">W poniższym przykładzie szczegóły połączenia bazy danych jako ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81089-217">The following example specifies the database connection details as app settings.</span></span> <span data-ttu-id="81089-218">Ponadto użyto *portu* zmienną do mapy PORT 5000 z Twojej kontenera Docker na odbieranie ruchu HTTP na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="81089-218">It also uses the *PORT* variable to map PORT 5000 from your Docker Container to receive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="81089-219">Konfigurowanie wdrożenia kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="81089-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="81089-220">Usługi aplikacji może automatycznie Pobierz i uruchom kontener Docker.</span><span class="sxs-lookup"><span data-stu-id="81089-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="81089-221">Zawsze, gdy aktualizacji kontenera Docker lub zmienić ustawienia, uruchom ponownie aplikację.</span><span class="sxs-lookup"><span data-stu-id="81089-221">Whenever you update the Docker container or change the settings, restart the app.</span></span> <span data-ttu-id="81089-222">Ponowne uruchomienie gwarantuje, że wszystkie ustawienia są stosowane i kontenerze najnowsze są pobierane z rejestru.</span><span class="sxs-lookup"><span data-stu-id="81089-222">Restarting ensures that all settings are applied and the latest container is pulled from the registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="81089-223">Przejdź do aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="81089-223">Browse to the Azure web app</span></span> 

<span data-ttu-id="81089-224">Przejdź do wdrożonej aplikacji sieci web za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="81089-224">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="81089-225">Aplikacja sieci web obsługuje żądanie dłużej załadować, ponieważ kontener ma zostać pobrana i uruchomić po zmianie konfiguracji kontenera.</span><span class="sxs-lookup"><span data-stu-id="81089-225">The web app takes longer to load because the container has to be downloaded and started after the container configuration is changed.</span></span>

<span data-ttu-id="81089-226">Widać wcześniej zarejestrowanego gości, które zostały zapisane w bazie danych Azure środowiska produkcyjnego w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="81089-226">You see previously registered guests that were saved to the Azure production database in the previous step.</span></span>

![Docker na podstawie kontenera platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="81089-228">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="81089-228">**Congratulations!**</span></span> <span data-ttu-id="81089-229">Używasz Docker aplikacji platformy Python Flask kontenera w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="81089-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="81089-230">Aktualizacja modelu danych i utwórz je ponownie</span><span class="sxs-lookup"><span data-stu-id="81089-230">Update data model and redeploy</span></span>

<span data-ttu-id="81089-231">W tym kroku dodaniu liczba uczestników do każdej rejestracji zdarzeń, aktualizując modelu gościa.</span><span class="sxs-lookup"><span data-stu-id="81089-231">In this step, you add the number of attendees to each event registration by updating the Guest model.</span></span>

<span data-ttu-id="81089-232">Zapoznaj się z *migracji 0,2* wersji przy użyciu następującego polecenia git:</span><span class="sxs-lookup"><span data-stu-id="81089-232">Check out the *0.2-migration* release with the following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="81089-233">Tej wersji zostały już wprowadzone niezbędne widoki, kontrolery i modelu.</span><span class="sxs-lookup"><span data-stu-id="81089-233">This release already made the necessary changes to views, controllers, and model.</span></span> <span data-ttu-id="81089-234">Obejmuje też migracja bazy danych, wygenerowane za pomocą *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="81089-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="81089-235">Można wyświetlić wszystkie zmiany dokonane za pomocą następujących poleceń git:</span><span class="sxs-lookup"><span data-stu-id="81089-235">You can see all changes made via the following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="81089-236">Przetestuj zmiany lokalnie</span><span class="sxs-lookup"><span data-stu-id="81089-236">Test your changes locally</span></span>

<span data-ttu-id="81089-237">Uruchom następujące polecenia, aby przetestować zmiany lokalnie, uruchamiając serwera platformy flask.</span><span class="sxs-lookup"><span data-stu-id="81089-237">Run the following commands to test your changes locally by running the flask server.</span></span>

<span data-ttu-id="81089-238">Mac / Linux:</span><span class="sxs-lookup"><span data-stu-id="81089-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="81089-239">Przejdź do http://127.0.0.1:5000 w przeglądarce, aby zobaczyć zmiany.</span><span class="sxs-lookup"><span data-stu-id="81089-239">Navigate to http://127.0.0.1:5000 in your browser to view the changes.</span></span> <span data-ttu-id="81089-240">Utwórz rejestracji testu.</span><span class="sxs-lookup"><span data-stu-id="81089-240">Create a test registration.</span></span>

![Docker na podstawie kontenera platformy Python Flask aplikacji uruchomionej na komputerze lokalnym](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-to-azure"></a><span data-ttu-id="81089-242">Publikowanie zmian na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="81089-242">Publish changes to Azure</span></span>

<span data-ttu-id="81089-243">Utwórz nowy obraz docker wypchnąć go do rejestru kontenera i uruchom ponownie aplikację.</span><span class="sxs-lookup"><span data-stu-id="81089-243">Build the new docker image, push it to the container registry, and restart the app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="81089-244">Przejdź do aplikacji sieci web platformy Azure i ponownie wypróbowanie nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="81089-244">Navigate to your Azure web app and try out the new functionality again.</span></span> <span data-ttu-id="81089-245">Utwórz inną rejestracja zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="81089-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Docker Python Flask aplikacji w usłudze aplikacji Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="81089-247">Zarządzanie aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="81089-247">Manage your Azure web app</span></span>

<span data-ttu-id="81089-248">Przejdź do [portalu Azure](https://portal.azure.com) zobaczyć aplikacji sieci web został utworzony.</span><span class="sxs-lookup"><span data-stu-id="81089-248">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="81089-249">W lewym menu kliknij pozycję **App Services**, a następnie kliknij nazwę swojej aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="81089-249">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Nawigacja w portalu do aplikacji sieci Web platformy Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="81089-251">Domyślnie portalu zawiera aplikację sieci web **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="81089-251">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="81089-252">Ta strona udostępnia widok sposobu działania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81089-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="81089-253">Tutaj możesz również wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="81089-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="81089-254">W lewej części strony kartach stron innej konfiguracji może być otwarty.</span><span class="sxs-lookup"><span data-stu-id="81089-254">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Strona usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="81089-256">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="81089-256">Next steps</span></span>

<span data-ttu-id="81089-257">Przejdź do następnego samouczek, aby dowiedzieć się, jak zamapować niestandardową nazwę DNS na aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="81089-257">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="81089-258">Map an existing custom DNS name to Azure Web Apps (Mapowanie istniejącej niestandardowej nazwy DNS na aplikacje internetowe platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="81089-258">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
