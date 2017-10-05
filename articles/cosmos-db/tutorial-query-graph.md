---
title: "Jak wykonać zapytanie dotyczące danych wykresu w usłudze Azure DB rozwiązania Cosmos? | Microsoft Docs"
description: "Dowiedz się, jak dane wykresu zapytania w usłudze Azure DB rozwiązania Cosmos"
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
ms.openlocfilehash: 81713c72da037f127e81239d214d7a877247dca1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-how-to-query-with-the-graph-api-preview"></a><span data-ttu-id="36cd8-104">Azure DB rozwiązania Cosmos: Jak wykonać zapytanie z interfejsu API programu Graph (wersja zapoznawcza)?</span><span class="sxs-lookup"><span data-stu-id="36cd8-104">Azure Cosmos DB: How to query with the Graph API (preview)?</span></span>

<span data-ttu-id="36cd8-105">Azure DB rozwiązania Cosmos [interfejsu API programu Graph](graph-introduction.md) (wersja zapoznawcza) obsługuje [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) zapytania.</span><span class="sxs-lookup"><span data-stu-id="36cd8-105">The Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="36cd8-106">W tym artykule przedstawiono przykładowe dokumentach i zapytaniach ułatwiających rozpoczęcie pracy.</span><span class="sxs-lookup"><span data-stu-id="36cd8-106">This article provides sample documents and queries to get you started.</span></span> <span data-ttu-id="36cd8-107">A szczegółowe Gremlin odwołanie znajduje się w [Obsługa Gremlin](gremlin-support.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="36cd8-107">A detailed Gremlin reference is provided in the [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="36cd8-108">W tym artykule opisano następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="36cd8-108">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="36cd8-109">Wykonywanie zapytania na danych z Gremlin</span><span class="sxs-lookup"><span data-stu-id="36cd8-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36cd8-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="36cd8-110">Prerequisites</span></span>

<span data-ttu-id="36cd8-111">Dla tych zapytań do pracy musi mieć konto bazy danych Azure rozwiązania Cosmos i danych wykresu w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="36cd8-111">For these queries to work, you must have an Azure Cosmos DB account and have graph data in the container.</span></span> <span data-ttu-id="36cd8-112">Nie masz żadnego z tych?</span><span class="sxs-lookup"><span data-stu-id="36cd8-112">Don't have any of those?</span></span> <span data-ttu-id="36cd8-113">Zakończenie [szybkiego startu 5-minutowy](create-graph-dotnet.md) lub [samouczek developer](tutorial-query-graph.md) Tworzenie konta usługi i umieścić w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="36cd8-113">Complete the [5-minute quickstart](create-graph-dotnet.md) or the [developer tutorial](tutorial-query-graph.md) to create an account and populate your database.</span></span> <span data-ttu-id="36cd8-114">Można uruchomić następujące kwerendy przy użyciu [Azure rozwiązania Cosmos DB .NET wykresu biblioteki](graph-sdk-dotnet.md), [konsoli Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), lub sterownika Gremlin ulubionych.</span><span class="sxs-lookup"><span data-stu-id="36cd8-114">You can run the following queries using the [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-the-graph"></a><span data-ttu-id="36cd8-115">Liczba wierzchołki na wykresie</span><span class="sxs-lookup"><span data-stu-id="36cd8-115">Count vertices in the graph</span></span>

<span data-ttu-id="36cd8-116">Poniższy fragment kodu przedstawia sposób liczbę wierzchołki na wykresie:</span><span class="sxs-lookup"><span data-stu-id="36cd8-116">The following snippet shows how to count the number of vertices in the graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="36cd8-117">Filtry</span><span class="sxs-lookup"><span data-stu-id="36cd8-117">Filters</span></span>

<span data-ttu-id="36cd8-118">Można wykonywać przy użyciu jego Gremlin filtry `has` i `hasLabel` kroki i połączenie ich za pomocą `and`, `or`, i `not` do tworzenia bardziej złożonych filtrów.</span><span class="sxs-lookup"><span data-stu-id="36cd8-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters.</span></span> <span data-ttu-id="36cd8-119">Azure DB rozwiązania Cosmos zapewnia niezależny od schematu indeksowania wszystkich właściwości w danej wierzchołki i stopni szybkiego zapytań:</span><span class="sxs-lookup"><span data-stu-id="36cd8-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="36cd8-120">Projekcji</span><span class="sxs-lookup"><span data-stu-id="36cd8-120">Projection</span></span>

<span data-ttu-id="36cd8-121">Niektóre właściwości wyników zapytania za pomocą można projektu `values` krok:</span><span class="sxs-lookup"><span data-stu-id="36cd8-121">You can project certain properties in the query results using the `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="36cd8-122">Znajdź krawędzi pokrewne i wierzchołków</span><span class="sxs-lookup"><span data-stu-id="36cd8-122">Find related edges and vertices</span></span>

<span data-ttu-id="36cd8-123">Firma Microsoft do tej pory tylko przedstawiono operatorów zapytań, które działają w dowolnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="36cd8-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="36cd8-124">Wykresy są szybkie i wydajne dla operacji przechodzenia, gdy musisz przejść do krawędzi pokrewne i wierzchołków.</span><span class="sxs-lookup"><span data-stu-id="36cd8-124">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="36cd8-125">Spróbujmy wszystkich znajomych blogu Thomasa.</span><span class="sxs-lookup"><span data-stu-id="36cd8-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="36cd8-126">Firma Microsoft to zrobić przy użyciu jego Gremlin `outE` krok, aby znaleźć wszystkie wyjściowego krawędzi blogu Thomasa, a następnie przechodzenie do wierzchołków w z tych krawędzi przy użyciu jego Gremlin `inV` krok:</span><span class="sxs-lookup"><span data-stu-id="36cd8-126">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="36cd8-127">Zapytanie dalej wykonuje dwie przeskoków w celu znalezienia wszystkich blogu Thomasa "znajomych przyjaciół", wywołując `outE` i `inV` dwa razy.</span><span class="sxs-lookup"><span data-stu-id="36cd8-127">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="36cd8-128">Można tworzyć bardziej złożone kwerendy i wdrożyć logikę przechodzenie zaawansowanych wykresu przy użyciu Gremlin, tym wyrażeniach filtru mieszanie wykonywania pętli przy użyciu `loop` krok i wykonawcze przy użyciu warunkowego nawigacji `choose` kroku.</span><span class="sxs-lookup"><span data-stu-id="36cd8-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="36cd8-129">Dowiedz się więcej o co można zrobić z [Obsługa Gremlin](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="36cd8-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="36cd8-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36cd8-130">Next steps</span></span>

<span data-ttu-id="36cd8-131">W tym samouczku wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="36cd8-131">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="36cd8-132">Przedstawiono sposób zapytań przy użyciu wykresu</span><span class="sxs-lookup"><span data-stu-id="36cd8-132">Learned how to query using Graph</span></span> 

<span data-ttu-id="36cd8-133">Możesz teraz przejść do następnym samouczku informacje na temat dystrybucji danych globalnie.</span><span class="sxs-lookup"><span data-stu-id="36cd8-133">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="36cd8-134">Globalny dystrybucji danych</span><span class="sxs-lookup"><span data-stu-id="36cd8-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)