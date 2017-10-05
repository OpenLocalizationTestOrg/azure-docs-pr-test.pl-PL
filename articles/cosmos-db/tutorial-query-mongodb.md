---
title: "Azure DB rozwiązania Cosmos: Jak wykonać zapytanie, za pomocą interfejsu API usługi DocumentDB? | Microsoft Docs"
description: "Dowiedz się, jak zapytania przy użyciu interfejsu API usługi DocumentDB dla bazy danych Azure rozwiązania Cosmos"
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
ms.openlocfilehash: feffc553a9aa931d96cec71c101674fce08a466b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-with-api-for-mongodb"></a><span data-ttu-id="cc48e-104">Azure DB rozwiązania Cosmos: Jak zbadać za pomocą interfejsu API dla bazy danych MongoDB?</span><span class="sxs-lookup"><span data-stu-id="cc48e-104">Azure Cosmos DB: How to query with API for MongoDB?</span></span>

<span data-ttu-id="cc48e-105">Azure DB rozwiązania Cosmos [interfejsu API dla bazy danych MongoDB](mongodb-introduction.md) obsługuje [zapytania powłoki MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="cc48e-105">The Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="cc48e-106">W tym artykule opisano następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="cc48e-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="cc48e-107">Wykonywanie zapytania na danych z bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="cc48e-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="cc48e-108">Przykładowy dokument</span><span class="sxs-lookup"><span data-stu-id="cc48e-108">Sample document</span></span>

<span data-ttu-id="cc48e-109">Zapytania w tym artykule, użyj następujących przykładowy dokument.</span><span class="sxs-lookup"><span data-stu-id="cc48e-109">The queries in this article use the following sample document.</span></span>

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
## <span data-ttu-id="cc48e-110"><a id="examplequery1"></a>Przykładowe Zapytanie 1</span><span class="sxs-lookup"><span data-stu-id="cc48e-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="cc48e-111">Podana dokument rodziny próbki powyżej, następujące zapytanie zwraca dokumenty Jeśli w polu identyfikatora odpowiada `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="cc48e-111">Given the sample family document above, the following query returns the documents where the id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="cc48e-112">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="cc48e-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="cc48e-113">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="cc48e-113">**Results**</span></span>

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

## <span data-ttu-id="cc48e-114"><a id="examplequery2"></a>Przykładowe zapytanie 2</span><span class="sxs-lookup"><span data-stu-id="cc48e-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="cc48e-115">Dalej zapytanie zwraca wszystkie elementy podrzędne w rodzinie.</span><span class="sxs-lookup"><span data-stu-id="cc48e-115">The next query returns all the children in the family.</span></span> 

<span data-ttu-id="cc48e-116">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="cc48e-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="cc48e-117">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="cc48e-117">**Results**</span></span>

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


## <span data-ttu-id="cc48e-118"><a id="examplequery3"></a>Przykładowe zapytanie 3</span><span class="sxs-lookup"><span data-stu-id="cc48e-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="cc48e-119">Dalej zapytanie zwraca wszystkie rodziny, które zostały zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="cc48e-119">The next query returns all the families which are registered.</span></span> 

<span data-ttu-id="cc48e-120">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="cc48e-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="cc48e-121">**Wyniki** zostanie zwrócony żaden dokument.</span><span class="sxs-lookup"><span data-stu-id="cc48e-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="cc48e-122"><a id="examplequery4"></a>Przykładowe zapytanie 4</span><span class="sxs-lookup"><span data-stu-id="cc48e-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="cc48e-123">Dalej zapytanie zwraca wszystkie rodziny, które nie zostały zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="cc48e-123">The next query returns all the families which are not registered.</span></span> 

<span data-ttu-id="cc48e-124">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="cc48e-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="cc48e-125">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="cc48e-125">**Results**</span></span>

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
<span data-ttu-id="cc48e-126">}</span><span class="sxs-lookup"><span data-stu-id="cc48e-126">}</span></span>

## <span data-ttu-id="cc48e-127"><a id="examplequery5"></a>Przykładowe zapytanie 5</span><span class="sxs-lookup"><span data-stu-id="cc48e-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="cc48e-128">Dalej zapytanie zwraca rodziny, które nie są zarejestrowane i stan jest NY.</span><span class="sxs-lookup"><span data-stu-id="cc48e-128">The next query returns all the families which are not registered and state is NY.</span></span> 

<span data-ttu-id="cc48e-129">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="cc48e-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="cc48e-130">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="cc48e-130">**Results**</span></span>

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
<span data-ttu-id="cc48e-131">}</span><span class="sxs-lookup"><span data-stu-id="cc48e-131">}</span></span>


## <span data-ttu-id="cc48e-132"><a id="examplequery6"></a>Przykładowe zapytanie 6</span><span class="sxs-lookup"><span data-stu-id="cc48e-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="cc48e-133">Dalej zapytanie zwraca wszystkich rodzin, w których 8 klas podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="cc48e-133">The next query returns all the families where children grades are 8.</span></span>

<span data-ttu-id="cc48e-134">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="cc48e-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="cc48e-135">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="cc48e-135">**Results**</span></span>

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
<span data-ttu-id="cc48e-136">}</span><span class="sxs-lookup"><span data-stu-id="cc48e-136">}</span></span>

## <span data-ttu-id="cc48e-137"><a id="examplequery7"></a>Przykładowe zapytanie 7</span><span class="sxs-lookup"><span data-stu-id="cc48e-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="cc48e-138">Dalej zapytanie zwraca wszystkich rodzin, których rozmiar tablicy elementów podrzędnych to 3.</span><span class="sxs-lookup"><span data-stu-id="cc48e-138">The next query returns all the families where size of children array is 3.</span></span>

<span data-ttu-id="cc48e-139">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="cc48e-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="cc48e-140">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="cc48e-140">**Results**</span></span>

<span data-ttu-id="cc48e-141">Nie będzie można zwrócić wyników, ponieważ nie ma więcej niż 2 elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="cc48e-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="cc48e-142">Tylko wtedy, gdy parametr 2 to zapytanie powiodło się i zwróć pełnego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="cc48e-142">Only when parameter is 2 this query will succeed and return the full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc48e-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cc48e-143">Next steps</span></span>

<span data-ttu-id="cc48e-144">W tym samouczku wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="cc48e-144">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cc48e-145">Przedstawiono sposób zapytań przy użyciu bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="cc48e-145">Learned how to query using MongoDB</span></span> 

<span data-ttu-id="cc48e-146">Możesz teraz przejść do następnym samouczku informacje na temat dystrybucji danych globalnie.</span><span class="sxs-lookup"><span data-stu-id="cc48e-146">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cc48e-147">Globalny dystrybucji danych</span><span class="sxs-lookup"><span data-stu-id="cc48e-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

