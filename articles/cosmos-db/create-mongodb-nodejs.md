---
title: "aaaConnect tooAzure aplikacji bazy danych MongoDB rozwiązania Cosmos bazy danych przy użyciu środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect istniejących aplikacji Node.js bazy danych MongoDB tooAzure DB rozwiązania Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a><span data-ttu-id="f9e00-103">Azure Cosmos DB: migracja istniejącej aplikacji sieci Web MongoDB w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="f9e00-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span></span> 

<span data-ttu-id="f9e00-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f9e00-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="f9e00-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f9e00-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="f9e00-106">Ta opcja szybkiego startu przedstawia sposób toouse istniejące [MongoDB](mongodb-introduction.md) aplikacji napisanych w Node.js i podłącz go bazy danych Azure DB rozwiązania Cosmos tooyour, która obsługuje połączenia klienta bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f9e00-106">This quickstart demonstrates how toouse an existing [MongoDB](mongodb-introduction.md) app written in Node.js and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span> <span data-ttu-id="f9e00-107">Innymi słowy aplikację Node.js tylko wie, że nawiązuje połączenie tooa bazy danych przy użyciu interfejsów API bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f9e00-107">In other words, your Node.js application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="f9e00-108">Jest niewidoczne toohello aplikacji hello dane są przechowywane w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f9e00-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="f9e00-109">Gdy wszystko będzie gotowe, aplikacja MEAN (MongoDB, Express, AngularJS i Node.js) będzie uruchomiona dla bazy danych [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="f9e00-109">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> 

![Aplikacja MEAN.js uruchomiona w usłudze Azure App Service](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f9e00-111">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f9e00-111">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f9e00-112">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="f9e00-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f9e00-113">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f9e00-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f9e00-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f9e00-114">Prerequisites</span></span> 
<span data-ttu-id="f9e00-115">Ponadto tooAzure interfejsu wiersza polecenia, należy [Node.js](https://nodejs.org/) i [Git](http://www.git-scm.com/downloads) zainstalowane lokalnie toorun `npm` i `git` poleceń.</span><span class="sxs-lookup"><span data-stu-id="f9e00-115">In addition tooAzure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally toorun `npm` and `git` commands.</span></span>

<span data-ttu-id="f9e00-116">Niezbędna jest praktyczna wiedza na temat Node.js.</span><span class="sxs-lookup"><span data-stu-id="f9e00-116">You should have working knowledge of Node.js.</span></span> <span data-ttu-id="f9e00-117">Ta opcja szybkiego startu nie jest zamierzone toohelp z ogólnie opracowywanie aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="f9e00-117">This quickstart is not intended toohelp you with developing Node.js applications in general.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="f9e00-118">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="f9e00-118">Clone hello sample application</span></span>

<span data-ttu-id="f9e00-119">Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="f9e00-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

<span data-ttu-id="f9e00-120">Hello uruchom następujące polecenia tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="f9e00-120">Run hello following commands tooclone hello sample repository.</span></span> <span data-ttu-id="f9e00-121">To repozytorium przykładowej zawiera domyślne hello [MEAN.js](http://meanjs.org/) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f9e00-121">This sample repository contains hello default [MEAN.js](http://meanjs.org/) application.</span></span> 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a><span data-ttu-id="f9e00-122">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="f9e00-122">Run hello application</span></span>

<span data-ttu-id="f9e00-123">Instalowanie pakietów hello wymagane, a następnie uruchom aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="f9e00-123">Install hello required packages and start hello application.</span></span>

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a><span data-ttu-id="f9e00-124">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="f9e00-124">Log in tooAzure</span></span>

<span data-ttu-id="f9e00-125">Jeśli używane są zainstalowane wiersza polecenia platformy Azure, zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="f9e00-125">If you are using an installed Azure CLI, log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="f9e00-126">Ten krok można pominąć, jeśli używasz hello powłoki chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="f9e00-126">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a><span data-ttu-id="f9e00-127">Dodaj moduł Azure DB rozwiązania Cosmos hello</span><span class="sxs-lookup"><span data-stu-id="f9e00-127">Add hello Azure Cosmos DB module</span></span>

<span data-ttu-id="f9e00-128">Jeśli używane są zainstalowane wiersza polecenia platformy Azure, określ, czy toosee hello `cosmosdb` uruchamiając hello jest już zainstalowany składnik `az` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9e00-128">If you are using an installed Azure CLI, check toosee if hello `cosmosdb` component is already installed by running hello `az` command.</span></span> <span data-ttu-id="f9e00-129">Jeśli `cosmosdb` jest hello listy poleceń podstawowej, kontynuować toohello następnego polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9e00-129">If `cosmosdb` is in hello list of base commands, proceed toohello next command.</span></span> <span data-ttu-id="f9e00-130">Ten krok można pominąć, jeśli używasz hello powłoki chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="f9e00-130">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

<span data-ttu-id="f9e00-131">Jeśli `cosmosdb` nie jest w hello listę poleceń, podstawowe, należy ponownie zainstalować [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f9e00-131">If `cosmosdb` is not in hello list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="f9e00-132">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="f9e00-132">Create a resource group</span></span>

<span data-ttu-id="f9e00-133">Utwórz [grupy zasobów](../azure-resource-manager/resource-group-overview.md) z hello [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f9e00-133">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f9e00-134">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure, takich jak aplikacje sieci Web, bazy danych i konta magazynu, oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="f9e00-134">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="f9e00-135">Witaj poniższy przykład tworzy grupę zasobów w regionie Europy Zachodniej hello.</span><span class="sxs-lookup"><span data-stu-id="f9e00-135">hello following example creates a resource group in hello West Europe region.</span></span> <span data-ttu-id="f9e00-136">Wybierz unikatową nazwę grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="f9e00-136">Choose a unique name for hello resource group.</span></span>

<span data-ttu-id="f9e00-137">Jeśli korzystasz z powłoki chmury Azure, kliknij przycisk **spróbuj on**, wykonaj toologin wyświetlanymi na ekranie powitania, a następnie skopiuj hello polecenie w wierszu polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="f9e00-137">If you are using Azure Cloud Shell, click **Try It**, follow hello onscreen prompts toologin, then copy hello command into hello command prompt.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="f9e00-138">Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f9e00-138">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="f9e00-139">Tworzenie konta bazy danych Azure rozwiązania Cosmos z hello [az cosmosdb utworzyć](/cli/azure/cosmosdb#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9e00-139">Create an Azure Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="f9e00-140">W hello następujące polecenia, należy zastąpić własną unikatową nazwę konta bazy danych Azure rozwiązania Cosmos której występuje hello `<cosmosdb-name>` symbolu zastępczego.</span><span class="sxs-lookup"><span data-stu-id="f9e00-140">In hello following command, please substitute your own unique Azure Cosmos DB account name where you see hello `<cosmosdb-name>` placeholder.</span></span> <span data-ttu-id="f9e00-141">Ta nazwa będzie służyć jako część bazy danych Azure rozwiązania Cosmos punktu końcowego (`https://<cosmosdb-name>.documents.azure.com/`), więc nazwa hello musi toobe unikatowy wszystkich kont Azure DB rozwiązania Cosmos na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f9e00-141">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so hello name needs toobe unique across all Azure Cosmos DB accounts in Azure.</span></span> 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="f9e00-142">Witaj `--kind MongoDB` parametru zapewnia połączeń klienckich bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f9e00-142">hello `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="f9e00-143">Po utworzeniu konta bazy danych Azure rozwiązania Cosmos hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f9e00-143">When hello Azure Cosmos DB account is created, hello Azure CLI shows information similar toohello following example.</span></span> 

> [!NOTE]
> <span data-ttu-id="f9e00-144">W tym przykładzie używane JSON jako hello Azure CLI format wyjściowy hello domyślne.</span><span class="sxs-lookup"><span data-stu-id="f9e00-144">This example uses JSON as hello Azure CLI output format, which is hello default.</span></span> <span data-ttu-id="f9e00-145">toouse output inny format, zobacz [formatów poleceń Azure CLI 2.0](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f9e00-145">toouse another output format, see [Output formats for Azure CLI 2.0 commands](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span></span>

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a><span data-ttu-id="f9e00-146">Połączenia bazy danych toohello aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="f9e00-146">Connect your Node.js application toohello database</span></span>

<span data-ttu-id="f9e00-147">W tym kroku połączenie MEAN.js przykładowej bazy danych aplikacji tooan bazy danych Azure rozwiązania Cosmos utworzony, przy użyciu parametrów połączenia bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f9e00-147">In this step, you connect your MEAN.js sample application tooan Azure Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="f9e00-148">Konfigurowanie parametrów połączenia hello w aplikacji Node.js</span><span class="sxs-lookup"><span data-stu-id="f9e00-148">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="f9e00-149">W repozytorium MEAN.js otwórz plik `config/env/local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="f9e00-149">In your MEAN.js repository, open `config/env/local-development.js`.</span></span>

<span data-ttu-id="f9e00-150">Zastąp hello następującego kodu hello zawartości tego pliku.</span><span class="sxs-lookup"><span data-stu-id="f9e00-150">Replace hello content of this file with hello following code.</span></span> <span data-ttu-id="f9e00-151">Tooalso Zastąp hello dwa upewnij się, `<cosmosdb-name>` symbole zastępcze nazwą konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f9e00-151">Be sure tooalso replace hello two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span></span>

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a><span data-ttu-id="f9e00-152">Pobierz klucz hello</span><span class="sxs-lookup"><span data-stu-id="f9e00-152">Retrieve hello key</span></span>

<span data-ttu-id="f9e00-153">W kolejności tooconnect tooan bazy danych Azure rozwiązania Cosmos bazy danych należy hello klucza bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f9e00-153">In order tooconnect tooan Azure Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="f9e00-154">Użyj hello [az cosmosdb listy kluczy](/cli/azure/cosmosdb#list-keys) klucz podstawowy hello tooretrieve polecenia.</span><span class="sxs-lookup"><span data-stu-id="f9e00-154">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

<span data-ttu-id="f9e00-155">Hello Azure CLI generuje informacje toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f9e00-155">hello Azure CLI outputs information similar toohello following example.</span></span> 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

<span data-ttu-id="f9e00-156">Skopiuj wartość hello `primaryMasterKey`.</span><span class="sxs-lookup"><span data-stu-id="f9e00-156">Copy hello value of `primaryMasterKey`.</span></span> <span data-ttu-id="f9e00-157">Wklej to za pośrednictwem hello `<primary_master_key>` w `local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="f9e00-157">Paste this over hello  `<primary_master_key>` in `local-development.js`.</span></span>

<span data-ttu-id="f9e00-158">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="f9e00-158">Save your changes.</span></span>

### <a name="run-hello-application-again"></a><span data-ttu-id="f9e00-159">Uruchom ponownie aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="f9e00-159">Run hello application again.</span></span>

<span data-ttu-id="f9e00-160">Uruchom ponownie polecenie `npm start`.</span><span class="sxs-lookup"><span data-stu-id="f9e00-160">Run `npm start` again.</span></span> 

```bash
npm start
```

<span data-ttu-id="f9e00-161">Komunikat konsoli powinna teraz informujące, że środowisko projektowe hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="f9e00-161">A console message should now tell you that hello development environment is up and running.</span></span> 

<span data-ttu-id="f9e00-162">Przejdź do zbyt`http://localhost:3000` w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="f9e00-162">Navigate too`http://localhost:3000` in a browser.</span></span> <span data-ttu-id="f9e00-163">Kliknij przycisk **Utwórz konto** w górnego menu i spróbuj toocreate hello fikcyjny dwóch użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f9e00-163">Click **Sign Up** in hello top menu and try toocreate two dummy users.</span></span> 

<span data-ttu-id="f9e00-164">Witaj MEAN.js Przykładowa aplikacja przechowuje dane użytkownika w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="f9e00-164">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="f9e00-165">Jeśli pomyślnie i MEAN.js automatycznie zaloguje się do hello utworzony użytkownik, a następnie połączenie bazy danych Azure rozwiązania Cosmos działa.</span><span class="sxs-lookup"><span data-stu-id="f9e00-165">If you are successful and MEAN.js automatically signs into hello created user, then your Azure Cosmos DB connection is working.</span></span> 

![MEAN.js pomyślnie łączy tooMongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a><span data-ttu-id="f9e00-167">Wyświetlanie danych w Eksploratorze danych</span><span class="sxs-lookup"><span data-stu-id="f9e00-167">View data in Data Explorer</span></span>

<span data-ttu-id="f9e00-168">Dane przechowywane przez bazy danych Azure rozwiązania Cosmos jest dostępne tooview, zapytań i wykonywania logiki biznesowej w w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f9e00-168">Data stored by an Azure Cosmos DB is available tooview, query, and run business-logic on in hello Azure portal.</span></span>

<span data-ttu-id="f9e00-169">tooview, zapytań i pracować z danymi użytkownika hello utworzone hello poprzedniego kroku, logowania toohello [portalu Azure](https://portal.azure.com) w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="f9e00-169">tooview, query, and work with hello user data created in hello previous step, login toohello [Azure portal](https://portal.azure.com) in your web browser.</span></span>

<span data-ttu-id="f9e00-170">W polu wyszukiwania górnego hello wpisz bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f9e00-170">In hello top Search box, type Azure Cosmos DB.</span></span> <span data-ttu-id="f9e00-171">Po otwarciu bloku konta usługi Cosmos DB wybierz swoje konto usługi Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f9e00-171">When your Cosmos DB account blade opens, select your Cosmos DB account.</span></span> <span data-ttu-id="f9e00-172">W hello lewy pasek nawigacyjny kliknij przycisk Eksploratora danych.</span><span class="sxs-lookup"><span data-stu-id="f9e00-172">In hello left navigation, click Data Explorer.</span></span> <span data-ttu-id="f9e00-173">Rozwiń w okienku Kolekcje hello kolekcji, a następnie można wyświetlać dokumenty hello w kolekcji hello, dane hello kwerendy i nawet utworzyć i uruchomić procedur składowanych, wyzwalaczy i funkcji UDF.</span><span class="sxs-lookup"><span data-stu-id="f9e00-173">Expand your collection in hello Collections pane, and then you can view hello documents in hello collection, query hello data, and even create and run stored procedures, triggers, and UDFs.</span></span> 

![Eksplorator danych w hello portalu Azure](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a><span data-ttu-id="f9e00-175">Wdrażanie tooAzure aplikacji Node.js hello</span><span class="sxs-lookup"><span data-stu-id="f9e00-175">Deploy hello Node.js application tooAzure</span></span>

<span data-ttu-id="f9e00-176">W tym kroku możesz wdrożyć tooAzure aplikacji programu Node.js połączenia bazy danych MongoDB DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f9e00-176">In this step, you deploy your MongoDB-connected Node.js application tooAzure Cosmos DB.</span></span>

<span data-ttu-id="f9e00-177">Można zauważyć czy plik konfiguracyjny hello, który został zmodyfikowany wcześniej jest przeznaczony dla środowiska deweloperskiego hello (`/config/env/local-development.js`).</span><span class="sxs-lookup"><span data-stu-id="f9e00-177">You may have noticed that hello configuration file that you changed earlier is for hello development environment (`/config/env/local-development.js`).</span></span> <span data-ttu-id="f9e00-178">Podczas wdrażania tooApp Twojej aplikacji usługi, domyślnie jest uruchamiana w środowisku produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="f9e00-178">When you deploy your application tooApp Service, it will run in hello production environment by default.</span></span> <span data-ttu-id="f9e00-179">Dlatego teraz należy toomake hello same zmiany toohello odpowiednich konfiguracji pliku.</span><span class="sxs-lookup"><span data-stu-id="f9e00-179">So now, you need toomake hello same change toohello respective configuration file.</span></span>

<span data-ttu-id="f9e00-180">W repozytorium MEAN.js otwórz plik `config/env/production.js`.</span><span class="sxs-lookup"><span data-stu-id="f9e00-180">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="f9e00-181">W hello `db` obiektów, zastąp wartość hello `uri` jako Pokaż w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f9e00-181">In hello `db` object, replace hello value of `uri` as show in hello following example.</span></span> <span data-ttu-id="f9e00-182">Należy się tooreplace hello symbole zastępcze jako przed.</span><span class="sxs-lookup"><span data-stu-id="f9e00-182">Be sure tooreplace hello placeholders as before.</span></span>

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> <span data-ttu-id="f9e00-183">Witaj `ssl=true` opcji ważne jest, ponieważ [bazy danych rozwiązania Cosmos Azure wymaga protokołu SSL](connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="f9e00-183">hello `ssl=true` option is important because [Azure Cosmos DB requires SSL](connect-mongodb-account.md#connection-string-requirements).</span></span> 
>
>

<span data-ttu-id="f9e00-184">W terminalu hello Zatwierdź wszystkie zmiany do Git.</span><span class="sxs-lookup"><span data-stu-id="f9e00-184">In hello terminal, commit all your changes into Git.</span></span> <span data-ttu-id="f9e00-185">Możesz kopiować zarówno toorun polecenia je razem.</span><span class="sxs-lookup"><span data-stu-id="f9e00-185">You can copy both commands toorun them together.</span></span>

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a><span data-ttu-id="f9e00-186">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="f9e00-186">Clean up resources</span></span>

<span data-ttu-id="f9e00-187">Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f9e00-187">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="f9e00-188">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="f9e00-188">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="f9e00-189">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="f9e00-189">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9e00-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9e00-190">Next steps</span></span>

<span data-ttu-id="f9e00-191">W tym szybkiego startu, kiedy znasz już jak toocreate bazy danych Azure rozwiązania Cosmos konta, a następnie utwórz kolekcję bazy danych MongoDB przy użyciu hello Eksploratora danych.</span><span class="sxs-lookup"><span data-stu-id="f9e00-191">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and create a MongoDB collection using hello Data Explorer.</span></span> <span data-ttu-id="f9e00-192">Teraz można migrować tooAzure danych z bazy danych MongoDB DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f9e00-192">You can now migrate your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9e00-193">Importowanie danych z bazy danych MongoDB do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f9e00-193">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
