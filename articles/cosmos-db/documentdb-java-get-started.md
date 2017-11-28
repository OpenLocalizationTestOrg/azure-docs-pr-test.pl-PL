---
title: "Samouczek NoSQL: usługi DocumentDB interfejsu API Azure rozwiązania Cosmos DB Java SDK | Dokumentacja firmy Microsoft"
description: "Samouczek NoSQL, który powoduje utworzenie bazy danych w trybie online i aplikację konsoli języka Java przy użyciu interfejsu API usługi DocumentDB dla bazy danych Azure rozwiązania Cosmos. Usługa Azure DocumentDB jest bazą danych NoSQL dla formatu JSON."
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
ms.openlocfilehash: 5c4bcda308f001572e1c34e991616fc209250a02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="78786-105">Samouczek NoSQL: tworzenie aplikacji konsoli Java interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="78786-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="78786-106">.NET</span><span class="sxs-lookup"><span data-stu-id="78786-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="78786-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="78786-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="78786-108">Node.js dla MongoDB</span><span class="sxs-lookup"><span data-stu-id="78786-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="78786-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="78786-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="78786-110">Java</span><span class="sxs-lookup"><span data-stu-id="78786-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="78786-111">C++</span><span class="sxs-lookup"><span data-stu-id="78786-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="78786-112">Witamy w samouczku NoSQL dla interfejsu API usługi DocumentDB Azure rozwiązania Cosmos DB Java SDK!</span><span class="sxs-lookup"><span data-stu-id="78786-112">Welcome to the NoSQL tutorial for the DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="78786-113">W ramach tego samouczka zostanie utworzona aplikacja konsolowa, która tworzy zasoby usługi Azure Cosmos DB i wykonuje dla nich zapytania.</span><span class="sxs-lookup"><span data-stu-id="78786-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="78786-114">Zostaną opisane:</span><span class="sxs-lookup"><span data-stu-id="78786-114">We cover:</span></span>

* <span data-ttu-id="78786-115">Tworzenie konta usługi Azure Cosmos DB i łączenie się z nim</span><span class="sxs-lookup"><span data-stu-id="78786-115">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="78786-116">Konfigurowanie rozwiązania Visual Studio</span><span class="sxs-lookup"><span data-stu-id="78786-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="78786-117">Tworzenie bazy danych w trybie online</span><span class="sxs-lookup"><span data-stu-id="78786-117">Creating an online database</span></span>
* <span data-ttu-id="78786-118">Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="78786-118">Creating a collection</span></span>
* <span data-ttu-id="78786-119">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="78786-119">Creating JSON documents</span></span>
* <span data-ttu-id="78786-120">Wykonywanie zapytań względem kolekcji</span><span class="sxs-lookup"><span data-stu-id="78786-120">Querying the collection</span></span>
* <span data-ttu-id="78786-121">Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="78786-121">Creating JSON documents</span></span>
* <span data-ttu-id="78786-122">Wykonywanie zapytań względem kolekcji</span><span class="sxs-lookup"><span data-stu-id="78786-122">Querying the collection</span></span>
* <span data-ttu-id="78786-123">Zastępowanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="78786-123">Replacing a document</span></span>
* <span data-ttu-id="78786-124">Usuwanie dokumentu</span><span class="sxs-lookup"><span data-stu-id="78786-124">Deleting a document</span></span>
* <span data-ttu-id="78786-125">Usuwanie bazy danych</span><span class="sxs-lookup"><span data-stu-id="78786-125">Deleting the database</span></span>

<span data-ttu-id="78786-126">Teraz do dzieła!</span><span class="sxs-lookup"><span data-stu-id="78786-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78786-127">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="78786-127">Prerequisites</span></span>
<span data-ttu-id="78786-128">Upewnij się, że masz:</span><span class="sxs-lookup"><span data-stu-id="78786-128">Make sure you have the following:</span></span>

* <span data-ttu-id="78786-129">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="78786-129">An active Azure account.</span></span> <span data-ttu-id="78786-130">Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="78786-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="78786-131">Na potrzeby tego samouczka możesz także użyć [emulatora usługi Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="78786-131">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="78786-132">Git</span><span class="sxs-lookup"><span data-stu-id="78786-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="78786-133">[Zestaw Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="78786-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="78786-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="78786-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="78786-135">Krok 1. Tworzenie konta usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="78786-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="78786-136">Utwórzmy konto usługi Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="78786-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="78786-137">Jeśli masz już konto, którego chcesz użyć, możesz przejść od razu do kroku [Klonowanie projektu GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="78786-137">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span></span> <span data-ttu-id="78786-138">Jeśli używasz emulatora usługi Azure Cosmos DB, wykonaj czynności opisane w temacie [Emulator usługi Azure Cosmos DB](local-emulator.md), aby skonfigurować emulator, a następnie przejdź do kroku [Klonowanie projektu GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="78786-138">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="78786-139"><a id="GitClone"></a>Krok 2. Klonowanie projektu GitHub</span><span class="sxs-lookup"><span data-stu-id="78786-139"><a id="GitClone"></a>Step 2: Clone the GitHub project</span></span>
<span data-ttu-id="78786-140">Możesz rozpocząć od sklonowania repozytorium GitHub na potrzeby pracy z tematem [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started) (Rozpoczynanie pracy z usługą Azure Cosmos DB i językiem Java).</span><span class="sxs-lookup"><span data-stu-id="78786-140">You can get started by cloning the GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="78786-141">Na przykład z katalogu lokalnego uruchom następujące polecenie, aby lokalnie pobrać przykładowy projekt.</span><span class="sxs-lookup"><span data-stu-id="78786-141">For example, from a local directory run the following to retrieve the sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="78786-142">Katalog zawiera `pom.xml` dla projektu i `src` folder zawierający kod źródłowy Java w tym `Program.java` które pokazuje sposób wykonywaniem prostych operacji dotyczących bazy danych rozwiązania Cosmos platformy Azure, takich jak tworzenie dokumentów i wykonywanie zapytania na danych w ramach kolekcji .</span><span class="sxs-lookup"><span data-stu-id="78786-142">The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="78786-143">Plik `pom.xml` zawiera zależność dla [zestawu Java SDK bazy danych DocumentDB w Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="78786-143">The `pom.xml` includes a dependency on the [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="78786-144"><a id="Connect"></a>Krok 3. Łączenie się z kontem usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="78786-144"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="78786-145">Następnie wróć do witryny [Azure Portal](https://portal.azure.com), aby pobrać punkt końcowy i główny klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="78786-145">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span></span> <span data-ttu-id="78786-146">Klucz podstawowy i punkt końcowy usługi Azure Cosmos DB są niezbędne, aby aplikacja wiedziała, z jakim elementem ma się połączyć, oraz aby usługa Azure Cosmos DB ufała połączeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="78786-146">The Azure Cosmos DB endpoint and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="78786-147">W witrynie Azure Portal przejdź do swojego konta usługi Azure Cosmos DB i kliknij pozycję **Klucze**.</span><span class="sxs-lookup"><span data-stu-id="78786-147">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="78786-148">Skopiuj identyfikator URI z portalu i wklej go w miejsce `https://FILLME.documents.azure.com` w pliku Program.java.</span><span class="sxs-lookup"><span data-stu-id="78786-148">Copy the URI from the portal and paste it into `https://FILLME.documents.azure.com` in the Program.java file.</span></span> <span data-ttu-id="78786-149">Następnie skopiuj KLUCZ PODSTAWOWY z portalu i wklej go w miejsce `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="78786-149">Then copy the PRIMARY KEY from the portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Zrzut ekranu przedstawiający witrynę Azure Portal używaną przez samouczek NoSQL do tworzenia aplikacji konsolowej Java.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="78786-152">Krok 4. Tworzenie bazy danych</span><span class="sxs-lookup"><span data-stu-id="78786-152">Step 4: Create a database</span></span>
<span data-ttu-id="78786-153">Własną [bazę danych](documentdb-resources.md#databases) usługi Azure Cosmos DB można utworzyć za pomocą metody [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="78786-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of the **DocumentClient** class.</span></span> <span data-ttu-id="78786-154">Baza danych jest kontenerem logicznym magazynu dokumentów JSON podzielonym na partycje w kolekcjach.</span><span class="sxs-lookup"><span data-stu-id="78786-154">A database is the logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="78786-155"><a id="CreateColl"></a>Krok 5. Tworzenie kolekcji</span><span class="sxs-lookup"><span data-stu-id="78786-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="78786-156">Metoda **createCollection** tworzy nową kolekcję z zarezerwowaną przepływnością, co ma wpływ na cenę.</span><span class="sxs-lookup"><span data-stu-id="78786-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="78786-157">Aby uzyskać więcej informacji, odwiedź naszą [stronę cennika](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="78786-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="78786-158">[Kolekcję](documentdb-resources.md#collections) można utworzyć za pomocą metody [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="78786-158">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of the **DocumentClient** class.</span></span> <span data-ttu-id="78786-159">Kolekcja jest kontenerem dokumentów JSON i skojarzonej logiki aplikacji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="78786-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="78786-160"><a id="CreateDoc"></a>Krok 6. Tworzenie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="78786-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="78786-161">[Dokument](documentdb-resources.md#documents) można utworzyć za pomocą metody [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) klasy **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="78786-161">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of the **DocumentClient** class.</span></span> <span data-ttu-id="78786-162">Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną).</span><span class="sxs-lookup"><span data-stu-id="78786-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="78786-163">Można teraz wstawić jeden lub więcej dokumentów.</span><span class="sxs-lookup"><span data-stu-id="78786-163">We can now insert one or more documents.</span></span> <span data-ttu-id="78786-164">Jeśli masz już dane, które chcesz przechowywać w bazie danych, możesz użyć Azure rozwiązania Cosmos DB [narzędzia migracji danych](import-data.md) do importowania danych do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="78786-164">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) to import the data into a database.</span></span>

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

![Diagram pokazujący hierarchiczną relację między kontem, bazą danych w trybie online, kolekcją i dokumentami używanymi przez samouczek NoSQL do tworzenia aplikacji konsolowej Java](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="78786-166"><a id="Query"></a>Krok 7. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="78786-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="78786-167">Usługa Azure Cosmos DB obsługuje zaawansowane [zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="78786-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="78786-168">Następujący przykładowy kod przedstawia sposób wykonania zapytania względem dokumentów w usłudze Azure Cosmos DB przy użyciu składni SQL za pomocą metody [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments).</span><span class="sxs-lookup"><span data-stu-id="78786-168">The following sample code shows how to query documents in Azure Cosmos DB using SQL syntax with the [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="78786-169"><a id="ReplaceDocument"></a>Krok 8. Zastępowanie dokumentu JSON</span><span class="sxs-lookup"><span data-stu-id="78786-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="78786-170">Usługa Azure Cosmos DB obsługuje aktualizowanie dokumentów JSON za pomocą metody [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument).</span><span class="sxs-lookup"><span data-stu-id="78786-170">Azure Cosmos DB supports updating JSON documents using the [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="78786-171"><a id="DeleteDocument"></a>Krok 9. Usuwanie dokumentu JSON</span><span class="sxs-lookup"><span data-stu-id="78786-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="78786-172">Podobnie usługa Azure Cosmos DB obsługuje usuwanie dokumentów JSON za pomocą metody [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument).</span><span class="sxs-lookup"><span data-stu-id="78786-172">Similarly, Azure Cosmos DB supports deleting JSON documents using the [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="78786-173"><a id="DeleteDatabase"></a>Krok 10. Usuwanie bazy danych</span><span class="sxs-lookup"><span data-stu-id="78786-173"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="78786-174">Usunięcie utworzonej bazy danych usunie bazę danych i wszystkie zasoby podrzędne (kolekcje, dokumenty itd.).</span><span class="sxs-lookup"><span data-stu-id="78786-174">Deleting the created database removes the database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="78786-175"><a id="Run"></a>Krok 11. Uruchamianie całej aplikacji konsolowej Java!</span><span class="sxs-lookup"><span data-stu-id="78786-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="78786-176">Aby uruchomić aplikację z poziomu konsoli, przejdź do folderu projektu i skompilować za pomocą programu Maven:</span><span class="sxs-lookup"><span data-stu-id="78786-176">To run the application from the console, navigate to the project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="78786-177">Uruchomienie polecenia `mvn package` spowoduje pobranie najnowszej biblioteki Azure Cosmos DB z narzędzia Maven i utworzenie pliku `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="78786-177">Running `mvn package` downloads the latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="78786-178">Następnie można uruchomić aplikację za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="78786-178">Then run the app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="78786-179">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="78786-179">Congratulations!</span></span> <span data-ttu-id="78786-180">Pomyślnie ukończono ten samouczek NoSQL i utworzono działającą aplikację konsolową Java!</span><span class="sxs-lookup"><span data-stu-id="78786-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="78786-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="78786-181">Next steps</span></span>
* <span data-ttu-id="78786-182">Czy chcesz samouczek aplikacji sieci Web w języku Java?</span><span class="sxs-lookup"><span data-stu-id="78786-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="78786-183">Zobacz [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md) (Tworzenie aplikacji internetowej w języku Java przy użyciu usługi Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="78786-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="78786-184">Dowiedz się, jak [monitorować konto usługi Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="78786-184">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="78786-185">Uruchom zapytania względem naszego przykładowego zestawu danych na [placu zabaw dla zapytań](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="78786-185">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="78786-186">Dowiedz się więcej o modelu programowania w sekcji Dla deweloperów [strony dokumentacji usługi Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="78786-186">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
