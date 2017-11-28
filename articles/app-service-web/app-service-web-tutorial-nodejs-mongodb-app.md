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
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="0ce20-103">Tworzenie aplikacji sieci web Node.js i bazy danych MongoDB na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0ce20-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="0ce20-104">Aplikacje sieci Web platformy Azure oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web.</span><span class="sxs-lookup"><span data-stu-id="0ce20-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="0ce20-105">Ten samouczek pokazuje, jak toocreate Node.js sieci web aplikacji na platformie Azure i podłącz go tooa baza danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ce20-105">This tutorial shows how toocreate a Node.js web app in Azure and connect it tooa MongoDB database.</span></span> <span data-ttu-id="0ce20-106">Gdy wszystko będzie gotowe, będziesz mieć uruchomionej aplikacji średniej (bazy danych MongoDB, Express AngularJS i Node.js) w [usłudze Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ce20-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="0ce20-107">Dla uproszczenia hello Przykładowa aplikacja korzysta hello [platforma sieci web MEAN.js](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="0ce20-107">For simplicity, hello sample application uses hello [MEAN.js web framework](http://meanjs.org/).</span></span>

![Aplikacja MEAN.js uruchomiona w usłudze Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="0ce20-109">Zawartość:</span><span class="sxs-lookup"><span data-stu-id="0ce20-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0ce20-110">Tworzenie bazy danych MongoDB na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0ce20-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="0ce20-111">Połącz tooMongoDB aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="0ce20-111">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="0ce20-112">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="0ce20-112">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="0ce20-113">Aktualizacja modelu danych hello i wdrożenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="0ce20-113">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="0ce20-114">Strumieniowe przesyłanie dzienników diagnostycznych z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0ce20-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="0ce20-115">Zarządzanie aplikacją hello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0ce20-115">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ce20-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0ce20-116">Prerequisites</span></span>

<span data-ttu-id="0ce20-117">toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="0ce20-117">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="0ce20-118">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="0ce20-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="0ce20-119">Zainstaluj środowisko Node.js i menedżer NPM</span><span class="sxs-lookup"><span data-stu-id="0ce20-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="0ce20-120">[Zainstaluj Gulp.js](http://gulpjs.com/) (wymagany przez [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span><span class="sxs-lookup"><span data-stu-id="0ce20-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="0ce20-121">Zainstaluj i uruchom MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="0ce20-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0ce20-122">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="0ce20-122">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0ce20-123">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="0ce20-123">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0ce20-124">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0ce20-124">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="0ce20-125">Test lokalnej bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="0ce20-125">Test local MongoDB</span></span>

<span data-ttu-id="0ce20-126">Witaj Otwórz okno terminala i `cd` toohello `bin` katalogu instalacji bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ce20-126">Open hello terminal window and `cd` toohello `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="0ce20-127">Wszystkie polecenia hello toorun to okno terminalu można użyć w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="0ce20-127">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

<span data-ttu-id="0ce20-128">Uruchom `mongo` w hello terminali tooconnect tooyour MongoDB serwera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="0ce20-128">Run `mongo` in hello terminal tooconnect tooyour local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="0ce20-129">Jeśli połączenie zostanie nawiązane, bazy danych MongoDB już jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="0ce20-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="0ce20-130">Jeśli nie, upewnij się, że lokalnej bazy danych MongoDB została uruchomiona, wykonując kroki hello na [zainstalować bazy danych MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="0ce20-130">If not, make sure that your local MongoDB database is started by following hello steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="0ce20-131">Często jest zainstalowana baza danych MongoDB, ale nadal potrzebujesz toostart ją, uruchamiając `mongod`.</span><span class="sxs-lookup"><span data-stu-id="0ce20-131">Often, MongoDB is installed, but you still need toostart it by running `mongod`.</span></span> 

<span data-ttu-id="0ce20-132">Po zakończeniu testowania bazy danych MongoDB, wpisz `Ctrl+C` w hello terminala.</span><span class="sxs-lookup"><span data-stu-id="0ce20-132">When you're done testing your MongoDB database, type `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="0ce20-133">Tworzenie lokalnych aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="0ce20-133">Create local Node.js app</span></span>

<span data-ttu-id="0ce20-134">Ten krok umożliwia zdefiniowanie hello lokalnego Node.js projektu.</span><span class="sxs-lookup"><span data-stu-id="0ce20-134">In this step, you set up hello local Node.js project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="0ce20-135">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="0ce20-135">Clone hello sample application</span></span>

<span data-ttu-id="0ce20-136">Okno terminalu hello `cd` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="0ce20-136">In hello terminal window, `cd` tooa working directory.</span></span>  

<span data-ttu-id="0ce20-137">Hello uruchom następujące polecenie tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0ce20-137">Run hello following command tooclone hello sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="0ce20-138">To repozytorium przykładowej zawiera kopię hello [repozytorium MEAN.js](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="0ce20-138">This sample repository contains a copy of hello [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="0ce20-139">Jest zmodyfikowany toorun w usłudze aplikacji (Aby uzyskać więcej informacji, zobacz repozytorium MEAN.js hello [Plik README](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="0ce20-139">It is modified toorun on App Service (for more information, see hello MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-hello-application"></a><span data-ttu-id="0ce20-140">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="0ce20-140">Run hello application</span></span>

<span data-ttu-id="0ce20-141">Uruchom następujące polecenia tooinstall hello wymaganych pakietów hello i uruchomienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0ce20-141">Run hello following commands tooinstall hello required packages and start hello application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="0ce20-142">Po całkowitym załadowaniem aplikacji hello pojawić coś podobnego toohello następującego komunikatu:</span><span class="sxs-lookup"><span data-stu-id="0ce20-142">When hello app is fully loaded, you see something similar toohello following message:</span></span>

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

<span data-ttu-id="0ce20-143">Przejdź toohttp://localhost:3000 w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="0ce20-143">Navigate toohttp://localhost:3000 in a browser.</span></span> <span data-ttu-id="0ce20-144">Kliknij przycisk **Utwórz konto** w menu u góry hello i tworzenie użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0ce20-144">Click **Sign Up** in hello top menu and create a test user.</span></span> 

<span data-ttu-id="0ce20-145">Witaj MEAN.js Przykładowa aplikacja przechowuje dane użytkownika w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="0ce20-145">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="0ce20-146">W przypadku pomyślnego tworzenia użytkownika i logowanie, aplikację zapisywania danych toohello lokalnej bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ce20-146">If you are successful at creating a user and signing in, then your app is writing data toohello local MongoDB database.</span></span>

![MEAN.js pomyślnie łączy tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="0ce20-148">Wybierz **Admin > Zarządzaj artykuły** tooadd niektórych artykułach.</span><span class="sxs-lookup"><span data-stu-id="0ce20-148">Select **Admin > Manage Articles** tooadd some articles.</span></span>

<span data-ttu-id="0ce20-149">toostop Node.js w dowolnym momencie, naciśnij klawisz `Ctrl+C` w hello terminala.</span><span class="sxs-lookup"><span data-stu-id="0ce20-149">toostop Node.js at any time, press `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="0ce20-150">Utwórz produkcyjnej bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="0ce20-150">Create production MongoDB</span></span>

<span data-ttu-id="0ce20-151">W tym kroku utworzysz bazę danych MongoDB na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce20-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="0ce20-152">Gdy aplikacji jest wdrożony tooAzure, używa tej bazy danych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0ce20-152">When your app is deployed tooAzure, it uses this cloud database.</span></span>

<span data-ttu-id="0ce20-153">Bazy danych mongodb, w tym samouczku używana [bazy danych Azure rozwiązania Cosmos](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="0ce20-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="0ce20-154">Rozwiązania cosmos bazy danych obsługuje połączenia klienta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ce20-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="0ce20-155">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="0ce20-155">Log in tooAzure</span></span>

<span data-ttu-id="0ce20-156">Użyjesz hello Azure CLI 2.0 toocreate hello zasobów niezbędnych toohost aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce20-156">You'll use hello Azure CLI 2.0 toocreate hello resources needed toohost your app in Azure.</span></span> <span data-ttu-id="0ce20-157">Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="0ce20-157">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="0ce20-158">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="0ce20-158">Create a resource group</span></span>

<span data-ttu-id="0ce20-159">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0ce20-159">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="0ce20-160">Witaj poniższy przykład tworzy grupę zasobów w regionie Europy Zachodniej hello.</span><span class="sxs-lookup"><span data-stu-id="0ce20-160">hello following example creates a resource group in hello West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="0ce20-161">Użyj hello [appservice az listy lokalizacje](/cli/azure/appservice#list-locations) toolist dostępne lokalizacje polecenia wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce20-161">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="0ce20-162">Tworzenie konta bazy danych rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="0ce20-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="0ce20-163">Tworzenie konta bazy danych rozwiązania Cosmos z hello [az cosmosdb utworzyć](/cli/azure/cosmosdb#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0ce20-163">Create a Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="0ce20-164">W hello następujące polecenia, należy zastąpić unikatową nazwę bazy danych rozwiązania Cosmos hello  *\<cosmosdb_name >* symbolu zastępczego.</span><span class="sxs-lookup"><span data-stu-id="0ce20-164">In hello following command, substitute a unique Cosmos DB name for hello *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="0ce20-165">Ta nazwa jest używana jako część hello hello DB rozwiązania Cosmos punktu końcowego, `https://<cosmosdb_name>.documents.azure.com/`, więc nazwa hello musi toobe unikatowy wszystkich kont rozwiązania Cosmos bazy danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce20-165">This name is used as hello part of hello Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so hello name needs toobe unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="0ce20-166">Nazwa Hello musi zawierać tylko małe litery, cyfry i znaki łącznika (-) hello i musi mieć długość od 3 do 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="0ce20-166">hello name must contain only lowercase letters, numbers, and hello hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="0ce20-167">Witaj *--rodzaju bazy danych MongoDB* parametru zapewnia połączeń klienckich bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ce20-167">hello *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="0ce20-168">Po utworzeniu hello konto bazy danych rozwiązania Cosmos hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="0ce20-168">When hello Cosmos DB account is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="connect-app-tooproduction-mongodb"></a><span data-ttu-id="0ce20-169">Łączenie aplikacji tooproduction bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="0ce20-169">Connect app tooproduction MongoDB</span></span>

<span data-ttu-id="0ce20-170">W tym kroku połączenie MEAN.js przykładowej bazy danych aplikacji toohello DB rozwiązania Cosmos utworzony, przy użyciu parametrów połączenia bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ce20-170">In this step, you connect your MEAN.js sample application toohello Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-hello-database-key"></a><span data-ttu-id="0ce20-171">Pobrać hello klucza bazy danych</span><span class="sxs-lookup"><span data-stu-id="0ce20-171">Retrieve hello database key</span></span>

<span data-ttu-id="0ce20-172">bazy danych DB rozwiązania Cosmos toohello tooconnect, należy hello klucza bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0ce20-172">tooconnect toohello Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="0ce20-173">Użyj hello [az cosmosdb listy kluczy](/cli/azure/cosmosdb#list-keys) klucz podstawowy hello tooretrieve polecenia.</span><span class="sxs-lookup"><span data-stu-id="0ce20-173">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="0ce20-174">Hello interfejsu wiersza polecenia Azure zawiera informacje o toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="0ce20-174">hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Skopiuj wartość hello `primaryMasterKey`. <span data-ttu-id="0ce20-176">Należy te informacje w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="0ce20-176">You need this information in hello next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="0ce20-177">Konfigurowanie parametrów połączenia hello w aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="0ce20-177">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="0ce20-178">Otwórz w repozytorium MEAN.js _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="0ce20-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="0ce20-179">W hello `db` obiektów, zaktualizuj wartość hello `uri`:</span><span class="sxs-lookup"><span data-stu-id="0ce20-179">In hello `db` object, update hello value of `uri`:</span></span>

* <span data-ttu-id="0ce20-180">Zastąp hello dwa  *\<cosmosdb_name >* symbole zastępcze nazwą bazy danych DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0ce20-180">Replace hello two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="0ce20-181">Zastąp hello  *\<primary_master_key >* symbol zastępczy hello klucza skopiowany w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="0ce20-181">Replace hello *\<primary_master_key>* placeholder with hello key you copied in hello previous step.</span></span>

<span data-ttu-id="0ce20-182">Witaj poniższy kod przedstawia hello `db` obiektu:</span><span class="sxs-lookup"><span data-stu-id="0ce20-182">hello following code shows hello `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="0ce20-183">Witaj `ssl=true` opcja jest wymagana, ponieważ [DB rozwiązania Cosmos wymaga protokołu SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="0ce20-183">hello `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="0ce20-184">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="0ce20-184">Save your changes.</span></span>

### <a name="test-hello-application-in-production-mode"></a><span data-ttu-id="0ce20-185">Testowanie aplikacji hello w trybie produkcyjnym</span><span class="sxs-lookup"><span data-stu-id="0ce20-185">Test hello application in production mode</span></span> 

<span data-ttu-id="0ce20-186">Uruchom następujące polecenie toominify i pakietu skryptów w środowisku produkcyjnym hello hello.</span><span class="sxs-lookup"><span data-stu-id="0ce20-186">Run hello following command toominify and bundle scripts for hello production environment.</span></span> <span data-ttu-id="0ce20-187">Ten proces generuje hello pliki wymagane przez hello środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0ce20-187">This process generates hello files needed by hello production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="0ce20-188">Hello uruchom następujące polecenie toouse hello ciąg połączenia został skonfigurowany w _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="0ce20-188">Run hello following command toouse hello connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="0ce20-189">`NODE_ENV=production`Ustawia zmienną środowiskową hello informujący o Node.js toorun w środowisku produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="0ce20-189">`NODE_ENV=production` sets hello environment variable that tells Node.js toorun in hello production environment.</span></span>  <span data-ttu-id="0ce20-190">`node server.js`Uruchamia hello Node.js server z `server.js` w katalogu głównym repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0ce20-190">`node server.js` starts hello Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="0ce20-191">Jest to, jak załadowano aplikację Node.js na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce20-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="0ce20-192">Podczas ładowania aplikacji hello Sprawdź toomake się, że jest uruchomiony w środowisku produkcyjnym hello:</span><span class="sxs-lookup"><span data-stu-id="0ce20-192">When hello app is loaded, check toomake sure that it's running in hello production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="0ce20-193">Przejdź toohttp://localhost:8443 w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="0ce20-193">Navigate toohttp://localhost:8443 in a browser.</span></span> <span data-ttu-id="0ce20-194">Kliknij przycisk **Utwórz konto** w menu u góry hello i tworzenie użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0ce20-194">Click **Sign Up** in hello top menu and create a test user.</span></span> <span data-ttu-id="0ce20-195">Jeśli tworzenie użytkownika i logowanie powiodło się, aplikacja jest zapisywanie bazy danych DB rozwiązania Cosmos toohello danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce20-195">If you are successful creating a user and signing in, then your app is writing data toohello Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="0ce20-196">W terminalu hello, Zatrzymaj Node.js, wpisując `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="0ce20-196">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-tooazure"></a><span data-ttu-id="0ce20-197">Wdrażanie aplikacji tooAzure</span><span class="sxs-lookup"><span data-stu-id="0ce20-197">Deploy app tooAzure</span></span>

<span data-ttu-id="0ce20-198">W tym kroku możesz wdrożyć tooAzure aplikacji programu Node.js połączenia bazy danych MongoDB usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ce20-198">In this step, you deploy your MongoDB-connected Node.js application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="0ce20-199">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="0ce20-199">Create an App Service plan</span></span>

<span data-ttu-id="0ce20-200">Tworzenie planu usługi aplikacji z hello [Tworzenie planu usług aplikacji az](/cli/azure/appservice/plan#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0ce20-200">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="0ce20-201">Witaj poniższy przykład tworzy plan usługi aplikacji o nazwie _myAppServicePlan_ przy użyciu hello **wolne** warstwa cenowa:</span><span class="sxs-lookup"><span data-stu-id="0ce20-201">hello following example creates an App Service plan named _myAppServicePlan_ using hello **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="0ce20-202">Po utworzeniu planu usługi aplikacji hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="0ce20-202">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="0ce20-203">Tworzenie aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="0ce20-203">Create a web app</span></span>

<span data-ttu-id="0ce20-204">Tworzenie aplikacji sieci web w hello `myAppServicePlan` planu usługi aplikacji z hello [tworzenie aplikacji sieci Web az](/cli/azure/webapp#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0ce20-204">Create a web app in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="0ce20-205">umożliwia aplikacji sieci web Hello możesz hosting miejsce toodeploy kodu i zawiera adres URL dla Ciebie tooview hello wdrożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ce20-205">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="0ce20-206">Użyj aplikacji sieci web hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0ce20-206">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="0ce20-207">Witaj następujące polecenia, Zastąp hello  *\<nazwa_aplikacji >* symbol zastępczy unikatowej nazwy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ce20-207">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="0ce20-208">Ta nazwa jest używana jako część hello hello domyślny adres URL dla aplikacji sieci web hello, więc nazwa hello musi toobe unikatowy przez wszystkie aplikacje w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0ce20-208">This name is used as hello part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="0ce20-209">Podczas tworzenia aplikacji sieci web hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="0ce20-209">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-an-environment-variable"></a><span data-ttu-id="0ce20-210">Skonfigurować zmienną środowiskową</span><span class="sxs-lookup"><span data-stu-id="0ce20-210">Configure an environment variable</span></span>

<span data-ttu-id="0ce20-211">Wcześniej w hello samouczek, zostanie zapisane na stałe hello parametry połączenia bazy danych w _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="0ce20-211">Earlier in hello tutorial, you hardcoded hello database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="0ce20-212">Zgodnie z zaleceniami dotyczącymi zabezpieczeń ma tookeep danych poufnych poza repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="0ce20-212">In keeping with security best practice, you want tookeep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="0ce20-213">Dla aplikacji działających na platformie Azure będzie zamiast tego użyć zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="0ce20-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="0ce20-214">W usłudze App Service można ustawić zmienne środowiskowe jako _ustawień aplikacji_ przy użyciu hello [zaktualizować appsettings konfiguracji aplikacji sieci Web az](/cli/azure/webapp/config/appsettings#update) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0ce20-214">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="0ce20-215">Witaj poniższy przykład konfiguruje `MONGODB_URI` ustawienie aplikacji w aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce20-215">hello following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="0ce20-216">Zastąp hello  *\<nazwa_aplikacji >*,  *\<cosmosdb_name >*, i  *\<primary_master_key >* symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="0ce20-216">Replace hello *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="0ce20-217">W kodzie Node.js dostępu to ustawienie aplikacji o `process.env.MONGODB_URI`, tak jak będzie dostęp do wszelkich zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="0ce20-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="0ce20-218">Teraz Cofnij too_config/env/production.js_ Twoje zmiany z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="0ce20-218">Now, undo your changes too_config/env/production.js_ with hello following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="0ce20-219">Otwórz _config/env/production.js_ ponownie.</span><span class="sxs-lookup"><span data-stu-id="0ce20-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="0ce20-220">Należy pamiętać, aplikacja hello domyślnego MEAN.js jest już skonfigurowany toouse hello `MONGODB_URI` zmienną środowiskową, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="0ce20-220">Note that hello default MEAN.js app is already configured toouse hello `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="0ce20-221">Konfigurowanie lokalnego wdrożenia narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="0ce20-221">Configure local git deployment</span></span> 

<span data-ttu-id="0ce20-222">Użyj hello [ustawiono użytkownika wdrożenia aplikacji sieci Web az](/cli/azure/webapp/deployment/user#set) polecenia toocreate poświadczeń do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0ce20-222">Use hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command toocreate credentials for deployment.</span></span>

<span data-ttu-id="0ce20-223">Można wdrożyć tooAzure Twojej aplikacji usługi App Service na różne sposoby, w tym FTP, Git lokalnego GitHub, Visual Studio Team Services i BitBucket.</span><span class="sxs-lookup"><span data-stu-id="0ce20-223">You can deploy your application tooAzure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="0ce20-224">FTP i lokalne Git, konieczne jest toohave użytkownika wdrożenia skonfigurowane na powitania serwera tooauthenticate wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0ce20-224">For FTP and local Git, it is necessary toohave a deployment user configured on hello server tooauthenticate your deployment.</span></span> <span data-ttu-id="0ce20-225">Ten użytkownik wdrożenia poziomie konta i różni się od konta subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce20-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="0ce20-226">Wystarczy tooconfigure tego użytkownika wdrożenia raz.</span><span class="sxs-lookup"><span data-stu-id="0ce20-226">You only need tooconfigure this deployment user once.</span></span>

<span data-ttu-id="0ce20-227">Zastąp następujące polecenie, w hello  *\<nazwa użytkownika >* i  *\<hasło >* nową nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="0ce20-227">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="0ce20-228">Witaj, nazwa użytkownika musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="0ce20-228">hello user name must be unique.</span></span> <span data-ttu-id="0ce20-229">Witaj hasło musi mieć co najmniej ośmiu znaków, przy użyciu dwóch hello następujące trzy elementy: liter, cyfr, symboli.</span><span class="sxs-lookup"><span data-stu-id="0ce20-229">hello password must be at least eight characters long, with two of hello following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="0ce20-230">Jeśli otrzymasz ` 'Conflict'. Details: 409` błąd, username hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="0ce20-230">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="0ce20-231">Jeśli wystąpił błąd ` 'Bad Request'. Details: 400`, użyj silniejszego hasła.</span><span class="sxs-lookup"><span data-stu-id="0ce20-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="0ce20-232">Nazwa użytkownika hello rekordu i hasło do użycia w kolejnych krokach podczas wdrażania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0ce20-232">Record hello user name and password for use in later steps when you deploy hello app.</span></span>

<span data-ttu-id="0ce20-233">Użyj hello [źródło wdrożenia az aplikacji sieci Web — config lokalnych git](/cli/azure/webapp/deployment/source#config-local-git) polecenia tooconfigure lokalnego Git dostępu toohello aplikacji sieci web Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce20-233">Use hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command tooconfigure local Git access toohello Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="0ce20-234">Po skonfigurowaniu użytkownika wdrażania hello hello Azure CLI zawiera hello adres URL wdrożenia dla aplikacji sieci web platformy Azure w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="0ce20-234">When hello deployment user is configured, hello Azure CLI shows hello deployment URL for your Azure web app in hello following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="0ce20-235">Skopiować hello dane wyjściowe z hello terminal, będzie on używany w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="0ce20-235">Copy hello output from hello terminal, as it will be used in hello next step.</span></span> 

### <a name="push-tooazure-from-git"></a><span data-ttu-id="0ce20-236">Wypychać tooAzure za pomocą narzędzia Git</span><span class="sxs-lookup"><span data-stu-id="0ce20-236">Push tooAzure from Git</span></span>

<span data-ttu-id="0ce20-237">Dodaj Azure tooyour zdalnego lokalnego repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="0ce20-237">Add an Azure remote tooyour local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="0ce20-238">Wypchnij toohello Azure toodeploy zdalnego aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="0ce20-238">Push toohello Azure remote toodeploy your Node.js application.</span></span> <span data-ttu-id="0ce20-239">Pojawi się monit dla hello hasło wcześniej w ramach tworzenia hello hello wdrożenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0ce20-239">You will be prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="0ce20-240">Podczas wdrażania usługi Azure App Service komunikuje się postęp za pomocą narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="0ce20-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

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

<span data-ttu-id="0ce20-241">Można zauważyć, że proces wdrażania hello uruchamia [system Gulp](http://gulpjs.com/) po `npm install`.</span><span class="sxs-lookup"><span data-stu-id="0ce20-241">You may notice that hello deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="0ce20-242">Usługi aplikacji Gulp lub Grunt zadań nie jest uruchamiane podczas wdrażania, więc to repozytorium przykładowej ma dwa dodatkowe pliki w jego tooenable katalogu głównego go:</span><span class="sxs-lookup"><span data-stu-id="0ce20-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory tooenable it:</span></span> 

- <span data-ttu-id="0ce20-243">_.Deployment_ -toorun usługi aplikacji określa, że ten plik `bash deploy.sh` jako hello niestandardowe wdrożenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="0ce20-243">_.deployment_ - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
- <span data-ttu-id="0ce20-244">_Deploy.sh_ — Witaj niestandardowe wdrożenie skryptu.</span><span class="sxs-lookup"><span data-stu-id="0ce20-244">_deploy.sh_ - hello custom deployment script.</span></span> <span data-ttu-id="0ce20-245">Jeśli możesz przejrzeć plik hello, zobaczysz, że działa `gulp prod` po `npm install` i `bower install`.</span><span class="sxs-lookup"><span data-stu-id="0ce20-245">If you review hello file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="0ce20-246">Tooadd tej metody można użyć dowolnego kroku tooyour wdrożenia na podstawie Git.</span><span class="sxs-lookup"><span data-stu-id="0ce20-246">You can use this approach tooadd any step tooyour Git-based deployment.</span></span> <span data-ttu-id="0ce20-247">W przypadku ponownego uruchomienia aplikacji sieci web platformy Azure w dowolnym momencie, usługi aplikacji nie ponownie te zadania automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="0ce20-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="0ce20-248">Przeglądaj toohello aplikacji sieci web Azure</span><span class="sxs-lookup"><span data-stu-id="0ce20-248">Browse toohello Azure web app</span></span> 

<span data-ttu-id="0ce20-249">Przeglądaj toohello wdrożyć aplikację sieci web przy użyciu przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="0ce20-249">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="0ce20-250">Kliknij przycisk **Utwórz konto** w menu u góry hello i Utwórz użytkownika zastępczego.</span><span class="sxs-lookup"><span data-stu-id="0ce20-250">Click **Sign Up** in hello top menu and create a dummy user.</span></span> 

<span data-ttu-id="0ce20-251">Jeśli pomyślnie i automatycznie loguje aplikacji hello toohello utworzyć użytkownika, a następnie MEAN.js aplikacji na platformie Azure ma bazy danych MongoDB (DB rozwiązania Cosmos) toohello łączności.</span><span class="sxs-lookup"><span data-stu-id="0ce20-251">If you are successful and hello app automatically signs in toohello created user, then your MEAN.js app in Azure has connectivity toohello MongoDB (Cosmos DB) database.</span></span> 

![Aplikacja MEAN.js uruchomiona w usłudze Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="0ce20-253">Wybierz **Admin > Zarządzaj artykuły** tooadd niektórych artykułach.</span><span class="sxs-lookup"><span data-stu-id="0ce20-253">Select **Admin > Manage Articles** tooadd some articles.</span></span> 

<span data-ttu-id="0ce20-254">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="0ce20-254">**Congratulations!**</span></span> <span data-ttu-id="0ce20-255">Używasz aplikacji Node.js opartych na danych w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0ce20-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="0ce20-256">Aktualizacja modelu danych i utwórz je ponownie</span><span class="sxs-lookup"><span data-stu-id="0ce20-256">Update data model and redeploy</span></span>

<span data-ttu-id="0ce20-257">W tym kroku, możesz zmienić hello `article` danych model i opublikuj tooAzure Twoje zmiany.</span><span class="sxs-lookup"><span data-stu-id="0ce20-257">In this step, you change hello `article` data model and publish your change tooAzure.</span></span>

### <a name="update-hello-data-model"></a><span data-ttu-id="0ce20-258">Model danych hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="0ce20-258">Update hello data model</span></span>

<span data-ttu-id="0ce20-259">Otwórz _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="0ce20-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="0ce20-260">W `ArticleSchema`, Dodaj `String` typu o nazwie `comment`.</span><span class="sxs-lookup"><span data-stu-id="0ce20-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="0ce20-261">Gdy wszystko będzie gotowe, schemat kod powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="0ce20-261">When you're done, your schema code should look like this:</span></span>

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

### <a name="update-hello-articles-code"></a><span data-ttu-id="0ce20-262">Zaktualizuj kod artykuły hello</span><span class="sxs-lookup"><span data-stu-id="0ce20-262">Update hello articles code</span></span>

<span data-ttu-id="0ce20-263">Zaktualizuj hello reszty Twojej `articles` kodu toouse `comment`.</span><span class="sxs-lookup"><span data-stu-id="0ce20-263">Update hello rest of your `articles` code toouse `comment`.</span></span>

<span data-ttu-id="0ce20-264">Jest pięć plików należy toomodify: hello serwera kontrolera i hello cztery widoki klientów.</span><span class="sxs-lookup"><span data-stu-id="0ce20-264">There are five files you need toomodify: hello server controller and hello four client views.</span></span> 

<span data-ttu-id="0ce20-265">Otwórz _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="0ce20-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="0ce20-266">W hello `update` funkcji, należy dodać przydziału `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="0ce20-266">In hello `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="0ce20-267">Witaj poniższy kod przedstawia ukończyć powitalnych `update` funkcji:</span><span class="sxs-lookup"><span data-stu-id="0ce20-267">hello following code shows hello completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="0ce20-268">Otwórz _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="0ce20-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="0ce20-269">Powyżej zamknięcia hello `</section>` tagów, Dodaj powitania po wierszu toodisplay `comment` wraz z hello pozostałe dane artykułu hello:</span><span class="sxs-lookup"><span data-stu-id="0ce20-269">Just above hello closing `</section>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="0ce20-270">Otwórz _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="0ce20-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="0ce20-271">Powyżej zamknięcia hello `</a>` tagów, Dodaj powitania po wierszu toodisplay `comment` wraz z hello pozostałe dane artykułu hello:</span><span class="sxs-lookup"><span data-stu-id="0ce20-271">Just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="0ce20-272">Otwórz _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="0ce20-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="0ce20-273">Wewnątrz hello `<div class="list-group">` element i nad zamknięciem hello `</a>` tagów, Dodaj powitania po wierszu toodisplay `comment` wraz z hello pozostałe dane artykułu hello:</span><span class="sxs-lookup"><span data-stu-id="0ce20-273">Inside hello `<div class="list-group">` element and just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="0ce20-274">Otwórz _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="0ce20-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="0ce20-275">Znajdź hello `<div class="form-group">` element, który zawiera przycisk Prześlij hello, która wygląda podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="0ce20-275">Find hello `<div class="form-group">` element that contains hello submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="0ce20-276">Powyżej tego tagu, dodać kolejne `<div class="form-group">` elementu można edytować hello `comment` pola.</span><span class="sxs-lookup"><span data-stu-id="0ce20-276">Just above this tag, add another `<div class="form-group">` element that lets people edit hello `comment` field.</span></span> <span data-ttu-id="0ce20-277">Nazwę nowego elementu powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="0ce20-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="0ce20-278">Przetestuj zmiany lokalnie</span><span class="sxs-lookup"><span data-stu-id="0ce20-278">Test your changes locally</span></span>

<span data-ttu-id="0ce20-279">Zapisz wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="0ce20-279">Save all your changes.</span></span>

<span data-ttu-id="0ce20-280">Ponownie przetestuj zmiany w trybie produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="0ce20-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="0ce20-281">Należy pamiętać, że Twoje _config/env/production.js_ została wycofana i hello `MONGODB_URI` zmiennej środowiskowej ustawiono tylko w aplikacji sieci web platformy Azure, a nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="0ce20-281">Remember that your _config/env/production.js_ has been reverted, and hello `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="0ce20-282">Podczas przeglądania w pliku konfiguracyjnym hello okaże się, że hello toouse ustawienia domyślne konfiguracji produkcji lokalnej bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0ce20-282">If you look at hello config file, you find that hello production configuration defaults toouse a local MongoDB database.</span></span> <span data-ttu-id="0ce20-283">Dzięki temu nie ruszaj danych produkcyjnych podczas testowania zmiany kodu lokalnie.</span><span class="sxs-lookup"><span data-stu-id="0ce20-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="0ce20-284">Przejdź do zbyt`http://localhost:8443` w przeglądarce i upewnij się, że użytkownik jest zalogowany.</span><span class="sxs-lookup"><span data-stu-id="0ce20-284">Navigate too`http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="0ce20-285">Wybierz **Admin > Zarządzaj artykuły**, następnie dodać artykułu, wybierając hello  **+**  przycisku.</span><span class="sxs-lookup"><span data-stu-id="0ce20-285">Select **Admin > Manage Articles**, then add an article by selecting hello **+** button.</span></span>

<span data-ttu-id="0ce20-286">Witaj Zobacz nowe `Comment` teraz pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="0ce20-286">You see hello new `Comment` textbox now.</span></span>

![Komentarz dodany tooArticles pola](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="0ce20-288">W terminalu hello, Zatrzymaj Node.js, wpisując `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="0ce20-288">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-tooazure"></a><span data-ttu-id="0ce20-289">Publikowanie zmian tooAzure</span><span class="sxs-lookup"><span data-stu-id="0ce20-289">Publish changes tooAzure</span></span>

<span data-ttu-id="0ce20-290">Zatwierdź zmiany w usłudze Git, a następnie Wypchnij tooAzure zmiany kodu hello.</span><span class="sxs-lookup"><span data-stu-id="0ce20-290">Commit your changes in Git, then push hello code changes tooAzure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="0ce20-291">Raz hello `git push` jest zakończenie, przejdź tooyour aplikacji sieci web platformy Azure i wypróbować hello nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="0ce20-291">Once hello `git push` is complete, navigate tooyour Azure web app and try out hello new functionality.</span></span>

![Zmiany modelu i bazy danych publikowanych tooAzure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="0ce20-293">Jeśli wcześniej dodane artykułów, nadal widać je.</span><span class="sxs-lookup"><span data-stu-id="0ce20-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="0ce20-294">Istniejące dane w bazie danych z rozwiązania Cosmos nie zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="0ce20-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="0ce20-295">Ponadto schemat danych toohello aktualizacji i pozostawienie bez zmian do istniejących danych.</span><span class="sxs-lookup"><span data-stu-id="0ce20-295">Also, your updates toohello data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="0ce20-296">Dzienniki diagnostyczne strumienia</span><span class="sxs-lookup"><span data-stu-id="0ce20-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="0ce20-297">Podczas wykonywania aplikacji Node.js w usłudze Azure App Service można uzyskać tooyour gazociągami dzienniki konsoli hello terminala.</span><span class="sxs-lookup"><span data-stu-id="0ce20-297">While your Node.js application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="0ce20-298">W ten sposób można uzyskać hello tego samego komunikaty diagnostyczne toohelp Debugowanie błędów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ce20-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="0ce20-299">Dziennik toostart przesyłania strumieniowego, użyj hello [końcowego fragmentu dziennika aplikacji sieci Web az](/cli/azure/webapp/log#tail) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0ce20-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="0ce20-300">Po rozpoczęciu przesyłania strumieniowego dzienników odświeżanie aplikacji sieci web platformy Azure w tooget przeglądarki hello część ruchu w sieci web.</span><span class="sxs-lookup"><span data-stu-id="0ce20-300">Once log streaming has started, refresh your Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="0ce20-301">Pojawi się dzienniki konsoli przetwarzana potokowo tooyour terminala.</span><span class="sxs-lookup"><span data-stu-id="0ce20-301">You now see console logs piped tooyour terminal.</span></span>

<span data-ttu-id="0ce20-302">Dziennik zatrzymania przesyłania strumieniowego w dowolnym momencie, wpisując `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="0ce20-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="0ce20-303">Zarządzanie aplikacji sieci web platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0ce20-303">Manage your Azure web app</span></span>

<span data-ttu-id="0ce20-304">Przejdź toohello [portalu Azure](https://portal.azure.com) aplikacji sieci web hello toosee został utworzony.</span><span class="sxs-lookup"><span data-stu-id="0ce20-304">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="0ce20-305">W menu po lewej stronie powitania kliknij **usługi aplikacji**, następnie kliknij nazwę hello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce20-305">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="0ce20-307">Domyślnie hello portal przedstawiono aplikację sieci web **omówienie** strony.</span><span class="sxs-lookup"><span data-stu-id="0ce20-307">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="0ce20-308">Ta strona udostępnia widok sposobu działania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ce20-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="0ce20-309">Tutaj możesz również wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie.</span><span class="sxs-lookup"><span data-stu-id="0ce20-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="0ce20-310">Witaj w lewej części strony hello hello kartach hello innej konfiguracji stron, które można otworzyć.</span><span class="sxs-lookup"><span data-stu-id="0ce20-310">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Strona usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="0ce20-312">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ce20-312">Next steps</span></span>

<span data-ttu-id="0ce20-313">Wiadomości:</span><span class="sxs-lookup"><span data-stu-id="0ce20-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0ce20-314">Tworzenie bazy danych MongoDB na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0ce20-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="0ce20-315">Połącz tooMongoDB aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="0ce20-315">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="0ce20-316">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="0ce20-316">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="0ce20-317">Aktualizacja modelu danych hello i wdrożenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="0ce20-317">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="0ce20-318">Strumieniowe przesyłanie dzienników z Azure tooyour terminali</span><span class="sxs-lookup"><span data-stu-id="0ce20-318">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="0ce20-319">Zarządzanie aplikacją hello w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0ce20-319">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="0ce20-320">Przejść dalej toolearn samouczka toohello jak toomap DNS niestandardowej nazwy tooyour aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="0ce20-320">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="0ce20-321">Mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="0ce20-321">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
