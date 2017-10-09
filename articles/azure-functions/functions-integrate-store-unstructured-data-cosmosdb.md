---
title: "aaaStore danych niestrukturalnych przy użyciu usługi Azure Functions i DB rozwiązania Cosmos"
description: "Przechowywanie danych niestrukturalnych przy użyciu usług Azure Functions i Cosmos DB"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure functions, functions, przetwarzanie zdarzeń, Cosmos DB, obliczanie dynamiczne, architektura bez serwera"
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 48d6899c20d3e6f6b062725fca329972ead3c696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a>Przechowywanie danych niestrukturalnych przy użyciu usług Azure Functions i Cosmos DB

[Azure DB rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) to doskonały sposób toostore bez struktury i dane JSON. Dzięki połączeniu usług Azure Functions i Cosmos DB przechowywanie danych staje się szybkie i proste oraz wymaga znacznie krótszego kodu niż w przypadku przechowywania danych w relacyjnej bazie danych.

W środowisku Azure Functions powiązań wejściowych i wyjściowych Podaj dane deklaratywne tooconnect tooexternal usługi z funkcji. W tym temacie Dowiedz się, jak tooupdate istniejących C# funkcji tooadd powiązania wyjściowego, który przechowywania danych niestrukturalnych w dokumencie DB rozwiązania Cosmos. 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka:

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a>Dodawanie powiązania danych wyjściowych

1. Rozwiń aplikację funkcji i funkcję.

1. Wybierz **integracji** i **+ nowe dane wyjściowe**, które jest w hello z góry po prawej stronie powitania. Wybierz pozycję **Azure Cosmos DB** i kliknij przycisk **Wybierz**.

    ![Dodawanie powiązania danych wyjściowych usługi Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. Użyj hello **wyjście bazy danych Azure rozwiązania Cosmos** ustawień określonych w tabeli hello: 

    ![Konfigurowanie powiązania danych wyjściowych Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | Ustawienie      | Sugerowana wartość  | Opis                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **Nazwa parametru dokumentu** | taskDocument | Nazwa, która odwołuje się obiekt DB rozwiązania Cosmos toohello w kodzie. |
    | **Nazwa bazy danych** | taskDatabase | Nazwa bazy danych toosave dokumentów. |
    | **Nazwa kolekcji** | TaskCollection | Nazwa kolekcji baz danych Cosmos DB. |
    | **Jeśli PRAWDA, tworzy hello rozwiązania Cosmos bazy danych z bazy danych i kolekcji** | Zaznaczone | Kolekcja Hello nie już istnieje, więc można go utworzyć. |

4. Wybierz **nowy** dalej toohello **połączenie dokumentu DB rozwiązania Cosmos** etykiety, a następnie wybierz **+ Utwórz nowy**. 

5. Użyj hello **nowe konto** ustawień określonych w tabeli hello: 

    ![Konfigurowanie połączenia dokumentu Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | Ustawienie      | Sugerowana wartość  | Opis                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **Identyfikator** | Nazwa bazy danych | Unikatowy identyfikator dla bazy danych DB rozwiązania Cosmos hello  |
    | **Interfejs API** | SQL (DocumentDB) | Wybierz hello interfejsu API z bazy danych dokumentu.  |
    | **Subskrypcja** | Subskrypcja platformy Azure | Subskrypcja platformy Azure  |
    | **Grupa zasobów** | myResourceGroup |  Użyj hello istniejącą grupę zasobów zawierającą aplikację funkcji. |
    | **Lokalizacja**  | WestEurope | Wybierz lokalizację w pobliżu tooeither aplikacji funkcji lub tooother aplikacji, które używają hello przechowywanych dokumentów.  |

6. Kliknij przycisk **OK** toocreate hello w bazie danych. Może upłynąć kilka minut toocreate hello bazy danych. Po utworzeniu bazy danych hello parametry połączenia bazy danych hello jest przechowywana jako ustawienie aplikacji funkcji. nazwę tego ustawienia aplikacji Hello jest wstawiana **rozwiązania Cosmos bazy danych konta połączenia**. 
 
8. Po ustawieniu parametrów połączenia hello wybierz **zapisać** toocreate hello powiązania.

## <a name="update-hello-function-code"></a>Zaktualizuj kod funkcja hello

Zastąp hello istniejącego kodu C# funkcja hello następującego kodu:

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
Ten przykładowy kod odczytuje hello żądania HTTP ciągów zapytania i przypisuje je toofields w hello `taskDocument` obiektu. Witaj `taskDocument` powiązania wysyła dane obiektu hello z tym toobe parametru powiązania przechowywane w bazie danych dokumentu powiązanego hello. Witaj utworzona baza danych jest hello pierwszym uruchomieniu funkcja hello.

## <a name="test-hello-function-and-database"></a>Funkcja hello testu i bazy danych

1. Witaj w prawym okienku rozwiń i wybierz **testu**. W obszarze **zapytania**, kliknij przycisk **+ Dodaj parametr** i Dodaj powitania po ciągu zapytania toohello parametry:

    + `name`
    + `task`
    + `duedate`

2. Kliknij pozycję **Uruchom** i sprawdź, czy zwracany jest stan 200.

    ![Konfigurowanie powiązania danych wyjściowych Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. Na powitania po lewej stronie powitania portalu Azure, rozwiń pasku ikon hello typu `cosmos` w hello Wyszukaj pola i wybierz pozycję **bazy danych Azure rozwiązania Cosmos**.

    ![Wyszukaj hello usługi DB rozwiązania Cosmos](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. Wybierz hello bazy danych została utworzona, następnie wybierz **Eksploratora danych**. Rozwiń węzeł hello **kolekcje** węzłów, wybierz hello nowy dokument i Potwierdź dokumentu hello zawiera wartości ciągu zapytania, wraz z niektóre dodatkowe metadane. 

    ![Sprawdzanie wpisu w bazie danych Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

Pomyślnie dodano wyzwalacza HTTP tooyour powiązania przechowywania danych niestrukturalnych w bazie danych DB rozwiązania Cosmos.

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

Aby uzyskać więcej informacji o powiązaniu tooa DB rozwiązania Cosmos w bazie danych, zobacz [powiązania bazy danych Azure funkcji rozwiązania Cosmos](functions-bindings-documentdb.md).
