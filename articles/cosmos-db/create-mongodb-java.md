---
title: "Azure rozwiązania Cosmos bazy danych: Tworzenie aplikacji konsoli z językiem Java i hello bazy danych MongoDB interfejsu API | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod języka Java, można użyć zapytania tooand tooconnect hello interfejsu API Azure rozwiązania Cosmos bazy danych MongoDB"
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
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a>Azure DB rozwiązania Cosmos: Tworzenie aplikacji konsoli API bazy danych MongoDB z językiem Java i hello portalu Azure

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i przy użyciu kolekcji hello portalu Azure. Będzie tworzenie i wdrażanie aplikacji konsoli oparty na powitania [sterownik bazy danych MongoDB Java](https://docs.mongodb.com/ecosystem/drivers/java/). 

## <a name="prerequisites"></a>Wymagania wstępne

* Przed uruchomieniem tego przykładu, musi mieć hello następujące wymagania wstępne:
   * Zestaw JDK 1.7 lub nowszy (uruchom polecenie `apt-get install default-jdk`, jeśli zestaw JDK nie jest zainstalowany)
   * Narzędzie Maven (uruchom polecenie `apt-get install maven`, jeśli narzędzie Maven nie jest zainstalowane)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a>Dodawanie kolekcji

Nadaj nazwę **db** nowej bazie danych i nazwę **coll** nowej kolekcji.

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Teraz załóżmy aplikacji w klonowania API bazy danych MongoDB z witryny github, Ustaw ciąg połączenia hello i uruchom go. Zobaczysz, jak łatwo jest toowork z danymi programowo. 

1. Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.  

2. Hello uruchom następujące polecenie tooclone hello próbki repozytorium. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. Następnie otwórz plik rozwiązania hello w programie Visual Studio. 

## <a name="review-hello-code"></a>Przejrzyj hello kodu

Upewnijmy szybki przegląd działania wykonywane w aplikacji hello. Otwórz hello `Program.cs` pliku, a dane znajdziesz, te wiersze kodu utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos. 

* zainicjowano Hello DocumentClient.

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* Tworzenie nowej bazy danych i kolekcji.

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* Wstawianie dokumentów za pomocą metody `MongoCollection.insertOne`

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* Wykonywanie zapytań za pomocą metody `MongoCollection.find`

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a>Aktualizowanie parametrów połączenia

Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.

1. Hello konta, zaznacz **Szybki Start**, wybierz Java, a następnie skopiuj do Schowka tooyour ciąg połączenia hello

2. Otwórz hello `Program.java` plików, Zamień Konstruktor MongoClientURI toohello argument hello hello parametry połączenia. Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos. 
    
## <a name="run-hello-console-app"></a>Uruchamianie aplikacji konsoli hello

1. Uruchom `mvn package` w terminalu tooinstall wymagane moduły npm

2. Uruchom `mvn exec:java -D exec.mainClass=GetStarted.Program` w terminalu toostart aplikacji Java.

Można teraz używać [Robomongo](mongodb-robomongo.md) / [3T w Studio](mongodb-mongochef.md) tooquery, modyfikowania i pracy z tym nowych danych.

## <a name="review-slas-in-hello-azure-portal"></a>Przejrzyj umowy SLA w hello portalu Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym szybkiego startu kiedy znasz już jak utworzyć kolekcję za pomocą Eksploratora danych hello toocreate konto bazy danych Azure rozwiązania Cosmos i uruchamianie aplikacji konsoli. Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane. 

> [!div class="nextstepaction"]
> [Importowanie danych z bazy danych MongoDB do usługi Azure Cosmos DB](mongodb-migrate.md)


