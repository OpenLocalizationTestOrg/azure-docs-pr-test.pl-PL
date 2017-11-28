---
title: "Azure Cosmos DB: Budowanie aplikacji za pomocą języka Python i interfejsu API usługi DocumentDB | Microsoft Docs"
description: "Przykładowy kod w języku Python, którego można użyć do nawiązywania połączenia z interfejsem API usługi DocumentDB usługi Azure Cosmos DB i do wykonywania w niej zapytań"
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
ms.openlocfilehash: 08d467ea27484e7d1d07d6c21b2e04b6525fbcd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-the-azure-portal"></a><span data-ttu-id="c1d04-103">Azure Cosmos DB: Budowanie aplikacji interfejsu API usługi DocumentDB za pomocą języka Python i witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c1d04-103">Azure Cosmos DB: Build a DocumentDB API app with Python and the Azure portal</span></span>

<span data-ttu-id="c1d04-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c1d04-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="c1d04-105">Dzięki wykorzystaniu dystrybucji globalnej i możliwości skalowania poziomego opartego na usłudze Azure Cosmos DB, można szybko tworzyć i za pomocą zapytań badać bazy danych dokumentów, par klucz/wartość i grafów.</span><span class="sxs-lookup"><span data-stu-id="c1d04-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="c1d04-106">Ten przewodnik Szybki start przedstawia sposób tworzenia konta usługi Azure Cosmos DB, bazy danych dokumentów i kolekcji przy użyciu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c1d04-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="c1d04-107">Następnie za pomocą [interfejsu API usługi DocumentDB języka Python](documentdb-sdk-python.md) zbudujesz i uruchomisz aplikację konsoli.</span><span class="sxs-lookup"><span data-stu-id="c1d04-107">You then build and run a console app built on the [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1d04-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c1d04-108">Prerequisites</span></span>

* <span data-ttu-id="c1d04-109">Przed uruchomieniem tego przykładu muszą być spełnione następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="c1d04-109">Before you can run this sample, you must have the following prerequisites:</span></span>
    * <span data-ttu-id="c1d04-110">[Program Visual Studio w wersji 2015](http://www.visualstudio.com/) lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c1d04-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="c1d04-111">Narzędzia Python Tools for Visual Studio pobrane z witryny [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="c1d04-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="c1d04-112">W tym samouczku są używane narzędzia Python Tools for VS 2015.</span><span class="sxs-lookup"><span data-stu-id="c1d04-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="c1d04-113">Środowisko Python w wersji 2.7 pobrane z witryny [python.org](https://www.python.org/downloads/release/python-2712/)</span><span class="sxs-lookup"><span data-stu-id="c1d04-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="c1d04-114">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="c1d04-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="c1d04-115">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="c1d04-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="c1d04-116">Klonowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="c1d04-116">Clone the sample application</span></span>

<span data-ttu-id="c1d04-117">Teraz sklonujemy aplikację interfejsu API usługi DocumentDB z repozytorium github, ustawimy parametry połączenia i uruchomimy ją.</span><span class="sxs-lookup"><span data-stu-id="c1d04-117">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="c1d04-118">Zobaczysz, jak łatwo jest pracować programowo z danymi.</span><span class="sxs-lookup"><span data-stu-id="c1d04-118">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="c1d04-119">Otwórz okno terminalu usługi Git, na przykład git bash, i za pomocą polecenia `cd` przejdź do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="c1d04-119">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="c1d04-120">Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="c1d04-120">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-the-code"></a><span data-ttu-id="c1d04-121">Przeglądanie kodu</span><span class="sxs-lookup"><span data-stu-id="c1d04-121">Review the code</span></span>

<span data-ttu-id="c1d04-122">Dokonajmy szybkiego przeglądu działań wykonywanych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c1d04-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="c1d04-123">Otwórz plik DocumentDBGetStarted.py i zobacz, że następujące wiersze kodu tworzą zasoby usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c1d04-123">Open the DocumentDBGetStarted.py file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="c1d04-124">Inicjowanie klienta DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="c1d04-124">The DocumentClient is initialized.</span></span>

    ```python
    # Initialize the Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="c1d04-125">Tworzenie nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c1d04-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="c1d04-126">Tworzenie nowej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c1d04-126">A new collection is created.</span></span>

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

* <span data-ttu-id="c1d04-127">Tworzenie kilku dokumentów.</span><span class="sxs-lookup"><span data-stu-id="c1d04-127">Some documents are created.</span></span>

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

* <span data-ttu-id="c1d04-128">Wykonywanie zapytania przy użyciu programu SQL.</span><span class="sxs-lookup"><span data-stu-id="c1d04-128">A query is performed using SQL</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="c1d04-129">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="c1d04-129">Update your connection string</span></span>

<span data-ttu-id="c1d04-130">Teraz wróć do witryny Azure Portal, aby uzyskać informacje o parametrach połączenia i skopiować je do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c1d04-130">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="c1d04-131">W witrynie [Azure Portal](http://portal.azure.com/), korzystając ze swojego konta usługi Azure Cosmos DB, kliknij na lewym panelu nawigacyjnym pozycję **Klucze**, a następnie pozycję **Klucze odczytu i zapisu**.</span><span class="sxs-lookup"><span data-stu-id="c1d04-131">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="c1d04-132">W następnym kroku, korzystając z przycisków kopiowania dostępnych po prawej stronie ekranu, skopiujesz identyfikator URI i klucz podstawowy do pliku `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="c1d04-132">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `DocumentDBGetStarted.py` file in the next step.</span></span>

    ![Wyświetlanie i kopiowanie klucza dostępu w witrynie Azure Portal, blok Klucze](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="c1d04-134">Otwórz plik `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="c1d04-134">In Open the `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="c1d04-135">Skopiuj wartość identyfikatora URI z portalu (przy użyciu przycisku kopiowania) i przypisz ją do klucza endpoint w pliku `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="c1d04-135">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="c1d04-136">Następnie skopiuj wartość klucza podstawowego z portalu i przypisz ją do klucza `config.MASTERKEY` w pliku `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="c1d04-136">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="c1d04-137">Aplikacja została zaktualizowana i zawiera teraz wszystkie informacje potrzebne do nawiązania komunikacji z usługą Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c1d04-137">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="c1d04-138">Uruchomienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="c1d04-138">Run the app</span></span>
1. <span data-ttu-id="c1d04-139">W programie Visual Studio kliknij prawym przyciskiem myszy projekt w **Eksploratorze rozwiązań**, wybierz bieżące środowisko Python, a następnie kliknij je prawym przyciskiem myszy.</span><span class="sxs-lookup"><span data-stu-id="c1d04-139">In Visual Studio, right-click on the project in **Solution Explorer**, select the current Python environment, then right click.</span></span>

2. <span data-ttu-id="c1d04-140">Wybierz polecenie Zainstaluj pakiet języka Python, a następnie wpisz ciąg **pydocumentdb**.</span><span class="sxs-lookup"><span data-stu-id="c1d04-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="c1d04-141">Naciśnij klawisz F5, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="c1d04-141">Run F5 to run the application.</span></span> <span data-ttu-id="c1d04-142">Aplikacja zostanie wyświetlona w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="c1d04-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="c1d04-143">Teraz można wrócić do Eksploratora danych i zobaczyć, jak się pracuje z nowymi danymi, modyfikuje je i tworzy zapytania o nie.</span><span class="sxs-lookup"><span data-stu-id="c1d04-143">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="c1d04-144">Przeglądanie umów SLA w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c1d04-144">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="c1d04-145">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="c1d04-145">Clean up resources</span></span>

<span data-ttu-id="c1d04-146">Jeśli nie zamierzasz w przyszłości korzystać z tej aplikacji, wykonaj następujące czynności, aby usunąć wszystkie zasoby utworzone w witrynie Azure Portal w ramach tego przewodnika Szybki start:</span><span class="sxs-lookup"><span data-stu-id="c1d04-146">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="c1d04-147">W menu znajdującym się po lewej stronie w witrynie Azure Portal kliknij pozycję **Grupy zasobów**, a następnie kliknij nazwę utworzonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="c1d04-147">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="c1d04-148">Na stronie grupy zasobów kliknij pozycję **Usuń**, wpisz w polu tekstowym nazwę zasobu do usunięcia, a następnie kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="c1d04-148">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1d04-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c1d04-149">Next steps</span></span>

<span data-ttu-id="c1d04-150">W tym przewodniku Szybki start wyjaśniono sposób tworzenia konta usługi Azure Cosmos DB, tworzenia kolekcji za pomocą Eksploratora danych i uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c1d04-150">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="c1d04-151">Teraz możesz zaimportować dodatkowe dane do swojego konta usługi Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c1d04-151">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="c1d04-152">Importowanie danych do usługi Azure Cosmos DB na potrzeby interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c1d04-152">Import data into Azure Cosmos DB for the DocumentDB API</span></span>](import-data.md)


