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
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a>Samouczek NoSQL: tworzenie aplikacji konsoli Java interfejsu API usługi DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js dla MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Samouczek NoSQL powitalnej toohello dla hello interfejsu API Azure rozwiązania Cosmos DB Java SDK usługi DocumentDB! W ramach tego samouczka zostanie utworzona aplikacja konsolowa, która tworzy zasoby usługi Azure Cosmos DB i wykonuje dla nich zapytania.

Zostaną opisane:

* Tworzenie i łączenie tooan konta bazy danych Azure rozwiązania Cosmos
* Konfigurowanie rozwiązania Visual Studio
* Tworzenie bazy danych w trybie online
* Tworzenie kolekcji
* Tworzenie dokumentów JSON
* Wykonywanie zapytania hello kolekcji
* Tworzenie dokumentów JSON
* Wykonywanie zapytania hello kolekcji
* Zastępowanie dokumentu
* Usuwanie dokumentu
* Usunięcie hello bazy danych

Teraz do dzieła!

## <a name="prerequisites"></a>Wymagania wstępne
Upewnij się, że masz następujące hello:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/). Alternatywnie można użyć hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) w tym samouczku.
* [Git](https://git-scm.com/downloads)
* [Zestaw Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Maven](http://maven.apache.org/download.cgi).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Krok 1. Tworzenie konta usługi Azure Cosmos DB
Utwórzmy konto usługi Azure Cosmos DB. Jeśli masz już konto ma toouse, możesz przejść od razu zbyt[projektu GitHub hello w klonowania](#GitClone). Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, wykonaj czynności hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) tooset Konfigurowanie hello emulatora i przejść od razu zbyt[projektu GitHub hello w klonowania](#GitClone).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a>Krok 2: Klonowania hello GitHub projektu
Możesz rozpocząć pracę w klonowania repozytorium GitHub hello [Rozpoczynanie pracy z bazy danych Azure rozwiązania Cosmos i Java](https://github.com/Azure-Samples/documentdb-java-getting-started). Na przykład z katalogu lokalnego uruchamiania powitania po tooretrieve hello przykładowy projekt lokalnie.

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

katalog Hello zawiera `pom.xml` hello projektu i `src` folder zawierający kod źródłowy Java w tym `Program.java` które pokazuje sposób wykonywaniem prostych operacji dotyczących bazy danych rozwiązania Cosmos platformy Azure, takich jak tworzenie dokumentów i wykonywanie zapytania na danych w ramach Kolekcja. Witaj `pom.xml` zawiera zależności hello [zestawu SDK Java usługi DocumentDB w przypadku Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a>Krok 3: Łączenie tooan konta bazy danych Azure rozwiązania Cosmos
Następnie head kopii toohello [Azure Portal](https://portal.azure.com) tooretrieve punktu końcowego, a podstawowy klucz główny. Hello Azure DB rozwiązania Cosmos punktu końcowego i klucz podstawowy są niezbędne do Twojej aplikacji toounderstand gdzie tooconnect na oraz bazy danych Azure rozwiązania Cosmos tootrust połączeniu aplikacji.

W hello portalu Azure, przejdź do konta bazy danych Azure rozwiązania Cosmos tooyour, a następnie kliknij **klucze**. Skopiuj hello identyfikatora URI z portalu hello i wklej ją do `https://FILLME.documents.azure.com` w pliku Program.java hello. Następnie kopiowania hello klucza podstawowego z portalu hello i wklej ją do `FILLME`.

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Zrzut ekranu przedstawiający hello Portal Azure używany przez hello toocreate samouczka NoSQL aplikację konsoli języka Java. Pokazuje bazy danych Azure rozwiązania Cosmos konto, z wyróżnionym, AKTYWNYM Centrum hello hello przyciskiem KLUCZE wyróżnionym w bloku konta usługi Azure DB rozwiązania Cosmos hello i hello wartości identyfikatora URI, klucz podstawowy i klucz POMOCNICZY wyróżnionymi w hello bloku klucze][keys]

## <a name="step-4-create-a-database"></a>Krok 4. Tworzenie bazy danych
Bazy danych programu Azure rozwiązania Cosmos [bazy danych](documentdb-resources.md#databases) można tworzyć przy użyciu hello [metody createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) metody hello **DocumentClient** klasy. Baza danych jest hello kontenerem logicznym magazynu dokumentów JSON podzielonym na partycje w kolekcjach.

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a>Krok 5. Tworzenie kolekcji
> [!WARNING]
> Metoda **createCollection** tworzy nową kolekcję z zarezerwowaną przepływnością, co ma wpływ na cenę. Aby uzyskać więcej informacji, odwiedź naszą [stronę cennika](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

A [kolekcji](documentdb-resources.md#collections) można tworzyć przy użyciu hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) metody hello **DocumentClient** klasy. Kolekcja jest kontenerem dokumentów JSON i skojarzonej logiki aplikacji JavaScript.


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a>Krok 6. Tworzenie dokumentów JSON
A [dokumentu](documentdb-resources.md#documents) można tworzyć przy użyciu hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) metody hello **DocumentClient** klasy. Dokumenty są zawartością JSON zdefiniowaną przez użytkownika (dowolną). Można teraz wstawić jeden lub więcej dokumentów. Jeśli masz już dane, które chcesz toostore w bazie danych, możesz użyć Azure rozwiązania Cosmos DB [narzędzia migracji danych](import-data.md) tooimport hello danych do bazy danych.

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

## <a id="Query"></a>Krok 7. Wykonanie zapytania względem zasobów usługi Azure Cosmos DB
Usługa Azure Cosmos DB obsługuje zaawansowane [zapytania](documentdb-sql-query.md) względem dokumentów JSON przechowywanych w każdej kolekcji.  powitania po przykładowy kod przedstawia sposób tooquery dokumentów w usłudze Azure DB rozwiązania Cosmos przy użyciu składni SQL z hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) metody.

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a>Krok 8. Zastępowanie dokumentu JSON
Aktualizowanie dokumentów JSON przy użyciu hello obsługuje bazę danych systemu Azure rozwiązania Cosmos [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) metody.

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a>Krok 9. Usuwanie dokumentu JSON
Podobnie, bazy danych rozwiązania Cosmos Azure obsługuje usuwanie dokumentów JSON przy użyciu hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) metody.  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a>Krok 10: Usuwanie hello bazy danych
Trwa usuwanie hello utworzone bazy danych usuwa hello bazy danych i wszystkich zasobów podrzędnych (kolekcji, dokumentów itd.).

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a>Krok 11. Uruchamianie całej aplikacji konsolowej Java!
Aplikacja hello toorun z konsoli hello Przejdź toohello projektu i kompilacji za pomocą programu Maven:
    
    mvn package

Uruchomiona `mvn package` pobiera najnowsze biblioteki Azure DB rozwiązania Cosmos hello z Maven i tworzy `GetStarted-0.0.1-SNAPSHOT.jar`. Następnie uruchomienie aplikacji hello za:

    mvn exec:java -D exec.mainClass=GetStarted.Program

Gratulacje! Pomyślnie ukończono ten samouczek NoSQL i utworzono działającą aplikację konsolową Java!

## <a name="next-steps"></a>Następne kroki
* Czy chcesz samouczek aplikacji sieci Web w języku Java? Zobacz [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md) (Tworzenie aplikacji internetowej w języku Java przy użyciu usługi Azure Cosmos DB).
* Dowiedz się, jak za[monitorować konto bazy danych Azure rozwiązania Cosmos](monitor-accounts.md).
* Uruchom zapytania względem naszego przykładowego zestawu danych w hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo).
* Dowiedz się więcej o modelu programowania hello w hello opracowanie części hello [stronę dokumentacji bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
