---
title: "Tworzenie bazy danych dokumentów usługi Azure Cosmos DB przy użyciu języka Java | Microsoft Docs"
description: "Przykładowy kod w języku Java, którego można użyć do nawiązywania połączenia z interfejsem API usługi DocumentDB usługi Azure Cosmos DB i do wykonywania w niej zapytań"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: df1a25d703a7b8082bdabb4f7d593cb005d416fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-the-azure-portal"></a><span data-ttu-id="1a473-103">Azure Cosmos DB: Tworzenie bazy danych dokumentów przy użyciu języka Java i witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1a473-103">Azure Cosmos DB: Create a document database using Java and the Azure portal</span></span>

<span data-ttu-id="1a473-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1a473-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="1a473-105">Dzięki wykorzystaniu dystrybucji globalnej i możliwości skalowania poziomego opartego na usłudze Azure Cosmos DB, można szybko tworzyć i za pomocą zapytań badać bazy danych dokumentów, par klucz/wartość i grafów.</span><span class="sxs-lookup"><span data-stu-id="1a473-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="1a473-106">Ten przewodnik Szybki start tworzy bazę danych dokumentów przy użyciu narzędzi witryny Azure Portal dla usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a473-106">This quickstart creates a document database using the Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="1a473-107">Ponadto ten przewodnik Szybki start pokazuje, jak szybko utworzyć aplikację konsolową Java przy użyciu [interfejsu API języka Java usługi DocumentDB](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="1a473-107">This quickstart also shows you how to quickly create a Java console app using the [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="1a473-108">Instrukcje podane w tym przewodniku Szybki start można wykonać w dowolnym systemie operacyjnym, w którym można uruchomić oprogramowanie Java.</span><span class="sxs-lookup"><span data-stu-id="1a473-108">The instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="1a473-109">Realizując ten przewodnik Szybki start, zaznajomisz się z tworzeniem i modyfikowaniem zasobów bazy danych dokumentów z wykorzystaniem interfejsu użytkownika lub programowo, zgodnie z preferencjami.</span><span class="sxs-lookup"><span data-stu-id="1a473-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either the UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a473-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1a473-110">Prerequisites</span></span>

* [<span data-ttu-id="1a473-111">Zestaw Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="1a473-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="1a473-112">W systemie Ubuntu uruchom polecenie `apt-get install default-jdk`, aby zainstalować zestaw JDK.</span><span class="sxs-lookup"><span data-stu-id="1a473-112">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="1a473-113">Upewnij się, że zmienna środowiskowa JAVA_HOME wskazuje folder, w którym zainstalowano zestaw JDK.</span><span class="sxs-lookup"><span data-stu-id="1a473-113">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="1a473-114">[Pobierz](http://maven.apache.org/download.cgi) i [zainstaluj](http://maven.apache.org/install.html) archiwum binarne [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="1a473-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="1a473-115">W systemie Ubuntu możesz uruchomić polecenie `apt-get install maven`, aby zainstalować narzędzie Maven.</span><span class="sxs-lookup"><span data-stu-id="1a473-115">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="1a473-116">Git</span><span class="sxs-lookup"><span data-stu-id="1a473-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="1a473-117">W systemie Ubuntu możesz uruchomić polecenie `sudo apt-get install git`, aby zainstalować usługę Git.</span><span class="sxs-lookup"><span data-stu-id="1a473-117">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="1a473-118">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="1a473-118">Create a database account</span></span>

<span data-ttu-id="1a473-119">Przed utworzeniem bazy danych dokumentów musisz utworzyć konto bazy danych SQL (DocumentDB) z użyciem usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a473-119">Before you can create a document database, you need to create a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="1a473-120">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="1a473-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="1a473-121">Dodawanie danych przykładowych</span><span class="sxs-lookup"><span data-stu-id="1a473-121">Add sample data</span></span>

<span data-ttu-id="1a473-122">Teraz można dodać dane do nowej kolekcji za pomocą Eksploratora danych.</span><span class="sxs-lookup"><span data-stu-id="1a473-122">You can now add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="1a473-123">W Eksploratorze danych nowa baza danych jest wyświetlana w okienku Kolekcje.</span><span class="sxs-lookup"><span data-stu-id="1a473-123">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="1a473-124">Rozwiń bazę danych **Tasks**, rozwiń kolekcję **Items**, kliknij pozycję **Dokumenty**, a następnie kliknij pozycję **Nowe dokumenty**.</span><span class="sxs-lookup"><span data-stu-id="1a473-124">Expand the **Tasks** database, expand the **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Tworzenie nowych dokumentów w Eksploratorze danych w witrynie Azure Portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="1a473-126">Teraz dodaj do kolekcji dokument o następującej strukturze.</span><span class="sxs-lookup"><span data-stu-id="1a473-126">Now add a document to the collection with the following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="1a473-127">Po dodaniu danych json do karty **Dokumenty** kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1a473-127">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![Kopiowanie danych json i klikanie pozycji Zapisz w Eksploratorze danych w witrynie Azure Portal](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="1a473-129">Utwórz i zapisz jeszcze jeden dokument, w którym wstawisz unikatową wartość dla właściwości `id` i zmienisz inne właściwości wedle uznania.</span><span class="sxs-lookup"><span data-stu-id="1a473-129">Create and save one more document where you insert a unique value for the `id` property, and change the other properties as you see fit.</span></span> <span data-ttu-id="1a473-130">Nowe dokumenty mogą mieć dowolną strukturę, ponieważ usługa Azure Cosmos DB nie wymusza żadnego schematu danych.</span><span class="sxs-lookup"><span data-stu-id="1a473-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="1a473-131">Teraz możesz używać zapytań w Eksploratorze danych, aby pobierać dane, klikając przyciski **Edytuj filtr** i **Zastosuj filtr**.</span><span class="sxs-lookup"><span data-stu-id="1a473-131">You can now use queries in Data Explorer to retrieve your data by clicking the **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="1a473-132">Domyślnie Eksplorator danych używa instrukcji `SELECT * FROM c` do pobrania wszystkich dokumentów w kolekcji, ale można zmienić tę instrukcję na inne [zapytanie SQL](documentdb-sql-query.md), np. `SELECT * FROM c ORDER BY c._ts DESC`, aby zwrócić wszystkie dokumenty w kolejności malejącej w oparciu o sygnaturę czasową.</span><span class="sxs-lookup"><span data-stu-id="1a473-132">By default, Data Explorer uses `SELECT * FROM c` to retrieve all documents in the collection, but you can change that to a different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, to return all the documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="1a473-133">Eksplorator danych umożliwia również tworzenie procedur składowanych, funkcji definiowanych przez użytkownika (UDF) i wyzwalaczy w celu wykonania logiki biznesowej po stronie serwera oraz skalowania przepływności.</span><span class="sxs-lookup"><span data-stu-id="1a473-133">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="1a473-134">Eksplorator danych udostępnia wszystkie wbudowane programowe procedury dostępu do danych w interfejsach API, ale umożliwia łatwy dostęp do danych za pośrednictwem witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1a473-134">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="1a473-135">Klonowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="1a473-135">Clone the sample application</span></span>

<span data-ttu-id="1a473-136">Teraz przejdźmy do pracy z kodem.</span><span class="sxs-lookup"><span data-stu-id="1a473-136">Now let's switch to working with code.</span></span> <span data-ttu-id="1a473-137">Sklonujemy aplikację interfejsu API usługi DocumentDB z repozytorium GitHub, ustawimy parametry połączenia i uruchomimy ją.</span><span class="sxs-lookup"><span data-stu-id="1a473-137">Let's clone a DocumentDB API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="1a473-138">Zobaczysz, jak łatwo jest pracować programowo z danymi.</span><span class="sxs-lookup"><span data-stu-id="1a473-138">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="1a473-139">Otwórz okno terminalu usługi Git, na przykład git bash, i za pomocą polecenia `CD` przejdź do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="1a473-139">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="1a473-140">Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1a473-140">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="1a473-141">Przeglądanie kodu</span><span class="sxs-lookup"><span data-stu-id="1a473-141">Review the code</span></span>

<span data-ttu-id="1a473-142">Dokonajmy szybkiego przeglądu działań wykonywanych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a473-142">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="1a473-143">Otwórz plik `Program.java` z folderu \src\GetStarted i znajdź następujące wiersze kodu tworzące zasoby usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a473-143">Open the `Program.java` file from the \src\GetStarted folder, and find these lines of code that create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="1a473-144">Inicjowanie obiektu `DocumentClient`.</span><span class="sxs-lookup"><span data-stu-id="1a473-144">The `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="1a473-145">Tworzenie nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1a473-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="1a473-146">Tworzenie nowej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="1a473-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="1a473-147">Tworzenie kilku dokumentów.</span><span class="sxs-lookup"><span data-stu-id="1a473-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written to Azure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="1a473-148">Wykonywanie zapytania SQL w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="1a473-148">A SQL query over JSON is performed.</span></span>

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="1a473-149">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="1a473-149">Update your connection string</span></span>

<span data-ttu-id="1a473-150">Teraz wróć do witryny Azure Portal, aby uzyskać informacje o parametrach połączenia i skopiować je do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a473-150">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="1a473-151">Umożliwi to aplikacji komunikację z hostowaną bazą danych.</span><span class="sxs-lookup"><span data-stu-id="1a473-151">This will enable your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="1a473-152">W witrynie [Azure Portal](http://portal.azure.com/), korzystając ze swojego konta usługi Azure Cosmos DB, kliknij na lewym panelu nawigacyjnym pozycję **Klucze**, a następnie pozycję **Klucze odczytu i zapisu**.</span><span class="sxs-lookup"><span data-stu-id="1a473-152">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="1a473-153">W następnym kroku, korzystając z przycisków kopiowania dostępnych po prawej stronie ekranu, skopiujesz wartości IDENTYFIKATOR URI i KLUCZ PODSTAWOWY do pliku `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="1a473-153">You'll use the copy buttons on the right side of the screen to copy the URI and PRIMARY KEY into the `Program.java` file in the next step.</span></span>

    ![Wyświetlanie i kopiowanie klucza dostępu w witrynie Azure Portal, blok Klucze](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="1a473-155">Po otworzeniu pliku `Program.java` skopiuj wartość IDENTYFIKATOR URI z portalu (przy użyciu przycisku kopiowania) i przypisz ją jako wartość punktu końcowego konstruktora DocumentClient w pliku `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="1a473-155">In the open `Program.java` file, copy your URI value from the portal (using the copy button) and make it the value of the endpoint to the DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="1a473-156">Następnie skopiuj wartość KLUCZ PODSTAWOWY z portalu i wklej ją zamiast ciągu „FILLME”. W ten sposób stanie się ona drugim parametrem w konstruktorze DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="1a473-156">Then copy your PRIMARY KEY value from the portal and paste it over “FILLME”, making it the second parameter in the DocumentClient constructor.</span></span> <span data-ttu-id="1a473-157">Aplikacja została zaktualizowana i zawiera teraz wszystkie informacje potrzebne do nawiązania komunikacji z usługą Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a473-157">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-app"></a><span data-ttu-id="1a473-158">Uruchomienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="1a473-158">Run the app</span></span>

1. <span data-ttu-id="1a473-159">W oknie terminalu usługi Git za pomocą polecenia `cd` przejdź do folderu azure-cosmos-db-documentdb-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="1a473-159">In the git terminal window, `cd` to the azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="1a473-160">W oknie terminalu usługi Git wpisz polecenie `mvn package`, aby zainstalować wymagane pakiety języka Java.</span><span class="sxs-lookup"><span data-stu-id="1a473-160">In the git terminal window, type `mvn package` to install the required Java packages.</span></span>

3. <span data-ttu-id="1a473-161">W oknie terminalu usługi Git uruchom polecenie `mvn exec:java -D exec.mainClass=GetStarted.Program`, aby uruchomić aplikację Java.</span><span class="sxs-lookup"><span data-stu-id="1a473-161">In the git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in the terminal window to start your Java application.</span></span>

    <span data-ttu-id="1a473-162">W oknie terminalu otrzymasz powiadomienie o utworzeniu bazy danych FamilyDB oraz monit o naciśnięcie klawisza w celu kontynuowania.</span><span class="sxs-lookup"><span data-stu-id="1a473-162">In the terminal window, you'll receive notification that the FamilyDB database was created, and to press a key to continue.</span></span> <span data-ttu-id="1a473-163">Naciśnij klawisz, aby utworzyć bazę danych, a następnie przejdź do Eksploratora danych, a zobaczysz, że teraz zawiera bazę danych FamilyDB.</span><span class="sxs-lookup"><span data-stu-id="1a473-163">Press a key to create the database, then switch to the Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="1a473-164">Kontynuuj naciskanie klawiszy, aby utworzyć kolekcję i dokumenty, a następnie wykonaj zapytanie.</span><span class="sxs-lookup"><span data-stu-id="1a473-164">Continue to press keys to create the collection and the documents and then perform a query.</span></span> <span data-ttu-id="1a473-165">Po zakończeniu projektu zasoby zostaną usunięte z Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="1a473-165">When the project completes, the resources are deleted from your account.</span></span> 

    ![Wyświetlanie i kopiowanie klucza dostępu w witrynie Azure Portal, blok Klucze](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="1a473-167">Przeglądanie umów SLA w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1a473-167">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="1a473-168">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="1a473-168">Clean up resources</span></span>

<span data-ttu-id="1a473-169">Jeśli nie zamierzasz w przyszłości korzystać z tej aplikacji, wykonaj następujące czynności, aby usunąć wszystkie zasoby utworzone w witrynie Azure Portal w ramach tego przewodnika Szybki start:</span><span class="sxs-lookup"><span data-stu-id="1a473-169">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="1a473-170">W menu znajdującym się po lewej stronie w witrynie Azure Portal kliknij pozycję **Grupy zasobów**, a następnie kliknij nazwę utworzonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="1a473-170">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="1a473-171">Na stronie grupy zasobów kliknij pozycję **Usuń**, wpisz w polu tekstowym nazwę zasobu do usunięcia, a następnie kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="1a473-171">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a473-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1a473-172">Next steps</span></span>

<span data-ttu-id="1a473-173">W tym przewodniku Szybki start wyjaśniono sposób tworzenia konta usługi Azure Cosmos DB, bazy danych dokumentów i kolekcji za pomocą Eksploratora danych oraz uruchamiania aplikacji w celu wykonania tych samych czynności w sposób programowy.</span><span class="sxs-lookup"><span data-stu-id="1a473-173">In this quickstart, you've learned how to create an Azure Cosmos DB account, document database, and collection using the Data Explorer, and run an app to do the same thing programmatically.</span></span> <span data-ttu-id="1a473-174">Teraz możesz zaimportować dodatkowe dane do swojego konta usługi Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a473-174">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1a473-175">Importowanie danych do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1a473-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


