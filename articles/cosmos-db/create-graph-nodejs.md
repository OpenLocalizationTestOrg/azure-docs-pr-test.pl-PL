---
title: "Tworzenie aplikacji Node.js usługi Azure Cosmos DB za pomocą interfejsu API programu Graph | Microsoft Docs"
description: "Przykładowy kod Node.js, którego można używać do nawiązywania połączeń z usługą Azure Cosmos DB i wykonywania w niej zapytań"
services: cosmos-db
documentationcenter: 
author: luisbosquez
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 01/08/2018
ms.author: lbosq
ms.openlocfilehash: 95c0ac43e468d3655cfddc7ae0de6cefb649131d
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/08/2018
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a>Azure Cosmos DB: Tworzenie aplikacji Node.js za pomocą interfejsu API programu Graph

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Dzięki wykorzystaniu dystrybucji globalnej i możliwości skalowania poziomego opartego na usłudze Azure Cosmos DB, możesz szybko tworzyć i za pomocą zapytań badać bazy danych dokumentów, par klucz/wartość oraz grafów. 

Ten artykuł Szybki start przedstawia sposób tworzenia konta usługi Azure Cosmos DB dla interfejsu API programu Graph, bazy danych i grafu przy użyciu witryny Azure Portal. Następnie przy użyciu sterownika open source [Node.js Gremlin](https://www.npmjs.com/package/gremlin) zostanie utworzona i uruchomiona aplikacja konsoli.

## <a name="prerequisites"></a>Wymagania wstępne

Przed uruchomieniem tego przykładu muszą być spełnione następujące wymagania wstępne:
* [Node.js](https://nodejs.org/en/) w wersji 0.10.29 lub nowszej
* [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Dodawanie grafu

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a>Klonowanie przykładowej aplikacji

Teraz sklonujemy aplikację interfejsu API programu Graph z repozytorium GitHub, ustawimy parametry połączenia i uruchomimy ją. Zobaczysz, jak łatwo jest pracować programowo z danymi. 

1. Otwórz okno terminala usługi Git, na przykład Git Bash, i za pomocą polecenia `cd` przejdź do katalogu roboczego.

2. Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium: 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. Otwórz plik rozwiązania w programie Visual Studio. 

## <a name="review-the-code"></a>Przeglądanie kodu

Dokonajmy szybkiego przeglądu działań wykonywanych w aplikacji. Otwórz plik `app.js`, w którym zobaczysz następujące wiersze kodu. 

* Tworzenie klienta języka Gremlin.

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  Wszystkie konfiguracje są w pliku `config.js`, który będziemy edytować w [następnej sekcji](#update-your-connection-string).

* W celu wykonywania różnych operacji języka Gremlin zdefiniowano serie funkcji. To jest jedna z nich:

    ```nodejs
    function addVertex1(callback)
    {
        console.log('Running Add Vertex1'); 
        client.execute("g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44).property('userid', 1)", { }, (err, results) => {
          if (err) callback(console.error(err));
          console.log("Result: %s\n", JSON.stringify(results));
          callback(null)
        });
    }
    ```

* Każda funkcja wykonuje metodę `client.execute` z parametrem ciągu zapytania języka Gremlin. Oto przykład wykonywania metody `g.V().count()`:

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

* Na końcu pliku wszystkie metody są wywoływane przy użyciu metody `async.waterfall()`. Powoduje wykonywanie ich jedna po drugiej:

    ```nodejs
    try{
        async.waterfall([
            dropGraph,
            addVertex1,
            addVertex2,
            addEdge,
            countVertices
            ], finish);
    } catch(err) {
        console.log(err)
    }
    ```


## <a name="update-your-connection-string"></a>Aktualizowanie parametrów połączenia

1. Otwórz plik config.js. 

2. W pliku config.js przypisz kluczowi `config.endpoint` wartość **Identyfikator URI Gremlin** ze strony **Przegląd** w witrynie Azure Portal. 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Wyświetlanie i kopiowanie klucza dostępu w witrynie Azure Portal, blok Klucze](./media/create-graph-nodejs/gremlin-uri.png)

   Jeśli wartość **Identyfikator URI Gremlin** jest pusta, można wygenerować wartość ze strony **Klucze** w portalu. Użyj wartości **URI**, usuń ciąg https:// i zmień wartość documents na wartość gremlin.cosmosdb. Jeśli konto programu Graph zostało utworzone przed 20 grudnia 2017 zmień wartość documents na wartość graphs. 

   Punkt końcowy Gremlin musi być samą nazwą hosta, bez protokołu/numeru portu, czyli powinien mieć postać `mygraphdb.gremlin.cosmosdb.azure.com` (a nie `https://mygraphdb.gremlin.cosmosdb.azure.com` lub `mygraphdb.gremlin.cosmosdb.azure.com:433`).

3. W pliku config.js przypisz elementowi config.primaryKey wartość z pola **Klucz podstawowy** na stronie **Klucze** w witrynie Azure Portal. 

    `config.primaryKey = "PRIMARYKEY";`

   ![Blok „Klucze” w witrynie Azure Portal](./media/create-graph-nodejs/keys.png)

4. Wprowadź nazwę bazy danych i nazwę grafu (kontenera) dla wartości parametrów config.database i config.collection. 

Oto przykład wypełnionego pliku config.js:

```nodejs
var config = {}

// Note that this must not have HTTPS or the port number
config.endpoint = "testgraphacct.gremlin.cosmosdb.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-the-console-app"></a>Uruchamianie aplikacji konsolowej

1. Otwórz okno terminala i za pomocą polecenia `cd` przejdź do katalogu instalacyjnego pliku package.json uwzględnionego w projekcie.

2. Uruchom polecenie `npm install`, aby zainstalować wymagane moduły npm, w tym `gremlin`.

3. Uruchom polecenie `node app.js` w terminalu, aby uruchomić aplikację Node.

## <a name="browse-with-data-explorer"></a>Przeglądanie w Eksploratorze danych

Teraz możesz wrócić do Eksploratora danych w witrynie Azure Portal, aby wyświetlać nowe dane grafu, wykonywać o nie zapytania, modyfikować je i pracować z nimi.

W Eksploratorze danych nowa baza danych jest wyświetlana w okienku **Grafy**. Rozwiń bazę danych, a następnie kolekcję i wybierz pozycję **Graf**.

Dane generowane przez aplikację przykładową będą wyświetlane w kolejnym okienku na karcie **Graf**, gdy wybierzesz przycisk **Zastosuj filtr**.

Spróbuj uzupełnić wartość `g.V()` ciągiem `.has('firstName', 'Thomas')`, aby przetestować filtr. Pamiętaj, że w wartości jest uwzględniana wielkość liter.

## <a name="review-slas-in-the-azure-portal"></a>Przeglądanie umów SLA w witrynie Azure Portal

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a>Czyszczenie zasobów

Jeśli nie planujesz dalszego korzystania z tej aplikacji, usuń wszystkie zasoby utworzone zgodnie z tym artykułem, wykonując następujące czynności: 

1. W witrynie Azure Portal, w menu nawigacji po lewej stronie wybierz pozycję **Grupy zasobów**. Następnie wybierz nazwę utworzonego zasobu. 

2. Na stronie grupy zasobów wybierz pozycję **Usuń**. Wpisz nazwę zasobu, który ma zostać usunięty, a następnie wybierz pozycję **Usuń**.

## <a name="next-steps"></a>Następne kroki

W tym artykule wyjaśniono sposób tworzenia konta usługi Azure Cosmos DB, tworzenia grafu za pomocą Eksploratora danych i uruchamiania aplikacji. Teraz możesz tworzyć bardziej złożone zapytania i implementować zaawansowaną logikę przechodzenia grafu za pomocą języka Gremlin. 

> [!div class="nextstepaction"]
> [Wykonywanie zapytań przy użyciu języka Gremlin](tutorial-query-graph.md)
