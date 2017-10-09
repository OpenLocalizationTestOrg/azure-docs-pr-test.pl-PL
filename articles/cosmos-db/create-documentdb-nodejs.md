---
title: "Azure rozwiązania Cosmos bazy danych: Tworzenie aplikacji za pomocą języka Node.js i hello interfejsu API usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod Node.js, można użyć zapytania tooand tooconnect hello interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a>Azure DB rozwiązania Cosmos: Tworzenie aplikacji interfejsu API usługi DocumentDB za pomocą języka Node.js i hello portalu Azure

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i przy użyciu kolekcji hello portalu Azure. Następnie skompilować i uruchomić aplikację konsoli oparty na powitania [interfejsu API środowiska Node.js usługi DocumentDB](documentdb-sdk-node.md).

## <a name="prerequisites"></a>Wymagania wstępne

* Przed uruchomieniem tego przykładu, musi mieć hello następujące wymagania wstępne:
    * [Node.js](https://nodejs.org/en/) w wersji 0.10.29 lub nowszej
    * [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Dodawanie kolekcji

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Teraz załóżmy aplikacji w klonowania interfejs API usługi DocumentDB z serwisu github, Ustaw ciąg połączenia hello i uruchom go. Zobacz, jak łatwo jest toowork z danymi programowo. 

1. Otwórz okno terminala git, np. git bash, i `CD` tooa katalog roboczy.  

2. Hello uruchom następujące polecenie tooclone hello próbki repozytorium. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a>Przejrzyj hello kodu

Upewnijmy szybki przegląd działania wykonywane w aplikacji hello. Otwórz hello `app.js` plików i można znaleźć, te wiersze kodu utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos. 

* Witaj `documentClient` został zainicjowany.

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* Tworzenie nowej bazy danych.

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Tworzenie nowej kolekcji.

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Tworzenie kilku dokumentów.

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Wykonywanie zapytania SQL w formacie JSON.

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a>Aktualizowanie parametrów połączenia

Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.

1. W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**. Użyjesz przyciski Kopia hello na powitania po prawej stronie powitania toocopy ekranie powitania identyfikatora URI oraz Primary Key do hello `config.js` pliku w następnym kroku hello.

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-documentdb-dotnet/keys.png)

2. W otwartych hello `config.js` pliku. 

3. Skopiuj wartość identyfikatora URI z portalu hello (przy użyciu przycisku Kopiuj hello) i przydzielić mu hello wartością klucza punktu końcowego hello `config.js`. 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. Skopiuj wartość klucza podstawowego z portalu hello i stał się hello wartość hello `config.primaryKey` w `config.js`. Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos. 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a>Uruchamianie aplikacji hello
1. Uruchom `npm install` w terminalu tooinstall wymagane moduły npm

2. Uruchom `node app.js` w terminalu toostart aplikacji węzła.

Teraz można wrócić do poprzedniej strony tooData Explorer i zobacz zapytania, modyfikowania i pracy z tym nowych danych. 

## <a name="review-slas-in-hello-azure-portal"></a>Przejrzyj umowy SLA w hello portalu Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym szybkiego startu kiedy znasz już jak utworzyć kolekcję za pomocą Eksploratora danych hello toocreate konto bazy danych Azure rozwiązania Cosmos i uruchamianie aplikacji. Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane. 

> [!div class="nextstepaction"]
> [Importowanie danych do usługi Azure Cosmos DB](import-data.md)


