---
title: "Azure rozwiązania Cosmos bazy danych: Tworzenie aplikacji sieci web z platformą .NET i hello bazy danych MongoDB interfejsu API | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod .NET, można użyć zapytania tooand tooconnect hello interfejsu API Azure rozwiązania Cosmos bazy danych MongoDB"
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
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a>Azure DB rozwiązania Cosmos: Tworzenie aplikacji sieci web interfejsu API bazy danych MongoDB z platformą .NET i hello portalu Azure

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i przy użyciu kolekcji hello portalu Azure. Będzie tworzenie i wdrażanie aplikacji sieci web listy zadań oparty na powitania [sterownik bazy danych MongoDB .NET](https://docs.mongodb.com/ecosystem/drivers/csharp/). 

## <a name="prerequisites"></a>Wymagania wstępne

Jeśli nie masz jeszcze programu Visual Studio 2017 r zainstalowany, możesz pobrać i użyć hello **wolnego** [programu Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Upewnij się, że możesz włączyć **Azure programowanie** podczas instalacji programu Visual Studio hello.
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Teraz załóżmy aplikacji w klonowania API bazy danych MongoDB z witryny github, Ustaw ciąg połączenia hello i uruchom go. Zobaczysz, jak łatwo jest toowork z danymi programowo. 

1. Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.  

2. Hello uruchom następujące polecenie tooclone hello próbki repozytorium. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. Następnie otwórz plik rozwiązania hello w programie Visual Studio. 

## <a name="review-hello-code"></a>Przejrzyj hello kodu

Upewnijmy szybki przegląd działania wykonywane w aplikacji hello. Otwórz hello **Dal.cs** plik pod hello **DAL** katalogu i można znaleźć, te wiersze kodu utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos. 

* Inicjowanie powitania klienta Mongo.

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* Pobrać hello bazy danych i kolekcji hello.

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* Pobieranie wszystkich dokumentów.

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a>Aktualizowanie parametrów połączenia

Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.

1. W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **ciąg połączenia**, a następnie kliknij przycisk **odczytu i zapisu kluczy**. Użyjesz przyciski Kopia powitania po prawej stronie powitania hello toocopy ekranie powitania nazwę użytkownika, hasło i hosta do pliku Dal.cs hello w hello następnego kroku.

2. Otwórz hello **Dal.cs** pliku w hello **DAL** katalogu. 

3. Kopiowania z **nazwy użytkownika** wartości z portalu hello (przy użyciu przycisku Kopiuj hello) i przekształcenie go w hello wartość hello **username** w Twojej **Dal.cs** pliku. 

4. Następnie skopiuj z **hosta** wartości z portalu hello i zapewnić ich hello wartość hello **hosta** w Twojej **Dal.cs** pliku. 

5. Koniec skopiować z **hasło** wartości z portalu hello i przekształcenie go w hello wartość hello **hasło** w Twojej **Dal.cs** pliku. 

Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos. 
    
## <a name="run-hello-web-app"></a>Uruchamianie aplikacji sieci web hello

1. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** , a następnie kliknij przycisk **Zarządzaj pakietami NuGet**. 

2. W hello NuGet **Przeglądaj** wpisz *MongoDB.Driver*.

3. Wyniki hello zainstalować hello **MongoDB.Driver** biblioteki. Spowoduje to zainstalowanie pakietu MongoDB.Driver hello, a także wszystkie zależności.

4. Kliknij polecenie CTRL + F5 toorun hello aplikacji. Aplikacja zostanie wyświetlona w przeglądarce. 

5. Kliknij przycisk **Utwórz** w hello przeglądarki i Utwórz kilka nowych zadań w aplikacji listy zadań.

## <a name="review-slas-in-hello-azure-portal"></a>Przejrzyj umowy SLA w hello portalu Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym szybkiego startu kiedy znasz już jak toocreate konta bazy danych Azure rozwiązania Cosmos i uruchomić aplikacji sieci web przy użyciu hello interfejsu API dla bazy danych MongoDB. Teraz można importować konto bazy danych rozwiązania Cosmos tooyour dodatkowe dane. 

> [!div class="nextstepaction"]
> [Importowanie danych do bazy danych Azure rozwiązania Cosmos dla hello API bazy danych MongoDB](mongodb-migrate.md)

