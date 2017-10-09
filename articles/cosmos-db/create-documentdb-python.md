---
title: "Azure rozwiązania Cosmos bazy danych: Tworzenie aplikacji za pomocą języka Python i hello interfejsu API usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod języka Python, można użyć zapytania tooand tooconnect hello interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a><span data-ttu-id="bd3a8-103">Azure DB rozwiązania Cosmos: Tworzenie aplikacji interfejsu API usługi DocumentDB z języka Python i hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bd3a8-103">Azure Cosmos DB: Build a DocumentDB API app with Python and hello Azure portal</span></span>

<span data-ttu-id="bd3a8-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="bd3a8-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="bd3a8-106">To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i przy użyciu kolekcji hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="bd3a8-107">Następnie skompilować i uruchomić aplikację konsoli oparty na powitania [interfejsu API języka Python usługi DocumentDB](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="bd3a8-107">You then build and run a console app built on hello [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd3a8-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bd3a8-108">Prerequisites</span></span>

* <span data-ttu-id="bd3a8-109">Przed uruchomieniem tego przykładu, musi mieć hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="bd3a8-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="bd3a8-110">[Program Visual Studio w wersji 2015](http://www.visualstudio.com/) lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="bd3a8-111">Narzędzia Python Tools for Visual Studio pobrane z witryny [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="bd3a8-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="bd3a8-112">W tym samouczku są używane narzędzia Python Tools for VS 2015.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="bd3a8-113">Środowisko Python w wersji 2.7 pobrane z witryny [python.org](https://www.python.org/downloads/release/python-2712/)</span><span class="sxs-lookup"><span data-stu-id="bd3a8-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="bd3a8-114">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="bd3a8-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="bd3a8-115">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="bd3a8-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="bd3a8-116">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="bd3a8-116">Clone hello sample application</span></span>

<span data-ttu-id="bd3a8-117">Teraz załóżmy aplikacji w klonowania interfejs API usługi DocumentDB z serwisu github, Ustaw ciąg połączenia hello i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-117">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="bd3a8-118">Zobacz, jak łatwo jest toowork z danymi programowo.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-118">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="bd3a8-119">Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="bd3a8-120">Hello uruchom następujące polecenie tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a><span data-ttu-id="bd3a8-121">Przejrzyj hello kodu</span><span class="sxs-lookup"><span data-stu-id="bd3a8-121">Review hello code</span></span>

<span data-ttu-id="bd3a8-122">Upewnijmy szybki przegląd działania wykonywane w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="bd3a8-123">Otwórz hello DocumentDBGetStarted.py pliku, a dane tam, że te wiersze kodu utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-123">Open hello DocumentDBGetStarted.py file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="bd3a8-124">zainicjowano Hello DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-124">hello DocumentClient is initialized.</span></span>

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="bd3a8-125">Tworzenie nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="bd3a8-126">Tworzenie nowej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-126">A new collection is created.</span></span>

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* <span data-ttu-id="bd3a8-127">Tworzenie kilku dokumentów.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-127">Some documents are created.</span></span>

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* <span data-ttu-id="bd3a8-128">Wykonywanie zapytania przy użyciu programu SQL.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-128">A query is performed using SQL</span></span>

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="bd3a8-129">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="bd3a8-129">Update your connection string</span></span>

<span data-ttu-id="bd3a8-130">Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-130">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="bd3a8-131">W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-131">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="bd3a8-132">Użyjesz przyciski Kopia hello na powitania po prawej stronie powitania toocopy ekranie powitania identyfikatora URI oraz Primary Key do hello `DocumentDBGetStarted.py` pliku w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-132">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `DocumentDBGetStarted.py` file in hello next step.</span></span>

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="bd3a8-134">W otwartych hello `DocumentDBGetStarted.py` pliku.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-134">In Open hello `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="bd3a8-135">Skopiuj wartość identyfikatora URI z portalu hello (przy użyciu przycisku Kopiuj hello) i przydzielić mu hello wartością klucza punktu końcowego hello `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-135">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="bd3a8-136">Skopiuj wartość klucza podstawowego z portalu hello i stał się hello wartość hello `config.MASTERKEY` w `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-136">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="bd3a8-137">Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-137">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="bd3a8-138">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="bd3a8-138">Run hello app</span></span>
1. <span data-ttu-id="bd3a8-139">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań**, wybierz hello bieżącego środowiska Python, a następnie kliknij prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-139">In Visual Studio, right-click on hello project in **Solution Explorer**, select hello current Python environment, then right click.</span></span>

2. <span data-ttu-id="bd3a8-140">Wybierz polecenie Zainstaluj pakiet języka Python, a następnie wpisz ciąg **pydocumentdb**.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="bd3a8-141">Uruchamianie aplikacji hello toorun F5.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-141">Run F5 toorun hello application.</span></span> <span data-ttu-id="bd3a8-142">Aplikacja zostanie wyświetlona w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="bd3a8-143">Teraz można wrócić do poprzedniej strony tooData Explorer i zobacz zapytania, modyfikowania i pracy z tym nowych danych.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-143">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="bd3a8-144">Przejrzyj umowy SLA w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bd3a8-144">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="bd3a8-145">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="bd3a8-145">Clean up resources</span></span>

<span data-ttu-id="bd3a8-146">Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bd3a8-146">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="bd3a8-147">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-147">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="bd3a8-148">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-148">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd3a8-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd3a8-149">Next steps</span></span>

<span data-ttu-id="bd3a8-150">W tym szybkiego startu kiedy znasz już jak utworzyć kolekcję za pomocą Eksploratora danych hello toocreate konto bazy danych Azure rozwiązania Cosmos i uruchamianie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-150">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="bd3a8-151">Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="bd3a8-151">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="bd3a8-152">Importowanie danych do bazy danych Azure rozwiązania Cosmos dla hello interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="bd3a8-152">Import data into Azure Cosmos DB for hello DocumentDB API</span></span>](import-data.md)


