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
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a><span data-ttu-id="16fdb-104">Azure DB rozwiązania Cosmos: Jak tooquery z hello interfejsu API programu Graph (wersja zapoznawcza)?</span><span class="sxs-lookup"><span data-stu-id="16fdb-104">Azure Cosmos DB: How tooquery with hello Graph API (preview)?</span></span>

<span data-ttu-id="16fdb-105">Hello Azure DB rozwiązania Cosmos [interfejsu API programu Graph](graph-introduction.md) (wersja zapoznawcza) obsługuje [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) zapytania.</span><span class="sxs-lookup"><span data-stu-id="16fdb-105">hello Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="16fdb-106">Ten artykuł zawiera przykładowe dokumenty i zapytanie tooget, który został uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="16fdb-106">This article provides sample documents and queries tooget you started.</span></span> <span data-ttu-id="16fdb-107">Szczegółowe odwołanie Gremlin znajduje się w hello [Obsługa Gremlin](gremlin-support.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="16fdb-107">A detailed Gremlin reference is provided in hello [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="16fdb-108">W tym artykule omówiono hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="16fdb-108">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="16fdb-109">Wykonywanie zapytania na danych z Gremlin</span><span class="sxs-lookup"><span data-stu-id="16fdb-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16fdb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16fdb-110">Prerequisites</span></span>

<span data-ttu-id="16fdb-111">Dla tych toowork zapytania musi mieć konto bazy danych Azure rozwiązania Cosmos i danych wykresu w kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="16fdb-111">For these queries toowork, you must have an Azure Cosmos DB account and have graph data in hello container.</span></span> <span data-ttu-id="16fdb-112">Nie masz żadnego z tych?</span><span class="sxs-lookup"><span data-stu-id="16fdb-112">Don't have any of those?</span></span> <span data-ttu-id="16fdb-113">Zakończenie hello [szybkiego startu 5-minutowy](create-graph-dotnet.md) lub hello [samouczek developer](tutorial-query-graph.md) toocreate konta i wypełnić bazę danych.</span><span class="sxs-lookup"><span data-stu-id="16fdb-113">Complete hello [5-minute quickstart](create-graph-dotnet.md) or hello [developer tutorial](tutorial-query-graph.md) toocreate an account and populate your database.</span></span> <span data-ttu-id="16fdb-114">Można uruchomić następującego zapytania, używając hello hello [Azure rozwiązania Cosmos DB .NET wykresu biblioteki](graph-sdk-dotnet.md), [konsoli Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), lub sterownika Gremlin ulubionych.</span><span class="sxs-lookup"><span data-stu-id="16fdb-114">You can run hello following queries using hello [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-hello-graph"></a><span data-ttu-id="16fdb-115">Liczba wierzchołków hello wykresu</span><span class="sxs-lookup"><span data-stu-id="16fdb-115">Count vertices in hello graph</span></span>

<span data-ttu-id="16fdb-116">powitania po fragment kodu przedstawia, jak toocount hello liczbę wierzchołków w grafie hello:</span><span class="sxs-lookup"><span data-stu-id="16fdb-116">hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="16fdb-117">Filtry</span><span class="sxs-lookup"><span data-stu-id="16fdb-117">Filters</span></span>

<span data-ttu-id="16fdb-118">Można wykonywać przy użyciu jego Gremlin filtry `has` i `hasLabel` kroki i połączenie ich za pomocą `and`, `or`, i `not` toobuild bardziej złożone filtry.</span><span class="sxs-lookup"><span data-stu-id="16fdb-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters.</span></span> <span data-ttu-id="16fdb-119">Azure DB rozwiązania Cosmos zapewnia niezależny od schematu indeksowania wszystkich właściwości w danej wierzchołki i stopni szybkiego zapytań:</span><span class="sxs-lookup"><span data-stu-id="16fdb-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="16fdb-120">Projekcji</span><span class="sxs-lookup"><span data-stu-id="16fdb-120">Projection</span></span>

<span data-ttu-id="16fdb-121">Niektóre właściwości hello wyników zapytania za pomocą hello można projektu `values` krok:</span><span class="sxs-lookup"><span data-stu-id="16fdb-121">You can project certain properties in hello query results using hello `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="16fdb-122">Znajdź krawędzi pokrewne i wierzchołków</span><span class="sxs-lookup"><span data-stu-id="16fdb-122">Find related edges and vertices</span></span>

<span data-ttu-id="16fdb-123">Firma Microsoft do tej pory tylko przedstawiono operatorów zapytań, które działają w dowolnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="16fdb-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="16fdb-124">Wykresy są szybkie i wydajne dla operacji przechodzenia, gdy potrzebujesz toonavigate toorelated krawędzi oraz wierzchołków.</span><span class="sxs-lookup"><span data-stu-id="16fdb-124">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="16fdb-125">Spróbujmy wszystkich znajomych blogu Thomasa.</span><span class="sxs-lookup"><span data-stu-id="16fdb-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="16fdb-126">Firma Microsoft to zrobić przy użyciu jego Gremlin `outE` krok toofind wszystkie hello wyjściowego krawędzi z blogu Thomasa, a następnie przechodzenie toohello w wierzchołki z tych krawędzi przy użyciu jego Gremlin `inV` krok:</span><span class="sxs-lookup"><span data-stu-id="16fdb-126">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="16fdb-127">Zapytanie dalej Hello wykonuje dwie toofind przeskoków wszystkich blogu Thomasa "znajomych przyjaciół", wywołując `outE` i `inV` dwa razy.</span><span class="sxs-lookup"><span data-stu-id="16fdb-127">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="16fdb-128">Można tworzyć bardziej złożone kwerendy i wdrożyć logikę przechodzenie zaawansowanych wykresu przy użyciu Gremlin, takie jak filtr mieszania hello wyrażenia wykonywania pętli przy użyciu `loop` krok i implementujący nawigacji warunkowego przy użyciu hello `choose` kroku.</span><span class="sxs-lookup"><span data-stu-id="16fdb-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="16fdb-129">Dowiedz się więcej o co można zrobić z [Obsługa Gremlin](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="16fdb-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="16fdb-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16fdb-130">Next steps</span></span>

<span data-ttu-id="16fdb-131">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="16fdb-131">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="16fdb-132">Przedstawiono sposób tooquery przy użyciu wykresu</span><span class="sxs-lookup"><span data-stu-id="16fdb-132">Learned how tooquery using Graph</span></span> 

<span data-ttu-id="16fdb-133">Można teraz kontynuować toohello następny samouczek toolearn jak toodistribute danych globalnie.</span><span class="sxs-lookup"><span data-stu-id="16fdb-133">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="16fdb-134">Globalny dystrybucji danych</span><span class="sxs-lookup"><span data-stu-id="16fdb-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)