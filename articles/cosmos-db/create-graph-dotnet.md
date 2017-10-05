---
title: "Tworzenie aplikacji .NET usługi Azure Cosmos DB za pomocą interfejsu API programu Graph | Microsoft Docs"
description: "Przykładowy kod programu .NET, którego można używać do nawiązywania połączeń z usługą Azure Cosmos DB i wykonywania w niej zapytań"
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
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: a973b81ea5b06c5826cc31c399aae9dec43f5b72
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-the-graph-api"></a><span data-ttu-id="905f1-103">Azure Cosmos DB: Tworzenie aplikacji .NET za pomocą interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="905f1-103">Azure Cosmos DB: Build a .NET application using the Graph API</span></span>

<span data-ttu-id="905f1-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="905f1-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="905f1-105">Dzięki wykorzystaniu dystrybucji globalnej i możliwości skalowania poziomego opartego na usłudze Azure Cosmos DB, można szybko tworzyć i za pomocą zapytań badać bazy danych dokumentów, par klucz/wartość i grafów.</span><span class="sxs-lookup"><span data-stu-id="905f1-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="905f1-106">Ten przewodnik Szybki start przedstawia sposób tworzenia konta usługi Azure Cosmos DB, bazy danych i grafu (kontenera) przy użyciu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="905f1-106">This quick start demonstrates how to create an Azure Cosmos DB account, database, and graph (container) using the Azure portal.</span></span> <span data-ttu-id="905f1-107">Następnie przy użyciu [interfejsu API programu Graph](graph-sdk-dotnet.md) (wersja zapoznawcza) zostanie utworzona i uruchomiona aplikacja konsolowa.</span><span class="sxs-lookup"><span data-stu-id="905f1-107">You then build and run a console app built on the [Graph API](graph-sdk-dotnet.md) (preview).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="905f1-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="905f1-108">Prerequisites</span></span>

<span data-ttu-id="905f1-109">Jeśli nie masz jeszcze zainstalowanego programu Visual Studio 2017, możesz pobrać program [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/) i używać go **bezpłatnie**.</span><span class="sxs-lookup"><span data-stu-id="905f1-109">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="905f1-110">Podczas instalacji programu Visual Studio upewnij się, że jest włączona opcja **Programowanie na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="905f1-110">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="905f1-111">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="905f1-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="905f1-112">Dodawanie grafu</span><span class="sxs-lookup"><span data-stu-id="905f1-112">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="905f1-113">Klonowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="905f1-113">Clone the sample application</span></span>

<span data-ttu-id="905f1-114">Teraz sklonujemy aplikację interfejsu API programu Graph z repozytorium GitHub, ustawimy parametry połączenia i uruchomimy ją.</span><span class="sxs-lookup"><span data-stu-id="905f1-114">Now let's clone a Graph API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="905f1-115">Zobaczysz, jak łatwo jest pracować programowo z danymi.</span><span class="sxs-lookup"><span data-stu-id="905f1-115">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="905f1-116">Otwórz okno terminalu usługi Git, na przykład git bash, i za pomocą polecenia `cd` przejdź do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="905f1-116">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="905f1-117">Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="905f1-117">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. <span data-ttu-id="905f1-118">Następnie otwórz program Visual Studio i otwórz plik rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="905f1-118">Then open Visual Studio and open the solution file.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="905f1-119">Przeglądanie kodu</span><span class="sxs-lookup"><span data-stu-id="905f1-119">Review the code</span></span>

<span data-ttu-id="905f1-120">Dokonajmy szybkiego przeglądu działań wykonywanych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="905f1-120">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="905f1-121">Otwórz plik Program.cs i zobacz, że następujące wiersze kodu tworzą zasoby usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="905f1-121">Open the Program.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="905f1-122">Inicjowanie klienta DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="905f1-122">The DocumentClient is initialized.</span></span> <span data-ttu-id="905f1-123">W wersji zapoznawczej dodaliśmy interfejs API rozszerzenia grafu w kliencie usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="905f1-123">In the preview, we added a graph extension API on the Azure Cosmos DB client.</span></span> <span data-ttu-id="905f1-124">Pracujemy nad autonomicznym klientem grafu całkowicie niezależnym od zasobów i klienta usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="905f1-124">We are working on a standalone graph client decoupled from the Azure Cosmos DB client and resources.</span></span>

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* <span data-ttu-id="905f1-125">Tworzenie nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="905f1-125">A new database is created.</span></span>

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* <span data-ttu-id="905f1-126">Tworzenie nowego grafu.</span><span class="sxs-lookup"><span data-stu-id="905f1-126">A new graph is created.</span></span>

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* <span data-ttu-id="905f1-127">Wykonywanie serii kroków języka Gremlin przy użyciu metody `CreateGremlinQuery`.</span><span class="sxs-lookup"><span data-stu-id="905f1-127">A series of Gremlin steps are executed using the `CreateGremlinQuery` method.</span></span>

    ```csharp
    // The CreateGremlinQuery method extensions allow you to execute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="905f1-128">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="905f1-128">Update your connection string</span></span>

<span data-ttu-id="905f1-129">Teraz wróć do witryny Azure Portal, aby uzyskać informacje o parametrach połączenia i skopiować je do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="905f1-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="905f1-130">W programie Visual Studio 2017 otwórz plik App.config.</span><span class="sxs-lookup"><span data-stu-id="905f1-130">In Visual Studio 2017, open the App.config file.</span></span> 

2. <span data-ttu-id="905f1-131">W witrynie Azure Portal, korzystając ze swojego konta usługi Azure Cosmos DB, kliknij pozycję **Klucze** na lewym panelu nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="905f1-131">In the Azure portal, in your Azure Cosmos DB account, click **Keys** in the left navigation.</span></span> 

    ![Wyświetlanie i kopiowanie klucza podstawowego w witrynie Azure Portal, na stronie Klucze](./media/create-graph-dotnet/keys.png)

3. <span data-ttu-id="905f1-133">Skopiuj wartość **Identyfikator URI** z portalu i przypisz ją do klucza punktu końcowego w pliku App.config.</span><span class="sxs-lookup"><span data-stu-id="905f1-133">Copy your **URI** value from the portal and make it the value of the Endpoint key in App.config.</span></span> <span data-ttu-id="905f1-134">Aby skopiować wartość, możesz użyć przycisku kopiowania, jak pokazano na poprzednim zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="905f1-134">You can use the copy button as shown in the preceding screenshot to copy the value.</span></span>

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. <span data-ttu-id="905f1-135">Skopiuj wartość **KLUCZ PODSTAWOWY** z portalu i przypisz ją do klucza AuthKey w pliku App.config, a następnie zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="905f1-135">Copy your **PRIMARY KEY** value from the portal, and make it the value of the AuthKey key in App.config, then save your changes.</span></span> 

    `<add key="AuthKey" value="FILLME" />`

<span data-ttu-id="905f1-136">Aplikacja została zaktualizowana i zawiera teraz wszystkie informacje potrzebne do nawiązania komunikacji z usługą Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="905f1-136">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="run-the-console-app"></a><span data-ttu-id="905f1-137">Uruchamianie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="905f1-137">Run the console app</span></span>

1. <span data-ttu-id="905f1-138">W programie Visual Studio kliknij prawym przyciskiem myszy projekt **GraphGetStarted** w **Eksploratorze rozwiązań**, a następnie kliknij polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="905f1-138">In Visual Studio, right-click on the **GraphGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="905f1-139">W polu **Przeglądaj** obszaru pakietów NuGet wpisz ciąg *Microsoft.Azure.Graphs* i zaznacz pole **Obejmuje wersje wstępne**.</span><span class="sxs-lookup"><span data-stu-id="905f1-139">In the NuGet **Browse** box, type *Microsoft.Azure.Graphs* and check the **Includes prerelease** box.</span></span> 

3. <span data-ttu-id="905f1-140">Korzystając z wyników, zainstaluj bibliotekę **Microsoft.Azure.Graphs**.</span><span class="sxs-lookup"><span data-stu-id="905f1-140">From the results, install the **Microsoft.Azure.Graphs** library.</span></span> <span data-ttu-id="905f1-141">Spowoduje to zainstalowanie pakietu biblioteki rozszerzenia grafu usługi Azure Cosmos DB oraz wszystkich jego zależności.</span><span class="sxs-lookup"><span data-stu-id="905f1-141">This installs the Azure Cosmos DB graph extension library package and all dependencies.</span></span>

    <span data-ttu-id="905f1-142">Jeśli zostanie wyświetlony komunikat dotyczący przejrzenia zmian wprowadzonych w rozwiązaniu, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="905f1-142">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="905f1-143">Jeśli wyświetlany jest komunikat o akceptacji licencji, kliknij pozycję **Akceptuję**.</span><span class="sxs-lookup"><span data-stu-id="905f1-143">If you get a message about license acceptance, click **I accept**.</span></span>

4. <span data-ttu-id="905f1-144">Naciśnij klawisze CTRL + F5, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="905f1-144">Click CTRL + F5 to run the application.</span></span>

   <span data-ttu-id="905f1-145">W oknie konsoli będą widoczne wierzchołki i krawędzie dodawane do grafu.</span><span class="sxs-lookup"><span data-stu-id="905f1-145">The console window displays the vertexes and edges being added to the graph.</span></span> <span data-ttu-id="905f1-146">Po zakończeniu działania skryptu naciśnij klawisz ENTER dwa razy, aby zamknąć okno konsoli.</span><span class="sxs-lookup"><span data-stu-id="905f1-146">When the script completes, press ENTER twice to close the console window.</span></span> 

## <a name="browse-using-the-data-explorer"></a><span data-ttu-id="905f1-147">Przeglądanie za pomocą Eksploratora danych</span><span class="sxs-lookup"><span data-stu-id="905f1-147">Browse using the Data Explorer</span></span>

<span data-ttu-id="905f1-148">Teraz możesz wrócić do Eksploratora danych w witrynie Azure Portal, aby przeglądać nowe dane i wykonywać zapytania względem nich.</span><span class="sxs-lookup"><span data-stu-id="905f1-148">You can now go back to Data Explorer in the Azure portal and browse and query your new graph data.</span></span>

1. <span data-ttu-id="905f1-149">W Eksploratorze danych nowa baza danych jest wyświetlana w okienku Grafy.</span><span class="sxs-lookup"><span data-stu-id="905f1-149">In Data Explorer, the new database appears in the Graphs pane.</span></span> <span data-ttu-id="905f1-150">Rozwiń węzeł **graphdb** i **graphcollz**, a następnie kliknij pozycję **Graf**.</span><span class="sxs-lookup"><span data-stu-id="905f1-150">Expand **graphdb**, **graphcollz**, and then click **Graph**.</span></span>

2. <span data-ttu-id="905f1-151">Kliknij przycisk **Zastosuj filtr**, aby użyć domyślnego zapytania do wyświetlenia wszystkich wierzchołków grafu.</span><span class="sxs-lookup"><span data-stu-id="905f1-151">Click the **Apply Filter** button to use the default query to view all the verticies in the graph.</span></span> <span data-ttu-id="905f1-152">Dane wygenerowane przez przykładową aplikację zostaną wyświetlone w okienku Grafy.</span><span class="sxs-lookup"><span data-stu-id="905f1-152">The data generated by the sample app is displayed in the Graphs pane.</span></span>

    <span data-ttu-id="905f1-153">Możesz powiększać i zmniejszać graf, rozszerzać obszar wyświetlania grafu, dodawać kolejne wierzchołki oraz przenosić wierzchołki na wyświetlanej powierzchni.</span><span class="sxs-lookup"><span data-stu-id="905f1-153">You can zoom in and out of the graph, you can expand the graph display space, add additional verticies, and move verticies on the display surface.</span></span>

    ![Wyświetlanie grafu w Eksploratorze danych w witrynie Azure Portal](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="905f1-155">Przeglądanie umów SLA w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="905f1-155">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="905f1-156">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="905f1-156">Clean up resources</span></span>

<span data-ttu-id="905f1-157">Jeśli nie zamierzasz w przyszłości korzystać z tej aplikacji, wykonaj następujące czynności, aby usunąć wszystkie zasoby utworzone w witrynie Azure Portal w ramach tego przewodnika Szybki start:</span><span class="sxs-lookup"><span data-stu-id="905f1-157">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="905f1-158">W menu znajdującym się po lewej stronie w witrynie Azure Portal kliknij pozycję **Grupy zasobów**, a następnie kliknij nazwę utworzonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="905f1-158">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="905f1-159">Na stronie grupy zasobów kliknij pozycję **Usuń**, wpisz w polu tekstowym nazwę zasobu do usunięcia, a następnie kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="905f1-159">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="905f1-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="905f1-160">Next steps</span></span>

<span data-ttu-id="905f1-161">W tym przewodniku Szybki start wyjaśniono sposób tworzenia konta usługi Azure Cosmos DB, tworzenia grafu za pomocą Eksploratora danych i uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="905f1-161">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span></span> <span data-ttu-id="905f1-162">Teraz możesz tworzyć bardziej złożone zapytania i implementować zaawansowaną logikę przechodzenia grafu za pomocą języka Gremlin.</span><span class="sxs-lookup"><span data-stu-id="905f1-162">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="905f1-163">Wykonywanie zapytań przy użyciu języka Gremlin</span><span class="sxs-lookup"><span data-stu-id="905f1-163">Query using Gremlin</span></span>](tutorial-query-graph.md)

