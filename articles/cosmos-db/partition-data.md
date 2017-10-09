---
title: "aaaPartitioning i skalowanie w poziomie w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o sposobie partycjonowania działania w usłudze Azure DB rozwiązania Cosmos, jak tooconfigure partycjonowania i kluczy partycji i jak toopick hello prawo partycji klucz dla aplikacji."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: cac9a8cd-b5a3-4827-8505-d40bb61b2416
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87d56db8c4ccc6b94b1650baff0fcfb3db6d1777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopartition-and-scale-in-azure-cosmos-db"></a>Jak toopartition i skali w usłudze Azure DB rozwiązania Cosmos

[Bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) jest toohelp zaprojektowanej globalna baza danych rozproszone i wiele modeli, można osiągnąć szybkie, przewidywalną wydajność i skalę bezproblemowo wraz z aplikacji jako ich przyrostu. Ten artykuł zawiera omówienie sposobu partycjonowania działa w przypadku wszystkich danych hello modeli w usłudze Azure DB rozwiązania Cosmos, i zawiera opis sposobu konfigurowania bazy danych Azure rozwiązania Cosmos kontenery tooeffectively skalowania aplikacji.

Partycjonowanie i klucze partycji są uwzględniane w tym Azure piątek wideo z Scott Hanselman i Azure rozwiązania Cosmos DB główny Engineering Menedżer Shireesh Thota.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Podział na partycje w Azure rozwiązania Cosmos bazy danych
W usłudze Azure DB rozwiązania Cosmos można przechowywać i zapytania na danych bez schematu wraz z czasem odpowiedzi kolejności z milisekundy na dowolnym poziomie. Rozwiązania cosmos DB zawiera kontenery do przechowywania danych o nazwie **kolekcje (dla dokumentu), wykresy lub tabele**. Kontenery są zasoby logiczne i może obejmować co najmniej jednej partycji fizycznej lub serwerów. Hello partycji jest określana na podstawie rozwiązania Cosmos bazy danych na podstawie rozmiaru magazynu hello i udostępnionej przepływności hello hello kontenera. Każdej partycji w bazie danych rozwiązania Cosmos ma stałą kopie dysków SSD magazynu skojarzone z nim i są replikowane w celu zapewnienia wysokiej dostępności. Zarządzanie partycji pełni zarządza bazy danych Azure rozwiązania Cosmos i nie masz toowrite złożonego kodu lub Zarządzanie partycjami. Kontenery DB rozwiązania cosmos jest nieograniczony pod względem pamięci masowej i przepływność. 

![poziomy](./media/introduction/azure-cosmos-db-partitioning.png) 

Podział na partycje jest przezroczysty tooyour aplikacji. Rozwiązania cosmos bazy danych obsługuje szybkie odczyty i zapisy, zapytania logiki transakcyjnej, poziomy spójności i szczegółowej kontroli dostępu za pomocą metody/API tooa jeden kontener zasobów. Usługa Hello obsługuje dystrybuowanie danych na partycje i routingu żądań toohello prawo partycji kwerendy. 

Jak działa partycjonowania? Każdy element musi mieć klucz partycji i klucz wiersza, które identyfikują go. Klucz partycji działa jako partycji logicznej danych oraz zapewnia rozwiązania Cosmos DB z granicą fizycznych dystrybucję danych partycji. Krótko mówiąc Oto jak partycjonowania działa w usłudze Azure DB rozwiązania Cosmos:

* Udostępnić kontener DB rozwiązania Cosmos z `T` przepływności żądania/s
* Tle hello DB rozwiązania Cosmos przepisy partycje wymagane tooserve `T` żądania/s. Jeśli `T` jest większa niż maksymalna przepustowość hello przypadających na partycję `t`, następnie DB rozwiązania Cosmos przepisy `N`  =  `T/t` partycji
* Rozwiązania cosmos DB przydziela hello miejsca klucza partycji klawiszy skrótów równomiernie między hello `N` partycji. Tak każda partycja (partycji fizycznej) obsługuje wartości klucza partycji 1-N (partycje logiczne)
* Gdy partycji fizycznej `p` osiągnie limit magazynu DB rozwiązania Cosmos bezproblemowo dzieli `p` do dwóch nowych partycji `p1` i `p2` i rozpowszechnia wartości tooroughly połowa hello klucze tooeach z hello partycje. Tę samą operację jest niewidoczne tooyour aplikacji.
* Podobnie, podczas udostępniania przepływności wyższy niż `t*N` przepływności, DB rozwiązania Cosmos dzieli się co najmniej jeden z partycji toosupport hello wyższej przepustowości

Hello kluczy partycji semantyka semantyki hello nieco inne toomatch każdego interfejsu API, jak pokazano w poniższej tabeli hello:

| Interfejs API | Klucz partycji | Klucz wiersza |
| --- | --- | --- |
| DocumentDB | Ścieżka do klucza partycji niestandardowych | stałe`id` | 
| MongoDB | klucz w niezależnych niestandardowych  | stałe`_id` | 
| Graph | Właściwość klucza partycji niestandardowych | stałe`id` | 
| Tabela | stałe`PartitionKey` | stałe`RowKey` | 

Rozwiązania cosmos DB używa skrótu na podstawie partycjonowania. Podczas zapisywania elementu DB rozwiązania Cosmos skróty hello wartość klucza partycji i hello Użyj skrótu toodetermine wynik elementu hello toostore partycji na. Wszystkie elementy z hello tego samego klucza partycji w magazynach rozwiązania cosmos DB hello tej samej partycji fizycznej. Wybór Hello klucza partycji hello jest bardzo ważne ma toomake w czasie projektowania. Należy wybrać nazwę właściwości, który ma szeroki zakres wartości i ma nawet wzorce dostępu.

> [!NOTE]
> Jest najlepszym toohave praktyki klucza partycji z wielu różnych wartości (co najmniej 100s-1000).
>

Kontenery DB rozwiązania Cosmos Azure mogą być tworzone jako "fixed" lub "nieograniczone." Kontenery o stałym rozmiarze mieć maksymalnie 10 GB i 10 000 RU/s przepustowości. Niektóre funkcje interfejsu API umożliwiają toobe klucza partycji hello pominięcia kontenerów o stałym rozmiarze. toocreate kontenera jako nieograniczone, należy określić minimalną przepustowość 2500 RU/s.

## <a name="partitioning-and-provisioned-throughput"></a>Partycjonowania i zainicjowaną przepływności
Rozwiązania cosmos DB zaprojektowano pod kątem przewidywalnej wydajności. Po utworzeniu kontenera zarezerwować przepływność w zakresie  **[jednostek żądania](request-units.md) (RU) na sekundę z dodatkiem potencjalnych dla RU minutę**. Każde żądanie przypisano dodatkowego jednostki żądania, która jest proporcjonalny toohello ilość zasobów systemowych, takich jak procesor CPU, pamięci i używane przez hello operacji We/Wy. Odczyt dokumentu 1 KB z spójność sesji zużywa jednostki żądania. Odczytu wynosi 1 RU niezależnie od hello liczba elementów przechowywane lub hello liczbę jednoczesnych żądań, w którym są uruchomione w hello tym samym czasie. Większe elementy wymagają wyższych jednostki żądania, w zależności od wielkości hello. Jeśli znasz hello rozmiar jednostki i hello liczba odczytów toosupport dla aplikacji, można udostępnić hello dokładną ilość wymaganych przez aplikację do odczytu wymaga przepływności. 

> [!NOTE]
> tooachieve hello pełnej przepływności hello kontenera, musisz wybrać klucza partycji, która pozwala tooevenly dystrybucję żądań między niektórych wartości klucza partycji distinct.
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-hello-azure-cosmos-db-apis"></a>Praca z hello Azure rozwiązania Cosmos DB API
Można użyć hello portalu Azure lub interfejsu wiersza polecenia Azure toocreate kontenerów i skalować je w dowolnym momencie. W tej sekcji przedstawiono sposób toocreate kontenery i określ hello przepływności i partycji definicji klucza w każdym hello obsługiwane interfejsów API.

### <a name="documentdb-api"></a>Interfejs API usługi DocumentDB
następujące przykładowe Hello pokazuje, jak toocreate kontenera (kolekcja) przy użyciu hello interfejsu API usługi DocumentDB. Szczegółowe informacje można znaleźć [partycjonowania z interfejsem API usługi DocumentDB](partition-data.md).

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

Można znaleźć elementu (dokument) przy użyciu hello `GET` w hello interfejsu API REST lub przy użyciu metody `ReadDocumentAsync` w jednym z hello zestawów SDK.

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>Interfejs API usługi MongoDB
Z hello API bazy danych MongoDB można utworzyć kolekcję podzielonej przez ulubionego narzędzia, sterownika lub zestawu SDK. W tym przykładzie używamy hello powłoki Mongo hello tworzenia kolekcji.

W hello powłoki Mongo:

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
Wyniki:

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a>Interfejs API tabel

Z hello API tabeli określ hello przepływności dla tabel w hello appSettings konfiguracji aplikacji:

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

Następnie utworzysz tabelę przy użyciu magazynu tabel Azure hello zestawu SDK. Klucz partycji Hello niejawnie zostanie utworzona jako hello `PartitionKey` wartość. 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

Można pobrać pojedynczą jednostką przy użyciu następującego fragmentu hello:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
Zobacz [programowania z użyciem hello API tabeli](tutorial-develop-table-dotnet.md) więcej szczegółów.

### <a name="graph-api"></a>Interfejs API programu Graph

Z hello interfejsu API programu Graph należy użyć hello portalu Azure lub interfejsu wiersza polecenia toocreate kontenerów. Ponieważ bazy danych Azure rozwiązania Cosmos jest wiele modeli, można użyć jednej z hello toocreate innych modeli i skalować kontenera programu graph.

Możesz przeczytać wierzchołków ani przy użyciu klucza partycji hello i identyfikator w Gremlin krawędzi. Na przykład na wykresie region ("USA") jako klucza partycji hello i "Seattle" jako klucza wiersza hello, można znaleźć wierzchołka przy użyciu składni hello:

```
g.V(['USA', 'Seattle'])
```

Takie same z krawędziami, możesz odwoływać się krawędzi przy użyciu hello klucz partycji i klucz wiersza.

```
g.E(['USA', 'I5'])
```

Zobacz [Gremlin Obsługa rozwiązania Cosmos DB](gremlin-support.md) więcej szczegółów.


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>Projektowanie dla partycji
tooscale skutecznie z bazy danych rozwiązania Cosmos platformy Azure, należy toopick stanowi dobry klucz partycji podczas tworzenia Twojej kontenera. Istnieją dwie najważniejsze kwestie dotyczące wybierania klucza partycji:

* **Granic zapytania i transakcji**: wybór klucza partycji zrównoważenia hello potrzeby tooenable hello użycie transakcje hello wymaganie toodistribute jednostek wielu tooensure kluczy partycji skalowalne rozwiązanie. W jednym extreme można ustawić hello tego samego klucza partycji dla wszystkich elementów, ale może ograniczać skalowalność hello rozwiązania. Na powitania y. można przypisać klucza partycji unikatowy dla każdego elementu, którego będzie wysoce skalowalna, ale może uniemożliwić korzystanie z transakcji krzyżowego dokumentu za pomocą procedur składowanych i wyzwalaczy. Klucz partycji idealne jest jednym umożliwiająca toouse wydajność zapytań, na którym jest wystarczająca Kardynalność tooensure jest skalowalne rozwiązanie. 
* **Nie magazynu i wydajności wąskich gardeł**: koniecznie toopick właściwość, która umożliwia zapisuje toobe dystrybuowana do różnych różne wartości. Żądania toohello tego samego klucza partycji nie może przekraczać przepływności hello jednej partycji i są ograniczane. Dlatego jest ważne toopick klucza partycji, który nie powoduje "punkty aktywne" w aplikacji. Ponieważ wszystkie dane powitania dla klucza jednej partycji muszą być przechowywane w partycji, zalecane jest również tooavoid klucze partycji o dużych ilości danych dla hello tę samą wartość. 

Oto kilka rzeczywistych scenariuszy i klucze partycji dla każdego:
* W przypadku wdrażania zaplecza profilu użytkownika, identyfikator użytkownika hello jest dobrym rozwiązaniem w przypadku klucza partycji.
* Jeśli są przechowywane dane IoT na przykład stanu urządzenia, identyfikator urządzenia jest dobrym rozwiązaniem w przypadku klucza partycji.
* Jeśli używasz bazy danych Azure rozwiązania Cosmos rejestrowanie dane szeregów czasowych, następnie hello nazwę hosta lub identyfikator procesu jest dobrym rozwiązaniem dla klucza partycji.
* Jeśli masz architektura wielodostępnej, identyfikator dzierżawy hello jest dobrym rozwiązaniem w przypadku klucza partycji.

W niektórych zastosowań jak IoT i profilów użytkownika, powitalne klucz partycji może być hello sam jako identyfikatora (klucz dokumentu). W innych, takie jak hello czasu serii danych może mieć klucza partycji, który jest inny niż identyfikator hello.

### <a name="partitioning-and-loggingtime-series-data"></a>Partycjonowania i rejestrowanie szeregi danych
Jeden z hello typowe przypadki użycia DB rozwiązania Cosmos jest rejestrowanie i telemetrii. Jest ważne toopick stanowi dobry klucz partycji, ponieważ może być konieczne tooread/zapisu ogromnych ilości danych. Wybór Hello zależy od odczytu i zapisu stawki i rodzajów kwerend czy spodziewasz się toorun. Poniżej przedstawiono kilka wskazówek dotyczących toochoose stanowi dobry klucz partycji.

* Jeśli Twoje przypadek użycia obejmuje mała liczba zapisuje grupowania w długim okresie czasu i należy tooquery przez zakresy sygnatury czasowe i inne filtry, a następnie za pomocą pakietu zbiorczego hello sygnatury czasowej, na przykład data jako klucza partycji jest dobre rozwiązanie. Dzięki temu można tooquery przez wszystkie dane hello daty z jednej partycji. 
* Jeśli obciążenie napisano ciężki, który jest bardziej popularne, należy użyć klucza partycji, który nie jest oparty na sygnatury czasowej, dzięki czemu DB rozwiązania Cosmos można rozpowszechniają zapisy równomiernie różnych partycji. W tym miejscu nazwę hosta, identyfikator procesu, identyfikator działania lub inna właściwość o dużej kardynalności jest dobrym rozwiązaniem. 
* Trzeci podejście jest hybrydowego co gdzie masz wiele kontenerów, po jednym dla każdego dnia miesięcznie, a klucz partycji hello szczegółowego właściwości, takie jak nazwa hosta. To ustawienie hello korzyści, które można ustawić różne przepływności oparte na powitania przedział czasu, na przykład hello kontener dla bieżącego miesiąca hello jest udostępniane z wyższej przepustowości ponieważ służy on odczyty i zapisy, ostatnich miesięcy z niższą przepływność od służą one tylko operacji odczytu.

### <a name="partitioning-and-multi-tenancy"></a>Partycjonowanie i obsługi wielu dzierżawców
W przypadku wdrażania aplikacji wielodostępnych, przy użyciu rozwiązania Cosmos DB, istnieją dwa popularne wzorce — klucz partycji co dla każdego dzierżawcy i jeden kontener dla każdego dzierżawcy. Poniżej przedstawiono hello zalet i wad dla każdego:

* Jeden klucz partycji dla poszczególnych dzierżawców: W tym modelu dzierżaw są zawsze umieszczane w jeden kontener. Ale zapytań i wstawiania dla elementów w ramach pojedynczej dzierżawy można wykonywać na jednej partycji. Można też wdrożyć logiki transakcyjnej dla wszystkich elementów w ramach dzierżawy. Ponieważ wielu dzierżawców udostępnić kontener, można zmniejszyć koszty pamięci masowej i przepływność puli zasobów dla dzierżawcy w jeden kontener zamiast inicjowania obsługi administracyjnej dodatkowych wysokość dla każdego dzierżawcy. Wadą Hello jest ma izolację wydajności dla każdego dzierżawcy. Zwiększa wydajność/przepływności dotyczą toohello całego kontenera vs docelowe zwiększa dzierżaw.
* Jeden kontener dla poszczególnych dzierżawców: każdy dzierżawca ma własnych kontenera. W tym modelu może zarezerwować wydajności dla każdego dzierżawcy. Rozwiązania Cosmos DB nowe Obsługa administracyjna model cenowy, ten model jest bardziej ekonomiczne rozwiązanie dla wielu dzierżawców aplikacji z kilku dzierżawcami.

Można również użyć kombinacji/warstwowego podejścia, umożliwiający collocates małych dzierżawcy i przeprowadzanie migracji większych kontenera własnych dzierżaw tootheir.

## <a name="next-steps"></a>Następne kroki
W tym artykule podaliśmy omówienie omówienie pojęć i najlepsze rozwiązania dotyczące partycjonowania z jakiegokolwiek interfejsu API Azure rozwiązania Cosmos bazy danych. 

* Dowiedz się więcej o [udostępnionej przepływności w usłudze Azure DB rozwiązania Cosmos](request-units.md)
* Dowiedz się więcej o [globalne dystrybucji w usłudze Azure DB rozwiązania Cosmos](distribute-data-globally.md)



