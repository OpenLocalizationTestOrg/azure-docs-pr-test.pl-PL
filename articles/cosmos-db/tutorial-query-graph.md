---
title: "dane wykresu tooquery aaaHow w usłudze Azure DB rozwiązania Cosmos? | Microsoft Docs"
description: "Dowiedz się, dane wykresu tooquery w usłudze Azure DB rozwiązania Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a>Azure DB rozwiązania Cosmos: Jak tooquery z hello interfejsu API programu Graph (wersja zapoznawcza)?

Hello Azure DB rozwiązania Cosmos [interfejsu API programu Graph](graph-introduction.md) (wersja zapoznawcza) obsługuje [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) zapytania. Ten artykuł zawiera przykładowe dokumenty i zapytanie tooget, który został uruchomiony. Szczegółowe odwołanie Gremlin znajduje się w hello [Obsługa Gremlin](gremlin-support.md) artykułu.

W tym artykule omówiono hello następujące zadania: 

> [!div class="checklist"]
> * Wykonywanie zapytania na danych z Gremlin

## <a name="prerequisites"></a>Wymagania wstępne

Dla tych toowork zapytania musi mieć konto bazy danych Azure rozwiązania Cosmos i danych wykresu w kontenerze hello. Nie masz żadnego z tych? Zakończenie hello [szybkiego startu 5-minutowy](create-graph-dotnet.md) lub hello [samouczek developer](tutorial-query-graph.md) toocreate konta i wypełnić bazę danych. Można uruchomić następującego zapytania, używając hello hello [Azure rozwiązania Cosmos DB .NET wykresu biblioteki](graph-sdk-dotnet.md), [konsoli Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), lub sterownika Gremlin ulubionych.

## <a name="count-vertices-in-hello-graph"></a>Liczba wierzchołków hello wykresu

powitania po fragment kodu przedstawia, jak toocount hello liczbę wierzchołków w grafie hello:

```
g.V().count()
```

## <a name="filters"></a>Filtry

Można wykonywać przy użyciu jego Gremlin filtry `has` i `hasLabel` kroki i połączenie ich za pomocą `and`, `or`, i `not` toobuild bardziej złożone filtry. Azure DB rozwiązania Cosmos zapewnia niezależny od schematu indeksowania wszystkich właściwości w danej wierzchołki i stopni szybkiego zapytań:

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>Projekcji

Niektóre właściwości hello wyników zapytania za pomocą hello można projektu `values` krok:

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>Znajdź krawędzi pokrewne i wierzchołków

Firma Microsoft do tej pory tylko przedstawiono operatorów zapytań, które działają w dowolnej bazy danych. Wykresy są szybkie i wydajne dla operacji przechodzenia, gdy potrzebujesz toonavigate toorelated krawędzi oraz wierzchołków. Spróbujmy wszystkich znajomych blogu Thomasa. Firma Microsoft to zrobić przy użyciu jego Gremlin `outE` krok toofind wszystkie hello wyjściowego krawędzi z blogu Thomasa, a następnie przechodzenie toohello w wierzchołki z tych krawędzi przy użyciu jego Gremlin `inV` krok:

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

Zapytanie dalej Hello wykonuje dwie toofind przeskoków wszystkich blogu Thomasa "znajomych przyjaciół", wywołując `outE` i `inV` dwa razy. 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

Można tworzyć bardziej złożone kwerendy i wdrożyć logikę przechodzenie zaawansowanych wykresu przy użyciu Gremlin, takie jak filtr mieszania hello wyrażenia wykonywania pętli przy użyciu `loop` krok i implementujący nawigacji warunkowego przy użyciu hello `choose` kroku. Dowiedz się więcej o co można zrobić z [Obsługa Gremlin](gremlin-support.md)!

## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu hello następujące czynności:

> [!div class="checklist"]
> * Przedstawiono sposób tooquery przy użyciu wykresu 

Można teraz kontynuować toohello następny samouczek toolearn jak toodistribute danych globalnie.

> [!div class="nextstepaction"]
> [Globalny dystrybucji danych](tutorial-global-distribution-documentdb.md)