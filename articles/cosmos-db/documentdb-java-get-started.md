---
title: "Samouczek NoSQL: usługi DocumentDB interfejsu API Azure rozwiązania Cosmos DB Java SDK | Dokumentacja firmy Microsoft"
description: "Samouczek NoSQL, który powoduje utworzenie bazy danych w trybie online i aplikację konsoli języka Java przy użyciu hello interfejsu API usługi DocumentDB dla bazy danych Azure rozwiązania Cosmos. Usługa Azure DocumentDB jest bazą danych NoSQL dla formatu JSON."
keywords: nosql tutorial, online database, java console application
services: cosmos-db
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/22/2017
ms.author: arramac
ms.openlocfilehash: 1a298a15ab911d140b9df30ad52cfe0fa07c55b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="160f4-105">Samouczek NoSQL: tworzenie aplikacji konsoli Java interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="160f4-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="160f4-106">.NET</span><span class="sxs-lookup"><span data-stu-id="160f4-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="160f4-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="160f4-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="160f4-108">Node.js dla MongoDB</span><span class="sxs-lookup"><span data-stu-id="160f4-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="160f4-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="160f4-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="160f4-110">Java</span><span class="sxs-lookup"><span data-stu-id="160f4-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="160f4-111">C++</span><span class="sxs-lookup"><span data-stu-id="160f4-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="160f4-112">Samouczek NoSQL powitalnej toohello dla hello interfejsu API Azure rozwiązania Cosmos DB Java SDK usługi DocumentDB!</span><span class="sxs-lookup"><span data-stu-id="160f4-112">Welcome toohello NoSQL tutorial for hello DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="160f4-113">W ramach tego samouczka zostanie utworzona aplikacja konsolowa, która tworzy zasoby usługi Azure Cosmos DB i wykonuje dla nich zapytania.</span><span class="sxs-lookup"><span data-stu-id="160f4-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="160f4-114">Zostaną opisane:</span><span class="sxs-lookup"><span data-stu-id="160f4-114">We cover:</span></span>

* <span data-ttu-id="160f4-115">Tworzenie i łączenie tooan konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="160f4-115">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="160f4-116">Konfigurowanie rozwiązania Visual Studio</span><span class="sxs-lookup"><span data-stu-id="160f4-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="160f4-117">Tworzenie bazy danych w trybie online</span><span class="sxs-lookup"><span data-stu-id="160f4-117">Creating an online database</span></span>
* <span data-ttu-id="160f4-118">Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="160f4-118">Creating a collection</span></span>
* <span data-ttu-id="160f4-119">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="160f4-119">Creating JSON documents</span></span>
* <span data-ttu-id="160f4-120">Wykonywanie zapytania hello kolekcji</span><span class="sxs-lookup"><span data-stu-id="160f4-120">Querying hello collection</span></span>
* <span data-ttu-id="160f4-121">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="160f4-121">Creating JSON documents</span></span>
* <span data-ttu-id="160f4-122">Wykonywanie zapytania hello kolekcji</span><span class="sxs-lookup"><span data-stu-id="160f4-122">Querying hello collection</span></span>
* <span data-ttu-id="160f4-123">Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="160f4-123">Replacing a document</span></span>
* <span data-ttu-id="160f4-124">Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="160f4-124">Deleting a document</span></span>
* <span data-ttu-id="160f4-125">Usunięcie hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="160f4-125">Deleting hello database</span></span>

<span data-ttu-id="160f4-126">Teraz do dzieła!</span><span class="sxs-lookup"><span data-stu-id="160f4-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="160f4-127">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="160f4-127">Prerequisites</span></span>
<span data-ttu-id="160f4-128">Upewnij się, że masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="160f4-128">Make sure you have hello following:</span></span>

* <span data-ttu-id="160f4-129">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="160f4-129">An active Azure account.</span></span> <span data-ttu-id="160f4-130">Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="160f4-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="160f4-131">Alternatywnie można użyć hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="160f4-131">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="160f4-132">Git</span><span class="sxs-lookup"><span data-stu-id="160f4-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="160f4-133">[Zestaw Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="160f4-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="160f4-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="160f4-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="160f4-135">Krok 1. Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="160f4-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="160f4-136">Utwórzmy konto usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="160f4-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="160f4-137">Jeśli masz już konto ma toouse, możesz przejść od razu zbyt[projektu GitHub hello w klonowania](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="160f4-137">If you already have an account you want toouse, you can skip ahead too[Clone hello GitHub project](#GitClone).</span></span> <span data-ttu-id="160f4-138">Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, wykonaj czynności hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) tooset Konfigurowanie hello emulatora i przejść od razu zbyt[projektu GitHub hello w klonowania](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="160f4-138">If you are using hello Azure Cosmos DB Emulator, follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) tooset up hello emulator and skip ahead too[Clone hello GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="160f4-139"><a id="GitClone"></a>Krok 2: Klonowania hello GitHub projektu</span><span class="sxs-lookup"><span data-stu-id="160f4-139"><a id="GitClone"></a>Step 2: Clone hello GitHub project</span></span>
<span data-ttu-id="160f4-140">Możesz rozpocząć pracę w klonowania repozytorium GitHub hello [Rozpoczynanie pracy z bazy danych Azure rozwiązania Cosmos i Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="160f4-140">You can get started by cloning hello GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="160f4-141">Na przykład z katalogu lokalnego uruchamiania powitania po tooretrieve hello przykładowy projekt lokalnie.</span><span class="sxs-lookup"><span data-stu-id="160f4-141">For example, from a local directory run hello following tooretrieve hello sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="160f4-142">katalog Hello zawiera `pom.xml` hello projektu i `src` folder zawierający kod źródłowy Java w tym `Program.java` które pokazuje sposób wykonywaniem prostych operacji dotyczących bazy danych rozwiązania Cosmos platformy Azure, takich jak tworzenie dokumentów i wykonywanie zapytania na danych w ramach Kolekcja.</span><span class="sxs-lookup"><span data-stu-id="160f4-142">hello directory contains a `pom.xml` for hello project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="160f4-143">Witaj `pom.xml` zawiera zależności hello [zestawu SDK Java usługi DocumentDB w przypadku Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="160f4-143">hello `pom.xml` includes a dependency on hello [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="160f4-144"><a id="Connect"></a>Krok 3: Łączenie tooan konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="160f4-144"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="160f4-145">Następnie head kopii toohello [Azure Portal](https://portal.azure.com) tooretrieve punktu końcowego, a podstawowy klucz główny.</span><span class="sxs-lookup"><span data-stu-id="160f4-145">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint and primary master key.</span></span> <span data-ttu-id="160f4-146">Hello Azure DB rozwiązania Cosmos punktu końcowego i klucz podstawowy są niezbędne do Twojej aplikacji toounderstand gdzie tooconnect na oraz bazy danych Azure rozwiązania Cosmos tootrust połączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="160f4-146">hello Azure Cosmos DB endpoint and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="160f4-147">W hello portalu Azure, przejdź do konta bazy danych Azure rozwiązania Cosmos tooyour, a następnie kliknij **klucze**.</span><span class="sxs-lookup"><span data-stu-id="160f4-147">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="160f4-148">Skopiuj hello identyfikatora URI z portalu hello i wklej ją do `https://FILLME.documents.azure.com` w pliku Program.java hello.</span><span class="sxs-lookup"><span data-stu-id="160f4-148">Copy hello URI from hello portal and paste it into `https://FILLME.documents.azure.com` in hello Program.java file.</span></span> <span data-ttu-id="160f4-149">Następnie kopiowania hello klucza podstawowego z portalu hello i wklej ją do `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="160f4-149">Then copy hello PRIMARY KEY from hello portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Zrzut ekranu przedstawiający hello Portal Azure używany przez hello toocreate samouczka NoSQL aplikację konsoli języka Java.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="160f4-152">Krok 4. Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="160f4-152">Step 4: Create a database</span></span>
<span data-ttu-id="160f4-153">Bazy danych programu Azure rozwiązania Cosmos [bazy danych](documentdb-resources.md#databases) można tworzyć przy użyciu hello [metody createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) metody hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="160f4-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="160f4-154">Baza danych jest hello kontenerem logicznym magazynu dokumentów JSON podzielonym na partycje w kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="160f4-154">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="160f4-155"><a id="CreateColl"></a>Krok 5. Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="160f4-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="160f4-156">Metoda **createCollection** tworzy nową kolekcję z zarezerwowaną przepływnością, co ma wpływ na cenę.</span><span class="sxs-lookup"><span data-stu-id="160f4-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="160f4-157">Aby uzyskać więcej informacji, odwiedź naszą [stronę cennika](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="160f4-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="160f4-158">A [kolekcji](documentdb-resources.md#collections) można tworzyć przy użyciu hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) metody hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="160f4-158">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="160f4-159">Kolekcja jest kontenerem dokumentów JSON i skojarzonej logiki aplikacji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="160f4-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="160f4-160"><a id="CreateDoc"></a>Krok 6. Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="160f4-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="160f4-161">A [dokumentu](documentdb-resources.md#documents) można tworzyć przy użyciu hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) metody hello **DocumentClient** klasy.</span><span class="sxs-lookup"><span data-stu-id="160f4-161">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="160f4-162">Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną).</span><span class="sxs-lookup"><span data-stu-id="160f4-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="160f4-163">Można teraz wstawić jeden lub więcej dokumentów.</span><span class="sxs-lookup"><span data-stu-id="160f4-163">We can now insert one or more documents.</span></span> <span data-ttu-id="160f4-164">Jeśli masz już dane, które chcesz toostore w bazie danych, możesz użyć Azure rozwiązania Cosmos DB [narzędzia migracji danych](import-data.md) tooimport hello danych do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="160f4-164">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![Diagram ilustrujący hello hierarchiczną relację między hello konta, hello online bazy danych, kolekcji hello i hello dokumentami używanymi przez hello toocreate samouczka NoSQL aplikację konsoli języka Java](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="160f4-166"><a id="Query"></a>Krok 7. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="160f4-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="160f4-167">Usługa Azure Cosmos DB obsługuje zaawansowane [zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="160f4-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="160f4-168">powitania po przykładowy kod przedstawia sposób tooquery dokumentów w usłudze Azure DB rozwiązania Cosmos przy użyciu składni SQL z hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) metody.</span><span class="sxs-lookup"><span data-stu-id="160f4-168">hello following sample code shows how tooquery documents in Azure Cosmos DB using SQL syntax with hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="160f4-169"><a id="ReplaceDocument"></a>Krok 8. Zastępowanie dokumentu JSON</span><span class="sxs-lookup"><span data-stu-id="160f4-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="160f4-170">Aktualizowanie dokumentów JSON przy użyciu hello obsługuje bazę danych systemu Azure rozwiązania Cosmos [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) metody.</span><span class="sxs-lookup"><span data-stu-id="160f4-170">Azure Cosmos DB supports updating JSON documents using hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="160f4-171"><a id="DeleteDocument"></a>Krok 9. Usuwanie dokumentu JSON</span><span class="sxs-lookup"><span data-stu-id="160f4-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="160f4-172">Podobnie, bazy danych rozwiązania Cosmos Azure obsługuje usuwanie dokumentów JSON przy użyciu hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) metody.</span><span class="sxs-lookup"><span data-stu-id="160f4-172">Similarly, Azure Cosmos DB supports deleting JSON documents using hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="160f4-173"><a id="DeleteDatabase"></a>Krok 10: Usuwanie hello bazy danych</span><span class="sxs-lookup"><span data-stu-id="160f4-173"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="160f4-174">Trwa usuwanie hello utworzone bazy danych usuwa hello bazy danych i wszystkich zasobów podrzędnych (kolekcji, dokumentów itd.).</span><span class="sxs-lookup"><span data-stu-id="160f4-174">Deleting hello created database removes hello database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="160f4-175"><a id="Run"></a>Krok 11. Uruchamianie całej aplikacji konsolowej Java!</span><span class="sxs-lookup"><span data-stu-id="160f4-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="160f4-176">Aplikacja hello toorun z konsoli hello Przejdź toohello projektu i kompilacji za pomocą programu Maven:</span><span class="sxs-lookup"><span data-stu-id="160f4-176">toorun hello application from hello console, navigate toohello project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="160f4-177">Uruchomiona `mvn package` pobiera najnowsze biblioteki Azure DB rozwiązania Cosmos hello z Maven i tworzy `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="160f4-177">Running `mvn package` downloads hello latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="160f4-178">Następnie uruchomienie aplikacji hello za:</span><span class="sxs-lookup"><span data-stu-id="160f4-178">Then run hello app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="160f4-179">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="160f4-179">Congratulations!</span></span> <span data-ttu-id="160f4-180">Pomyślnie ukończono ten samouczek NoSQL i utworzono działającą aplikację konsolową Java!</span><span class="sxs-lookup"><span data-stu-id="160f4-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="160f4-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="160f4-181">Next steps</span></span>
* <span data-ttu-id="160f4-182">Czy chcesz samouczek aplikacji sieci Web w języku Java?</span><span class="sxs-lookup"><span data-stu-id="160f4-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="160f4-183">Zobacz [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md) (Tworzenie aplikacji internetowej w języku Java przy użyciu usługi Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="160f4-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="160f4-184">Dowiedz się, jak za[monitorować konto bazy danych Azure rozwiązania Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="160f4-184">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="160f4-185">Uruchom zapytania względem naszego przykładowego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="160f4-185">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="160f4-186">Dowiedz się więcej o modelu programowania hello w hello opracowanie części hello [stronę dokumentacji bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="160f4-186">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
