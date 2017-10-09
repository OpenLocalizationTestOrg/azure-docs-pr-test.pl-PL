---
title: "aaaCreate bazą danych dokumentów bazy danych Azure rozwiązania Cosmos z językiem Java | Dokumentacja firmy Microsoft | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod języka Java, można użyć zapytania tooand tooconnect hello interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB"
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
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="b6107-103">Azure DB rozwiązania Cosmos: Tworzenie bazy danych dokumentów przy użyciu języka Java i hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b6107-103">Azure Cosmos DB: Create a document database using Java and hello Azure portal</span></span>

<span data-ttu-id="b6107-104">Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b6107-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b6107-105">Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b6107-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b6107-106">Ta opcja szybkiego startu tworzy dokument bazy danych przy użyciu hello narzędzi portalu platformy Azure dla bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b6107-106">This quickstart creates a document database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="b6107-107">Ta opcja szybkiego startu przedstawiono również sposób tooquickly Utwórz aplikację konsoli języka Java przy użyciu hello [interfejsu API języka Java usługi DocumentDB](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="b6107-107">This quickstart also shows you how tooquickly create a Java console app using hello [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="b6107-108">instrukcje Hello tego przewodnika Szybki Start można wykonać w dowolnym systemie operacyjnym, który jest w stanie uruchomić oprogramowanie Java.</span><span class="sxs-lookup"><span data-stu-id="b6107-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="b6107-109">Wykonując tego przewodnika Szybki Start będzie znane tworzenia i modyfikowania zasobów bazy danych dokumentów w hello interfejsu użytkownika lub programowo, nastąpi swoich preferencji.</span><span class="sxs-lookup"><span data-stu-id="b6107-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either hello UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6107-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b6107-110">Prerequisites</span></span>

* [<span data-ttu-id="b6107-111">Zestaw Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="b6107-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="b6107-112">Uruchom na Ubuntu, `apt-get install default-jdk` tooinstall hello JDK.</span><span class="sxs-lookup"><span data-stu-id="b6107-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="b6107-113">Jest zainstalowanym hello JDK czy tooset hello JAVA_HOME środowiska zmiennej toopoint toohello folder.</span><span class="sxs-lookup"><span data-stu-id="b6107-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="b6107-114">[Pobierz](http://maven.apache.org/download.cgi) i [zainstaluj](http://maven.apache.org/install.html) archiwum binarne [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="b6107-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="b6107-115">Na Ubuntu, można uruchomić `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="b6107-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="b6107-116">Git</span><span class="sxs-lookup"><span data-stu-id="b6107-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="b6107-117">Na Ubuntu, można uruchomić `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="b6107-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="b6107-118">Tworzenie konta bazy danych</span><span class="sxs-lookup"><span data-stu-id="b6107-118">Create a database account</span></span>

<span data-ttu-id="b6107-119">Przed utworzeniem dokumentów bazy danych należy toocreate konta bazy danych SQL (DocumentDB) z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b6107-119">Before you can create a document database, you need toocreate a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="b6107-120">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="b6107-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="b6107-121">Dodawanie danych przykładowych</span><span class="sxs-lookup"><span data-stu-id="b6107-121">Add sample data</span></span>

<span data-ttu-id="b6107-122">Teraz można dodać danych tooyour nowej kolekcji za pomocą Eksploratora danych.</span><span class="sxs-lookup"><span data-stu-id="b6107-122">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="b6107-123">W Eksploratorze danych hello nowej bazy danych zostanie wyświetlona w okienku Kolekcje hello.</span><span class="sxs-lookup"><span data-stu-id="b6107-123">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="b6107-124">Rozwiń hello **zadania** bazy danych, a następnie rozwiń hello **elementów** kolekcji, kliknij przycisk **dokumenty**, a następnie kliknij przycisk **nowych dokumentów**.</span><span class="sxs-lookup"><span data-stu-id="b6107-124">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Tworzenie nowych dokumentów w Eksploratorze danych w hello portalu Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="b6107-126">Teraz Dodaj toohello kolekcji dokumentów o hello następujące struktury.</span><span class="sxs-lookup"><span data-stu-id="b6107-126">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="b6107-127">Po dodaniu hello json toohello **dokumenty** , kliknij pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="b6107-127">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Skopiuj dane json, a następnie kliknij przycisk Zapisz w Eksploratorze danych w hello portalu Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="b6107-129">Tworzenie i zapisywanie jeden dokument więcej gdzie wstawić unikatową wartość hello `id` właściwości i zmień hello inne właściwości zgodnie z własnymi potrzebami.</span><span class="sxs-lookup"><span data-stu-id="b6107-129">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="b6107-130">Nowe dokumenty mogą mieć dowolną strukturę, ponieważ usługa Azure Cosmos DB nie wymusza żadnego schematu danych.</span><span class="sxs-lookup"><span data-stu-id="b6107-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="b6107-131">Można teraz Użyj zapytania w programie Eksplorator danych tooretrieve dane, klikając hello **edytowanie filtru** i **Zastosuj filtr** przycisków.</span><span class="sxs-lookup"><span data-stu-id="b6107-131">You can now use queries in Data Explorer tooretrieve your data by clicking hello **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="b6107-132">Domyślnie korzysta z Eksploratora danych `SELECT * FROM c` tooretrieve wszystkich dokumentów w kolekcji hello, ale można zmienić tego tooa różnych [zapytania SQL](documentdb-sql-query.md), takich jak `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn wszystkie dokumenty hello w kolejności malejącej na podstawie sygnatur czasowych.</span><span class="sxs-lookup"><span data-stu-id="b6107-132">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="b6107-133">Można również użyć Eksploratora danych toocreate przechowywane procedury, funkcje UDF i logiki biznesowej po stronie serwera tooperform wyzwalaczy również jako przepływności skali.</span><span class="sxs-lookup"><span data-stu-id="b6107-133">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="b6107-134">Eksplorator danych udostępnia wszystkie hello wbudowanych programowy dostęp do danych dostępne w hello interfejsów API, ale zapewnia łatwy dostęp do danych tooyour w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b6107-134">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="b6107-135">Klonowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="b6107-135">Clone hello sample application</span></span>

<span data-ttu-id="b6107-136">Teraz załóżmy przełącznika tooworking z kodem.</span><span class="sxs-lookup"><span data-stu-id="b6107-136">Now let's switch tooworking with code.</span></span> <span data-ttu-id="b6107-137">Załóżmy sklonować aplikacji interfejsu API usługi DocumentDB w witrynie GitHub, Ustaw ciąg połączenia hello i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="b6107-137">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="b6107-138">Zobacz, jak łatwo jest toowork z danymi programowo.</span><span class="sxs-lookup"><span data-stu-id="b6107-138">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="b6107-139">Otwórz okno terminala git, np. git bash, i `CD` tooa katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="b6107-139">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="b6107-140">Hello uruchom następujące polecenie tooclone hello próbki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="b6107-140">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="b6107-141">Przejrzyj hello kodu</span><span class="sxs-lookup"><span data-stu-id="b6107-141">Review hello code</span></span>

<span data-ttu-id="b6107-142">Upewnijmy szybki przegląd działania wykonywane w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b6107-142">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="b6107-143">Otwórz hello `Program.java` plików z folderu \src\GetStarted hello i Znajdź te wiersze kodu, które utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b6107-143">Open hello `Program.java` file from hello \src\GetStarted folder, and find these lines of code that create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="b6107-144">Witaj `DocumentClient` został zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="b6107-144">hello `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="b6107-145">Tworzenie nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b6107-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="b6107-146">Tworzenie nowej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b6107-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="b6107-147">Tworzenie kilku dokumentów.</span><span class="sxs-lookup"><span data-stu-id="b6107-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="b6107-148">Wykonywanie zapytania SQL w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="b6107-148">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="b6107-149">Aktualizowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="b6107-149">Update your connection string</span></span>

<span data-ttu-id="b6107-150">Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b6107-150">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span> <span data-ttu-id="b6107-151">Spowoduje to włączenie toocommunicate Twojej aplikacji hostowanej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="b6107-151">This will enable your app toocommunicate with your hosted database.</span></span>

1. <span data-ttu-id="b6107-152">W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**.</span><span class="sxs-lookup"><span data-stu-id="b6107-152">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="b6107-153">Użyjesz przyciski Kopia hello na powitania po prawej stronie powitania toocopy ekranie powitania identyfikatora URI oraz PRIMARY KEY do hello `Program.java` pliku w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="b6107-153">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and PRIMARY KEY into hello `Program.java` file in hello next step.</span></span>

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="b6107-155">W hello Otwórz `Program.java` pliku, skopiuj wartość identyfikatora URI z portalu hello (przy użyciu przycisku Kopiuj hello) i stał się hello wartość hello punktu końcowego toohello DocumentClient konstruktora w `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="b6107-155">In hello open `Program.java` file, copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint toohello DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="b6107-156">Następnie skopiuj wartość klucza podstawowego z portalu hello i wklej go za pośrednictwem "FILLME", dzięki czemu hello drugi parametr w Konstruktorze DocumentClient hello.</span><span class="sxs-lookup"><span data-stu-id="b6107-156">Then copy your PRIMARY KEY value from hello portal and paste it over “FILLME”, making it hello second parameter in hello DocumentClient constructor.</span></span> <span data-ttu-id="b6107-157">Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b6107-157">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-app"></a><span data-ttu-id="b6107-158">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="b6107-158">Run hello app</span></span>

1. <span data-ttu-id="b6107-159">W oknie terminala git hello `cd` toohello azure-cosmos-db-documentdb-java-getting-started folderu.</span><span class="sxs-lookup"><span data-stu-id="b6107-159">In hello git terminal window, `cd` toohello azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="b6107-160">W oknie terminala git hello, wpisz `mvn package` tooinstall hello wymaganych pakietów języka Java.</span><span class="sxs-lookup"><span data-stu-id="b6107-160">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="b6107-161">W oknie terminala git hello, uruchom `mvn exec:java -D exec.mainClass=GetStarted.Program` w hello toostart okno terminalu aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="b6107-161">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

    <span data-ttu-id="b6107-162">W oknie terminala hello otrzymasz powiadomienie, że hello FamilyDB baza danych została utworzona i toopress toocontinue klucza.</span><span class="sxs-lookup"><span data-stu-id="b6107-162">In hello terminal window, you'll receive notification that hello FamilyDB database was created, and toopress a key toocontinue.</span></span> <span data-ttu-id="b6107-163">Naciśnij klawisz hello klucza toocreate bazy danych, następnie przełącz toohello Eksplorator danych i zobaczysz, że teraz zawiera FamilyDB bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b6107-163">Press a key toocreate hello database, then switch toohello Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="b6107-164">Kontynuować toopress klucze toocreate hello kolekcji i hello dokumentów, a następnie wykonaj zapytanie.</span><span class="sxs-lookup"><span data-stu-id="b6107-164">Continue toopress keys toocreate hello collection and hello documents and then perform a query.</span></span> <span data-ttu-id="b6107-165">Po ukończeniu projektu hello hello zasoby są usuwane z Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="b6107-165">When hello project completes, hello resources are deleted from your account.</span></span> 

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="b6107-167">Przejrzyj umowy SLA w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b6107-167">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b6107-168">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="b6107-168">Clean up resources</span></span>

<span data-ttu-id="b6107-169">Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b6107-169">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="b6107-170">Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="b6107-170">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="b6107-171">Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="b6107-171">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6107-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b6107-172">Next steps</span></span>

<span data-ttu-id="b6107-173">W tym szybkiego startu kiedy znasz już jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i kolekcji za pomocą hello Eksploratora danych, a następnie uruchom toodo aplikacji hello samo programowo.</span><span class="sxs-lookup"><span data-stu-id="b6107-173">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, document database, and collection using hello Data Explorer, and run an app toodo hello same thing programmatically.</span></span> <span data-ttu-id="b6107-174">Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="b6107-174">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b6107-175">Importowanie danych do usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b6107-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


