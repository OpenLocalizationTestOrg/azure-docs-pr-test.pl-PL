---
title: "Tworzenie bazy danych dokumentów usługi Azure Cosmos DB przy użyciu języka Java | Microsoft Docs"
description: "Przykładowy kod Java, którego można używać do nawiązywania połączeń z interfejsem API SQL usługi Azure Cosmos DB i wykonywania względem niego zapytań"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc, devcenter
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 12/15/2017
ms.author: mimig
ms.openlocfilehash: 85f8310235e0f5b038f2b55c94fe044d1a9d9719
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-the-azure-portal"></a>Azure Cosmos DB: Tworzenie bazy danych dokumentów przy użyciu języka Java i witryny Azure Portal

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)] 

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Usługa Azure Cosmos DB umożliwia szybkie tworzenie i wysyłanie zapytań do zarządzanych baz danych dokumentów, tabel i grafowych.

Ten przewodnik Szybki start tworzy bazę danych dokumentów przy użyciu narzędzi witryny Azure Portal dla usługi Azure Cosmos DB. Ponadto ten przewodnik Szybki start pokazuje, jak szybko utworzyć aplikację konsolową Java przy użyciu [interfejsu API SQL języka Java](sql-api-sdk-java.md). Instrukcje podane w tym przewodniku Szybki start można wykonać w dowolnym systemie operacyjnym, w którym można uruchomić oprogramowanie Java. Realizując ten przewodnik Szybki start, zaznajomisz się z tworzeniem i modyfikowaniem zasobów bazy danych dokumentów z wykorzystaniem interfejsu użytkownika lub programowo, zgodnie z preferencjami.

## <a name="prerequisites"></a>Wymagania wstępne

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 
[!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

Ponadto: 

* [Zestaw Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * W systemie Ubuntu uruchom polecenie `apt-get install default-jdk`, aby zainstalować zestaw JDK.
    * Upewnij się, że zmienna środowiskowa JAVA_HOME wskazuje folder, w którym zainstalowano zestaw JDK.
* [Pobierz](http://maven.apache.org/download.cgi) i [zainstaluj](http://maven.apache.org/install.html) archiwum binarne [Maven](http://maven.apache.org/)
    * W systemie Ubuntu możesz uruchomić polecenie `apt-get install maven`, aby zainstalować narzędzie Maven.
* [Git](https://www.git-scm.com/)
    * W systemie Ubuntu możesz uruchomić polecenie `sudo apt-get install git`, aby zainstalować usługę Git.

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

Przed utworzeniem bazy danych dokumentów musisz utworzyć konto bazy danych SQL przy użyciu usługi Azure Cosmos DB.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Dodawanie kolekcji

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Dodawanie danych przykładowych

Teraz można dodać dane do nowej kolekcji za pomocą Eksploratora danych.

1. Rozwiń kolekcję **Elementy**, kliknij pozycję **Dokumenty** > **Nowy dokument**.

   ![Tworzenie nowych dokumentów w Eksploratorze danych w witrynie Azure Portal](./media/create-sql-api-java/azure-cosmosdb-data-explorer-new-document.png)
  
2. Teraz dodaj dokument do kolekcji o następującej strukturze i kliknij przycisk **Zapisz**.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

    ![Kopiowanie danych json i klikanie pozycji Zapisz w Eksploratorze danych w witrynie Azure Portal](./media/create-sql-api-java/azure-cosmosdb-data-explorer-save-document.png)

3.  Utwórz i zapisz jeszcze jeden dokument, w którym wartość `id` została zmieniona na 2, i zmień inne właściwości wedle uznania. Nowe dokumenty mogą mieć dowolną strukturę, ponieważ usługa Azure Cosmos DB nie wymusza żadnego schematu danych.

## <a name="query-your-data"></a>Wysyłanie zapytań dotyczących danych

Teraz można użyć zapytań w Eksploratorze danych w celu pobrania i filtrowania danych.

1. Domyślnie zapytanie jest ustawione na `SELECT * FROM c`. To domyślne zapytanie pobiera i wyświetla wszystkie dokumenty w kolekcji. 

    ![Domyślne zapytanie w Eksploratorze danych to „SELECT * FROM c”](./media/create-sql-api-java/azure-cosmosdb-data-explorer-query.png)

2. Zmień zapytanie, klikając przycisk **Edytuj filtr**, dodając `ORDER BY c._ts DESC` do pola predykatu zapytania, a następnie klikając pozycję **Zastosuj filtr**.

    ![Zmień zapytanie domyślne przez dodanie ORDER BY c._ts DESC i kliknij pozycję Zastosuj filtr](./media/create-sql-api-java/azure-cosmosdb-data-explorer-edit-query.png)

To zmodyfikowane zapytanie wyświetla dokumenty w kolejności malejącej według ich sygnatury czasowej, więc drugi dokument jest wyświetlany na początku listy. Jeśli znasz składnię SQL, w tym polu możesz wprowadzić dowolne obsługiwane [zapytanie SQL](sql-api-sql-query.md). 

Na tym kończy się praca w Eksploratorze danych. Przed przejściem do pracy z kodem należy zapamiętać, że Eksplorator danych umożliwia również tworzenie procedur składowanych, funkcji definiowanych przez użytkownika (UDF) i wyzwalaczy w celu wykonania logiki biznesowej po stronie serwera oraz skalowania przepływności. Eksplorator danych udostępnia wszystkie wbudowane programowe procedury dostępu do danych w interfejsach API, ale umożliwia łatwy dostęp do danych za pośrednictwem witryny Azure Portal.

## <a name="clone-the-sample-application"></a>Klonowanie przykładowej aplikacji

Teraz przejdźmy do pracy z kodem. Sklonujmy aplikację interfejsu API SQL z serwisu GitHub, ustawmy parametry połączenia i uruchommy ją. Zobaczysz, jak łatwo jest pracować programowo z danymi. 

1. Otwórz wiersz polecenia, utwórz nowy folder o nazwie git-samples, a następnie zamknij wiersz polecenia.

    ```bash
    md "C:\git-samples"
    ```

2. Otwórz okno terminala usługi Git, np. git bash, i użyj polecenia `cd`, aby przejść do nowego folderu instalacji aplikacji przykładowej. 

    ```bash
    cd "C:\git-samples"
    ```

3. Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium. To polecenie tworzy kopię przykładowej aplikacji na komputerze.

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-the-code"></a>Przeglądanie kodu

Ten krok jest opcjonalny. Jeśli chcesz dowiedzieć się, jak zasoby bazy danych są tworzone w kodzie, możesz przejrzeć poniższe fragmenty kodu. Wszystkie fragmenty kodu pochodzą z pliku `Program.java` zainstalowanego w folderze C:\git-samples\azure-cosmos-db-documentdb-java-getting-started\src\GetStarted. W przeciwnym razie możesz od razu przejść do sekcji [Aktualizowanie parametrów połączenia](#update-your-connection-string). 

* Inicjowanie klienta `DocumentClient`. [DocumentClient](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._document_client) zapewnia logiczną reprezentację usługi bazy danych Azure Cosmos DB po stronie klienta. Ten klient jest używany do konfigurowania i wykonywania żądań dotyczących usługi.

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* Tworzenie elementu [Database](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._database).

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* Tworzenie elementu [DocumentCollection](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._document_collection).

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* Tworzenie dokumentów przy użyciu metody [createDocument](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._document_client.createdocument).

    ```java
    // Any Java object within your code can be serialized into JSON and written to Azure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* Zapytania SQL w formacie JSON są wykonywane przy użyciu metody [queryDocuments](https://docs.microsoft.com/java/api/com.microsoft.azure.documentdb._document_client.querydocuments).

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

Teraz wróć do witryny Azure Portal, aby uzyskać informacje o parametrach połączenia i skopiować je do aplikacji. Umożliwia to aplikacji komunikację z hostowaną bazą danych.

1. W witrynie [Azure Portal](http://portal.azure.com/) kliknij pozycję **Klucze**. 

    Użyj przycisków kopiowania po prawej stronie ekranu, aby skopiować najwyższą wartość, czyli identyfikator URI.

    ![Wyświetlanie i kopiowanie klucza dostępu w witrynie Azure Portal, strona Klucze](./media/create-sql-api-java/keys.png)

2. Otwórz plik `Program.java` w folderze C:\git-samples\azure-cosmos-db-documentdb-java-getting-started\src\GetStarted. 

3. Wklej wartość identyfikatora URI z portalu do elementu `https://FILLME.documents.azure.com` w wierszu 45.

4. Wróć do portalu i skopiuj wartość KLUCZA PODSTAWOWEGO, jak pokazano na zrzucie ekranu. Wklej wartość KLUCZA PODSTAWOWEGO z portalu do elementu `FILLME` w wierszu 46.

    Metoda getStartedDemo powinna teraz wyglądać podobnie do poniższej: 
    
    ```java
    private void getStartedDemo() throws DocumentClientException, IOException {
        this.client = new DocumentClient("https://youraccountname.documents.azure.com:443/",
                "your-primary-key...RJhQrqQ5QQ==", 
                new ConnectionPolicy(),
                ConsistencyLevel.Session);
    ```

5. Zapisz plik Program.java.

## <a name="run-the-app"></a>Uruchomienie aplikacji

1. W oknie terminalu usługi Git za pomocą polecenia `cd` przejdź do folderu azure-cosmos-db-documentdb-java-getting-started.

    ```git
    cd "C:\git-samples\azure-cosmos-db-documentdb-java-getting-started"
    ```

2. W oknie terminala usługi Git użyj następującego polecenia, aby zainstalować wymagane pakiety języka Java.

    ```
    mvn package
    ```

3. W oknie terminala usługi Git użyj następującego polecenia, aby uruchomić aplikację języka Java.

    ```
    mvn exec:java -D exec.mainClass=GetStarted.Program
    ```

    Okno terminala wyświetli powiadomienie o utworzeniu bazy danych FamilyDB. 
    
4. Naciśnij dowolny klawisz, aby utworzyć kolekcję. 

5. Wróć do Eksploratora danych, a zobaczysz, że teraz zawiera bazę danych FamilyDB.
    
6. Nadal naciskaj klawisze w oknie konsoli, aby kod tworzył dokumenty i wysyłał zapytania.
    
    Na końcu programu wszystkie zasoby z tej aplikacji są usuwane z konta, aby nie powodować naliczania żadnych opłat. 

    ![Dane wyjściowe konsoli](./media/create-sql-api-java/console-output.png)


## <a name="review-slas-in-the-azure-portal"></a>Przeglądanie umów SLA w witrynie Azure Portal

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start wyjaśniono sposób tworzenia konta usługi Azure Cosmos DB, bazy danych dokumentów i kolekcji za pomocą Eksploratora danych oraz uruchamiania aplikacji w celu wykonania tych samych czynności w sposób programowy. Teraz możesz zaimportować dodatkowe dane do kolekcji usługi Azure Cosmos DB. 

> [!div class="nextstepaction"]
> [Importowanie danych do usługi Azure Cosmos DB](import-data.md)


