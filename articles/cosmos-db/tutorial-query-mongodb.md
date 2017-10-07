---
title: "Azure DB rozwiązania Cosmos: Jak tooquery przy użyciu hello interfejsu API usługi DocumentDB? | Microsoft Docs"
description: "Dowiedz się tooquery z hello interfejsu API usługi DocumentDB dla bazy danych Azure rozwiązania Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: e3e5a49f7510942bcfb15330e5f86c5dd8b1e5d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a><span data-ttu-id="60eeb-104">Azure DB rozwiązania Cosmos: Jak tooquery z interfejsem API bazy danych mongodb?</span><span class="sxs-lookup"><span data-stu-id="60eeb-104">Azure Cosmos DB: How tooquery with API for MongoDB?</span></span>

<span data-ttu-id="60eeb-105">Hello Azure DB rozwiązania Cosmos [interfejsu API dla bazy danych MongoDB](mongodb-introduction.md) obsługuje [zapytania powłoki MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="60eeb-105">hello Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="60eeb-106">W tym artykule omówiono hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="60eeb-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="60eeb-107">Wykonywanie zapytania na danych z bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="60eeb-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="60eeb-108">Przykładowy dokument</span><span class="sxs-lookup"><span data-stu-id="60eeb-108">Sample document</span></span>

<span data-ttu-id="60eeb-109">Witaj zapytania w tym artykule Użyj powitania po przykładowy dokument.</span><span class="sxs-lookup"><span data-stu-id="60eeb-109">hello queries in this article use hello following sample document.</span></span>

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
## <span data-ttu-id="60eeb-110"><a id="examplequery1"></a>Przykładowe Zapytanie 1</span><span class="sxs-lookup"><span data-stu-id="60eeb-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="60eeb-111">Podana hello próbki rodziny dokumentu powyżej, hello następujące zapytanie zwraca hello dokumentów, jeśli pole identyfikatora hello odpowiada `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="60eeb-111">Given hello sample family document above, hello following query returns hello documents where hello id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="60eeb-112">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="60eeb-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="60eeb-113">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="60eeb-113">**Results**</span></span>

    {
    "_id": "ObjectId(\"58f65e1198f3a12c7090e68c\")",
    "id": "WakefieldFamily",
    "parents": [
      {
        "familyName": "Wakefield",
        "givenName": "Robin"
      },
      {
        "familyName": "Miller",
        "givenName": "Ben"
      }
    ],
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ],
    "address": {
      "state": "NY",
      "county": "Manhattan",
      "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
    }

## <span data-ttu-id="60eeb-114"><a id="examplequery2"></a>Przykładowe zapytanie 2</span><span class="sxs-lookup"><span data-stu-id="60eeb-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="60eeb-115">Witaj dalej zapytanie zwraca wszystkie elementy podrzędne hello hello rodziny.</span><span class="sxs-lookup"><span data-stu-id="60eeb-115">hello next query returns all hello children in hello family.</span></span> 

<span data-ttu-id="60eeb-116">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="60eeb-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="60eeb-117">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="60eeb-117">**Results**</span></span>

    {
    "_id": "ObjectId("58f65e1198f3a12c7090e68c")",
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ]
    }


## <span data-ttu-id="60eeb-118"><a id="examplequery3"></a>Przykładowe zapytanie 3</span><span class="sxs-lookup"><span data-stu-id="60eeb-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="60eeb-119">Witaj dalej zapytanie zwraca wszystkich rodzin hello, które zostały zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="60eeb-119">hello next query returns all hello families which are registered.</span></span> 

<span data-ttu-id="60eeb-120">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="60eeb-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="60eeb-121">**Wyniki** zostanie zwrócony żaden dokument.</span><span class="sxs-lookup"><span data-stu-id="60eeb-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="60eeb-122"><a id="examplequery4"></a>Przykładowe zapytanie 4</span><span class="sxs-lookup"><span data-stu-id="60eeb-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="60eeb-123">Witaj dalej zapytanie zwraca wszystkich rodzin hello, które nie zostały zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="60eeb-123">hello next query returns all hello families which are not registered.</span></span> 

<span data-ttu-id="60eeb-124">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="60eeb-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="60eeb-125">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="60eeb-125">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="60eeb-126">}</span><span class="sxs-lookup"><span data-stu-id="60eeb-126">}</span></span>

## <span data-ttu-id="60eeb-127"><a id="examplequery5"></a>Przykładowe zapytanie 5</span><span class="sxs-lookup"><span data-stu-id="60eeb-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="60eeb-128">Hello dalej zapytanie zwraca wszystkie rodzin hello, które nie są zarejestrowane i stan NY.</span><span class="sxs-lookup"><span data-stu-id="60eeb-128">hello next query returns all hello families which are not registered and state is NY.</span></span> 

<span data-ttu-id="60eeb-129">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="60eeb-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="60eeb-130">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="60eeb-130">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="60eeb-131">}</span><span class="sxs-lookup"><span data-stu-id="60eeb-131">}</span></span>


## <span data-ttu-id="60eeb-132"><a id="examplequery6"></a>Przykładowe zapytanie 6</span><span class="sxs-lookup"><span data-stu-id="60eeb-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="60eeb-133">Hello dalej zapytanie zwraca wszystkich rodzin hello, w których 8 klas podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="60eeb-133">hello next query returns all hello families where children grades are 8.</span></span>

<span data-ttu-id="60eeb-134">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="60eeb-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="60eeb-135">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="60eeb-135">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="60eeb-136">}</span><span class="sxs-lookup"><span data-stu-id="60eeb-136">}</span></span>

## <span data-ttu-id="60eeb-137"><a id="examplequery7"></a>Przykładowe zapytanie 7</span><span class="sxs-lookup"><span data-stu-id="60eeb-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="60eeb-138">Hello dalej zapytanie zwraca wszystkich rodzin hello, w których rozmiar tablicy elementów podrzędnych jest 3.</span><span class="sxs-lookup"><span data-stu-id="60eeb-138">hello next query returns all hello families where size of children array is 3.</span></span>

<span data-ttu-id="60eeb-139">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="60eeb-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="60eeb-140">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="60eeb-140">**Results**</span></span>

<span data-ttu-id="60eeb-141">Nie będzie można zwrócić wyników, ponieważ nie ma więcej niż 2 elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="60eeb-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="60eeb-142">Tylko wtedy, gdy parametr 2 to zapytanie powiodło się i zwróć hello pełnego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="60eeb-142">Only when parameter is 2 this query will succeed and return hello full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60eeb-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="60eeb-143">Next steps</span></span>

<span data-ttu-id="60eeb-144">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="60eeb-144">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="60eeb-145">Przedstawiono sposób tooquery przy użyciu bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="60eeb-145">Learned how tooquery using MongoDB</span></span> 

<span data-ttu-id="60eeb-146">Można teraz kontynuować toohello następny samouczek toolearn jak toodistribute danych globalnie.</span><span class="sxs-lookup"><span data-stu-id="60eeb-146">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="60eeb-147">Globalny dystrybucji danych</span><span class="sxs-lookup"><span data-stu-id="60eeb-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

