---
title: "Azure DB rozwiązania Cosmos: Opracowywania hello interfejsu API programu Graph w .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodevelop z interfejsem API usługi DocumentDB DB rozwiązania Cosmos Azure przy użyciu platformy .NET"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a>Azure DB rozwiązania Cosmos: Opracowywania hello interfejsu API programu Graph w .NET
Azure DB rozwiązania Cosmos jest usługa globalnie rozproszone wielu modelu bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

Ten samouczek pokazuje, jak toocreate konta bazy danych rozwiązania Cosmos Azure przy użyciu hello portalu Azure i jak toocreate wykres bazy danych i kontenera. następnie aplikacja Hello tworzy prosty sieci społecznościowych cztery osoby korzystające z hello [interfejsu API programu Graph](graph-sdk-dotnet.md) (wersja zapoznawcza), a następnie przechodzi przez i zapytanie hello wykresu przy użyciu Gremlin.

Ten samouczek obejmuje hello następujące zadania:

> [!div class="checklist"]
> * Tworzenie konta usługi Azure Cosmos DB 
> * Tworzenie bazy danych wykresu i kontenera
> * Serializować obiektów too.NET wierzchołki i krawędzi.
> * Dodaj wierzchołki i krawędzi.
> * Wykres hello zapytania przy użyciu Gremlin

## <a name="graphs-in-azure-cosmos-db"></a>Wykresy w Azure rozwiązania Cosmos bazy danych
Można użyć bazy danych Azure rozwiązania Cosmos toocreate, aktualizacji i wykresy zapytania przy użyciu hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) biblioteki. Biblioteka Microsoft.Azure.Graph Hello udostępnia metody rozszerzenia pojedynczego `CreateGremlinQuery<T>` na powitania `DocumentClient` klasy tooexecute Gremlin zapytania.

Gremlin jest funkcjonalny język programowania, który obsługuje zapisu operacji zapytań i przechodzenie i operacje (DML). Firma Microsoft obejmuje kilka przykładów w tym artykule tooget Twojego uruchomiony z Gremlin. Zobacz [zapytania Gremlin](gremlin-support.md) Aby uzyskać szczegółowe wskazówki Gremlin funkcji dostępnych w usłudze Azure DB rozwiązania Cosmos. 

## <a name="prerequisites"></a>Wymagania wstępne
Upewnij się, że masz następujące hello:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/). 
    * Alternatywnie można użyć hello [emulatora usługi Azure DocumentDB](local-emulator.md) w tym samouczku.
* Program [Visual Studio](http://www.visualstudio.com/).

## <a name="create-database-account"></a>Tworzenie konta bazy danych

Zacznijmy od utworzenia konta Azure DB rozwiązania Cosmos w hello portalu Azure.  

> [!TIP]
> * Masz już konto bazy danych rozwiązania Cosmos Azure? Jeśli tak, przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS)
> * Czy miał konto usługi Azure DocumentDB? Jeśli tak, Twoje konto jest kontem bazy danych Azure rozwiązania Cosmos i możesz przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS).  
> * Jeśli używasz hello Azure rozwiązania Cosmos DB emulatora, należy wykonać czynności hello na [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) toosetup hello emulatora i przejść od razu zbyt[konfigurowanie rozwiązania Visual Studio](#SetupVS). 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a id="SetupVS"></a>Konfigurowanie rozwiązania programu Visual Studio
1. Otwórz program **Visual Studio** na komputerze.
2. Na powitania **pliku** menu, wybierz opcję **nowy**, a następnie wybierz pozycję **projektu**.
3. W hello **nowy projekt** okno dialogowe, wybierz opcję **szablony** / **Visual C#** / **aplikacji konsoli (.NET Framework)**, nazwy projektu, a następnie kliknij przycisk **OK**.
4. W hello **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy nową aplikację konsolową, która znajduje się w obrębie rozwiązania Visual Studio, a następnie kliknij przycisk **Zarządzaj pakietami NuGet...**
5. W hello **NuGet** , kliknij pozycję **Przeglądaj**i wpisz **Microsoft.Azure.Graphs** w polu wyszukiwania hello a hello wyboru **obejmują wersje wstępne**.
6. W wynikach hello znaleźć **Microsoft.Azure.Graphs** i kliknij przycisk **zainstalować**.
   
   Jeśli zostanie wyświetlony komunikat o przegląd zmian toohello rozwiązania, kliknij przycisk **OK**. Jeśli wyświetlany jest komunikat o akceptacji licencji, kliknij pozycję **Akceptuję**.
   
    Witaj `Microsoft.Azure.Graphs` Biblioteka udostępnia metody rozszerzenia pojedynczego `CreateGremlinQuery<T>` do wykonywania operacji Gremlin. Gremlin jest funkcjonalny język programowania, który obsługuje zapisu operacji zapytań i przechodzenie i operacje (DML). Firma Microsoft obejmuje kilka przykładów w tym artykule tooget Twojego uruchomiony z Gremlin. [Zapytania gremlin](gremlin-support.md) ma szczegółowy przewodnik na temat możliwości Gremlin w usłudze Azure DB rozwiązania Cosmos.

## <a id="add-references"></a>Łączenie aplikacji

Dodaj te dwie stałe i *klienta* zmiennej w aplikacji. 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
Następnie head kopii toohello [portalu Azure](https://portal.azure.com) tooretrieve Twojego adresu URL punktu końcowego i klucz podstawowy. adres URL punktu końcowego Hello i klucza podstawowego są niezbędne do Twojej aplikacji toounderstand gdzie tooconnect na oraz bazy danych Azure rozwiązania Cosmos tootrust połączeniu aplikacji. 

W hello portalu Azure, przejdź do konta bazy danych Azure rozwiązania Cosmos tooyour, kliknij przycisk **klucze**, a następnie kliknij przycisk **odczytu i zapisu kluczy**. 

Skopiuj hello identyfikatora URI z portalu hello i wklej go za pośrednictwem `Endpoint` we właściwości punktu końcowego hello powyżej. Następnie kopiowania hello klucza podstawowego z portalu hello i wklej go do hello `AuthKey` właściwości powyżej. 

! [Zrzut ekranu przedstawiający hello Azure portal używany przez samouczek toocreate hello aplikacji C#. Pokazuje hello konta bazy danych Azure rozwiązania Cosmos, przyciskiem KLUCZE wyróżnionym w hello Azure DB rozwiązania Cosmos nawigacji i wartości URI oraz PRIMARY KEY hello wyróżnione na powitania bloku klucze] [klucze] 
 
## <a id="instantiate"></a>Utwórz wystąpienie hello DocumentClient 
Następnie utwórz nowe wystąpienie klasy hello **DocumentClient**.  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <a id="create-database"></a>Tworzenie bazy danych 

Teraz Utwórz bazę danych Azure rozwiązania Cosmos [bazy danych](documentdb-resources.md#databases) przy użyciu hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metody lub [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metody hello  **DocumentClient** klasy z hello [zestawu SDK .NET usługi DocumentDB](documentdb-sdk-dotnet.md).  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a>Tworzenie wykresu. 

Następnie należy utworzyć kontener wykresu przy użyciu hello przy użyciu hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metody lub [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metody hello **DocumentClient**  klasy. Kolekcja jest kontenerem jednostek wykresu. 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <a id="serializing"></a>Serializować obiektów too.NET wierzchołki i krawędzi.
Azure DB rozwiązania Cosmos używa hello [formacie łańcuchowym GraphSON](gremlin-support.md), który definiuje schematu JSON dla wierzchołków, krawędzie i właściwości. Hello Azure rozwiązania Cosmos DB .NET SDK zawiera struktury JSON.NET jako zależność, a to pozwala nam tooserialize/deserializacji GraphSON na obiekty .NET, które firma Microsoft może współpracować w kodzie.

Na przykład załóżmy współpracować z prostego sieci społecznościowych z czterech osób. Opisano, jak toocreate `Person` wierzchołków, Dodaj `Knows` relacji między nimi, a następnie zapytania i przechodzić między nimi hello wykres toofind "friend friend" relacji. 

Witaj `Microsoft.Azure.Graphs.Elements` przestrzeń nazw zawiera `Vertex`, `Edge`, `Property` i `VertexProperty` klasy do deserializacji obiektów zdefiniowanych przez toowell .NET programu GraphSON odpowiedzi.

## <a name="run-gremlin-using-creategremlinquery"></a>Uruchom przy użyciu CreateGremlinQuery Gremlin
Gremlin, takiego jak SQL, obsługuje odczytu, zapisu i operacje zapytań. Na przykład hello poniższy fragment kodu przedstawia sposób toocreate wierzchołków, krawędzi, wykonać niektóre przykładowe zapytania przy użyciu `CreateGremlinQuery<T>`i asynchronicznie iterację te wyniki za pomocą `ExecuteNextAsync` i "HasMoreResults.

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a>Dodaj wierzchołki i krawędzi.

Oto instrukcje Gremlin hello pokazano w powyższej sekcji hello więcej szczegółów. Pierwszy możemy niektórych wierzchołków przy użyciu jego Gremlin `addV` metody. Na przykład hello następujący fragment kodu tworzy wierzchołek "Blogu Thomasa Andersen" typu "Osoba" z właściwości imię i nazwisko, wiek.

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

Następnie utworzymy niektórych krawędzi między te wierzchołków przy użyciu jego Gremlin `addE` metody. 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

Możemy zaktualizować istniejące wierzchołków przy użyciu `properties` krok w Gremlin. Firma Microsoft pominąć hello wywołania tooexecute hello zapytanie przy użyciu `HasMoreResults` i `ExecuteNextAsync` hello pozostałej części hello przykłady.

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

Można usunąć krawędzi oraz wierzchołków przy użyciu jego Gremlin `drop` kroku. Oto fragment kodu, który pokazuje sposób toodelete a wierzchołka i krawędzi. Należy pamiętać, że porzucenie wierzchołek wykonuje kaskadowych usunięcie hello skojarzone krawędzi.

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a>Wykres hello zapytania

Można wykonać zapytania, a także za pomocą Gremlin traversals. Na przykład powitania po fragment kodu przedstawia, jak toocount hello liczbę wierzchołków w grafie hello:

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
Można wykonywać przy użyciu jego Gremlin filtry `has` i `hasLabel` kroki i połączenie ich za pomocą `and`, `or`, i `not` toobuild bardziej złożone filtry:

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

Niektóre właściwości hello wyników zapytania za pomocą hello można projektu `values` krok:

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

Firma Microsoft do tej pory tylko przedstawiono operatorów zapytań, które działają w dowolnej bazy danych. Wykresy są szybkie i wydajne dla operacji przechodzenia, gdy potrzebujesz toonavigate toorelated krawędzi oraz wierzchołków. Spróbujmy wszystkich znajomych blogu Thomasa. Firma Microsoft to zrobić przy użyciu jego Gremlin `outE` krok toofind wszystkie hello wyjściowego krawędzi z blogu Thomasa, a następnie przechodzenie toohello w wierzchołki z tych krawędzi przy użyciu jego Gremlin `inV` krok:

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

Zapytanie dalej Hello wykonuje dwie toofind przeskoków wszystkich blogu Thomasa "znajomych przyjaciół", wywołując `outE` i `inV` dwa razy. 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

Można tworzyć bardziej złożone kwerendy i wdrożyć logikę przechodzenie zaawansowanych wykresu przy użyciu Gremlin, takie jak filtr mieszania hello wyrażenia wykonywania pętli przy użyciu `loop` krok i implementujący nawigacji warunkowego przy użyciu hello `choose` kroku. Dowiedz się więcej o co można zrobić z [Obsługa Gremlin](gremlin-support.md)!

To wszystko, ten samouczek bazy danych Azure rozwiązania Cosmos została zakończona! 

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie będzie toocontinue toouse tej aplikacji, użyj hello następujące kroki toodelete wszystkie zasoby są tworzone w tym samouczku w hello portalu Azure.  

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu hello następujące czynności:

> [!div class="checklist"]
> * Utworzone konto bazy danych Azure rozwiązania Cosmos 
> * Utworzony wykres bazy danych i kontener
> * Obiekty too.NET zserializowane wierzchołków i krawędzi.
> * Dodano wierzchołków i krawędzi.
> * Przy użyciu Gremlin wykresu, którego dotyczy kwerenda hello

Teraz możesz tworzyć bardziej złożone zapytania i implementować zaawansowaną logikę przechodzenia grafu za pomocą języka Gremlin. 

> [!div class="nextstepaction"]
> [Wykonywanie zapytań przy użyciu języka Gremlin](tutorial-query-graph.md)
