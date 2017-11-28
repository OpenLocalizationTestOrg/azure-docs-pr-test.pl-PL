---
title: "Tworzenie aplikacji Node.js usługi Azure Cosmos DB za pomocą interfejsu API programu Graph | Microsoft Docs"
description: "Przykładowy kod Node.js, którego można używać do nawiązywania połączeń z usługą Azure Cosmos DB i wykonywania w niej zapytań"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 6d14719938af0ce825955389824441e111024869
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a><span data-ttu-id="5b3f1-103">Azure Cosmos DB: Tworzenie aplikacji Node.js za pomocą interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="5b3f1-103">Azure Cosmos DB: Build a Node.js application by using Graph API</span></span>

<span data-ttu-id="5b3f1-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-104">Azure Cosmos DB is the globally distributed multi-model database service from Microsoft.</span></span> <span data-ttu-id="5b3f1-105">Dzięki wykorzystaniu dystrybucji globalnej i możliwości skalowania poziomego opartego na usłudze Azure Cosmos DB, można szybko tworzyć i za pomocą zapytań badać bazy danych dokumentów, par klucz/wartość i grafów.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="5b3f1-106">Ten artykuł Szybki start przedstawia sposób tworzenia konta usługi Azure Cosmos DB dla interfejsu API programu Graph (wersja zapoznawcza), bazy danych i grafu przy użyciu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-106">This quick-start article demonstrates how to create an Azure Cosmos DB account for Graph API (preview), database, and graph by using the Azure portal.</span></span> <span data-ttu-id="5b3f1-107">Następnie przy użyciu sterownika open source [Node.js Gremlin](https://www.npmjs.com/package/gremlin-secure) zostanie utworzona i uruchomiona aplikacja konsoli.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-107">You then build and run a console app by using the open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span></span>  

> [!NOTE]
> <span data-ttu-id="5b3f1-108">Moduł npm `gremlin-secure` to zmodyfikowana wersja modułu `gremlin` z obsługą SSL i SASL wymaganych do łączenia się z bazą danych Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-108">The npm module `gremlin-secure` is a modified version of `gremlin` module, with support for SSL and SASL required for connecting with Azure Cosmos DB.</span></span> <span data-ttu-id="5b3f1-109">Kod źródłowy jest dostępny w usłudze [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span><span class="sxs-lookup"><span data-stu-id="5b3f1-109">Source code is available on [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="5b3f1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5b3f1-110">Prerequisites</span></span>

<span data-ttu-id="5b3f1-111">Przed uruchomieniem tego przykładu muszą być spełnione następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="5b3f1-111">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="5b3f1-112">[Node.js](https://nodejs.org/en/) w wersji 0.10.29 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="5b3f1-112">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span></span>
* [<span data-ttu-id="5b3f1-113">Git</span><span class="sxs-lookup"><span data-stu-id="5b3f1-113">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="5b3f1-114">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="5b3f1-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="5b3f1-115">Dodawanie grafu</span><span class="sxs-lookup"><span data-stu-id="5b3f1-115">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="5b3f1-116">Klonowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="5b3f1-116">Clone the sample application</span></span>

<span data-ttu-id="5b3f1-117">Teraz sklonujemy aplikację interfejsu API programu Graph z repozytorium GitHub, ustawimy parametry połączenia i uruchomimy ją.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-117">Now let's clone a Graph API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="5b3f1-118">Zobaczysz, jak łatwo jest pracować programowo z danymi.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-118">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="5b3f1-119">Otwórz okno terminala usługi Git, na przykład Git Bash, i za pomocą polecenia `cd` przejdź do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-119">Open a Git terminal window, such as Git Bash, and change (via `cd` command) to a working directory.</span></span>  

2. <span data-ttu-id="5b3f1-120">Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-120">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. <span data-ttu-id="5b3f1-121">Otwórz plik rozwiązania w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-121">Open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="5b3f1-122">Przeglądanie kodu</span><span class="sxs-lookup"><span data-stu-id="5b3f1-122">Review the code</span></span>

<span data-ttu-id="5b3f1-123">Dokonajmy szybkiego przeglądu działań wykonywanych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-123">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="5b3f1-124">Otwórz plik `app.js`, w którym znajdziesz następujące wiersze kodu.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-124">Open the `app.js` file, and you'll find the following lines of code.</span></span> 

* <span data-ttu-id="5b3f1-125">Tworzenie klienta języka Gremlin.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-125">The Gremlin client is created.</span></span>

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  <span data-ttu-id="5b3f1-126">Wszystkie konfiguracje są w pliku `config.js`, który będziemy edytować w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-126">The configurations are all in `config.js`, which we edit in the following section.</span></span>

* <span data-ttu-id="5b3f1-127">Seria kroków języka Gremlin jest wykonywana przy użyciu metody `client.execute`.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-127">A series of Gremlin steps are executed with the `client.execute` method.</span></span>

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="5b3f1-128">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="5b3f1-128">Update your connection string</span></span>

1. <span data-ttu-id="5b3f1-129">Otwórz plik config.js.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-129">Open the config.js file.</span></span> 

2. <span data-ttu-id="5b3f1-130">W pliku Config.js przypisz kluczowi config.endpoint wartość **Identyfikator URI Gremlin** ze strony **Przegląd** w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-130">In config.js, fill in the config.endpoint key with the **Gremlin URI** value from the **Overview** page of the Azure portal.</span></span> 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Wyświetlanie i kopiowanie klucza dostępu w witrynie Azure Portal, blok Klucze](./media/create-graph-nodejs/gremlin-uri.png)

   <span data-ttu-id="5b3f1-132">Jeśli wartość **Identyfikator URI Gremlin** jest pusta, na stronie **Klucze** w portalu możesz wygenerować tę wartość przy użyciu pozycji **Identyfikator URI** wartości, usuwając ciąg https:// i zmieniając dokumenty na grafy.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-132">If the **Gremlin URI** value is blank, you can generate the value from the **Keys** page in the portal, using the **URI** value, removing https://, and changing documents to graphs.</span></span>

   <span data-ttu-id="5b3f1-133">Punkt końcowy Gremlin musi być samą nazwą hosta, bez protokołu/numeru portu, czyli powinien mieć postać `mygraphdb.graphs.azure.com` (a nie `https://mygraphdb.graphs.azure.com` lub `mygraphdb.graphs.azure.com:433`).</span><span class="sxs-lookup"><span data-stu-id="5b3f1-133">The Gremlin endpoint must be only the host name without the protocol/port number, like `mygraphdb.graphs.azure.com` (not `https://mygraphdb.graphs.azure.com` or `mygraphdb.graphs.azure.com:433`).</span></span>

3. <span data-ttu-id="5b3f1-134">W pliku config.js przypisz elementowi config.primaryKey wartość z pola **Klucz podstawowy** na stronie **Klucze** w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-134">In config.js, fill in the config.primaryKey value in with the **Primary Key** value from the **Keys** page of the Azure portal.</span></span> 

    `config.primaryKey = "PRIMARYKEY";`

   ![Blok Klucze w witrynie Azure Portal](./media/create-graph-nodejs/keys.png)

4. <span data-ttu-id="5b3f1-136">Wprowadź nazwę bazy danych i nazwę grafu (kontenera) dla wartości parametrów config.database i config.collection.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-136">Enter the database name, and graph (container) name for the value of config.database and config.collection.</span></span> 

<span data-ttu-id="5b3f1-137">Oto przykład wypełnionego pliku config.js:</span><span class="sxs-lookup"><span data-stu-id="5b3f1-137">Here is an example of what your completed config.js file should look like:</span></span>

```nodejs
var config = {}

// Note that this must not have HTTPS or the port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-the-console-app"></a><span data-ttu-id="5b3f1-138">Uruchamianie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="5b3f1-138">Run the console app</span></span>

1. <span data-ttu-id="5b3f1-139">Otwórz okno terminala i za pomocą polecenia `cd` przejdź do katalogu instalacyjnego pliku package.json uwzględnionego w projekcie.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-139">Open a terminal window and change (via `cd` command) to the installation directory for the package.json file that's included in the project.</span></span>  

2. <span data-ttu-id="5b3f1-140">Uruchom polecenie `npm install`, aby zainstalować wymagane moduły npm, w tym `gremlin-secure`.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-140">Run `npm install` to install the required npm modules, including `gremlin-secure`.</span></span>

3. <span data-ttu-id="5b3f1-141">Uruchom polecenie `node app.js` w terminalu, aby uruchomić aplikację Node.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-141">Run `node app.js` in a terminal to start your node application.</span></span>

## <a name="browse-with-data-explorer"></a><span data-ttu-id="5b3f1-142">Przeglądanie w Eksploratorze danych</span><span class="sxs-lookup"><span data-stu-id="5b3f1-142">Browse with Data Explorer</span></span>

<span data-ttu-id="5b3f1-143">Teraz możesz wrócić do Eksploratora danych w witrynie Azure Portal, aby wyświetlać nowe dane grafu, wykonywać o nie zapytania, modyfikować je i pracować z nimi.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-143">You can now go back to Data Explorer in the Azure portal to view, query, modify, and work with your new graph data.</span></span>

<span data-ttu-id="5b3f1-144">W Eksploratorze danych nowa baza danych jest wyświetlana w okienku **Grafy**.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-144">In Data Explorer, the new database appears in the **Graphs** pane.</span></span> <span data-ttu-id="5b3f1-145">Rozwiń bazę danych, a następnie kolekcję i kliknij pozycję **Graf**.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-145">Expand the database, followed by the collection, then click **Graph**.</span></span>

<span data-ttu-id="5b3f1-146">Dane generowane przez aplikację przykładową będą wyświetlane w kolejnym okienku na karcie **Graf**, gdy klikniesz przycisk **Zastosuj filtr**.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-146">The data generated by the sample app is displayed in the next pane within the **Graph** tab when you click **Apply Filter**.</span></span>

<span data-ttu-id="5b3f1-147">Spróbuj uzupełnić wartość `g.V()` ciągiem `.has('firstName', 'Thomas')`, aby przetestować filtr.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-147">Try completing `g.V()` with `.has('firstName', 'Thomas')` to test the filter.</span></span> <span data-ttu-id="5b3f1-148">Pamiętaj, że w wartości jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-148">Do note that the value is case sensitive.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="5b3f1-149">Przeglądanie umów SLA w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5b3f1-149">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a><span data-ttu-id="5b3f1-150">Czyszczenie zasobów</span><span class="sxs-lookup"><span data-stu-id="5b3f1-150">Clean up your resources</span></span>

<span data-ttu-id="5b3f1-151">Jeśli nie planujesz dalszego korzystania z tej aplikacji, usuń wszystkie zasoby utworzone zgodnie z tym artykułem, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5b3f1-151">If you do not plan to continue using this app, delete all resources that you created in this article by doing the following:</span></span> 

1. <span data-ttu-id="5b3f1-152">W menu nawigacji po lewej stronie w witrynie Azure Portal kliknij pozycję **Grupy zasobów**, a następnie kliknij nazwę utworzonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-152">In the Azure portal, on the left navigation menu, click **Resource groups**, and then click the name of the resource that you created.</span></span> 
2. <span data-ttu-id="5b3f1-153">Na stronie grupy zasobów kliknij pozycję **Usuń**, wpisz nazwę zasobu do usunięcia, a następnie kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-153">On your resource group page, click **Delete**, type the name of the resource to be deleted, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b3f1-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5b3f1-154">Next steps</span></span>

<span data-ttu-id="5b3f1-155">W tym artykule wyjaśniono sposób tworzenia konta usługi Azure Cosmos DB, tworzenia grafu za pomocą Eksploratora danych i uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-155">In this article, you've learned how to create an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span></span> <span data-ttu-id="5b3f1-156">Teraz możesz tworzyć bardziej złożone zapytania i implementować zaawansowaną logikę przechodzenia grafu za pomocą języka Gremlin.</span><span class="sxs-lookup"><span data-stu-id="5b3f1-156">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="5b3f1-157">Wykonywanie zapytań przy użyciu języka Gremlin</span><span class="sxs-lookup"><span data-stu-id="5b3f1-157">Query using Gremlin</span></span>](tutorial-query-graph.md)
