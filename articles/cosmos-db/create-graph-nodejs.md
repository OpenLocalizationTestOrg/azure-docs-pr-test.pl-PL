---
title: "aaaBuild aplikacji Node.js DB rozwiązania Cosmos Azure przy użyciu interfejsu API programu Graph | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod Node.js, można użyć tooconnect tooand zapytania bazy danych Azure rozwiązania Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 1445755842bc4e4a84ca2b2f789aadde8467e190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a>Azure Cosmos DB: Tworzenie aplikacji Node.js za pomocą interfejsu API programu Graph

Azure DB rozwiązania Cosmos jest hello globalnie rozproszone wielu modelu bazy danych usługi firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

W tym artykule szybki start przedstawiono, jak toocreate bazy danych Azure rozwiązania Cosmos konta dla interfejsu API programu Graph (wersja zapoznawcza), bazy danych i wykres przy użyciu hello portalu Azure. Następnie skompilować i uruchomić aplikację konsoli przy użyciu hello open source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) sterownika.  

> [!NOTE]
> Moduł npm Hello `gremlin-secure` jest zmodyfikowanej wersji `gremlin` modułu, z obsługą protokołu SSL i SASL wymagane do nawiązywania połączenia z bazy danych Azure rozwiązania Cosmos. Kod źródłowy jest dostępny w usłudze [GitHub](https://github.com/CosmosDB/gremlin-javascript).
>

## <a name="prerequisites"></a>Wymagania wstępne

Przed uruchomieniem tego przykładu, musi mieć hello następujące wymagania wstępne:
* [Node.js](https://nodejs.org/en/) w wersji 0.10.29 lub nowszej
* [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Dodawanie grafu

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Teraz załóżmy aplikacji w klonowania interfejs API programu Graph z serwisu GitHub, Ustaw ciąg połączenia hello i uruchom go. Zobaczysz, jak łatwo jest toowork z danymi programowo. 

1. Otwórz okno terminala Git, np. Git Bash i zmień (za pośrednictwem `cd` polecenie) tooa katalog roboczy.  

2. Hello uruchom następujące polecenie tooclone hello próbki repozytorium. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. Otwórz plik rozwiązania hello w programie Visual Studio. 

## <a name="review-hello-code"></a>Przejrzyj hello kodu

Upewnijmy szybki przegląd działania wykonywane w aplikacji hello. Otwórz hello `app.js` pliku, a znajdziesz hello następujące wiersze kodu. 

* Klient Gremlin Hello jest tworzony.

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

  Witaj konfiguracje są w `config.js`, które możemy edytować w hello następujących sekcji.

* Serie kroków Gremlin są wykonywane z hello `client.execute` metody.

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a>Aktualizowanie parametrów połączenia

1. Otwórz hello pliku config.js. 

2. Config.js, wypełnij hello config.endpoint klucza z hello **Gremlin URI** wartość z zakresu od hello **omówienie** strony hello portalu Azure. 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-graph-nodejs/gremlin-uri.png)

   Jeśli hello **Gremlin URI** wartość jest pusta, możesz wygenerować wartość hello na podstawie hello **klucze** strony w portalu hello, za pomocą hello **URI** wartości, usuwania https:// i zmiana toographs dokumentów.

   punkt końcowy Gremlin Hello musi być tylko nazwy hosta hello bez numeru portu protokołu/hello, tak samo, jak `mygraphdb.graphs.azure.com` (nie `https://mygraphdb.graphs.azure.com` lub `mygraphdb.graphs.azure.com:433`).

3. Wypełnij w config.js, wartość config.primaryKey hello się przy użyciu hello **klucza podstawowego** wartość z zakresu od hello **klucze** strony hello portalu Azure. 

    `config.primaryKey = "PRIMARYKEY";`

   ![Witaj bloku klucze portalu Azure](./media/create-graph-nodejs/keys.png)

4. Wprowadź nazwę bazy danych hello i wykres (kontener) nazwę wartości hello config.database i config.collection. 

Oto przykład wypełnionego pliku config.js:

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a>Uruchamianie aplikacji konsoli hello

1. Otwórz okno terminala i zmień (za pośrednictwem `cd` polecenie) katalog instalacyjny toohello dla pliku package.json hello, który znajduje się w projekcie hello.  

2. Uruchom `npm install` tooinstall hello wymagane moduły npm, w tym `gremlin-secure`.

3. Uruchom `node app.js` w terminalu toostart aplikacji węzła.

## <a name="browse-with-data-explorer"></a>Przeglądanie w Eksploratorze danych

Teraz można wrócić do poprzedniej strony tooData Explorer w hello tooview portalu Azure, zapytania, modyfikowania i pracować z nowych danych wykresu.

W Eksploratorze danych hello nowej bazy danych jest wyświetlana w hello **wykresy** okienka. Rozwiń bazę danych hello, następuje hello kolekcji, a następnie kliknij przycisk **wykresu**.

Hello dane generowane przez hello Przykładowa aplikacja jest wyświetlana w okienku dalej hello w hello **wykres** karcie po kliknięciu **Zastosuj filtr**.

Spróbuj Kończenie `g.V()` z `.has('firstName', 'Thomas')` tootest hello filtru. Należy pamiętać, że wartość hello jest uwzględniana wielkość liter.

## <a name="review-slas-in-hello-azure-portal"></a>Przejrzyj umowy SLA w hello portalu Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a>Czyszczenie zasobów

Jeśli nie planujesz toocontinue za pomocą tej aplikacji, należy usunąć wszystkie zasoby, które zostały utworzone w tym artykule, wykonując następujące hello: 

1. W portalu Azure, w menu nawigacji po lewej stronie powitania powitania kliknij **grup zasobów**, a następnie kliknij nazwę hello hello zasobu, który został utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toobe zasobów hello usunięte, a następnie kliknij przycisk **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym artykule kiedy znasz już jak toocreate konto bazy danych Azure rozwiązania Cosmos utworzyć wykres za pomocą Eksploratora danych i uruchom aplikację. Teraz możesz tworzyć bardziej złożone zapytania i implementować zaawansowaną logikę przechodzenia grafu za pomocą języka Gremlin. 

> [!div class="nextstepaction"]
> [Wykonywanie zapytań przy użyciu języka Gremlin](tutorial-query-graph.md)
