---
title: "Partycjonowanie i skalowanie w poziomie w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat działa jak partycjonowania bazy danych rozwiązania Cosmos Azure, jak skonfigurować partycje i kluczy partycji i Wybieranie klucza prawego partycji aplikacji."
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
ms.openlocfilehash: e2d2847276e553d7511241ff323c3e00aad8e5c9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-partition-and-scale-in-azure-cosmos-db"></a>Jak partycji i skali w usłudze Azure DB rozwiązania Cosmos

[Bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) jest usługą bazy danych globalnych, rozproszone i wiele modeli pomaga osiągnąć szybkie, przewidywalną wydajność i skalę bezproblemowo wraz z aplikacji jako ich przyrostu. Ten artykuł zawiera omówienie sposobu partycjonowania działa dla wszystkich modeli danych w usłudze Azure DB rozwiązania Cosmos i w tym artykule opisano, jak można skonfigurować bazy danych Azure rozwiązania Cosmos kontenery skutecznie skalowania aplikacji.

Partycjonowanie i klucze partycji są uwzględniane w tym Azure piątek wideo z Scott Hanselman i Azure rozwiązania Cosmos DB główny Engineering Menedżer Shireesh Thota.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Podział na partycje w Azure rozwiązania Cosmos bazy danych
W usłudze Azure DB rozwiązania Cosmos można przechowywać i zapytania na danych bez schematu wraz z czasem odpowiedzi kolejności z milisekundy na dowolnym poziomie. Rozwiązania cosmos DB zawiera kontenery do przechowywania danych o nazwie **kolekcje (dla dokumentu), wykresy lub tabele**. Kontenery są zasoby logiczne i może obejmować co najmniej jednej partycji fizycznej lub serwerów. Liczba partycji zależy od rozwiązania Cosmos bazy danych na podstawie rozmiaru magazynu i udostępnionej przepływności kontenera. Każdej partycji w bazie danych rozwiązania Cosmos ma stałą kopie dysków SSD magazynu skojarzone z nim i są replikowane w celu zapewnienia wysokiej dostępności. Zarządzanie partycji pełni zarządza bazy danych Azure rozwiązania Cosmos i nie trzeba pisania złożonego kodu lub Zarządzanie partycjami. Kontenery DB rozwiązania cosmos jest nieograniczony pod względem pamięci masowej i przepływność. 

![poziomy](./media/introduction/azure-cosmos-db-partitioning.png) 

Partycjonowanie jest niewidoczny dla aplikacji. Rozwiązania cosmos bazy danych obsługuje szybkie odczyty i zapisy, zapytania logiki transakcyjnej, poziomy spójności i szczegółowej kontroli dostępu za pomocą metody/interfejsów API do zasobu jeden kontener. Usługa obsługuje dystrybuowanie danych na partycje i routingu żądań zapytań do prawej partycji. 

Jak działa partycjonowania? Każdy element musi mieć klucz partycji i klucz wiersza, które identyfikują go. Klucz partycji działa jako partycji logicznej danych oraz zapewnia rozwiązania Cosmos DB z granicą fizycznych dystrybucję danych partycji. Krótko mówiąc Oto jak partycjonowania działa w usłudze Azure DB rozwiązania Cosmos:

* Udostępnić kontener DB rozwiązania Cosmos z `T` przepływności żądania/s
* W tle DB rozwiązania Cosmos przepisy potrzebny, aby obsługiwać partycje `T` żądania/s. Jeśli `T` jest większa niż maksymalna przepustowość dla każdej partycji `t`, następnie DB rozwiązania Cosmos przepisy `N`  =  `T/t` partycji
* Rozwiązania cosmos DB klawiszy skrótów obszaru klucza partycji są przydziela równomiernie w poprzek `N` partycji. Tak każda partycja (partycji fizycznej) obsługuje wartości klucza partycji 1-N (partycje logiczne)
* Gdy partycji fizycznej `p` osiągnie limit magazynu DB rozwiązania Cosmos bezproblemowo dzieli `p` do dwóch nowych partycji `p1` i `p2` i rozpowszechnia wartości odpowiadających około połowa klucze do każdej partycji. Tę samą operację jest niewidoczny dla aplikacji.
* Podobnie, podczas udostępniania przepływności wyższy niż `t*N` przepływności, DB rozwiązania Cosmos dzieli jedną lub więcej partycji do obsługi wyższej przepustowości

Semantyka kluczy partycji są nieco inne odpowiadające semantykę każdego API, jak pokazano w poniższej tabeli:

| Interfejs API | Klucz partycji | Klucz wiersza |
| --- | --- | --- |
| DocumentDB | Ścieżka do klucza partycji niestandardowych | stałe`id` | 
| MongoDB | klucz w niezależnych niestandardowych  | stałe`_id` | 
| Graph | Właściwość klucza partycji niestandardowych | stałe`id` | 
| Tabela | stałe`PartitionKey` | stałe`RowKey` | 

Rozwiązania cosmos DB używa skrótu na podstawie partycjonowania. Podczas zapisywania elementu DB rozwiązania Cosmos skróty wartość klucza partycji i umożliwia określenie, które partycji do przechowywania elementu w wyniku skrótu. Rozwiązania cosmos bazy danych są przechowywane wszystkie elementy z tym samym kluczem partycji w tej samej partycji fizycznej. Wybór klucza partycji jest ważnych decyzji, które należy podjąć w czasie projektowania. Należy wybrać nazwę właściwości, który ma szeroki zakres wartości i ma nawet wzorce dostępu.

> [!NOTE]
> Jest najlepszym rozwiązaniem będzie mieć klucz partycji wiele różnych wartości (co najmniej 100s-1000).
>

Kontenery DB rozwiązania Cosmos Azure mogą być tworzone jako "fixed" lub "nieograniczone." Kontenery o stałym rozmiarze mieć maksymalnie 10 GB i 10 000 RU/s przepustowości. Niektóre funkcje interfejsu API umożliwiają klucza partycji można pominąć kontenerów o stałym rozmiarze. Aby utworzyć kontener jako nieograniczone, należy określić minimalną przepustowość 2500 RU/s.

## <a name="partitioning-and-provisioned-throughput"></a>Partycjonowania i zainicjowaną przepływności
Rozwiązania cosmos DB zaprojektowano pod kątem przewidywalnej wydajności. Po utworzeniu kontenera zarezerwować przepływność w zakresie  **[jednostek żądania](request-units.md) (RU) na sekundę z dodatkiem potencjalnych dla RU minutę**. Każde żądanie przypisano dodatkowego jednostki żądania, która jest proporcjonalny do liczby zasobów systemowych, takich jak procesor CPU, pamięci i wykorzystanych w ramach operacji We/Wy. Odczyt dokumentu 1 KB z spójność sesji zużywa jednostki żądania. Odczytu wynosi 1 RU niezależnie od liczby elementów przechowywane i liczbę jednoczesnych żądań, w którym są uruchomione w tym samym czasie. Większe elementy wymagają wyższych jednostki żądania w zależności od rozmiaru. Jeśli wiesz, rozmiar jednostki i liczba odczytów potrzebnych do obsługi aplikacji, można udostępnić dokładną ilość wymaganych przez aplikację do odczytu wymaga przepływności. 

> [!NOTE]
> Uzyskanie pełnej przepływności kontenera, musisz wybrać klucza partycji, który umożliwia równomierne rozkładanie żądań między niektórych wartości klucza partycji distinct.
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-the-azure-cosmos-db-apis"></a>Praca z Azure rozwiązania Cosmos DB API
Portalu Azure lub interfejsu wiersza polecenia Azure umożliwia tworzenie kontenerów i skalować je w dowolnym momencie. W tej sekcji przedstawiono sposób tworzenia kontenery i określ definicję klucza przepływności i partycji w każdej z obsługiwanych interfejsów API.

### <a name="documentdb-api"></a>Interfejs API usługi DocumentDB
Poniższy przykład przedstawia sposób tworzenia kontenera (kolekcja) przy użyciu interfejsu API usługi DocumentDB. Szczegółowe informacje można znaleźć [partycjonowania z interfejsem API usługi DocumentDB](partition-data.md).

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

Można znaleźć elementu (dokument) przy użyciu `GET` metody interfejsu API REST lub przy użyciu `ReadDocumentAsync` w jednym z zestawów SDK.

```csharp
// Read document. Needs the partition key and the ID to be specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>Interfejs API usługi MongoDB
Przy użyciu interfejsu API bazy danych MongoDB można utworzyć kolekcję podzielonej przez ulubionego narzędzia, sterownika lub zestawu SDK. W tym przykładzie używamy powłoki Mongo w celu utworzenia kolekcji.

W powłoki Mongo:

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

Przy użyciu interfejsu API tabeli określ przepustowość dla tabel w konfiguracji appSettings dla aplikacji:

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

Następnie można utworzyć tabeli za pomocą magazynu tabel Azure SDK. Klucz partycji niejawnie zostanie utworzona jako `PartitionKey` wartość. 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

Można pobrać pojedynczą jednostką przy użyciu następującego fragmentu kodu:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
Zobacz [programowania z użyciem interfejsu API tabeli](tutorial-develop-table-dotnet.md) więcej szczegółów.

### <a name="graph-api"></a>Interfejs API programu Graph

Z interfejsu API programu Graph musi używać portalu Azure lub interfejsu wiersza polecenia utworzyć kontenerów. Alternatywnie ponieważ bazy danych Azure rozwiązania Cosmos jest wiele modeli, umożliwia jeden z innymi modelami tworzyć i skalować kontenera programu graph.

Możesz przeczytać wierzchołków ani przy użyciu klucza partycji i identyfikator w Gremlin krawędzi. Na przykład na wykresie region ("USA") jako klucza partycji i "Seattle" jako klucza wiersza, można znaleźć wierzchołka, używając następującej składni:

```
g.V(['USA', 'Seattle'])
```

Takie same z krawędziami, możesz odwoływać się krawędzi przy użyciu klucza partycji i klucz wiersza.

```
g.E(['USA', 'I5'])
```

Zobacz [Gremlin Obsługa rozwiązania Cosmos DB](gremlin-support.md) więcej szczegółów.


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>Projektowanie dla partycji
Skalować skutecznie bazy danych rozwiązania Cosmos platformy Azure, musisz wybierz stanowi dobry klucz partycji podczas tworzenia Twojej kontenera. Istnieją dwie najważniejsze kwestie dotyczące wybierania klucza partycji:

* **Granic zapytania i transakcji**: wybór klucza partycji powinien równoważyć potrzeby korzystanie z transakcje wymaganie rozpowszechniają jednostek wielu kluczy partycji, aby upewnić się, skalowalna. W jednym extreme można ustawić ten sam klucz partycji dla wszystkich elementów, ale może to ograniczyć skalowalności rozwiązania. Y. można przypisać klucza partycji unikatowy dla każdego elementu, którego będzie wysoce skalowalna, ale może uniemożliwić korzystanie z transakcji krzyżowego dokumentu za pomocą procedur składowanych i wyzwalaczy. Klucz partycji idealna to jedną, która pozwala na użycie wydajność zapytań i ma Kardynalność wystarczające do upewnij się, że rozwiązanie jest skalowalna. 
* **Nie magazynu i wydajności wąskich gardeł**: ważne jest, aby wybrać właściwość, która umożliwia zapis do być rozproszone na różnych różne wartości. Żądania do tego samego klucza partycji nie może przekraczać przepływność jednej partycji, są ograniczane. Dlatego jest ważne pobrać klucz partycji, który nie powoduje "punkty aktywne" w aplikacji. Ponieważ wszystkie dane dla klucza jednej partycji musi być przechowywany w partycji, zalecane jest aby uniknąć klucze partycji o dużych ilości danych dla tej samej wartości. 

Oto kilka rzeczywistych scenariuszy i klucze partycji dla każdego:
* W przypadku wdrażania zaplecza profilu użytkownika, identyfikator użytkownika jest dobrym rozwiązaniem w przypadku klucza partycji.
* Jeśli są przechowywane dane IoT na przykład stanu urządzenia, identyfikator urządzenia jest dobrym rozwiązaniem w przypadku klucza partycji.
* Jeśli używasz bazy danych Azure rozwiązania Cosmos rejestrowanie dane szeregów czasowych, identyfikator hosta lub procesu jest dobrym rozwiązaniem w przypadku klucza partycji.
* Jeśli masz architektura wielodostępnej, identyfikator dzierżawy jest dobrym rozwiązaniem w przypadku klucza partycji.

W niektórych zastosowań takich jak profile IoT i użytkownika, klucz partycji może być taki sam jak identyfikator (klucz dokumentu). W innych, takie jak czas dane serii może być kluczem partycji, który jest inny niż identyfikator.

### <a name="partitioning-and-loggingtime-series-data"></a>Partycjonowania i rejestrowanie szeregi danych
Jeden z typowe przypadki użycia DB rozwiązania Cosmos jest rejestrowanie i telemetrii. Należy wybrać stanowi dobry klucz partycji, ponieważ może być konieczne odczytu/zapisu ogromnych ilości danych. Wybór zależy od odczytu i zapisu stawki i rodzaje zapytań, które chcesz uruchomić. Poniżej przedstawiono kilka wskazówek na temat wybierania stanowi dobry klucz partycji.

* Jeśli Twoje przypadek użycia obejmuje mała liczba zapisuje nagromadzeniem dłuższy czas i trzeba zapytania według zakresów sygnatury czasowe i inne filtry, a następnie za pomocą pakietu zbiorczego sygnatury czasowej, na przykład data jako klucza partycji jest dobre rozwiązanie. Umożliwia zapytania przez wszystkie dane dotyczące daty z jednej partycji. 
* Jeśli obciążenie napisano ciężki, który jest bardziej popularne, należy użyć klucza partycji, który nie jest oparty na sygnatury czasowej, dzięki czemu DB rozwiązania Cosmos można rozpowszechniają zapisy równomiernie różnych partycji. W tym miejscu nazwę hosta, identyfikator procesu, identyfikator działania lub inna właściwość o dużej kardynalności jest dobrym rozwiązaniem. 
* Trzeci podejście jest hybrydowego co gdzie masz wiele kontenerów, po jednym dla każdego dnia miesięcznie, a klucz partycji to szczegółowe właściwości, takie jak nazwa hosta. To ustawienie korzyści, które można ustawić różne przepływności oparte na przedział czasu, na przykład kontener dla bieżącego miesiąca jest udostępniane z wyższej przepustowości ponieważ służy on odczyty i zapisy, ostatnich miesięcy z niższą przepływność od momentu ich tylko obsługiwać operacji odczytu.

### <a name="partitioning-and-multi-tenancy"></a>Partycjonowanie i obsługi wielu dzierżawców
W przypadku wdrażania aplikacji wielodostępnych, przy użyciu rozwiązania Cosmos DB, istnieją dwa popularne wzorce — klucz partycji co dla każdego dzierżawcy i jeden kontener dla każdego dzierżawcy. Poniżej przedstawiono zalet i wad dla każdego:

* Jeden klucz partycji dla poszczególnych dzierżawców: W tym modelu dzierżaw są zawsze umieszczane w jeden kontener. Ale zapytań i wstawiania dla elementów w ramach pojedynczej dzierżawy można wykonywać na jednej partycji. Można też wdrożyć logiki transakcyjnej dla wszystkich elementów w ramach dzierżawy. Ponieważ wielu dzierżawców udostępnić kontener, można zmniejszyć koszty pamięci masowej i przepływność puli zasobów dla dzierżawcy w jeden kontener zamiast inicjowania obsługi administracyjnej dodatkowych wysokość dla każdego dzierżawcy. Wadą jest to, że nie masz izolację wydajności dla każdego dzierżawcy. Zwiększa wydajność/przepływności dotyczą vs całego kontenera zwiększa docelowej dla dzierżawców.
* Jeden kontener dla poszczególnych dzierżawców: każdy dzierżawca ma własnych kontenera. W tym modelu może zarezerwować wydajności dla każdego dzierżawcy. Rozwiązania Cosmos DB nowe Obsługa administracyjna model cenowy, ten model jest bardziej ekonomiczne rozwiązanie dla wielu dzierżawców aplikacji z kilku dzierżawcami.

Można również użyć kombinacji/warstwowego podejścia, umożliwiający collocates małych dzierżawcy i przeprowadzanie migracji większych dzierżawcy do ich własnych kontenera.

## <a name="next-steps"></a>Następne kroki
W tym artykule podaliśmy omówienie omówienie pojęć i najlepsze rozwiązania dotyczące partycjonowania z jakiegokolwiek interfejsu API Azure rozwiązania Cosmos bazy danych. 

* Dowiedz się więcej o [udostępnionej przepływności w usłudze Azure DB rozwiązania Cosmos](request-units.md)
* Dowiedz się więcej o [globalne dystrybucji w usłudze Azure DB rozwiązania Cosmos](distribute-data-globally.md)



