---
title: "tooquery aaaHow z SQL w usłudze Azure DB rozwiązania Cosmos? | Microsoft Docs"
description: "Dowiedz się tooquery z usługi DocumentDB danych SQL w usłudze Azure DB rozwiązania Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a><span data-ttu-id="183fd-104">Azure DB rozwiązania Cosmos: Jak tooquery przy użyciu programu SQL?</span><span class="sxs-lookup"><span data-stu-id="183fd-104">Azure Cosmos DB: How tooquery using SQL?</span></span>

<span data-ttu-id="183fd-105">Hello Azure DB rozwiązania Cosmos [interfejsu API usługi DocumentDB](documentdb-introduction.md) obsługiwanych badania dokumentów za pomocą programu SQL.</span><span class="sxs-lookup"><span data-stu-id="183fd-105">hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="183fd-106">Ten artykuł zawiera przykładowy dokument i dwa przykładowe zapytania SQL oraz wyniki.</span><span class="sxs-lookup"><span data-stu-id="183fd-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="183fd-107">W tym artykule omówiono hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="183fd-107">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="183fd-108">Wykonywanie zapytania na danych z programu SQL</span><span class="sxs-lookup"><span data-stu-id="183fd-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="183fd-109">Przykładowy dokument</span><span class="sxs-lookup"><span data-stu-id="183fd-109">Sample document</span></span>

<span data-ttu-id="183fd-110">zapytania SQL Hello w tym artykule Użyj powitania po przykładowy dokument.</span><span class="sxs-lookup"><span data-stu-id="183fd-110">hello SQL queries in this article use hello following sample document.</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="183fd-111">Gdzie można uruchomić zapytania SQL</span><span class="sxs-lookup"><span data-stu-id="183fd-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="183fd-112">Można uruchomić zapytania, używając hello Eksploratora danych w portalu Azure za pośrednictwem hello hello [interfejsu API REST i zestawy SDK](documentdb-sdk-dotnet.md)i nawet hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo), która działa na podstawie istniejącego zestawu danych przykładowych zapytań.</span><span class="sxs-lookup"><span data-stu-id="183fd-112">You can run queries using hello Data Explorer in hello Azure portal, via hello [REST API and SDKs](documentdb-sdk-dotnet.md), and even hello [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="183fd-113">Aby uzyskać więcej informacji na temat kwerend SQL zobacz:</span><span class="sxs-lookup"><span data-stu-id="183fd-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="183fd-114">Zapytanie SQL i składni SQL</span><span class="sxs-lookup"><span data-stu-id="183fd-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="183fd-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="183fd-115">Prerequisites</span></span>

<span data-ttu-id="183fd-116">W tym samouczku założono, że masz konto bazy danych Azure rozwiązania Cosmos i kolekcji.</span><span class="sxs-lookup"><span data-stu-id="183fd-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="183fd-117">Nie masz żadnego z tych?</span><span class="sxs-lookup"><span data-stu-id="183fd-117">Don't have any of those?</span></span> <span data-ttu-id="183fd-118">Zakończenie hello [szybkiego startu 5-minutowy](create-mongodb-nodejs.md) lub hello [samouczek developer](tutorial-develop-mongodb.md) toocreate konto i kolekcji.</span><span class="sxs-lookup"><span data-stu-id="183fd-118">Complete hello [5-minute quickstart](create-mongodb-nodejs.md) or hello [developer tutorial](tutorial-develop-mongodb.md) toocreate an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="183fd-119">Przykładowe Zapytanie 1</span><span class="sxs-lookup"><span data-stu-id="183fd-119">Example query 1</span></span>

<span data-ttu-id="183fd-120">Podana hello próbki rodziny dokumentu powyżej, następujące zapytanie SQL zwraca hello dokumenty Jeśli pole identyfikatora hello odpowiada `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="183fd-120">Given hello sample family document above, following SQL query returns hello documents where hello id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="183fd-121">Ponieważ chodzi o `SELECT *` instrukcji, hello wyników kwerendy hello jest hello pełnego dokumentu JSON:</span><span class="sxs-lookup"><span data-stu-id="183fd-121">Since it's a `SELECT *` statement, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="183fd-122">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="183fd-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="183fd-123">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="183fd-123">**Results**</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

## <a name="example-query-2"></a><span data-ttu-id="183fd-124">Przykładowe zapytanie 2</span><span class="sxs-lookup"><span data-stu-id="183fd-124">Example query 2</span></span>

<span data-ttu-id="183fd-125">Hello dalej zapytanie zwraca podanymi nazwami hello dzieci w rodzinie hello odpowiada o identyfikatorze `WakefieldFamily` uporządkowanych według ich klasy.</span><span class="sxs-lookup"><span data-stu-id="183fd-125">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="183fd-126">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="183fd-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="183fd-127">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="183fd-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="183fd-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="183fd-128">Next steps</span></span>

<span data-ttu-id="183fd-129">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="183fd-129">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="183fd-130">Przedstawiono sposób tooquery przy użyciu programu SQL</span><span class="sxs-lookup"><span data-stu-id="183fd-130">Learned how tooquery using SQL</span></span>  

<span data-ttu-id="183fd-131">Można teraz kontynuować toohello następny samouczek toolearn jak toodistribute danych globalnie.</span><span class="sxs-lookup"><span data-stu-id="183fd-131">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="183fd-132">Globalny dystrybucji danych</span><span class="sxs-lookup"><span data-stu-id="183fd-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

