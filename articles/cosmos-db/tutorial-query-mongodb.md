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
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a>Azure DB rozwiązania Cosmos: Jak tooquery z interfejsem API bazy danych mongodb?

Hello Azure DB rozwiązania Cosmos [interfejsu API dla bazy danych MongoDB](mongodb-introduction.md) obsługuje [zapytania powłoki MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/). 

W tym artykule omówiono hello następujące zadania: 

> [!div class="checklist"]
> * Wykonywanie zapytania na danych z bazy danych MongoDB

## <a name="sample-document"></a>Przykładowy dokument

Witaj zapytania w tym artykule Użyj powitania po przykładowy dokument.

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
## <a id="examplequery1"></a>Przykładowe Zapytanie 1 

Podana hello próbki rodziny dokumentu powyżej, hello następujące zapytanie zwraca hello dokumentów, jeśli pole identyfikatora hello odpowiada `WakefieldFamily`.

**Zapytanie**
    
    db.families.find({ id: “WakefieldFamily”})

**Wyniki**

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

## <a id="examplequery2"></a>Przykładowe zapytanie 2 

Witaj dalej zapytanie zwraca wszystkie elementy podrzędne hello hello rodziny. 

**Zapytanie**
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

**Wyniki**

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


## <a id="examplequery3"></a>Przykładowe zapytanie 3 

Witaj dalej zapytanie zwraca wszystkich rodzin hello, które zostały zarejestrowane. 

**Zapytanie**
    
    db.families.find( { "isRegistered" : true })
**Wyniki** zostanie zwrócony żaden dokument. 

## <a id="examplequery4"></a>Przykładowe zapytanie 4

Witaj dalej zapytanie zwraca wszystkich rodzin hello, które nie zostały zarejestrowane. 

**Zapytanie**
    
    db.families.find( { "isRegistered" : false })
**Wyniki**

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
}

## <a id="examplequery5"></a>Przykładowe zapytanie 5

Hello dalej zapytanie zwraca wszystkie rodzin hello, które nie są zarejestrowane i stan NY. 

**Zapytanie**
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

**Wyniki**

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
}


## <a id="examplequery6"></a>Przykładowe zapytanie 6

Hello dalej zapytanie zwraca wszystkich rodzin hello, w których 8 klas podrzędnych.

**Zapytanie**
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

**Wyniki**

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
}

## <a id="examplequery7"></a>Przykładowe zapytanie 7

Hello dalej zapytanie zwraca wszystkich rodzin hello, w których rozmiar tablicy elementów podrzędnych jest 3.

**Zapytanie**
  
      db.Family.find( {children: { $size:3} } )

**Wyniki**

Nie będzie można zwrócić wyników, ponieważ nie ma więcej niż 2 elementów podrzędnych. Tylko wtedy, gdy parametr 2 to zapytanie powiodło się i zwróć hello pełnego dokumentu.

## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu hello następujące czynności:

> [!div class="checklist"]
> * Przedstawiono sposób tooquery przy użyciu bazy danych MongoDB 

Można teraz kontynuować toohello następny samouczek toolearn jak toodistribute danych globalnie.

> [!div class="nextstepaction"]
> [Globalny dystrybucji danych](tutorial-global-distribution-documentdb.md)

