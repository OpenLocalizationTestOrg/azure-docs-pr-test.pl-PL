---
title: "Azure Cosmos DB: Budowanie aplikacji za pomocą oprogramowania Node.js i interfejsu API usługi DocumentDB | Microsoft Docs"
description: "Przykładowy kod platformy Node.js, którego można użyć do nawiązywania połączenia z interfejsem API usługi DocumentDB usługi Azure Cosmos DB i do wykonywania w niej zapytań"
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
ms.openlocfilehash: 26e3548bf6aacbc60c4c46a5cc88749ca14cec01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-the-azure-portal"></a><span data-ttu-id="a4fc5-103">Azure Cosmos DB: Budowanie aplikacji interfejsu API usługi DocumentDB za pomocą oprogramowania Node.js i witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a4fc5-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and the Azure portal</span></span>

<span data-ttu-id="a4fc5-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="a4fc5-105">Dzięki wykorzystaniu dystrybucji globalnej i możliwości skalowania poziomego opartego na usłudze Azure Cosmos DB, można szybko tworzyć i za pomocą zapytań badać bazy danych dokumentów, par klucz/wartość i grafów.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="a4fc5-106">Ten przewodnik Szybki start przedstawia sposób tworzenia konta usługi Azure Cosmos DB, bazy danych dokumentów i kolekcji przy użyciu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="a4fc5-107">Następnie za pomocą [interfejsu API usługi DocumentDB oprogramowania Node.js](documentdb-sdk-node.md) zbudujesz i uruchomisz aplikację konsoli.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-107">You then build and run a console app built on the [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4fc5-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a4fc5-108">Prerequisites</span></span>

* <span data-ttu-id="a4fc5-109">Przed uruchomieniem tego przykładu muszą być spełnione następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="a4fc5-109">Before you can run this sample, you must have the following prerequisites:</span></span>
    * <span data-ttu-id="a4fc5-110">[Node.js](https://nodejs.org/en/) w wersji 0.10.29 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="a4fc5-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="a4fc5-111">Git</span><span class="sxs-lookup"><span data-stu-id="a4fc5-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="a4fc5-112">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="a4fc5-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="a4fc5-113">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="a4fc5-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="a4fc5-114">Klonowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="a4fc5-114">Clone the sample application</span></span>

<span data-ttu-id="a4fc5-115">Teraz sklonujemy aplikację interfejsu API usługi DocumentDB z repozytorium github, ustawimy parametry połączenia i uruchomimy ją.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-115">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="a4fc5-116">Zobaczysz, jak łatwo jest pracować programowo z danymi.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-116">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="a4fc5-117">Otwórz okno terminalu usługi Git, na przykład git bash, i za pomocą polecenia `CD` przejdź do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-117">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="a4fc5-118">Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-118">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="a4fc5-119">Przeglądanie kodu</span><span class="sxs-lookup"><span data-stu-id="a4fc5-119">Review the code</span></span>

<span data-ttu-id="a4fc5-120">Dokonajmy szybkiego przeglądu działań wykonywanych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-120">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="a4fc5-121">Gdy otworzysz plik `app.js`, zobaczysz, że następujące wiersze kodu tworzą zasoby usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-121">Open the `app.js` file and you find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="a4fc5-122">Inicjowanie obiektu `documentClient`.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-122">The `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="a4fc5-123">Tworzenie nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="a4fc5-124">Tworzenie nowej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="a4fc5-125">Tworzenie kilku dokumentów.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="a4fc5-126">Wykonywanie zapytania SQL w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-126">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="a4fc5-127">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="a4fc5-127">Update your connection string</span></span>

<span data-ttu-id="a4fc5-128">Teraz wróć do witryny Azure Portal, aby uzyskać informacje o parametrach połączenia i skopiować je do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-128">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="a4fc5-129">W witrynie [Azure Portal](http://portal.azure.com/), korzystając ze swojego konta usługi Azure Cosmos DB, kliknij na lewym panelu nawigacyjnym pozycję **Klucze**, a następnie pozycję **Klucze odczytu i zapisu**.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-129">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="a4fc5-130">W następnym kroku, korzystając z przycisków kopiowania dostępnych po prawej stronie ekranu, skopiujesz identyfikator URI i klucz podstawowy do pliku `config.js`.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-130">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `config.js` file in the next step.</span></span>

    ![Wyświetlanie i kopiowanie klucza dostępu w witrynie Azure Portal, blok Klucze](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="a4fc5-132">Otwórz plik `config.js`.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-132">In Open the `config.js` file.</span></span> 

3. <span data-ttu-id="a4fc5-133">Skopiuj wartość identyfikatora URI z portalu (przy użyciu przycisku kopiowania) i przypisz ją do klucza endpoint w pliku `config.js`.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-133">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="a4fc5-134">Następnie skopiuj wartość klucza podstawowego z portalu i przypisz ją do klucza `config.primaryKey` w pliku `config.js`.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-134">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="a4fc5-135">Aplikacja została zaktualizowana i zawiera teraz wszystkie informacje potrzebne do nawiązania komunikacji z usługą Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-135">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="a4fc5-136">Uruchomienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="a4fc5-136">Run the app</span></span>
1. <span data-ttu-id="a4fc5-137">Uruchom polecenie `npm install` w terminalu, aby zainstalować wymagane moduły npm.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-137">Run `npm install` in a terminal to install required npm modules</span></span>

2. <span data-ttu-id="a4fc5-138">Uruchom polecenie `node app.js` w terminalu, aby uruchomić aplikację Node.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-138">Run `node app.js` in a terminal to start your node application.</span></span>

<span data-ttu-id="a4fc5-139">Teraz można wrócić do Eksploratora danych i zobaczyć, jak się pracuje z nowymi danymi, modyfikuje je i tworzy zapytania o nie.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-139">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="a4fc5-140">Przeglądanie umów SLA w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a4fc5-140">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="a4fc5-141">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="a4fc5-141">Clean up resources</span></span>

<span data-ttu-id="a4fc5-142">Jeśli nie zamierzasz w przyszłości korzystać z tej aplikacji, wykonaj następujące czynności, aby usunąć wszystkie zasoby utworzone w witrynie Azure Portal w ramach tego przewodnika Szybki start:</span><span class="sxs-lookup"><span data-stu-id="a4fc5-142">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="a4fc5-143">W menu znajdującym się po lewej stronie w witrynie Azure Portal kliknij pozycję **Grupy zasobów**, a następnie kliknij nazwę utworzonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-143">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="a4fc5-144">Na stronie grupy zasobów kliknij pozycję **Usuń**, wpisz w polu tekstowym nazwę zasobu do usunięcia, a następnie kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-144">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4fc5-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a4fc5-145">Next steps</span></span>

<span data-ttu-id="a4fc5-146">W tym przewodniku Szybki start wyjaśniono sposób tworzenia konta usługi Azure Cosmos DB, tworzenia kolekcji za pomocą Eksploratora danych i uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-146">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="a4fc5-147">Teraz możesz zaimportować dodatkowe dane do swojego konta usługi Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a4fc5-147">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="a4fc5-148">Importowanie danych do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a4fc5-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


