---
title: "Azure rozwiązania Cosmos bazy danych: Tworzenie aplikacji sieci web z platformą .NET i hello interfejsu API usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod .NET, można użyć zapytania tooand tooconnect hello interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB"
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
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="c81d8-103">Azure DB rozwiązania Cosmos: Tworzenie aplikacji sieci web interfejsu API usługi DocumentDB z platformą .NET i hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c81d8-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="c81d8-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c81d8-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="c81d8-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c81d8-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="c81d8-106">To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i przy użyciu kolekcji hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c81d8-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="c81d8-107">Będzie tworzenie i wdrażanie aplikacji sieci web listy todo oparty na powitania [interfejsu API platformy .NET usługi DocumentDB](documentdb-sdk-dotnet.md), jak pokazano w hello następującego zrzutu ekranu.</span><span class="sxs-lookup"><span data-stu-id="c81d8-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in hello following screenshot.</span></span> 

![Aplikacja z listą zadań do wykonania z przykładowymi danymi](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="c81d8-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c81d8-109">Prerequisites</span></span>

<span data-ttu-id="c81d8-110">Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i użyć hello **wolnego** [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c81d8-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="c81d8-111">Upewnij się, że możesz włączyć **Azure programowanie** podczas instalacji programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="c81d8-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="c81d8-112">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="c81d8-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="c81d8-113">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="c81d8-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="c81d8-114">Dodawanie danych przykładowych</span><span class="sxs-lookup"><span data-stu-id="c81d8-114">Add sample data</span></span>

<span data-ttu-id="c81d8-115">Teraz można dodać danych tooyour nowej kolekcji za pomocą Eksploratora danych.</span><span class="sxs-lookup"><span data-stu-id="c81d8-115">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="c81d8-116">W Eksploratorze danych hello nowej bazy danych zostanie wyświetlona w okienku Kolekcje hello.</span><span class="sxs-lookup"><span data-stu-id="c81d8-116">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="c81d8-117">Rozwiń hello **zadania** bazy danych, a następnie rozwiń hello **elementów** kolekcji, kliknij przycisk **dokumenty**, a następnie kliknij przycisk **nowych dokumentów**.</span><span class="sxs-lookup"><span data-stu-id="c81d8-117">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Tworzenie nowych dokumentów w Eksploratorze danych w hello portalu Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="c81d8-119">Teraz Dodaj toohello kolekcji dokumentów o hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="c81d8-119">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="c81d8-120">Po dodaniu hello json toohello **dokumenty** , kliknij pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="c81d8-120">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Skopiuj dane json, a następnie kliknij przycisk Zapisz w Eksploratorze danych w hello portalu Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="c81d8-122">Tworzenie i zapisywanie jeden dokument więcej gdzie wstawić unikatową wartość hello `id` właściwości i zmień hello inne właściwości zgodnie z własnymi potrzebami.</span><span class="sxs-lookup"><span data-stu-id="c81d8-122">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="c81d8-123">Nowe dokumenty mogą mieć dowolną strukturę, ponieważ usługa Azure Cosmos DB nie wymusza żadnego schematu danych.</span><span class="sxs-lookup"><span data-stu-id="c81d8-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="c81d8-124">Można teraz używać zapytań w programie Eksplorator danych tooretrieve danych.</span><span class="sxs-lookup"><span data-stu-id="c81d8-124">You can now use queries in Data Explorer tooretrieve your data.</span></span> <span data-ttu-id="c81d8-125">Domyślnie korzysta z Eksploratora danych `SELECT * FROM c` tooretrieve wszystkich dokumentów w kolekcji hello, ale można zmienić tego tooa różnych [zapytania SQL](documentdb-sql-query.md), takich jak `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn wszystkie dokumenty hello w kolejności malejącej na podstawie sygnatur czasowych.</span><span class="sxs-lookup"><span data-stu-id="c81d8-125">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="c81d8-126">Można również użyć Eksploratora danych toocreate przechowywane procedury, funkcje UDF i logiki biznesowej po stronie serwera tooperform wyzwalaczy również jako przepływności skali.</span><span class="sxs-lookup"><span data-stu-id="c81d8-126">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="c81d8-127">Eksplorator danych udostępnia wszystkie hello wbudowanych programowy dostęp do danych dostępne w hello interfejsów API, ale zapewnia łatwy dostęp do danych tooyour w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c81d8-127">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="c81d8-128">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="c81d8-128">Clone hello sample application</span></span>

<span data-ttu-id="c81d8-129">Teraz załóżmy przełącznika tooworking z kodem.</span><span class="sxs-lookup"><span data-stu-id="c81d8-129">Now let's switch tooworking with code.</span></span> <span data-ttu-id="c81d8-130">Załóżmy sklonować aplikacji interfejsu API usługi DocumentDB w witrynie GitHub, Ustaw ciąg połączenia hello i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="c81d8-130">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="c81d8-131">Zobaczysz, jak łatwo jest toowork z danymi programowo.</span><span class="sxs-lookup"><span data-stu-id="c81d8-131">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="c81d8-132">Otwórz okno terminala git, np. git bash, i `CD` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="c81d8-132">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="c81d8-133">Hello uruchom następujące polecenie tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="c81d8-133">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="c81d8-134">Następnie otwórz plik rozwiązania todo hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c81d8-134">Then open hello todo solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="c81d8-135">Przejrzyj hello kodu</span><span class="sxs-lookup"><span data-stu-id="c81d8-135">Review hello code</span></span>

<span data-ttu-id="c81d8-136">Upewnijmy szybki przegląd działania wykonywane w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c81d8-136">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="c81d8-137">Otwórz hello DocumentDBRepository.cs pliku, a dane tam, że te wiersze kodu utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c81d8-137">Open hello DocumentDBRepository.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="c81d8-138">Witaj DocumentClient został zainicjowany w wierszu 73.</span><span class="sxs-lookup"><span data-stu-id="c81d8-138">hello DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="c81d8-139">Nowa baza danych jest tworzona w wierszu 88.</span><span class="sxs-lookup"><span data-stu-id="c81d8-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="c81d8-140">Nowa kolekcja jest tworzona w wierszu 107.</span><span class="sxs-lookup"><span data-stu-id="c81d8-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="c81d8-141">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="c81d8-141">Update your connection string</span></span>

<span data-ttu-id="c81d8-142">Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c81d8-142">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="c81d8-143">W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="c81d8-143">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="c81d8-144">W pliku web.config hello w następnym kroku hello użyjesz przyciski Kopia powitania po prawej stronie powitania hello toocopy ekranie powitania identyfikatora URI oraz Primary Key.</span><span class="sxs-lookup"><span data-stu-id="c81d8-144">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello web.config file in hello next step.</span></span>

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="c81d8-146">W programie Visual Studio 2017 r Otwórz plik web.config hello.</span><span class="sxs-lookup"><span data-stu-id="c81d8-146">In Visual Studio 2017, open hello web.config file.</span></span> 

3. <span data-ttu-id="c81d8-147">Skopiuj wartość identyfikatora URI z portalu hello (przy użyciu przycisku Kopiuj hello) i przydzielić mu hello wartość klucza punktu końcowego hello w pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="c81d8-147">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="c81d8-148">Skopiuj wartość klucza podstawowego z portalu hello i stał się hello wartość authKey hello w pliku web.config. Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c81d8-148">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello authKey in web.config. You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a><span data-ttu-id="c81d8-149">Uruchamianie aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="c81d8-149">Run hello web app</span></span>
1. <span data-ttu-id="c81d8-150">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** , a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c81d8-150">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="c81d8-151">W hello NuGet **Przeglądaj** wpisz *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="c81d8-151">In hello NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="c81d8-152">Wyniki hello zainstalować hello **Microsoft.Azure.DocumentDB** biblioteki.</span><span class="sxs-lookup"><span data-stu-id="c81d8-152">From hello results, install hello **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="c81d8-153">Spowoduje to zainstalowanie pakietu Microsoft.Azure.DocumentDB hello, a także wszystkie zależności.</span><span class="sxs-lookup"><span data-stu-id="c81d8-153">This installs hello Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="c81d8-154">Kliknij polecenie CTRL + F5 toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c81d8-154">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="c81d8-155">Aplikacja zostanie wyświetlona w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="c81d8-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="c81d8-156">Kliknij przycisk **Utwórz nowy** w hello przeglądarki i Utwórz kilka nowych zadań w aplikacji zadań do wykonania.</span><span class="sxs-lookup"><span data-stu-id="c81d8-156">Click **Create New** in hello browser and create a few new tasks in your to-do app.</span></span>

   ![Aplikacja z listą zadań do wykonania z przykładowymi danymi](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="c81d8-158">Teraz można wrócić do poprzedniej strony tooData Explorer i zobacz zapytania, modyfikowania i pracy z tym nowych danych.</span><span class="sxs-lookup"><span data-stu-id="c81d8-158">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="c81d8-159">Przejrzyj umowy SLA w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c81d8-159">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="c81d8-160">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="c81d8-160">Clean up resources</span></span>

<span data-ttu-id="c81d8-161">Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c81d8-161">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="c81d8-162">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="c81d8-162">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="c81d8-163">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="c81d8-163">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c81d8-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c81d8-164">Next steps</span></span>

<span data-ttu-id="c81d8-165">W tym szybkiego startu kiedy znasz już jak utworzyć kolekcję za pomocą Eksploratora danych hello toocreate konto bazy danych Azure rozwiązania Cosmos i uruchomienia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c81d8-165">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a web app.</span></span> <span data-ttu-id="c81d8-166">Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="c81d8-166">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="c81d8-167">Importowanie danych do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c81d8-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


