---
title: "Obsługa rozwiązania Cosmos DB Gremlin aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello języka Gremlin z TinkerPop Apache, funkcji i kroków i dostępne w usłudze Azure DB rozwiązania Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 6016ccba-0fb9-4218-892e-8f32a1bcc590
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/10/2017
ms.author: denlee
ms.openlocfilehash: f8c2ce50c6946e971f56fe1f3838b0899cb2ad8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-gremlin-graph-support"></a>Pomoc techniczna platformy Azure wykres Gremlin DB rozwiązania Cosmos
Obsługuje bazę danych systemu Azure rozwiązania Cosmos [Apache Tinkerpop](http://tinkerpop.apache.org) wykresu języka przechodzenie [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), która jest interfejs API programu Graph do tworzenia jednostek wykres i wykonywanie operacji zapytania wykresu. Można użyć hello Gremlin języka toocreate wykres jednostek (wierzchołki i krawędzi), modyfikowanie właściwości w ramach tych jednostek, wykonywanie kwerend i traversals i usuwanie jednostek. 

Azure DB rozwiązania Cosmos oferuje funkcje gotowe enterprise toograph baz danych. W tym globalnych dystrybucji, niezależne skalowanie magazynu i przepływności, opóźnienia przewidywalną milisekund jednocyfrowej automatycznego indeksowania i umów SLA 99,99%. Ponieważ bazy danych rozwiązania Cosmos Azure obsługuje TinkerPop/Gremlin, możesz łatwo przeprowadzić migrację aplikacji napisanych przy użyciu innej wykres bazy danych bez konieczności zmiany kodu toomake. Ponadto z obsługi Gremlin bazy danych rozwiązania Cosmos Azure bezproblemowo integruje się z włączony TinkerPop analytics platform takich jak [Apache Spark GraphX](http://spark.apache.org/graphx/). 

W tym artykule firma Microsoft stanowią Przewodnik Szybki Gremlin i wyliczania hello Gremlin funkcji i kroków, które są obsługiwane w wersji zapoznawczej hello obsługi interfejsu API programu Graph.

## <a name="gremlin-by-example"></a>Gremlin przykładzie
Użyjmy próbki toounderstand wykres, jak zapytania może zostać wyrażona w Gremlin. Witaj poniższej ilustracji przedstawiono aplikacja biznesowa, która zarządza dane o użytkownikach, udziałów i urządzeń w formie hello wykres.  

![Przykładowa baza danych przedstawiający osób, urządzeń i udziałów](./media/gremlin-support/sample-graph.png) 

Ten wykres ma hello następujące typy wierzchołków (po o nazwie "etykieta" w Gremlin):

- Osoby: hello wykres ma trzy osób, działanie okrężne blogu Thomasa i Ben
- Zainteresowań: ich zainteresowaniami, w tym przykładzie hello gry Football
- Urządzeń: hello urządzenia osób
- Systemy operacyjne: hello systemy operacyjne urządzeń hello na

Firma Microsoft reprezentują hello relacje między tych jednostek za pośrednictwem hello następujące typy/etykiety:

- Zna: na przykład "blogu Thomasa zna działania okrężnego"
- Planuje: zainteresowań hello toorepresent hello osób w naszym wykresu, na przykład "Ben jest zainteresowana Football"
- RunsOS: Uruchamia komputera przenośnego systemu operacyjnego Windows hello
- Używa: urządzenia, które osoba używa toorepresent. Na przykład działanie okrężne używa telefonu firmie o numerze seryjnym 77

Umożliwia uruchamianie niektórych operacji względem tego wykresu przy użyciu hello [konsoli Gremlin](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console). Można również wykonywać te operacje, sterowniki Gremlin platformy hello wybranych przez użytkownika (Java, Node.js, Python lub .NET).  Zanim przyjrzymy co to jest obsługiwana w usłudze Azure DB rozwiązania Cosmos Oto kilka przykładów tooget zapoznać się ze składnią hello.

Pierwszy Przyjrzyjmy się CRUD. Hello następująca instrukcja Gremlin wstawia hello "Blogu Thomasa" wierzchołków do wykresu hello:

```
:> g.addV('person').property('id', 'thomas.1').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44)
```

Następnie po instrukcji Gremlin hello wstawia krawędź "wie", między blogu Thomasa i działania okrężnego.

```
:> g.V('thomas.1').addE('knows').to(g.V('robin.1'))
```

Witaj następujące zapytanie zwraca wierzchołków "osoba" hello malejąco według ich imiona:
```
:> g.V().hasLabel('person').order().by('firstName', decr)
```

W przypadku wykresów świecisz gdy będziesz potrzebować tooanswer pytania "systemy operacyjne, które korzystają znajomych blogu Thomasa?". Możesz uruchomić to proste tooget przechodzenie Gremlin te informacje z wykresu hello:

```
:> g.V('thomas.1').out('knows').out('uses').out('runsos').group().by('name').by(count())
```
Teraz Przyjrzyjmy się bazy danych rozwiązania Cosmos Azure udostępnia deweloperom Gremlin.

## <a name="gremlin-features"></a>Funkcje gremlin
TinkerPop jest standard, który obejmuje wiele różnych technologii wykresu. W związku z tym ma toodescribe terminologii jakie funkcje są udostępniane przez dostawcę wykresu. Azure DB rozwiązania Cosmos zapewnia współbieżność trwałe, wysoka, bazy danych wykresu zapisywalny, która może zostać podzielony na partycje w wielu serwerów lub klastrów. 

Witaj poniższej tabeli wymieniono funkcje TinkerPop hello, które są implementowane przez bazy danych Azure rozwiązania Cosmos: 

| Kategoria | Implementacja rozwiązania Cosmos bazy danych Azure |  Uwagi | 
| --- | --- | --- |
| Funkcje wykresu | Zapewnia trwałość i ConcurrentAccess w wersji zapoznawczej. Zaprojektowany toosupport transakcji | Złącze Spark hello można zaimplementować metody komputera. |
| Funkcje zmiennych | Obsługuje wartość logiczną, liczbą całkowitą, Byte, kliknij dwukrotnie, Float, Integer, Long, ciąg | Obsługuje typy pierwotne, jest niezgodny z typami złożonymi za pośrednictwem modelu danych |
| Funkcje wierzchołków | Obsługuje RemoveVertices, MetaProperties, AddVertices, MultiProperties, StringIds, UserSuppliedIds, AddProperty, RemoveProperty  | Obsługuje tworzenie, modyfikowanie i usuwanie wierzchołków |
| Funkcje właściwości wierzchołków | StringIds, UserSuppliedIds, AddProperty, RemoveProperty, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Obsługuje tworzenie, modyfikowanie i usuwanie właściwości wierzchołków |
| Funkcje krawędzi | AddEges, RemoveEdges, StringIds, UserSuppliedIds, AddProperty, RemoveProperty | Obsługuje tworzenie, modyfikowanie i usuwanie krawędzi. |
| Funkcje właściwości Edge | Właściwości, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Obsługuje tworzenie, modyfikowanie i usuwanie właściwości edge |

## <a name="gremlin-wire-format-graphson"></a>Format przesyłania gremlin: GraphSON

Azure DB rozwiązania Cosmos używa hello [GraphSON format](https://github.com/thinkaurelius/faunus/wiki/GraphSON-Format) podczas zwracania wyników z Gremlin operacji. GraphSON jest hello Gremlin standardowy format wierzchołków, krawędzi oraz właściwości (jedno- i wielowartościowych właściwości), za pomocą formatu JSON. 

Na przykład hello poniższy fragment kodu przedstawia GraphSON reprezentację wierzchołek *zwrócił klienta toohello* z bazy danych usługi Azure rozwiązania Cosmos. 

```json
  {
    "id": "a7111ba7-0ea1-43c9-b6b2-efc5e3aea4c0",
    "label": "person",
    "type": "vertex",
    "outE": {
      "knows": [
        {
          "id": "3ee53a60-c561-4c5e-9a9f-9c7924bc9aef",
          "inV": "04779300-1c8e-489d-9493-50fd1325a658"
        },
        {
          "id": "21984248-ee9e-43a8-a7f6-30642bc14609",
          "inV": "a8e3e741-2ef7-4c01-b7c8-199f8e43e3bc"
        }
      ]
    },
    "properties": {
      "firstName": [
        {
          "value": "Thomas"
        }
      ],
      "lastName": [
        {
          "value": "Andersen"
        }
      ],
      "age": [
        {
          "value": 45
        }
      ]
    }
  }
```

używane przez GraphSON dla wierzchołków właściwości Hello są następujące hello:

| Właściwość | Opis |
| --- | --- |
| id | Identyfikator Hello hello wierzchołka. Muszą być unikatowe (w połączeniu z wartością hello _partition, jeśli ma to zastosowanie) |
| Etykiety | Etykieta Hello hello wierzchołka. To jest typem jednostki hello toodescribe opcjonalne i używane. |
| type | Wierzchołki toodistinguish używane z innych niż wykres — dokumenty |
| properties | Zbiór właściwości zdefiniowane przez użytkownika skojarzonych z hello wierzchołka. Każda właściwość może mieć wielu wartości. |
| _partition (można konfigurować) | Klucz partycji Hello hello wierzchołka. Może być używane tooscale się wykresy toomultiple serwerów |
| outE | Zawiera listę limit krawędzi wierzchołka. Przechowuje informacje sąsiedztwa hello z wierzchołków umożliwia szybkie wykonywanie traversals. Krawędzi są pogrupowane w oparciu o ich etykiety. |

I krawędzi hello zawiera powitania po toohelp informacji z częściami tooother nawigacji hello wykresu.

| Właściwość | Opis |
| --- | --- |
| id | Identyfikator Hello hello Edge. Muszą być unikatowe (w połączeniu z wartością hello _partition, jeśli ma to zastosowanie) |
| Etykiety | Etykieta Hello hello krawędzi. Ta właściwość jest typu relacji hello toodescribe opcjonalne i używane. |
| inV | Zawiera listę w wierzchołków Edge. Przechowuje informacje sąsiedztwa hello krawędzi hello umożliwia szybkie wykonywanie traversals. Wierzchołków są pogrupowane w oparciu o ich etykiety. |
| properties | Zbiór właściwości zdefiniowane przez użytkownika skojarzonych z hello krawędzi. Każda właściwość może mieć wielu wartości. |

Każda właściwość może przechowywać wiele wartości w tablicy. 

| Właściwość | Opis |
| --- | --- |
| wartość | wartość Hello hello właściwości

## <a name="gremlin-partitioning"></a>Partycjonowanie gremlin

W usłudze Azure DB rozwiązania Cosmos, wykresy są przechowywane w kontenerach, które mogą być skalowane niezależnie pod względem pamięci masowej i przepływność (wyrażony w znormalizowanej żądań na sekundę). Każdego kontenera należy określić opcjonalne, ale zalecane właściwości klucza partycji, określająca granicę partycji logicznej powiązanych danych. Każdy wierzchołek/krawędź musi mieć `id` właściwość, która jest unikatowa dla jednostek w ramach wartość klucza partycji. Witaj szczegółowe informacje znajdują się w [partycjonowania w usłudze Azure DB rozwiązania Cosmos](partition-data.md).

Operacje gremlin bezproblemowo działa między dane wykresu, obejmujących wiele partycji w usłudze Azure DB rozwiązania Cosmos. Jest jednak zalecane toochoose klucza partycji dla wykresów jest często używane jako filtru w zapytaniach, ma wiele unikatowych wartości i podobne częstotliwość dostępu do tych wartości. 

## <a name="gremlin-steps"></a>Kroki gremlin
Teraz Przyjrzyjmy się hello kroki Gremlin obsługiwane przez bazy danych Azure rozwiązania Cosmos. Aby uzyskać pełną dokumentację Gremlin, zobacz [odwołania TinkerPop](http://tinkerpop.apache.org/docs/current/reference).

| Krok | Opis | Dokumentacja TinkerPop 3.2 | Uwagi |
| --- | --- | --- | --- |
| `addE` | Dodaje krawędź między dwoma wierzchołków | [krok addE](http://tinkerpop.apache.org/docs/current/reference/#addedge-step) | |
| `addV` | Dodaje wykres toohello wierzchołków | [krok addV](http://tinkerpop.apache.org/docs/current/reference/#addvertex-step) | |
| `and` | Ensurest, że wszystkie traversals hello zwracają wartość | [i kroku](http://tinkerpop.apache.org/docs/current/reference/#and-step) | |
| `as` | Krok modulator tooassign wyjście zmiennej toohello kroku | [krok](http://tinkerpop.apache.org/docs/current/reference/#as-step) | |
| `by` | Używane z modulator krok `group` i`order` | [krok](http://tinkerpop.apache.org/docs/current/reference/#by-step) | |
| `coalesce` | Zwraca hello pierwszego przechodzenia zwracającą wynik | [połączenie kroku](http://tinkerpop.apache.org/docs/current/reference/#coalesce-step) | |
| `constant` | Zwraca wartość stałą. Używane z`coalesce`| [krok stałej](http://tinkerpop.apache.org/docs/current/reference/#constant-step) | |
| `count` | Zwraca liczbę hello z przechodzenie hello | [Liczba kroku](http://tinkerpop.apache.org/docs/current/reference/#count-step) | |
| `dedup` | Zwraca hello wartości usunięciu duplikatów hello | [krok deduplikacji](http://tinkerpop.apache.org/docs/current/reference/#dedup-step) | |
| `drop` | Porzucania hello wartości (wierzchołków/krawędź) | [Upuść krok](http://tinkerpop.apache.org/docs/current/reference/#drop-step) | |
| `fold` | Działa jako barierę oblicza agregacji hello wyników| [fold kroku](http://tinkerpop.apache.org/docs/current/reference/#fold-step) | |
| `group` | Grupy hello na podstawie etykiet hello określonej wartości| [krok grupa](http://tinkerpop.apache.org/docs/current/reference/#group-step) | |
| `has` | Użyć właściwości toofilter, wierzchołki i krawędzi. Obsługuje `hasLabel`, `hasId`, `hasNot`, i `has` wariantów. | [ma kroku](http://tinkerpop.apache.org/docs/current/reference/#has-step) | |
| `inject` | Wstaw wartości do strumienia| [Wstaw kroku](http://tinkerpop.apache.org/docs/current/reference/#inject-step) | |
| `is` | Używane tooperform filtru za pomocą wyrażenia logicznego | [jest kroku](http://tinkerpop.apache.org/docs/current/reference/#is-step) | |
| `limit` | Używane toolimit liczba elementów w przechodzenie hello| [krok limit](http://tinkerpop.apache.org/docs/current/reference/#limit-step) | |
| `local` | Lokalny opakowuje sekcję podzapytania przechodzenie, podobne tooa | [krok lokalnego](http://tinkerpop.apache.org/docs/current/reference/#local-step) | |
| `not` | Używane negacji hello tooproduce filtru | [nie kroku](http://tinkerpop.apache.org/docs/current/reference/#not-step) | |
| `optional` | Zwraca hello wynik hello określony przechodzenie, jeśli jego daje wynik else zwraca hello elementu wywołującego | [krok opcjonalny](http://tinkerpop.apache.org/docs/current/reference/#optional-step) | |
| `or` | Gwarantuje, że co najmniej jeden z hello traversals zwraca wartość | [lub krok](http://tinkerpop.apache.org/docs/current/reference/#or-step) | |
| `order` | Zwraca wyniki w hello określona kolejność sortowania | [krok kolejności](http://tinkerpop.apache.org/docs/current/reference/#order-step) | |
| `path` | Zwraca hello pełną ścieżkę przechodzenie hello | [krok ścieżki](http://tinkerpop.apache.org/docs/current/reference/#path-step) | |
| `project` | Mapy właściwości hello projektów | [krok projektu](http://tinkerpop.apache.org/docs/current/reference/#project-step) | |
| `properties` | Zwraca właściwości hello hello określonej etykiety | [krok właściwości](http://tinkerpop.apache.org/docs/current/reference/#properties-step) | |
| `range` | Filtry toohello określony zakres wartości| [krok zakresu](http://tinkerpop.apache.org/docs/current/reference/#range-step) | |
| `repeat` | Krok hello powtarza hello określona liczba razy. Używany do pętli | [Powtórz krok](http://tinkerpop.apache.org/docs/current/reference/#repeat-step) | |
| `sample` | Używane toosample wyników z przechodzenie hello | [krok próbki](http://tinkerpop.apache.org/docs/current/reference/#sample-step) | |
| `select` | Używane tooproject wyników z przechodzenie hello |  [Zaznacz krok](http://tinkerpop.apache.org/docs/current/reference/#select-step) | |
| `store` | Używane dla nieblokujące wartości zagregowanych z przechodzenie hello | [krok magazynu](http://tinkerpop.apache.org/docs/current/reference/#store-step) | |
| `tree` | Łączny ścieżek wierzchołków w drzewie | [krok drzewa](http://tinkerpop.apache.org/docs/current/reference/#tree-step) | |
| `unfold` | Skorzystaj z odwijania krokiem iteratora| [unfold — krok](http://tinkerpop.apache.org/docs/current/reference/#unfold-step) | |
| `union` | Wyniki z wielu traversals scalania| [krok Unii](http://tinkerpop.apache.org/docs/current/reference/#union-step) | |
| `V` | Obejmuje hello kroki niezbędne do traversals między wierzchołki i krawędzi `V`, `E`, `out`, `in`, `both`, `outE`, `inE`, `bothE`, `outV`, `inV`, `bothV`, i `otherV` dla | [kroki wierzchołków](http://tinkerpop.apache.org/docs/current/reference/#vertex-steps) | |
| `where` | Używane toofilter wyników z przechodzenie hello. Obsługuje `eq`, `neq`, `lt`, `lte`, `gt`, `gte`, i `between` operatorów  | [gdy krok](http://tinkerpop.apache.org/docs/current/reference/#where-step) | |

Aparat zoptymalizowanych pod kątem zapisu Azure DB rozwiązania Cosmos obsługuje automatycznego indeksowania wszystkie właściwości w wierzchołki i krawędzi domyślnie. W związku z tym zapytania z filtrami, zakres kwerendy, sortowanie, lub agregacji w dowolnej właściwości są przetwarzane z indeksu hello i skutecznie obsługiwane. Aby uzyskać więcej informacji na działa jak indeksowania w usłudze Azure DB rozwiązania Cosmos, zobacz nasze dokument na [indeksowania niezależny od schematu](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf).

## <a name="next-steps"></a>Następne kroki
* Rozpocząć tworzenie aplikacji wykres [przy użyciu nasze zestawy SDK](create-graph-dotnet.md) 
* Dowiedz się więcej o [Obsługa wykres DB rozwiązania Cosmos Azure](graph-introduction.md)
