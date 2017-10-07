---
title: "Wprowadzenie tooAzure rozwiązania Cosmos DB Graph API | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak można użyć bazy danych Azure rozwiązania Cosmos toostore, zapytań i wykresy ogromną przechodzenia z niskim opóźnieniem przy użyciu hello hello Gremlin wykres zapytania języka Apache TinkerPop."
services: cosmos-db
author: dennyglee
documentationcenter: 
ms.assetid: b916644c-4f28-4964-95fe-681faa6d6e08
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/21/2017
ms.author: denlee
ms.openlocfilehash: a4e79a4aa27976966baf0554928026177991ff69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-graph-api"></a>Wprowadzenie tooAzure DB rozwiązania Cosmos: interfejs API programu Graph

[Azure DB rozwiązania Cosmos](introduction.md) jest hello globalnie rozproszone i wiele modeli bazy danych usługi firmy Microsoft dla aplikacji o krytycznym znaczeniu. Udostępnia bazę danych systemu Azure rozwiązania Cosmos [dystrybucji globalne gotowe](distribute-data-globally.md), [elastyczne skalowanie przepływność i magazyn](partition-data.md) na całym świecie, jednocyfrowej milisekundy opóźnienia na powitania 99-ty percentyl [pięć dobrze zdefiniowane poziomy spójności](consistency-levels.md), zagwarantować wysokiej dostępności, wszystkie bazują na [SLA branży](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure DB rozwiązania Cosmos [automatycznie indeksuje danych](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) bez konieczności toodeal z zarządzania schematu i indeksu. To usługa wielomodelowa, obsługująca modele dokumentowe, klucz-wartość, wykresy i kolumny.

![Gremlin, wykres i bazy danych Azure rozwiązania Cosmos](./media/graph-introduction/graph-gremlin.png)

udostępnia Hello interfejsu API programu Graph usługi Azure rozwiązania Cosmos bazy danych:

- Wykres modelowania
- Traversal interfejsów API
- Globalne dystrybucji gotowe
- Elastyczne Skalowanie pamięci masowej i przepływność z mniej niż 10 ms odczytu opóźnienia i mniej niż 15 ms na powitania 99-ty percentyl
- Automatyczne indeksowanie z dostępności błyskawicznych zapytania
- Dostosowywalne poziomy spójności
- Kompleksowe umów SLA, w tym dostępności 99,99%

tooquery bazy danych Azure rozwiązania Cosmos, można użyć hello [Apache TinkerPop](http://tinkerpop.apache.org) wykresu języka przechodzenie [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), lub tak jak inne systemy wykres zgodnego TinkerPop [Apache Spark GraphX](spark-connector-graph.md).

Ten artykuł zawiera omówienie hello interfejsu API programu Graph usługi Azure rozwiązania Cosmos bazy danych i wyjaśniono, jak umożliwia wykresy ogromną toostore z miliardy wierzchołki i krawędzi. Można zbadać wykresy hello za pomocą milisekundy opóźnienia i łatwo rozwijać hello Wykres struktury i schematu.

## <a name="graph-database"></a>Baza danych wykresu
Dane w świecie rzeczywistym hello naturalnie są połączone. Modelowanie tradycyjnych danych skupia się na jednostek. Dla wielu aplikacji, jest również toomodel potrzeby lub toomodel zarówno jednostki i relacje naturalny.

A [wykres](http://mathworld.wolfram.com/Graph.html) jest strukturą, która składa się z [wierzchołków](http://mathworld.wolfram.com/GraphVertex.html) i [krawędzi](http://mathworld.wolfram.com/GraphEdge.html). Zarówno wierzchołki i krawędzi może mieć dowolną liczbę właściwości. Wierzchołki oznaczenia odrębny obiekty, takie jak osoby, miejsca lub zdarzenia. Krawędziach oznaczenia relacje między wierzchołków. Na przykład osoba może znać innej osobie, można zaangażowane w przypadku i został ostatnio w danej lokalizacji. Właściwości express informacji o hello wierzchołki i krawędzi. Przykład właściwości obejmują wierzchołek ma nazwę, wieku oraz krawędzi, którego sygnatura czasowa i/lub wagi. Więcej formalnie ten model jest nazywany [wykresu właściwości](http://tinkerpop.apache.org/docs/current/reference/#intro). Azure DB rozwiązania Cosmos obsługuje hello właściwość graph modelu.

Na przykład następujące hello przykładowe wykres przedstawia relacje między osób, urządzeń przenośnych, udziałów i systemów operacyjnych.

![Przykładowa baza danych przedstawiający osób, urządzeń i udziałów](./media/graph-introduction/sample-graph.png)

Wykresy są przydatne toounderstand szeroką gamę zestawów danych w nauki, technologii i biznesowych. Wykres bazy danych pozwalają modelu i przechowywania wykresy naturalnie i wydajne, który przydatne w różnych scenariuszach. Wykres baz danych są zwykle bazy danych NoSQL, ponieważ użycie tych przypadkach często również potrzeby elastyczność schematu i szybkie iteracji.

Wykresy oferują nowe i danych zaawansowanych technik modelowania. Ale ten fakt samodzielnie nie jest wystarczające toouse Przyczyna bazy danych wykresu. Dla wielu przypadki użycia i wzorce, które obejmują traversals wykresu wykresy przewyższyć tradycyjnych baz danych SQL i NoSQL o rzędów. Różnica w wydajności jest dalsze rozszerzone podczas przesyłania więcej niż jedną relację, takich jak friend z przyjaznego.

Traversals szybkiego hello zapewniające baz danych wykresu można połączyć z algorytmów wykresu, najpierw głębokość wyszukiwania, wyszukiwania szerokość pierwszej i Dijkstra przez algorytm, toosolve problemów w różnych domenach, takich jak sieci społecznościowych, zarządzania zawartością, dane geograficzne, i zalecenia.

## <a name="planet-scale-graphs-with-azure-cosmos-db"></a>Wykresy planety skali z bazy danych Azure rozwiązania Cosmos
Azure DB rozwiązania Cosmos jest bazy danych wykresu w pełni zarządzana, która oferuje dystrybucji globalnych, elastyczne Skalowanie pamięci masowej i przepływność, automatycznego indeksowania i zapytania dostosowywalne poziomy spójności i obsłudze standardu TinkerPop hello.  

![Architektura wykresu w usłudze Azure DB rozwiązania Cosmos](./media/graph-introduction/cosmosdb-graph-architecture.png)

Azure DB rozwiązania Cosmos oferuje następujące hello zróżnicowane możliwości w porównaniu baz danych wykresu tooother rynku hello:

* Elastycznie skalowalne przepływność i Magazyn

 Wykresy w świecie rzeczywistym hello muszą tooscale poza pojemność hello pojedynczego serwera. Z bazy danych rozwiązania Cosmos platformy Azure możesz bezproblemowo skalować wykresów na wielu serwerach. Możliwe jest także skalowanie hello przepływność wykresie niezależnie oparte na Twoich wzorców dostępu. Azure DB rozwiązania Cosmos obsługuje bazy danych wykresu, które mogą być skalowane toovirtually nieograniczonego rozmiaru magazynu i udostępnionej przepływności.

* W przypadku replikacji

 Azure DB rozwiązania Cosmos replikuje niewidocznie Twojej tooall obszarach danych wykresu skojarzone z Twoim kontem. Usługa replikacji umożliwia toodevelop aplikacji, które wymagają dostępu globalny toodata. W obszarach hello spójności, dostępności, wydajności i odpowiednie gwarancje są wady i zalety. Azure DB rozwiązania Cosmos zapewnia przezroczysty tryb failover regionalnych, z wielu interfejsów API. Między Witaj świecie można elastycznie skalować przepływność i magazyn.

* Szybkie zapytania i traversals z zwykłego składni Gremlin

 Przechowywanie heterogenicznych wierzchołki i krawędzi oraz nich zapytań przy użyciu zwykłego składni Gremlin. Azure DB rozwiązania Cosmos wykorzystuje wysoce współbieżną, zwolnić blokady, opartą na strukturze dziennika indeksowania technologii tooautomatically indeks całą zawartość. Ta funkcja umożliwia zaawansowane zapytania w czasie rzeczywistym i traversals bez hello wymagają toospecify wskazówek schematu, indeksów pomocniczych czy widoków. Dowiedz się więcej w [wykresy zapytania przy użyciu Gremlin](gremlin-support.md).

* W pełni zarządzana

 Azure DB rozwiązania Cosmos eliminuje hello potrzeby toomanage maszyn i bazy danych zasobów. Jako w pełni zarządzana usługa Microsoft Azure możesz nie nie potrzeba maszyn wirtualnych toomanage, wdrażanie i konfigurowanie oprogramowania, zarządzać skalowaniem lub postępowania w przypadku uaktualnienia złożonych warstwy danych. Każdy wykres jest automatycznie kopii zapasowej i chroniona przed regionalnymi awariami. Możesz łatwo dodać konto bazy danych Azure rozwiązania Cosmos i aprowizować pojemność odpowiednio do potrzeb, dzięki czemu można skupić się na aplikacji zamiast pracy i zarządzania bazą danych.

* Automatycznego indeksowania

 Domyślnie bazy danych Azure rozwiązania Cosmos automatycznie indeksuje wszystkie właściwości hello w węzłach i krawędzi wykresu hello i nie oczekują lub wymaga żadnego schematu lub tworzenia indeksów pomocniczych.

* Zgodność z Apache TinkerPop

 Azure DB rozwiązania Cosmos natywnie obsługuje standard Apache TinkerPop open source hello i może być zintegrowane z innymi systemami włączone TinkerPop wykresu. Tak, można łatwo przeprowadzić migrację z innej bazy danych wykresu, takich jak Titan lub Neo4j, lub przy użyciu bazy danych Azure rozwiązania Cosmos z wykresu analytics platform takich jak [Apache Spark GraphX](spark-connector-graph.md).

* Dostosowywalne poziomy spójności

 Wybierz z pięciu spójności dobrze zdefiniowanych poziomów tooachieve optymalnego kompromisu między wydajnością a spójnością. Dla zapytań i operacji odczytu usługa Azure Cosmos DB oferuje pięć różnych poziomów spójności: „silna”, „powiązana nieaktualność”, „sesja”, „spójny prefiks” i „ostateczna”. Te poziomy spójności szczegółowe, dokładnie zdefiniowane pozwalają toomake dźwięku wady i zalety korzystania spójności, dostępnością i opóźnieniem. Dowiedz się więcej w [przy użyciu spójności poziomy toomaximize dostępności i wydajności w usłudze DocumentDB](consistency-levels.md).

Azure DB rozwiązania Cosmos również użyć wielu modeli, takie jak dokument i wykres, poziomu hello kontenery tego samego lub bazy danych. Można użyć danych wykresu toostore kolekcji dokumentów równolegle z dokumentów. Można użyć zarówno zapytania SQL w formacie JSON i tooquery zapytań Gremlin hello tych samych danych co wykres.

## <a name="getting-started"></a>Wprowadzenie
Można użyć hello Azure interfejsu wiersza polecenia (CLI), programu Azure Powershell lub hello portalu Azure z obsługą kont Azure DB rozwiązania Cosmos toocreate interfejsu API graph. Po utworzeniu konta hello Azure portal udostępnia punkt końcowy usługi tak samo, jak `https://<youraccount>.graphs.azure.com`, Gremlin zapewnia frontonu protokołu WebSocket. Można skonfigurować z narzędzia TinkerPop zgodnego, takie jak hello [konsoli Gremin](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console), tooconnect toothis punktu końcowego i kompilacja aplikacji w języku Java, Node.js lub dowolnego Gremlin sterownika klienta.

Witaj poniższej tabeli przedstawiono popularne sterowniki Gremlin można względem bazy danych Azure rozwiązania Cosmos:

| Do pobrania | Dokumentacja |
| --- | --- |
| [Java](https://mvnrepository.com/artifact/com.tinkerpop.gremlin/gremlin-java) |[Gremlin JavaDoc](http://tinkerpop.apache.org/javadocs/current/full/) |
| [Node.js](https://www.npmjs.com/package/gremlin) |[Gremlin języka JavaScript w witrynie Github](https://github.com/jbmusso/gremlin-javascript) |
| [Gremlin konsoli](https://tinkerpop.apache.org/downloads.html) |[TinkerPop dokumentów](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console) |

Udostępnia biblioteki .NET, która zawiera metody rozszerzenia Gremlin u góry hello Azure DB rozwiązania Cosmos [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md) za pośrednictwem pakietu NuGet. Ta biblioteka zawiera serwer Gremlin "w toku" służy tooconnect bezpośrednio tooDocumentDB danych partycji.

| Do pobrania | Dokumentacja |
| --- | --- |
| [.NET](https://www.nuget.org/packages/Microsoft.Azure.Graphs/) |[Microsoft.Azure.Graphs](https://msdn.microsoft.com/library/azure/dn948556.aspx) |

Za pomocą hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md), można użyć toodevelop interfejsu API programu Graph hello i przetestować lokalnie, bez tworzenia subskrypcji platformy Azure lub ponoszenia kosztów. Po zakończeniu jak aplikacja działa na platformie hello emulatora, możesz przełączyć toousing konto bazy danych Azure rozwiązania Cosmos w chmurze hello.

## <a name="scenarios-for-graph-support-of-azure-cosmos-db"></a>Scenariusze obsługi wykres Azure DB rozwiązania Cosmos
Poniżej przedstawiono kilka scenariuszy, w której wykres obsługę bazy danych Azure rozwiązania Cosmos może służyć:

* Sieci społecznościowych

 Łącząc dane dotyczące klientów i ich interakcji z innymi osobami, można utworzyć spersonalizowanego doświadczenia, przewidzieć zachowania klienta lub uzyskuj osobom podobne zainteresowań osoby. Azure DB rozwiązania Cosmos można toomanage używanych sieci społecznościowych i śledzą preferencje klienta i danych.

* Aparaty zalecenia

 Ten scenariusz jest często stosowany w branży sprzedaży detalicznej hello. Łącząc informacji o produktach, użytkownikach i interakcji użytkownika, takich jak zakupu, przeglądanie lub klasyfikacji elementu, można tworzyć niestandardowe zalecenia. Witaj, małe opóźnienia, elastyczne skalowanie i native wykres obsługę bazy danych Azure rozwiązania Cosmos jest idealny dla modelowania tych interakcji.

* Dane geoprzestrzenne

 Wiele aplikacji w telekomunikacyjnych logistyki i planowania podróży konieczne toofind lokalizacji zainteresowania wewnątrz obszaru lub zlokalizować hello najkrótszy/optymalnej trasy między dwiema lokalizacjami. Azure DB rozwiązania Cosmos jest naturalna nadające się do tych problemów.

* Internet rzeczy

 Hello sieci i połączeń między urządzeniami IoT formę wykres możesz skompilować lepszego zrozumienia hello stanu urządzeń i zasobów i Dowiedz się, jak zmiany w jednej części sieci hello mogą wpłynąć na innej części.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat obsługi graph w usłudze Azure DB rozwiązania Cosmos, zobacz:

* Rozpoczynanie pracy z hello [samouczek wykres bazy danych Azure rozwiązania Cosmos](create-graph-dotnet.md).
* Dowiedz się więcej o zbyt[zapytania wykresy w usłudze Azure DB rozwiązania Cosmos przy użyciu Gremlin](gremlin-support.md).
