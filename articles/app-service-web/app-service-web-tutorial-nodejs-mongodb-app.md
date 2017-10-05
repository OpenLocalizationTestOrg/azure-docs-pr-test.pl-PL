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
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="4180e-103">Tworzenie aplikacji sieci web Node.js i bazy danych MongoDB na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="4180e-104">Aplikacje sieci Web platformy Azure oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web.</span><span class="sxs-lookup"><span data-stu-id="4180e-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="4180e-105">W tym samouczku przedstawiono sposób tworzenia aplikacji sieci web Node.js na platformie Azure i podłącz go do bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4180e-105">This tutorial shows how to create a Node.js web app in Azure and connect it to a MongoDB database.</span></span> <span data-ttu-id="4180e-106">Gdy wszystko będzie gotowe, będziesz mieć uruchomionej aplikacji średniej (bazy danych MongoDB, Express AngularJS i Node.js) w [usłudze Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4180e-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="4180e-107">Dla uproszczenia Przykładowa aplikacja korzysta z [platforma sieci web MEAN.js](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="4180e-107">For simplicity, the sample application uses the [MEAN.js web framework](http://meanjs.org/).</span></span>

![Aplikacja MEAN.js uruchomiona w usłudze Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="4180e-109">Zawartość:</span><span class="sxs-lookup"><span data-stu-id="4180e-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4180e-110">Tworzenie bazy danych MongoDB na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="4180e-111">Łączenie aplikacji Node.js z bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="4180e-111">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="4180e-112">Wdrażanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-112">Deploy the app to Azure</span></span>
> * <span data-ttu-id="4180e-113">Aktualizacja modelu danych i ponownie wdrożyć aplikację</span><span class="sxs-lookup"><span data-stu-id="4180e-113">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="4180e-114">Strumieniowe przesyłanie dzienników diagnostycznych z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="4180e-115">Zarządzanie aplikacją w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-115">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4180e-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4180e-116">Prerequisites</span></span>

<span data-ttu-id="4180e-117">W celu ukończenia tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="4180e-117">To complete this tutorial:</span></span>

1. [<span data-ttu-id="4180e-118">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="4180e-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="4180e-119">Zainstaluj środowisko Node.js i menedżer NPM</span><span class="sxs-lookup"><span data-stu-id="4180e-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="4180e-120">[Zainstaluj Gulp.js](http://gulpjs.com/) (wymagany przez [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span><span class="sxs-lookup"><span data-stu-id="4180e-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="4180e-121">Zainstaluj i uruchom MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="4180e-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4180e-122">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4180e-122">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4180e-123">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="4180e-123">Run `az --version` to find the version.</span></span> <span data-ttu-id="4180e-124">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4180e-124">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="4180e-125">Test lokalnej bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="4180e-125">Test local MongoDB</span></span>

<span data-ttu-id="4180e-126">Otwórz okno terminala i `cd` do `bin` katalogu instalacji bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4180e-126">Open the terminal window and `cd` to the `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="4180e-127">To okno terminalu służy do uruchamiania wszystkich poleceń w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="4180e-127">You can use this terminal window to run all the commands in this tutorial.</span></span>

<span data-ttu-id="4180e-128">Uruchom `mongo` w terminalu, aby połączyć się z lokalnym serwerem bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4180e-128">Run `mongo` in the terminal to connect to your local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="4180e-129">Jeśli połączenie zostanie nawiązane, bazy danych MongoDB już jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="4180e-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="4180e-130">Jeśli nie, upewnij się, że lokalnej bazy danych MongoDB została uruchomiona, wykonując kroki opisane w temacie [zainstalować bazy danych MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="4180e-130">If not, make sure that your local MongoDB database is started by following the steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="4180e-131">Często jest zainstalowana baza danych MongoDB, ale nadal należy ją uruchomić, uruchamiając `mongod`.</span><span class="sxs-lookup"><span data-stu-id="4180e-131">Often, MongoDB is installed, but you still need to start it by running `mongod`.</span></span> 

<span data-ttu-id="4180e-132">Po zakończeniu testowania bazy danych MongoDB, wpisz `Ctrl+C` w terminalu.</span><span class="sxs-lookup"><span data-stu-id="4180e-132">When you're done testing your MongoDB database, type `Ctrl+C` in the terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="4180e-133">Tworzenie lokalnych aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="4180e-133">Create local Node.js app</span></span>

<span data-ttu-id="4180e-134">Ten krok służy do konfigurowania lokalnego projektu Node.js.</span><span class="sxs-lookup"><span data-stu-id="4180e-134">In this step, you set up the local Node.js project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="4180e-135">Klonowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="4180e-135">Clone the sample application</span></span>

<span data-ttu-id="4180e-136">W oknie terminalu `cd` do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="4180e-136">In the terminal window, `cd` to a working directory.</span></span>  

<span data-ttu-id="4180e-137">Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="4180e-137">Run the following command to clone the sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="4180e-138">To repozytorium przykładowej zawiera kopię [repozytorium MEAN.js](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="4180e-138">This sample repository contains a copy of the [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="4180e-139">Są modyfikowane w celu uruchomienia w usłudze aplikacji (Aby uzyskać więcej informacji, zobacz repozytorium MEAN.js [Plik README](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="4180e-139">It is modified to run on App Service (for more information, see the MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-the-application"></a><span data-ttu-id="4180e-140">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="4180e-140">Run the application</span></span>

<span data-ttu-id="4180e-141">Uruchom następujące polecenia, aby zainstalować wymagane pakiety i uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="4180e-141">Run the following commands to install the required packages and start the application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="4180e-142">Gdy aplikacja zostanie całkowicie załadowany, zobacz podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="4180e-142">When the app is fully loaded, you see something similar to the following message:</span></span>

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

<span data-ttu-id="4180e-143">Przejdź do http://localhost: 3000 w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="4180e-143">Navigate to http://localhost:3000 in a browser.</span></span> <span data-ttu-id="4180e-144">Kliknij przycisk **Utwórz konto** w menu u góry i tworzenie użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="4180e-144">Click **Sign Up** in the top menu and create a test user.</span></span> 

<span data-ttu-id="4180e-145">Przykładowa aplikacja MEAN.js przechowuje dane użytkowników w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="4180e-145">The MEAN.js sample application stores user data in the database.</span></span> <span data-ttu-id="4180e-146">W przypadku pomyślnego tworzenia użytkownika i logowanie, aplikacja jest zapisywania danych do lokalnej bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4180e-146">If you are successful at creating a user and signing in, then your app is writing data to the local MongoDB database.</span></span>

![Pomyślne połączenie MEAN.js z MongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="4180e-148">Wybierz **Admin > Zarządzaj artykuły** można dodać niektórych artykułach.</span><span class="sxs-lookup"><span data-stu-id="4180e-148">Select **Admin > Manage Articles** to add some articles.</span></span>

<span data-ttu-id="4180e-149">Aby zatrzymać Node.js w dowolnym momencie, naciśnij klawisz `Ctrl+C` w terminalu.</span><span class="sxs-lookup"><span data-stu-id="4180e-149">To stop Node.js at any time, press `Ctrl+C` in the terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="4180e-150">Utwórz produkcyjnej bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="4180e-150">Create production MongoDB</span></span>

<span data-ttu-id="4180e-151">W tym kroku utworzysz bazę danych MongoDB na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4180e-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="4180e-152">Po wdrożeniu aplikacji na platformie Azure wykorzystuje tę bazę danych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="4180e-152">When your app is deployed to Azure, it uses this cloud database.</span></span>

<span data-ttu-id="4180e-153">Bazy danych mongodb, w tym samouczku używana [bazy danych Azure rozwiązania Cosmos](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="4180e-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="4180e-154">Rozwiązania cosmos bazy danych obsługuje połączenia klienta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4180e-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="4180e-155">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4180e-155">Log in to Azure</span></span>

<span data-ttu-id="4180e-156">Użyj interfejsu wiersza polecenia platformy Azure w wersji 2.0, aby utworzyć zasoby potrzebne do hostowania Twojej aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4180e-156">You'll use the Azure CLI 2.0 to create the resources needed to host your app in Azure.</span></span> <span data-ttu-id="4180e-157">Zaloguj się do subskrypcji platformy Azure za pomocą polecenia [az login](/cli/azure/#login) i postępuj zgodnie z instrukcjami wyświetlanymi na ekranie.</span><span class="sxs-lookup"><span data-stu-id="4180e-157">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="4180e-158">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="4180e-158">Create a resource group</span></span>

<span data-ttu-id="4180e-159">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4180e-159">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="4180e-160">Poniższy przykład obejmuje tworzenie grupy zasobów w regionie Europa Zachodnia.</span><span class="sxs-lookup"><span data-stu-id="4180e-160">The following example creates a resource group in the West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="4180e-161">Użyj [appservice az listy lokalizacje](/cli/azure/appservice#list-locations) polecenia wiersza polecenia platformy Azure do listy dostępnych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="4180e-161">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="4180e-162">Tworzenie konta bazy danych rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="4180e-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="4180e-163">Tworzenie konta bazy danych rozwiązania Cosmos z [az cosmosdb utworzyć](/cli/azure/cosmosdb#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="4180e-163">Create a Cosmos DB account with the [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="4180e-164">W poniższym poleceniu zastąp unikatową nazwę bazy danych rozwiązania Cosmos  *\<cosmosdb_name >* symbolu zastępczego.</span><span class="sxs-lookup"><span data-stu-id="4180e-164">In the following command, substitute a unique Cosmos DB name for the *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="4180e-165">Ta nazwa jest używana jako część rozwiązania Cosmos DB punkt końcowy, `https://<cosmosdb_name>.documents.azure.com/`, więc nazwa musi być unikatowa na wszystkich kontach DB rozwiązania Cosmos w programie Azure.</span><span class="sxs-lookup"><span data-stu-id="4180e-165">This name is used as the part of the Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so the name needs to be unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="4180e-166">Nazwa musi zawierać tylko małe litery, cyfry i znaki łącznika (-) i musi mieć długość od 3 do 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="4180e-166">The name must contain only lowercase letters, numbers, and the hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="4180e-167">*--Rodzaju bazy danych MongoDB* parametru zapewnia połączeń klienckich bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4180e-167">The *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="4180e-168">Po utworzeniu konta DB rozwiązania Cosmos interfejsu wiersza polecenia Azure zawiera informacje podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="4180e-168">When the Cosmos DB account is created, the Azure CLI shows information similar to the following example:</span></span>

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

## <a name="connect-app-to-production-mongodb"></a><span data-ttu-id="4180e-169">Łączenie aplikacji produkcyjnej bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="4180e-169">Connect app to production MongoDB</span></span>

<span data-ttu-id="4180e-170">W tym kroku połączenie aplikacji przykładowej MEAN.js do bazy danych DB rozwiązania Cosmos utworzony, przy użyciu parametrów połączenia bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4180e-170">In this step, you connect your MEAN.js sample application to the Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-the-database-key"></a><span data-ttu-id="4180e-171">Pobierz klucz bazy danych</span><span class="sxs-lookup"><span data-stu-id="4180e-171">Retrieve the database key</span></span>

<span data-ttu-id="4180e-172">Do połączenia z bazą danych rozwiązania Cosmos bazy danych, należy klucza bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4180e-172">To connect to the Cosmos DB database, you need the database key.</span></span> <span data-ttu-id="4180e-173">Aby pobrać klucz podstawowy, użyj polecenia [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys).</span><span class="sxs-lookup"><span data-stu-id="4180e-173">Use the [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command to retrieve the primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="4180e-174">Interfejsu wiersza polecenia Azure zawiera informacje podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="4180e-174">The Azure CLI shows information similar to the following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Skopiuj wartość `primaryMasterKey`. <span data-ttu-id="4180e-176">Ta informacja będzie potrzebna w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="4180e-176">You need this information in the next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-the-connection-string-in-your-nodejs-application"></a><span data-ttu-id="4180e-177">Konfigurowanie parametrów połączenia w aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="4180e-177">Configure the connection string in your Node.js application</span></span>

<span data-ttu-id="4180e-178">Otwórz w repozytorium MEAN.js _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="4180e-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="4180e-179">W `db` obiektów, zaktualizuj wartość `uri`:</span><span class="sxs-lookup"><span data-stu-id="4180e-179">In the `db` object, update the value of `uri`:</span></span>

* <span data-ttu-id="4180e-180">Zastąp dwa  *\<cosmosdb_name >* symbole zastępcze nazwą bazy danych DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="4180e-180">Replace the two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="4180e-181">Zastąp  *\<primary_master_key >* symbol zastępczy klucz został skopiowany w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="4180e-181">Replace the *\<primary_master_key>* placeholder with the key you copied in the previous step.</span></span>

<span data-ttu-id="4180e-182">Poniższy kod przedstawia `db` obiektu:</span><span class="sxs-lookup"><span data-stu-id="4180e-182">The following code shows the `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="4180e-183">`ssl=true` Opcja jest wymagana, ponieważ [DB rozwiązania Cosmos wymaga protokołu SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="4180e-183">The `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="4180e-184">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="4180e-184">Save your changes.</span></span>

### <a name="test-the-application-in-production-mode"></a><span data-ttu-id="4180e-185">Testowanie aplikacji w trybie produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="4180e-185">Test the application in production mode</span></span> 

<span data-ttu-id="4180e-186">Uruchom następujące polecenie w celu zminimalizowania i pakietów skryptów w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="4180e-186">Run the following command to minify and bundle scripts for the production environment.</span></span> <span data-ttu-id="4180e-187">Ten proces generuje pliki wymagane przez środowisko produkcyjne.</span><span class="sxs-lookup"><span data-stu-id="4180e-187">This process generates the files needed by the production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="4180e-188">Uruchom następujące polecenie, aby użyć skonfigurowane w ciągu połączenia _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="4180e-188">Run the following command to use the connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="4180e-189">`NODE_ENV=production`Ustawia zmienną środowiskową, informujący o Node.js do uruchamiania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="4180e-189">`NODE_ENV=production` sets the environment variable that tells Node.js to run in the production environment.</span></span>  <span data-ttu-id="4180e-190">`node server.js`Uruchamia serwer Node.js z `server.js` w katalogu głównym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="4180e-190">`node server.js` starts the Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="4180e-191">Jest to, jak załadowano aplikację Node.js na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4180e-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="4180e-192">Podczas ładowania aplikacji, należy sprawdzić, czy działa w środowisku produkcyjnym:</span><span class="sxs-lookup"><span data-stu-id="4180e-192">When the app is loaded, check to make sure that it's running in the production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="4180e-193">Przejdź do http://localhost:8443 w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="4180e-193">Navigate to http://localhost:8443 in a browser.</span></span> <span data-ttu-id="4180e-194">Kliknij przycisk **Utwórz konto** w menu u góry i tworzenie użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="4180e-194">Click **Sign Up** in the top menu and create a test user.</span></span> <span data-ttu-id="4180e-195">W przypadku pomyślnego tworzenia użytkownika i zaloguj się, aplikacja jest zapisywania danych do bazy danych DB rozwiązania Cosmos na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4180e-195">If you are successful creating a user and signing in, then your app is writing data to the Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="4180e-196">W terminalu, Zatrzymaj Node.js, wpisując `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="4180e-196">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-to-azure"></a><span data-ttu-id="4180e-197">Wdrażanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-197">Deploy app to Azure</span></span>

<span data-ttu-id="4180e-198">W tym kroku możesz wdrożyć aplikację Node.js połączenia bazy danych MongoDB w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4180e-198">In this step, you deploy your MongoDB-connected Node.js application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="4180e-199">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="4180e-199">Create an App Service plan</span></span>

<span data-ttu-id="4180e-200">Utwórz plan usługi App Service za pomocą polecenia [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="4180e-200">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="4180e-201">Poniższy przykład tworzy plan usługi aplikacji o nazwie _myAppServicePlan_ przy użyciu **wolne** warstwa cenowa:</span><span class="sxs-lookup"><span data-stu-id="4180e-201">The following example creates an App Service plan named _myAppServicePlan_ using the **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="4180e-202">Po utworzeniu planu usługi aplikacji Azure CLI pokazuje informacje podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="4180e-202">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="4180e-203">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="4180e-203">Create a web app</span></span>

<span data-ttu-id="4180e-204">Tworzenie aplikacji sieci web w `myAppServicePlan` planu usługi aplikacji z [tworzenie aplikacji sieci Web az](/cli/azure/webapp#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="4180e-204">Create a web app in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="4180e-205">Aplikacja sieci web udostępnia hostingu miejsca, aby wdrożyć kod i zawiera adres URL do wyświetlania wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4180e-205">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="4180e-206">Służy do tworzenia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4180e-206">Use  to create the web app.</span></span> 

<span data-ttu-id="4180e-207">W poniższym poleceniu zastąp  *\<nazwa_aplikacji >* symbol zastępczy unikatowej nazwy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4180e-207">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="4180e-208">Ta nazwa jest używana jako część domyślnego adresu URL dla aplikacji sieci web, więc nazwa musi być unikatowy w obrębie wszystkich aplikacji w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4180e-208">This name is used as the part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="4180e-209">Po utworzeniu aplikacji internetowej w interfejsie wiersza polecenia platformy Azure zostaną wyświetlone informacje podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="4180e-209">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-an-environment-variable"></a><span data-ttu-id="4180e-210">Skonfigurować zmienną środowiskową</span><span class="sxs-lookup"><span data-stu-id="4180e-210">Configure an environment variable</span></span>

<span data-ttu-id="4180e-211">Wcześniej w samouczku, zostanie zapisane na stałe połączenie z bazą danych ciąg w _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="4180e-211">Earlier in the tutorial, you hardcoded the database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="4180e-212">Zgodnie ze względów bezpieczeństwa chcesz zachować poufne dane poza repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="4180e-212">In keeping with security best practice, you want to keep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="4180e-213">Dla aplikacji działających na platformie Azure będzie zamiast tego użyć zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="4180e-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="4180e-214">W usłudze App Service można ustawić zmienne środowiskowe jako _ustawień aplikacji_ za pomocą [zaktualizować appsettings konfiguracji aplikacji sieci Web az](/cli/azure/webapp/config/appsettings#update) polecenia.</span><span class="sxs-lookup"><span data-stu-id="4180e-214">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="4180e-215">Poniższy przykład konfiguruje `MONGODB_URI` ustawienie aplikacji w aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4180e-215">The following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="4180e-216">Zastąp  *\<nazwa_aplikacji >*,  *\<cosmosdb_name >*, i  *\<primary_master_key >* symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="4180e-216">Replace the *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="4180e-217">W kodzie Node.js dostępu to ustawienie aplikacji o `process.env.MONGODB_URI`, tak jak będzie dostęp do wszelkich zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="4180e-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="4180e-218">Teraz, Cofnij zmiany _config/env/production.js_ przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4180e-218">Now, undo your changes to _config/env/production.js_ with the following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="4180e-219">Otwórz _config/env/production.js_ ponownie.</span><span class="sxs-lookup"><span data-stu-id="4180e-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="4180e-220">Należy pamiętać, że domyślna aplikacja MEAN.js jest już skonfigurowana do używania `MONGODB_URI` zmienną środowiskową, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="4180e-220">Note that the default MEAN.js app is already configured to use the `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="4180e-221">Konfigurowanie lokalnego wdrożenia narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="4180e-221">Configure local git deployment</span></span> 

<span data-ttu-id="4180e-222">Użyj [ustawiono użytkownika wdrożenia aplikacji sieci Web az](/cli/azure/webapp/deployment/user#set) polecenie, aby utworzyć poświadczenia dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4180e-222">Use the [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command to create credentials for deployment.</span></span>

<span data-ttu-id="4180e-223">Można wdrożyć aplikację w usłudze Azure App Service na różne sposoby, w tym FTP, Git lokalnego GitHub, Visual Studio Team Services i BitBucket.</span><span class="sxs-lookup"><span data-stu-id="4180e-223">You can deploy your application to Azure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="4180e-224">FTP i lokalne Git jest konieczne użytkownika wdrożenia skonfigurowane na serwerze do uwierzytelniania wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4180e-224">For FTP and local Git, it is necessary to have a deployment user configured on the server to authenticate your deployment.</span></span> <span data-ttu-id="4180e-225">Ten użytkownik wdrożenia poziomie konta i różni się od konta subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4180e-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="4180e-226">Wystarczy raz skonfigurować ten użytkownik wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4180e-226">You only need to configure this deployment user once.</span></span>

<span data-ttu-id="4180e-227">W poniższym poleceniu zastąp ciągi *\<user-name>* i *\<password>* nową nazwą użytkownika i hasłem.</span><span class="sxs-lookup"><span data-stu-id="4180e-227">In the following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="4180e-228">Nazwa użytkownika musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="4180e-228">The user name must be unique.</span></span> <span data-ttu-id="4180e-229">Hasło musi mieć długość co najmniej ośmiu znaków i zawierać dwa z następujących trzech elementów: litery, cyfry, symbole.</span><span class="sxs-lookup"><span data-stu-id="4180e-229">The password must be at least eight characters long, with two of the following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="4180e-230">Jeśli wystąpił błąd ` 'Conflict'. Details: 409`, zmień nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4180e-230">If you get a ` 'Conflict'. Details: 409` error, change the username.</span></span> <span data-ttu-id="4180e-231">Jeśli wystąpił błąd ` 'Bad Request'. Details: 400`, użyj silniejszego hasła.</span><span class="sxs-lookup"><span data-stu-id="4180e-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="4180e-232">Zapisz nazwę użytkownika i hasło do użycia w kolejnych krokach podczas wdrażania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4180e-232">Record the user name and password for use in later steps when you deploy the app.</span></span>

<span data-ttu-id="4180e-233">Użyj [źródło wdrożenia az aplikacji sieci Web — config lokalnych git](/cli/azure/webapp/deployment/source#config-local-git) polecenie, aby skonfigurować dostęp lokalny Git do aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4180e-233">Use the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command to configure local Git access to the Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="4180e-234">Po skonfigurowaniu użytkownika wdrażania interfejsu wiersza polecenia Azure zawiera adres URL wdrożenia dla aplikacji sieci web platformy Azure w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="4180e-234">When the deployment user is configured, the Azure CLI shows the deployment URL for your Azure web app in the following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="4180e-235">Skopiuj dane wyjściowe z terminala, ponieważ będzie on używany w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="4180e-235">Copy the output from the terminal, as it will be used in the next step.</span></span> 

### <a name="push-to-azure-from-git"></a><span data-ttu-id="4180e-236">Wypychanie z narzędzia Git na platformę Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-236">Push to Azure from Git</span></span>

<span data-ttu-id="4180e-237">Dodaj zdalną platformę Azure do lokalnego repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="4180e-237">Add an Azure remote to your local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="4180e-238">Wypychanie do platformy Azure zdalnego wdrażania aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="4180e-238">Push to the Azure remote to deploy your Node.js application.</span></span> <span data-ttu-id="4180e-239">Zostanie wyświetlony monit o podanie hasła określonego wcześniej w ramach tworzenia użytkownika wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4180e-239">You will be prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="4180e-240">Podczas wdrażania usługi Azure App Service komunikuje się postęp za pomocą narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="4180e-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

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

<span data-ttu-id="4180e-241">Można zauważyć, że proces wdrażania uruchamia [system Gulp](http://gulpjs.com/) po `npm install`.</span><span class="sxs-lookup"><span data-stu-id="4180e-241">You may notice that the deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="4180e-242">Usługi aplikacji nie działa Gulp lub Grunt zadań podczas wdrażania, dzięki czemu to repozytorium przykładowej mają dwa dodatkowe pliki w katalogu głównym ją włączyć:</span><span class="sxs-lookup"><span data-stu-id="4180e-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory to enable it:</span></span> 

- <span data-ttu-id="4180e-243">_.Deployment_ — ten plik zawiera usługę aplikacji w celu uruchomienia `bash deploy.sh` jako niestandardowe wdrożenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="4180e-243">_.deployment_ - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
- <span data-ttu-id="4180e-244">_Deploy.sh_ -niestandardowe wdrożenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="4180e-244">_deploy.sh_ - The custom deployment script.</span></span> <span data-ttu-id="4180e-245">Jeśli przejrzenie pliku, zobaczysz, że działa `gulp prod` po `npm install` i `bower install`.</span><span class="sxs-lookup"><span data-stu-id="4180e-245">If you review the file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="4180e-246">Ta metoda służy do dodawania każdy krok do wdrożenia na podstawie Git.</span><span class="sxs-lookup"><span data-stu-id="4180e-246">You can use this approach to add any step to your Git-based deployment.</span></span> <span data-ttu-id="4180e-247">W przypadku ponownego uruchomienia aplikacji sieci web platformy Azure w dowolnym momencie, usługi aplikacji nie ponownie te zadania automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="4180e-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="4180e-248">Przejdź do aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-248">Browse to the Azure web app</span></span> 

<span data-ttu-id="4180e-249">Przejdź do wdrożonej aplikacji sieci web za pomocą przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="4180e-249">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="4180e-250">Kliknij przycisk **Utwórz konto** w menu u góry i utworzyć fikcyjny użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4180e-250">Click **Sign Up** in the top menu and create a dummy user.</span></span> 

<span data-ttu-id="4180e-251">Jeśli aplikacja automatycznie loguje się do utworzonego użytkownika powiodą się, aplikacja MEAN.js na platformie Azure ma łączność z bazą danych MongoDB (DB rozwiązania Cosmos).</span><span class="sxs-lookup"><span data-stu-id="4180e-251">If you are successful and the app automatically signs in to the created user, then your MEAN.js app in Azure has connectivity to the MongoDB (Cosmos DB) database.</span></span> 

![Aplikacja MEAN.js uruchomiona w usłudze Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="4180e-253">Wybierz **Admin > Zarządzaj artykuły** można dodać niektórych artykułach.</span><span class="sxs-lookup"><span data-stu-id="4180e-253">Select **Admin > Manage Articles** to add some articles.</span></span> 

<span data-ttu-id="4180e-254">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="4180e-254">**Congratulations!**</span></span> <span data-ttu-id="4180e-255">Używasz aplikacji Node.js opartych na danych w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4180e-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="4180e-256">Aktualizacja modelu danych i utwórz je ponownie</span><span class="sxs-lookup"><span data-stu-id="4180e-256">Update data model and redeploy</span></span>

<span data-ttu-id="4180e-257">W tym kroku, możesz zmienić `article` danych model i opublikuj zmiany na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4180e-257">In this step, you change the `article` data model and publish your change to Azure.</span></span>

### <a name="update-the-data-model"></a><span data-ttu-id="4180e-258">Aktualizacja modelu danych</span><span class="sxs-lookup"><span data-stu-id="4180e-258">Update the data model</span></span>

<span data-ttu-id="4180e-259">Otwórz _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="4180e-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="4180e-260">W `ArticleSchema`, Dodaj `String` typu o nazwie `comment`.</span><span class="sxs-lookup"><span data-stu-id="4180e-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="4180e-261">Gdy wszystko będzie gotowe, schemat kod powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="4180e-261">When you're done, your schema code should look like this:</span></span>

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

### <a name="update-the-articles-code"></a><span data-ttu-id="4180e-262">Zaktualizuj kod artykułów</span><span class="sxs-lookup"><span data-stu-id="4180e-262">Update the articles code</span></span>

<span data-ttu-id="4180e-263">Zaktualizuj reszty Twojej `articles` kod, aby używał `comment`.</span><span class="sxs-lookup"><span data-stu-id="4180e-263">Update the rest of your `articles` code to use `comment`.</span></span>

<span data-ttu-id="4180e-264">Jest pięć plików, należy zmodyfikować: kontroler serwera i klienta cztery widoki.</span><span class="sxs-lookup"><span data-stu-id="4180e-264">There are five files you need to modify: the server controller and the four client views.</span></span> 

<span data-ttu-id="4180e-265">Otwórz _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="4180e-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="4180e-266">W `update` funkcji, należy dodać przydziału `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="4180e-266">In the `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="4180e-267">Poniższy kod przedstawia ukończonej `update` funkcji:</span><span class="sxs-lookup"><span data-stu-id="4180e-267">The following code shows the completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="4180e-268">Otwórz _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="4180e-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="4180e-269">Powyżej zamknięcia `</section>` tagów, Dodaj następujący wiersz do wyświetlenia `comment` wraz z resztą dane artykułu:</span><span class="sxs-lookup"><span data-stu-id="4180e-269">Just above the closing `</section>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="4180e-270">Otwórz _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="4180e-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="4180e-271">Powyżej zamknięcia `</a>` tagów, Dodaj następujący wiersz do wyświetlenia `comment` wraz z resztą dane artykułu:</span><span class="sxs-lookup"><span data-stu-id="4180e-271">Just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="4180e-272">Otwórz _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="4180e-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="4180e-273">Wewnątrz `<div class="list-group">` element i powyżej zamknięcia `</a>` tagów, Dodaj następujący wiersz do wyświetlenia `comment` wraz z resztą dane artykułu:</span><span class="sxs-lookup"><span data-stu-id="4180e-273">Inside the `<div class="list-group">` element and just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="4180e-274">Otwórz _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="4180e-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="4180e-275">Znajdź `<div class="form-group">` element, który zawiera przycisk Prześlij, która wygląda podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="4180e-275">Find the `<div class="form-group">` element that contains the submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="4180e-276">Powyżej tego tagu, dodać kolejne `<div class="form-group">` elementu można edytować `comment` pola.</span><span class="sxs-lookup"><span data-stu-id="4180e-276">Just above this tag, add another `<div class="form-group">` element that lets people edit the `comment` field.</span></span> <span data-ttu-id="4180e-277">Nazwę nowego elementu powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="4180e-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="4180e-278">Przetestuj zmiany lokalnie</span><span class="sxs-lookup"><span data-stu-id="4180e-278">Test your changes locally</span></span>

<span data-ttu-id="4180e-279">Zapisz wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="4180e-279">Save all your changes.</span></span>

<span data-ttu-id="4180e-280">Ponownie przetestuj zmiany w trybie produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="4180e-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="4180e-281">Należy pamiętać, że Twoje _config/env/production.js_ została wycofana i `MONGODB_URI` zmiennej środowiskowej ustawiono tylko w aplikacji sieci web platformy Azure, a nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="4180e-281">Remember that your _config/env/production.js_ has been reverted, and the `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="4180e-282">Należy sprawdzić plik konfiguracji, można znaleźć konfiguracji produkcji domyślnie korzystania z lokalnej bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4180e-282">If you look at the config file, you find that the production configuration defaults to use a local MongoDB database.</span></span> <span data-ttu-id="4180e-283">Dzięki temu nie ruszaj danych produkcyjnych podczas testowania zmiany kodu lokalnie.</span><span class="sxs-lookup"><span data-stu-id="4180e-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="4180e-284">Przejdź do `http://localhost:8443` w przeglądarce i upewnij się, że użytkownik jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="4180e-284">Navigate to `http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="4180e-285">Wybierz **Admin > Zarządzaj artykuły**, następnie dodać artykułu, wybierając  **+**  przycisku.</span><span class="sxs-lookup"><span data-stu-id="4180e-285">Select **Admin > Manage Articles**, then add an article by selecting the **+** button.</span></span>

<span data-ttu-id="4180e-286">Zostanie wyświetlony nowy `Comment` teraz pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="4180e-286">You see the new `Comment` textbox now.</span></span>

![Pole komentarz dodany do artykułów](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="4180e-288">W terminalu, Zatrzymaj Node.js, wpisując `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="4180e-288">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-to-azure"></a><span data-ttu-id="4180e-289">Publikowanie zmian na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-289">Publish changes to Azure</span></span>

<span data-ttu-id="4180e-290">Zatwierdź zmiany w usłudze Git, a następnie Wypchnij zmiany kodu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4180e-290">Commit your changes in Git, then push the code changes to Azure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="4180e-291">Raz `git push` jest zakończenie, przejdź do aplikacji sieci web platformy Azure i wypróbowanie nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="4180e-291">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality.</span></span>

![Zmiany modelu i bazy danych publikowanych w systemie Azure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="4180e-293">Jeśli wcześniej dodane artykułów, nadal widać je.</span><span class="sxs-lookup"><span data-stu-id="4180e-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="4180e-294">Istniejące dane w bazie danych z rozwiązania Cosmos nie zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="4180e-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="4180e-295">Ponadto aktualizacje schematu danych i pozostawienie bez zmian do istniejących danych.</span><span class="sxs-lookup"><span data-stu-id="4180e-295">Also, your updates to the data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="4180e-296">Dzienniki diagnostyczne strumienia</span><span class="sxs-lookup"><span data-stu-id="4180e-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="4180e-297">Podczas wykonywania aplikacji Node.js w usłudze Azure App Service można uzyskać dzienniki konsoli w potoku do terminalu.</span><span class="sxs-lookup"><span data-stu-id="4180e-297">While your Node.js application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="4180e-298">W ten sposób można uzyskać tego samego komunikaty diagnostyczne w celu ułatwienia debugowania błędów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4180e-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="4180e-299">Aby rozpocząć przesyłanie strumieniowe dziennika, użyj [końcowego fragmentu dziennika aplikacji sieci Web az](/cli/azure/webapp/log#tail) polecenia.</span><span class="sxs-lookup"><span data-stu-id="4180e-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="4180e-300">Po rozpoczęciu przesyłania strumieniowego dzienników odświeżanie aplikacji sieci web platformy Azure w przeglądarce, aby uzyskać pewne ruchu w sieci web.</span><span class="sxs-lookup"><span data-stu-id="4180e-300">Once log streaming has started, refresh your Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="4180e-301">Pojawi się w potoku do terminalu dzienniki konsoli.</span><span class="sxs-lookup"><span data-stu-id="4180e-301">You now see console logs piped to your terminal.</span></span>

<span data-ttu-id="4180e-302">Dziennik zatrzymania przesyłania strumieniowego w dowolnym momencie, wpisując `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="4180e-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="4180e-303">Zarządzanie aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-303">Manage your Azure web app</span></span>

<span data-ttu-id="4180e-304">Przejdź do [portalu Azure](https://portal.azure.com) zobaczyć aplikacji sieci web został utworzony.</span><span class="sxs-lookup"><span data-stu-id="4180e-304">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="4180e-305">W lewym menu kliknij pozycję **App Services**, a następnie kliknij nazwę swojej aplikacji sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4180e-305">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Nawigacja w portalu do aplikacji sieci Web platformy Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="4180e-307">Domyślnie portalu zawiera aplikację sieci web **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="4180e-307">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="4180e-308">Ta strona udostępnia widok sposobu działania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4180e-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="4180e-309">Tutaj możesz również wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="4180e-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="4180e-310">W lewej części strony kartach stron innej konfiguracji może być otwarty.</span><span class="sxs-lookup"><span data-stu-id="4180e-310">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Strona usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="4180e-312">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4180e-312">Next steps</span></span>

<span data-ttu-id="4180e-313">Wiadomości:</span><span class="sxs-lookup"><span data-stu-id="4180e-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4180e-314">Tworzenie bazy danych MongoDB na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="4180e-315">Łączenie aplikacji Node.js z bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="4180e-315">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="4180e-316">Wdrażanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-316">Deploy the app to Azure</span></span>
> * <span data-ttu-id="4180e-317">Aktualizacja modelu danych i ponownie wdrożyć aplikację</span><span class="sxs-lookup"><span data-stu-id="4180e-317">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="4180e-318">Strumieniowe przesyłanie dzienników z platformy Azure na terminalu</span><span class="sxs-lookup"><span data-stu-id="4180e-318">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="4180e-319">Zarządzanie aplikacją w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4180e-319">Manage the app in the Azure portal</span></span>

<span data-ttu-id="4180e-320">Przejdź do następnego samouczek, aby dowiedzieć się, jak zamapować niestandardową nazwę DNS na aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="4180e-320">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="4180e-321">Map an existing custom DNS name to Azure Web Apps (Mapowanie istniejącej niestandardowej nazwy DNS na aplikacje internetowe platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="4180e-321">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
