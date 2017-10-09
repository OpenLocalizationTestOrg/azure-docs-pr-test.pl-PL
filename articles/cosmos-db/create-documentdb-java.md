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
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a>Azure DB rozwiązania Cosmos: Tworzenie bazy danych dokumentów przy użyciu języka Java i hello portalu Azure

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

Ta opcja szybkiego startu tworzy dokument bazy danych przy użyciu hello narzędzi portalu platformy Azure dla bazy danych Azure rozwiązania Cosmos. Ta opcja szybkiego startu przedstawiono również sposób tooquickly Utwórz aplikację konsoli języka Java przy użyciu hello [interfejsu API języka Java usługi DocumentDB](documentdb-sdk-java.md). instrukcje Hello tego przewodnika Szybki Start można wykonać w dowolnym systemie operacyjnym, który jest w stanie uruchomić oprogramowanie Java. Wykonując tego przewodnika Szybki Start będzie znane tworzenia i modyfikowania zasobów bazy danych dokumentów w hello interfejsu użytkownika lub programowo, nastąpi swoich preferencji.

## <a name="prerequisites"></a>Wymagania wstępne

* [Zestaw Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * Uruchom na Ubuntu, `apt-get install default-jdk` tooinstall hello JDK.
    * Jest zainstalowanym hello JDK czy tooset hello JAVA_HOME środowiska zmiennej toopoint toohello folder.
* [Pobierz](http://maven.apache.org/download.cgi) i [zainstaluj](http://maven.apache.org/install.html) archiwum binarne [Maven](http://maven.apache.org/)
    * Na Ubuntu, można uruchomić `apt-get install maven` tooinstall Maven.
* [Git](https://www.git-scm.com/)
    * Na Ubuntu, można uruchomić `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

Przed utworzeniem dokumentów bazy danych należy toocreate konta bazy danych SQL (DocumentDB) z bazy danych Azure rozwiązania Cosmos.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Dodawanie kolekcji

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Dodawanie danych przykładowych

Teraz można dodać danych tooyour nowej kolekcji za pomocą Eksploratora danych.

1. W Eksploratorze danych hello nowej bazy danych zostanie wyświetlona w okienku Kolekcje hello. Rozwiń hello **zadania** bazy danych, a następnie rozwiń hello **elementów** kolekcji, kliknij przycisk **dokumenty**, a następnie kliknij przycisk **nowych dokumentów**. 

   ![Tworzenie nowych dokumentów w Eksploratorze danych w hello portalu Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. Teraz Dodaj toohello kolekcji dokumentów o hello następujące struktury.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. Po dodaniu hello json toohello **dokumenty** , kliknij pozycję **zapisać**.

    ![Skopiuj dane json, a następnie kliknij przycisk Zapisz w Eksploratorze danych w hello portalu Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  Tworzenie i zapisywanie jeden dokument więcej gdzie wstawić unikatową wartość hello `id` właściwości i zmień hello inne właściwości zgodnie z własnymi potrzebami. Nowe dokumenty mogą mieć dowolną strukturę, ponieważ usługa Azure Cosmos DB nie wymusza żadnego schematu danych.

     Można teraz Użyj zapytania w programie Eksplorator danych tooretrieve dane, klikając hello **edytowanie filtru** i **Zastosuj filtr** przycisków. Domyślnie korzysta z Eksploratora danych `SELECT * FROM c` tooretrieve wszystkich dokumentów w kolekcji hello, ale można zmienić tego tooa różnych [zapytania SQL](documentdb-sql-query.md), takich jak `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn wszystkie dokumenty hello w kolejności malejącej na podstawie sygnatur czasowych. 
 
     Można również użyć Eksploratora danych toocreate przechowywane procedury, funkcje UDF i logiki biznesowej po stronie serwera tooperform wyzwalaczy również jako przepływności skali. Eksplorator danych udostępnia wszystkie hello wbudowanych programowy dostęp do danych dostępne w hello interfejsów API, ale zapewnia łatwy dostęp do danych tooyour w hello portalu Azure.

## <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Teraz załóżmy przełącznika tooworking z kodem. Załóżmy sklonować aplikacji interfejsu API usługi DocumentDB w witrynie GitHub, Ustaw ciąg połączenia hello i uruchom go. Zobacz, jak łatwo jest toowork z danymi programowo. 

1. Otwórz okno terminala git, np. git bash, i `CD` tooa katalog roboczy.  

2. Hello uruchom następujące polecenie tooclone hello próbki repozytorium. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Przejrzyj hello kodu

Upewnijmy szybki przegląd działania wykonywane w aplikacji hello. Otwórz hello `Program.java` plików z folderu \src\GetStarted hello i Znajdź te wiersze kodu, które utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos. 

* Witaj `DocumentClient` został zainicjowany.

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* Tworzenie nowej bazy danych.

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* Tworzenie nowej kolekcji.

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* Tworzenie kilku dokumentów.

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* Wykonywanie zapytania SQL w formacie JSON.

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

## <a name="update-your-connection-string"></a>Aktualizowanie parametrów połączenia

Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello. Spowoduje to włączenie toocommunicate Twojej aplikacji hostowanej bazie danych.

1. W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**. Użyjesz przyciski Kopia hello na powitania po prawej stronie powitania toocopy ekranie powitania identyfikatora URI oraz PRIMARY KEY do hello `Program.java` pliku w następnym kroku hello.

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-documentdb-dotnet/keys.png)

2. W hello Otwórz `Program.java` pliku, skopiuj wartość identyfikatora URI z portalu hello (przy użyciu przycisku Kopiuj hello) i stał się hello wartość hello punktu końcowego toohello DocumentClient konstruktora w `Program.java`. 

    `"https://FILLME.documents.azure.com"`

4. Następnie skopiuj wartość klucza podstawowego z portalu hello i wklej go za pośrednictwem "FILLME", dzięki czemu hello drugi parametr w Konstruktorze DocumentClient hello. Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos. 
    
## <a name="run-hello-app"></a>Uruchamianie aplikacji hello

1. W oknie terminala git hello `cd` toohello azure-cosmos-db-documentdb-java-getting-started folderu.

2. W oknie terminala git hello, wpisz `mvn package` tooinstall hello wymaganych pakietów języka Java.

3. W oknie terminala git hello, uruchom `mvn exec:java -D exec.mainClass=GetStarted.Program` w hello toostart okno terminalu aplikacji Java.

    W oknie terminala hello otrzymasz powiadomienie, że hello FamilyDB baza danych została utworzona i toopress toocontinue klucza. Naciśnij klawisz hello klucza toocreate bazy danych, następnie przełącz toohello Eksplorator danych i zobaczysz, że teraz zawiera FamilyDB bazy danych. Kontynuować toopress klucze toocreate hello kolekcji i hello dokumentów, a następnie wykonaj zapytanie. Po ukończeniu projektu hello hello zasoby są usuwane z Twojego konta. 

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a>Przejrzyj umowy SLA w hello portalu Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym szybkiego startu kiedy znasz już jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i kolekcji za pomocą hello Eksploratora danych, a następnie uruchom toodo aplikacji hello samo programowo. Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane. 

> [!div class="nextstepaction"]
> [Importowanie danych do usługi Azure Cosmos DB](import-data.md)


