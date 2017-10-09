---
title: "Azure rozwiązania Cosmos bazy danych: Tworzenie aplikacji za pomocą języka Python i hello interfejsu API usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Przedstawia przykładowy kod języka Python, można użyć zapytania tooand tooconnect hello interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a>Azure DB rozwiązania Cosmos: Tworzenie aplikacji interfejsu API usługi DocumentDB z języka Python i hello portalu Azure

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazą danych dokumentów i przy użyciu kolekcji hello portalu Azure. Następnie skompilować i uruchomić aplikację konsoli oparty na powitania [interfejsu API języka Python usługi DocumentDB](documentdb-sdk-python.md).

## <a name="prerequisites"></a>Wymagania wstępne

* Przed uruchomieniem tego przykładu, musi mieć hello następujące wymagania wstępne:
    * [Program Visual Studio w wersji 2015](http://www.visualstudio.com/) lub nowszej.
    * Narzędzia Python Tools for Visual Studio pobrane z witryny [GitHub](http://microsoft.github.io/PTVS/). W tym samouczku są używane narzędzia Python Tools for VS 2015.
    * Środowisko Python w wersji 2.7 pobrane z witryny [python.org](https://www.python.org/downloads/release/python-2712/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Dodawanie kolekcji

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Klonowanie hello przykładowej aplikacji

Teraz załóżmy aplikacji w klonowania interfejs API usługi DocumentDB z serwisu github, Ustaw ciąg połączenia hello i uruchom go. Zobacz, jak łatwo jest toowork z danymi programowo. 

1. Otwórz okno terminala git, np. git bash, i `cd` tooa katalog roboczy.  

2. Hello uruchom następujące polecenie tooclone hello próbki repozytorium. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a>Przejrzyj hello kodu

Upewnijmy szybki przegląd działania wykonywane w aplikacji hello. Otwórz hello DocumentDBGetStarted.py pliku, a dane tam, że te wiersze kodu utworzyć hello zasobów bazy danych Azure rozwiązania Cosmos. 


* zainicjowano Hello DocumentClient.

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* Tworzenie nowej bazy danych.

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* Tworzenie nowej kolekcji.

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* Tworzenie kilku dokumentów.

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* Wykonywanie zapytania przy użyciu programu SQL.

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a>Aktualizowanie parametrów połączenia

Teraz przejdź wstecz toohello Azure tooget portalu użytkownika informacje o parametrach połączenia i skopiuj go do aplikacji hello.

1. W hello [portalu Azure](http://portal.azure.com/), w Azure rozwiązania Cosmos DB konta, na powitania lewy pasek nawigacyjny kliknij **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**. Użyjesz przyciski Kopia hello na powitania po prawej stronie powitania toocopy ekranie powitania identyfikatora URI oraz Primary Key do hello `DocumentDBGetStarted.py` pliku w następnym kroku hello.

    ![Wyświetlanie i kopiowanie klucza dostępu w hello portalu Azure, w bloku klucze](./media/create-documentdb-dotnet/keys.png)

2. W otwartych hello `DocumentDBGetStarted.py` pliku. 

3. Skopiuj wartość identyfikatora URI z portalu hello (przy użyciu przycisku Kopiuj hello) i przydzielić mu hello wartością klucza punktu końcowego hello `DocumentDBGetStarted.py`. 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. Skopiuj wartość klucza podstawowego z portalu hello i stał się hello wartość hello `config.MASTERKEY` w `DocumentDBGetStarted.py`. Użytkownik zaktualizował teraz aplikacji z wszystkie informacje hello musi toocommunicate z bazy danych Azure rozwiązania Cosmos. 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a>Uruchamianie aplikacji hello
1. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań**, wybierz hello bieżącego środowiska Python, a następnie kliknij prawym przyciskiem myszy.

2. Wybierz polecenie Zainstaluj pakiet języka Python, a następnie wpisz ciąg **pydocumentdb**.

3. Uruchamianie aplikacji hello toorun F5. Aplikacja zostanie wyświetlona w przeglądarce. 

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
> [Importowanie danych do bazy danych Azure rozwiązania Cosmos dla hello interfejsu API usługi DocumentDB](import-data.md)


