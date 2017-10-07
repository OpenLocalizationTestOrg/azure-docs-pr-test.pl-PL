---
title: "Azure rozwiązania Cosmos bazy danych: Tworzenie aplikacji sieci web z platformą .NET i hello interfejsu API usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod .NET, można użyć zapytania tooand tooconnect hello interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB"
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
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a>Azure DB rozwiązania Cosmos: Tworzenie aplikacji sieci web interfejsu API usługi DocumentDB z platformą .NET i hello portalu Azure

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i przy użyciu kolekcji hello portalu Azure. Będzie tworzenie i wdrażanie aplikacji sieci web listy todo oparty na powitania [interfejsu API platformy .NET usługi DocumentDB](documentdb-sdk-dotnet.md), jak pokazano w hello następującego zrzutu ekranu. 

![Aplikacja z listą zadań do wykonania z przykładowymi danymi](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a>Wymagania wstępne

Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i użyć hello **wolnego** [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Upewnij się, że możesz włączyć **Azure programowanie** podczas instalacji programu Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
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

     Można teraz używać zapytań w programie Eksplorator danych tooretrieve danych. Domyślnie korzysta z Eksploratora danych `SELECT * FROM c` tooretrieve wszystkich dokumentów w kolekcji hello, ale można zmienić tego tooa różnych [zapytania SQL](documentdb-sql-query.md), takich jak `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn wszystkie dokumenty hello w kolejności malejącej na podstawie sygnatur czasowych.
 
     Można również użyć Eksploratora danych toocreate przechowywane procedury, funkcje UDF i logiki biznesowej po stronie serwera tooperform wyzwalaczy również jako przepływności skali. Eksplorator danych udostępnia wszystkie hello wbudowanych programowy dostęp do danych dostępne w hello interfejsów API, ale zapewnia łatwy dostęp do danych tooyour w hello portalu Azure.

## <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Teraz załóżmy przełącznika tooworking z kodem. Załóżmy sklonować aplikacji interfejsu API usługi DocumentDB w witrynie GitHub, Ustaw ciąg połączenia hello i uruchom go. Zobaczysz, jak łatwo jest toowork z danymi programowo. 

1. Otwórz okno terminala git, np. git bash, i `CD` tooa katalog roboczy.  

2. Hello uruchom następujące polecenie tooclone hello próbki repozytorium. 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. Następnie otwórz plik rozwiązania todo hello w programie Visual Studio. 

## <a name="review-hello-code"></a>Przejrzyj hello kodu

Upewnijmy szybki przegląd działania wykonywane w aplikacji hello. Otwórz hello DocumentDBRepository.cs pliku, a dane tam, że te wiersze kodu utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos. 

* Witaj DocumentClient został zainicjowany w wierszu 73.

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* Nowa baza danych jest tworzona w wierszu 88.

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* Nowa kolekcja jest tworzona w wierszu 107.

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a>Aktualizowanie parametrów połączenia

Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.

1. W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**. W pliku web.config hello w następnym kroku hello użyjesz przyciski Kopia powitania po prawej stronie powitania hello toocopy ekranie powitania identyfikatora URI oraz Primary Key.

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-documentdb-dotnet/keys.png)

2. W programie Visual Studio 2017 r Otwórz plik web.config hello. 

3. Skopiuj wartość identyfikatora URI z portalu hello (przy użyciu przycisku Kopiuj hello) i przydzielić mu hello wartość klucza punktu końcowego hello w pliku web.config. 

    `<add key="endpoint" value="FILLME" />`

4. Skopiuj wartość klucza podstawowego z portalu hello i stał się hello wartość authKey hello w pliku web.config. Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos. 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a>Uruchamianie aplikacji sieci web hello
1. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** , a następnie kliknij przycisk **Zarządzaj pakietami NuGet**. 

2. W hello NuGet **Przeglądaj** wpisz *DocumentDB*.

3. Wyniki hello zainstalować hello **Microsoft.Azure.DocumentDB** biblioteki. Spowoduje to zainstalowanie pakietu Microsoft.Azure.DocumentDB hello, a także wszystkie zależności.

4. Kliknij polecenie CTRL + F5 toorun hello aplikacji. Aplikacja zostanie wyświetlona w przeglądarce. 

5. Kliknij przycisk **Utwórz nowy** w hello przeglądarki i Utwórz kilka nowych zadań w aplikacji zadań do wykonania.

   ![Aplikacja z listą zadań do wykonania z przykładowymi danymi](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

Teraz można wrócić do poprzedniej strony tooData Explorer i zobacz zapytania, modyfikowania i pracy z tym nowych danych. 

## <a name="review-slas-in-hello-azure-portal"></a>Przejrzyj umowy SLA w hello portalu Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym szybkiego startu kiedy znasz już jak utworzyć kolekcję za pomocą Eksploratora danych hello toocreate konto bazy danych Azure rozwiązania Cosmos i uruchomienia aplikacji sieci web. Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane. 

> [!div class="nextstepaction"]
> [Importowanie danych do usługi Azure Cosmos DB](import-data.md)


