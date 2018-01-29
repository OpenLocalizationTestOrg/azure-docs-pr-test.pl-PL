---
title: "Wprowadzenie do platformy Azure rozwiązania Cosmos DB Graph API | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak można użyć bazy danych rozwiązania Cosmos Azure do przechowywania, kwerendy i przechodzenia ogromną wykresów z niskim opóźnieniem przy użyciu języka zapytań wykres Gremlin Apache TinkerPop."
services: cosmos-db
author: luisbosquez
documentationcenter: 
ms.assetid: b916644c-4f28-4964-95fe-681faa6d6e08
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/05/2017
ms.author: lbosq
ms.openlocfilehash: 14921dbeb0b670e4ec29a224caca07da12bfb82b
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/08/2018
---
# <a name="introduction-to-azure-cosmos-db-graph-api"></a>Wprowadzenie do platformy Azure rozwiązania Cosmos DB: interfejs API programu Graph

[Azure DB rozwiązania Cosmos](introduction.md) globalnie rozproszone, multimodel bazy danych usługi firmy Microsoft dla aplikacji o krytycznym znaczeniu. Azure DB rozwiązania Cosmos zapewnia następujące funkcje, których wszystkie bazują na [SLA branży](https://azure.microsoft.com/support/legal/sla/cosmos-db/):

* [Gotowa do użytku dystrybucja globalna](distribute-data-globally.md)
* [Elastyczne skalowanie przepływność i magazyn](partition-data.md) na całym świecie
* Jednocyfrowej milisekundy opóźnienia w 99-ty percentyl
* [Pięć dobrze zdefiniowane poziomy spójności](consistency-levels.md)
* Zagwarantować wysokiej dostępności 

Usługa Azure Cosmos DB [automatycznie indeksuje dane](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) bez konieczności zarządzania schematami i indeksami. Jest multimodel i obsługuje dokumentu, klucz wartość, wykres i modeli danych kolumnowym.

Firma Microsoft zaleca, aby obejrzeć poniższego klipu wideo, w którym wyjaśniono, jak wprowadzenie wykresy dla bazy danych Azure rozwiązania Cosmos Kirill Gavrylyuk:

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Graphs-with-Azure-Cosmos-DB-Gremlin-API/player]
> 
> 

Udostępnia interfejs API Graph Azure rozwiązania Cosmos bazy danych:

- Wykres modelowania.
- Traversal interfejsów API.
- Gotowe dystrybucji globalnego.
- Elastyczne Skalowanie pamięci masowej i przepływność z mniej niż 10 ms odczytu opóźnienia i mniej niż 15 ms na 99-ty percentyl.
- Automatyczne indeksowanie z dostępności błyskawicznych zapytania.
- Dostosowywalne poziomy spójności.
- Kompleksowe SLA, w tym o dostępności 99,99% umowy SLA dla wszystkich kont w pojedynczym regionie i wszystkich kont w przypadku z swobodna spójności i 99,999% odczytu dostępności na wszystkich kontach w przypadku bazy danych.

Aby zapytania bazy danych Azure rozwiązania Cosmos, można użyć [Apache TinkerPop](http://tinkerpop.apache.org) wykresu języka przechodzenie [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), lub tak jak inne systemy wykres TinkerPop zgodnego [Apache Spark GraphX](spark-connector-graph.md).

Ten artykuł zawiera omówienie interfejsu API Graph usługi Azure rozwiązania Cosmos bazy danych i wyjaśniono, jak go użyć do przechowywania ogromną wykresów z miliardy wierzchołki i krawędzi. Można zbadać wykresów za pomocą milisekundy opóźnienia i łatwo rozwijać struktury wykres i schematu.

## <a name="graph-database"></a>Baza danych wykresu
Dane w świecie rzeczywistym naturalnie są połączone. Modelowanie tradycyjnych danych skupia się na jednostek. Dla wielu aplikacji jest również potrzebę modelu lub model naturalnie zarówno jednostki i relacje.

A [wykres](http://mathworld.wolfram.com/Graph.html) jest strukturą, która składa się z [wierzchołków](http://mathworld.wolfram.com/GraphVertex.html) i [krawędzi](http://mathworld.wolfram.com/GraphEdge.html). Zarówno wierzchołki i krawędzi może mieć dowolną liczbę właściwości. Wierzchołki oznaczenia odrębny obiekty, takie jak osoby, miejsca lub zdarzenia. Krawędziach oznaczenia relacje między wierzchołków. Na przykład osoba może znać innej osobie, można zaangażowane w przypadku i został ostatnio w danej lokalizacji. Właściwości express informacji o wierzchołki i krawędzi. Przykład właściwości obejmują wierzchołek ma nazwę, wieku oraz krawędzi, który ma sygnaturę czasową i/lub wagi. Więcej formalnie ten model jest nazywany [wykresu właściwości](http://tinkerpop.apache.org/docs/current/reference/#intro). Azure DB rozwiązania Cosmos obsługuje właściwości modelu wykresu.

Na przykład próbki Wykres ukazuje relacje osób, urządzeń przenośnych, udziałów i systemów operacyjnych:

![Przykładowa baza danych przedstawiający osób, urządzeń i udziałów](./media/graph-introduction/sample-graph.png)

Wykresy są przydatne zrozumienie szeroką gamę zestawów danych w nauki, technologii i biznesowych. Wykres bazy danych pozwalają modelu i przechowywania wykresy naturalnie i wydajne, który przydatne w różnych scenariuszach. Wykres baz danych są zwykle bazy danych NoSQL, ponieważ użycie tych przypadkach często również potrzeby elastyczność schematu i szybkie iteracji.

Wykresy oferują nowe i danych zaawansowanych technik modelowania. Ale ten fakt samodzielnie nie jest wystarczające powody do korzystania z bazy danych wykresu. Dla wielu przypadki użycia i wzorce, które obejmują traversals wykresu wykresy przewyższyć tradycyjnych baz danych SQL i NoSQL o rzędów. Różnica w wydajności jest dalsze rozszerzone podczas przesyłania więcej niż jedną relację, takich jak friend z przyjaznego.

Szybkie traversals, zapewniające baz danych wykresu można połączyć z algorytmów wykresu, takie jak pierwszy głębokość wyszukiwania, najpierw szerokość wyszukiwania i algorytmu Dijkstra w, do rozwiązywania problemów w różnych domenach, takich jak sieci społecznościowych, zarządzania zawartością, dane geograficzne, i zalecenia.

## <a name="planet-scale-graphs-with-azure-cosmos-db"></a>Wykresy planety skali z bazy danych Azure rozwiązania Cosmos
Azure DB rozwiązania Cosmos jest bazy danych wykresu w pełni zarządzana, która oferuje dystrybucji globalnych, elastyczne skalowanie magazynu i przepustowości, automatycznego indeksowania zapytania, dostosowywalne poziomy spójności i obsłudze standardu TinkerPop.

![Architektura wykresu w usłudze Azure DB rozwiązania Cosmos](./media/graph-introduction/cosmosdb-graph-architecture.png)

Azure DB rozwiązania Cosmos oferuje następujące możliwości zróżnicowanych w porównaniu do innych baz danych wykresu w rynku:

* Elastycznie skalowalne przepływność i Magazyn

 Wykresy w świecie rzeczywistym musi przebiegać proces skalowania poza pojemność pojedynczego serwera. Z bazy danych rozwiązania Cosmos platformy Azure możesz bezproblemowo skalować wykresów na wielu serwerach. Można również skalować przepływność wykresie niezależnie oparte na Twoich wzorców dostępu. Azure DB rozwiązania Cosmos obsługuje wykresu bazy danych, które można skalować do niemal nieograniczonego rozmiaru magazynu i udostępnionej przepływności.

* W przypadku replikacji

 Azure DB rozwiązania Cosmos niewidocznie replikuje dane wykresu do wszystkich regionów, które zostały skojarzone z Twoim kontem. Replikacji umożliwia tworzenie aplikacji, które wymagają globalnego dostępu do danych. W zakresie spójności, dostępności i wydajności oraz odpowiednie gwarancje są wady i zalety. Azure DB rozwiązania Cosmos zapewnia przezroczysty tryb failover regionalnych, z wielu interfejsów API. Można elastycznie skalować przepływność i magazyn na całym świecie.

* Szybkie zapytania i traversals z zwykłego składni Gremlin

 Przechowywanie heterogenicznych wierzchołki i krawędzi oraz nich zapytań przy użyciu zwykłego składni Gremlin. Azure DB rozwiązania Cosmos wykorzystuje wysoce współbieżną, zwolnić blokady, opartą na strukturze dziennika technologię indeksowania do automatycznego indeksowania całej zawartości. Ta funkcja umożliwia zaawansowane zapytania w czasie rzeczywistym i traversals bez konieczności określania wskazówek schematu, indeksów pomocniczych czy widoków. Dowiedz się więcej w [zapytanie wykresów za pomocą Gremlin](gremlin-support.md).

* W pełni zarządzana

 Azure DB rozwiązania Cosmos eliminuje konieczność zarządzania zasobami maszyn i bazy danych. Jako w pełni zarządzana usługa Microsoft Azure nie trzeba zarządzać maszynami wirtualnymi, wdrażanie i konfigurowanie oprogramowania, zarządzać skalowaniem ani postępowania w przypadku uaktualnienia złożonych warstwy danych. Każdy wykres jest automatycznie kopii zapasowej i chroniona przed regionalnymi awariami. Możesz łatwo dodać konto bazy danych Azure rozwiązania Cosmos i aprowizować pojemność odpowiednio do potrzeb, dzięki czemu można skupić się na aplikacji zamiast pracy i zarządzania bazą danych.

* Automatycznego indeksowania

 Domyślnie bazy danych rozwiązania Cosmos Azure automatycznie indeksuje wszystkie właściwości w węzłach i krawędzi na wykresie i nie oczekują lub wymaga żadnego schematu lub tworzenia indeksów pomocniczych.

* Zgodność z Apache TinkerPop

 Azure DB rozwiązania Cosmos natywnie obsługuje standard Apache TinkerPop open source i może być zintegrowane z innymi systemami włączone TinkerPop wykresu. Tak, można łatwo przeprowadzić migrację z innej bazy danych wykresu, takich jak Titan lub Neo4j, lub przy użyciu bazy danych Azure rozwiązania Cosmos z wykresu analytics platform takich jak [Apache Spark GraphX](spark-connector-graph.md).

* Dostosowywalne poziomy spójności

 Wybierz z pięciu dobrze zdefiniowane poziomy spójności, aby osiągnąć optymalną zależności między wydajnością a spójnością. Dla zapytań i operacji odczytu usługa Azure Cosmos DB oferuje pięć różnych poziomów spójności: „silna”, „powiązana nieaktualność”, „sesja”, „spójny prefiks” i „ostateczna”. Te poziomy spójności szczegółowe, dokładnie zdefiniowane umożliwiają dźwięku kompromisy między spójności, dostępnością i opóźnieniem. Dowiedz się więcej w [danych dostosowywalne poziomy spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md).

Azure DB rozwiązania Cosmos można również użyć wielu modeli, takie jak dokument i wykres w tej samej kontenery lub bazy danych. Kolekcja dokumentów służy do przechowywania danych wykresu równolegle z dokumentów. Zarówno zapytania SQL w formacie JSON i zapytań Gremlin umożliwia kwerendy te same dane w postaci wykresu.

## <a name="get-started"></a>Rozpoczęcie pracy
Służy Azure interfejsu wiersza polecenia (CLI), programu Azure PowerShell lub w portalu Azure z obsługą interfejsu API Graph do utworzenia konta Azure DB rozwiązania Cosmos. Po utworzeniu konta w portalu Azure tak samo, jak zawiera punkt końcowy usługi `https://<youraccount>.gremlin.cosmosdb.azure.com`, Gremlin zapewnia frontonu protokołu WebSocket. Tak samo, jak skonfigurować narzędziami TinkerPop zgodnego [konsoli Gremlin](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console), aby podłączyć się do tego punktu końcowego i tworzenie aplikacji w języku Java, Node.js lub dowolnego Gremlin sterownika klienta.

W poniższej tabeli przedstawiono popularne sterowniki Gremlin korzystających z bazy danych rozwiązania Cosmos Azure:

| Do pobrania | Dokumentacja |
| --- | --- |
| [Java](https://mvnrepository.com/artifact/com.tinkerpop.gremlin/gremlin-java) |[Gremlin JavaDoc](http://tinkerpop.apache.org/javadocs/current/full/) |
| [Node.js](https://www.npmjs.com/package/gremlin) |[Gremlin języka JavaScript w witrynie Github](https://github.com/jbmusso/gremlin-javascript) |
| [Gremlin konsoli](https://tinkerpop.apache.org/downloads.html) |[TinkerPop dokumentów](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console) |

Azure DB rozwiązania Cosmos zawiera także biblioteki .NET, która zawiera metody rozszerzenia Gremlin nad [zestawów SDK DB rozwiązania Cosmos Azure](sql-api-sdk-dotnet.md) za pośrednictwem pakietu NuGet. Ta biblioteka zawiera serwer Gremlin "w toku", który umożliwia bezpośrednie łączenie się z partycji danych.

| Do pobrania | Dokumentacja |
| --- | --- |
| [.NET](https://www.nuget.org/packages/Microsoft.Azure.Graphs/) |[Microsoft.Azure.Graphs](https://msdn.microsoft.com/library/azure/dn948556.aspx) |

Za pomocą [Azure rozwiązania Cosmos DB emulatora](local-emulator.md), można użyć interfejsu API Graph platformy .NET, które są powyżej umożliwiające opracowanie i przetestowanie lokalnie, bez tworzenia subskrypcji platformy Azure lub ponoszenia kosztów. Po zakończeniu jak aplikacja działa w emulatorze, możesz przełączyć się do korzystania z konta bazy danych Azure rozwiązania Cosmos w chmurze.

> [!NOTE]
> Obsługę weryfikacji zapytań Gremlin [Azure rozwiązania Cosmos DB emulatora](local-emulator.md) tylko jest dostępny za pośrednictwem interfejsu API Graph platformy .NET.

## <a name="scenarios-for-graph-support-of-azure-cosmos-db"></a>Scenariusze obsługi wykres Azure DB rozwiązania Cosmos
Poniżej przedstawiono kilka scenariuszy, w której wykres obsługę bazy danych Azure rozwiązania Cosmos może służyć:

* Sieci społecznościowych

 Łącząc dane dotyczące klientów i ich interakcji z innymi osobami, można utworzyć spersonalizowanego doświadczenia, przewidzieć zachowania klienta lub uzyskuj osobom podobne zainteresowań osoby. Azure DB rozwiązania Cosmos może służyć do zarządzania sieci społecznościowych i śledzenia preferencji klienta i dane.

* Aparaty zalecenia

 Ten scenariusz jest często stosowany w sprzedaży detalicznej. Łącząc informacji o produktach, użytkownikach i interakcji użytkownika, takich jak zakupu, przeglądanie lub klasyfikacji elementu, można tworzyć niestandardowe zalecenia. Małe opóźnienia, elastyczne skalowanie i native wykres obsługę bazy danych Azure rozwiązania Cosmos jest idealny dla modelowania tych interakcji.

* Dane geoprzestrzenne

 Wiele aplikacji w telekomunikacyjnych logistyki i planowania podróży muszą znaleźć lokalizację zainteresowania wewnątrz obszaru zlokalizować najkrótszy/optymalnej trasy między dwiema lokalizacjami. Azure DB rozwiązania Cosmos jest naturalna nadające się do tych problemów.

* Internet rzeczy

 Z siecią i połączeń między urządzeniami IoT formę wykres można tworzyć lepsze zrozumienie stanu urządzeń i zasobów. Możesz także dowiedzieć się jak zmiany w jednej części sieci mogą wpłynąć na innej części.

## <a name="next-steps"></a>Kolejne kroki
Aby dowiedzieć się więcej o obsłudze graph w usłudze Azure DB rozwiązania Cosmos, zobacz:

* Rozpoczynanie pracy z [samouczek wykres bazy danych Azure rozwiązania Cosmos](create-graph-dotnet.md).
* Więcej informacji na temat sposobu [zapytanie wykresy w usłudze Azure DB rozwiązania Cosmos za pomocą Gremlin](gremlin-support.md).
