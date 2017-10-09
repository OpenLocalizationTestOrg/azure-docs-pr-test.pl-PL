---
title: "Azure rozwiązania Cosmos bazy danych: Tworzenie aplikacji za pomocą języka Node.js i hello interfejsu API usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod Node.js, można użyć zapytania tooand tooconnect hello interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a><span data-ttu-id="90bb1-103">Azure DB rozwiązania Cosmos: Tworzenie aplikacji interfejsu API usługi DocumentDB za pomocą języka Node.js i hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="90bb1-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and hello Azure portal</span></span>

<span data-ttu-id="90bb1-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="90bb1-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="90bb1-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="90bb1-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="90bb1-106">To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i przy użyciu kolekcji hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="90bb1-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="90bb1-107">Następnie skompilować i uruchomić aplikację konsoli oparty na powitania [interfejsu API środowiska Node.js usługi DocumentDB](documentdb-sdk-node.md).</span><span class="sxs-lookup"><span data-stu-id="90bb1-107">You then build and run a console app built on hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90bb1-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="90bb1-108">Prerequisites</span></span>

* <span data-ttu-id="90bb1-109">Przed uruchomieniem tego przykładu, musi mieć hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="90bb1-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="90bb1-110">[Node.js](https://nodejs.org/en/) w wersji 0.10.29 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="90bb1-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="90bb1-111">Git</span><span class="sxs-lookup"><span data-stu-id="90bb1-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="90bb1-112">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="90bb1-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="90bb1-113">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="90bb1-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="90bb1-114">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="90bb1-114">Clone hello sample application</span></span>

<span data-ttu-id="90bb1-115">Teraz załóżmy aplikacji w klonowania interfejs API usługi DocumentDB z serwisu github, Ustaw ciąg połączenia hello i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="90bb1-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="90bb1-116">Zobacz, jak łatwo jest toowork z danymi programowo.</span><span class="sxs-lookup"><span data-stu-id="90bb1-116">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="90bb1-117">Otwórz okno terminala git, np. git bash, i `CD` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="90bb1-117">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="90bb1-118">Hello uruchom następujące polecenie tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="90bb1-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="90bb1-119">Przejrzyj hello kodu</span><span class="sxs-lookup"><span data-stu-id="90bb1-119">Review hello code</span></span>

<span data-ttu-id="90bb1-120">Upewnijmy szybki przegląd działania wykonywane w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="90bb1-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="90bb1-121">Otwórz hello `app.js` plików i można znaleźć, te wiersze kodu utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="90bb1-121">Open hello `app.js` file and you find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="90bb1-122">Witaj `documentClient` został zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="90bb1-122">hello `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="90bb1-123">Tworzenie nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="90bb1-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="90bb1-124">Tworzenie nowej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="90bb1-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="90bb1-125">Tworzenie kilku dokumentów.</span><span class="sxs-lookup"><span data-stu-id="90bb1-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="90bb1-126">Wykonywanie zapytania SQL w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="90bb1-126">A SQL query over JSON is performed.</span></span>

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="90bb1-127">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="90bb1-127">Update your connection string</span></span>

<span data-ttu-id="90bb1-128">Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="90bb1-128">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="90bb1-129">W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="90bb1-129">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="90bb1-130">Użyjesz przyciski Kopia hello na powitania po prawej stronie powitania toocopy ekranie powitania identyfikatora URI oraz Primary Key do hello `config.js` pliku w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="90bb1-130">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `config.js` file in hello next step.</span></span>

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="90bb1-132">W otwartych hello `config.js` pliku.</span><span class="sxs-lookup"><span data-stu-id="90bb1-132">In Open hello `config.js` file.</span></span> 

3. <span data-ttu-id="90bb1-133">Skopiuj wartość identyfikatora URI z portalu hello (przy użyciu przycisku Kopiuj hello) i przydzielić mu hello wartością klucza punktu końcowego hello `config.js`.</span><span class="sxs-lookup"><span data-stu-id="90bb1-133">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="90bb1-134">Skopiuj wartość klucza podstawowego z portalu hello i stał się hello wartość hello `config.primaryKey` w `config.js`.</span><span class="sxs-lookup"><span data-stu-id="90bb1-134">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="90bb1-135">Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="90bb1-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="90bb1-136">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="90bb1-136">Run hello app</span></span>
1. <span data-ttu-id="90bb1-137">Uruchom `npm install` w terminalu tooinstall wymagane moduły npm</span><span class="sxs-lookup"><span data-stu-id="90bb1-137">Run `npm install` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="90bb1-138">Uruchom `node app.js` w terminalu toostart aplikacji węzła.</span><span class="sxs-lookup"><span data-stu-id="90bb1-138">Run `node app.js` in a terminal toostart your node application.</span></span>

<span data-ttu-id="90bb1-139">Teraz można wrócić do poprzedniej strony tooData Explorer i zobacz zapytania, modyfikowania i pracy z tym nowych danych.</span><span class="sxs-lookup"><span data-stu-id="90bb1-139">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="90bb1-140">Przejrzyj umowy SLA w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="90bb1-140">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="90bb1-141">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="90bb1-141">Clean up resources</span></span>

<span data-ttu-id="90bb1-142">Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="90bb1-142">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="90bb1-143">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="90bb1-143">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="90bb1-144">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="90bb1-144">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90bb1-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90bb1-145">Next steps</span></span>

<span data-ttu-id="90bb1-146">W tym szybkiego startu kiedy znasz już jak utworzyć kolekcję za pomocą Eksploratora danych hello toocreate konto bazy danych Azure rozwiązania Cosmos i uruchamianie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="90bb1-146">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="90bb1-147">Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="90bb1-147">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="90bb1-148">Importowanie danych do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="90bb1-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


