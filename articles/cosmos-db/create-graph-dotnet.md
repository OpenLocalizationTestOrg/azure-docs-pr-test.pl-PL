---
title: "Interfejs API programu Graph hello aaaBuild aplikacji .NET DB rozwiązania Cosmos Azure przy użyciu | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod .NET, można użyć tooconnect tooand zapytania bazy danych Azure rozwiązania Cosmos"
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
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a>Azure rozwiązania Cosmos bazy danych: Tworzenie aplikacji platformy .NET przy użyciu interfejsu API programu Graph hello

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazy danych i wykres (kontener) przy użyciu hello portalu Azure. Następnie skompilować i uruchomić aplikację konsoli oparty na powitania [interfejsu API programu Graph](graph-sdk-dotnet.md) (wersja zapoznawcza).  

## <a name="prerequisites"></a>Wymagania wstępne

Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i użyć hello **wolnego** [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Upewnij się, że możesz włączyć **Azure programowanie** podczas instalacji programu Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Dodawanie grafu

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Teraz załóżmy aplikacji w klonowania interfejs API programu Graph z serwisu github, Ustaw ciąg połączenia hello i uruchom go. Zobaczysz, jak łatwo jest toowork z danymi programowo. 

1. Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.  

2. Hello uruchom następujące polecenie tooclone hello próbki repozytorium. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. Następnie otwórz program Visual Studio i hello Otwórz plik rozwiązania. 

## <a name="review-hello-code"></a>Przejrzyj hello kodu

Upewnijmy szybki przegląd działania wykonywane w aplikacji hello. Hello Otwórz plik Program.cs i tam, że te wiersze kodu utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos. 

* zainicjowano Hello DocumentClient. W podglądzie hello dodaliśmy rozszerzenia interfejsu API programu graph na powitania klienta bazy danych Azure rozwiązania Cosmos. Pracujemy nad klient wykres autonomiczny całkowicie niezależna od hello Azure DB rozwiązania Cosmos klienta i zasobów.

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* Tworzenie nowej bazy danych.

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* Tworzenie nowego grafu.

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* Serie kroków Gremlin są wykonywane przy użyciu hello `CreateGremlinQuery` metody.

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a>Aktualizowanie parametrów połączenia

Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.

1. W programie Visual Studio 2017 r Otwórz plik App.config hello. 

2. W portalu Azure na koncie Azure DB rozwiązania Cosmos powitania kliknij **kluczy** w hello lewy pasek nawigacyjny. 

    ![Wyświetlanie i kopiowanie klucza podstawowego w portalu Azure na stronie klucze hello hello](./media/create-graph-dotnet/keys.png)

3. Kopia Twojej **identyfikatora URI** wartość z portalu hello i zapewnić ich hello wartość klucza punktu końcowego hello w pliku App.config. Jak pokazano w hello wartość hello toocopy zrzut ekranu poprzedzającym, można użyć przycisku Kopiuj hello.

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. Kopiowania z **klucz podstawowy** wartość z portalu hello i zapewnić ich hello wartość klucza AuthKey hello w pliku App.config, a następnie zapisz zmiany. 

    `<add key="AuthKey" value="FILLME" />`

Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos. 

## <a name="run-hello-console-app"></a>Uruchamianie aplikacji konsoli hello

1. W programie Visual Studio, kliknij prawym przyciskiem myszy hello **GraphGetStarted** projektu w **Eksploratora rozwiązań** , a następnie kliknij przycisk **Zarządzaj pakietami NuGet**. 

2. W hello NuGet **Przeglądaj** wpisz *Microsoft.Azure.Graphs* i sprawdź hello **zawiera wersję wstępną** pole. 

3. Wyniki hello zainstalować hello **Microsoft.Azure.Graphs** biblioteki. Spowoduje to zainstalowanie hello Azure DB rozwiązania Cosmos wykres rozszerzenie biblioteki pakietu i wszystkie zależności.

    Jeśli zostanie wyświetlony komunikat o przegląd zmian toohello rozwiązania, kliknij przycisk **OK**. Jeśli wyświetlany jest komunikat o akceptacji licencji, kliknij pozycję **Akceptuję**.

4. Kliknij polecenie CTRL + F5 toorun hello aplikacji.

   okno konsoli Hello Wyświetla wierzchołków hello i krawędzi dodawany toohello wykresu. Gdy hello ukończeniu działania skryptu, naciśnij klawisz ENTER dwukrotnie tooclose okna konsoli hello. 

## <a name="browse-using-hello-data-explorer"></a>Przeglądaj przy użyciu hello Eksploratora danych

Można teraz wróć tooData Explorer w hello portalu Azure i Przeglądaj i wyszukiwać nowych danych wykresu.

1. W Eksploratorze danych hello nowej bazy danych zostanie wyświetlona w okienku wykresy hello. Rozwiń węzeł **graphdb** i **graphcollz**, a następnie kliknij pozycję **Graf**.

2. Kliknij przycisk hello **Zastosuj filtr** przycisk toouse hello domyślne zapytanie tooview wszystkie verticies hello hello wykresie. Hello dane generowane przez hello Przykładowa aplikacja jest wyświetlana w okienku wykresy hello.

    Można powiększyć i hello wykresu, rozwiń obszar wyświetlania wykresu hello, Dodaj dodatkowe verticies i przenieść verticies na powitania wyświetlić powierzchni.

    ![Wyświetl wykres hello w Eksploratorze danych w hello portalu Azure](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>Przejrzyj umowy SLA w hello portalu Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki: 

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym szybkiego startu kiedy znasz już jak toocreate konto bazy danych Azure rozwiązania Cosmos utworzyć wykres przy użyciu hello Eksploratora danych i uruchom aplikację. Teraz możesz tworzyć bardziej złożone zapytania i implementować zaawansowaną logikę przechodzenia grafu za pomocą języka Gremlin. 

> [!div class="nextstepaction"]
> [Wykonywanie zapytań przy użyciu języka Gremlin](tutorial-query-graph.md)

