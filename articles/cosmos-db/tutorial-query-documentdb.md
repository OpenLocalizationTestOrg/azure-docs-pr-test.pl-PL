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
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a>Azure DB rozwiązania Cosmos: Jak tooquery przy użyciu programu SQL?

Hello Azure DB rozwiązania Cosmos [interfejsu API usługi DocumentDB](documentdb-introduction.md) obsługiwanych badania dokumentów za pomocą programu SQL. Ten artykuł zawiera przykładowy dokument i dwa przykładowe zapytania SQL oraz wyniki.

W tym artykule omówiono hello następujące zadania: 

> [!div class="checklist"]
> * Wykonywanie zapytania na danych z programu SQL

## <a name="sample-document"></a>Przykładowy dokument

zapytania SQL Hello w tym artykule Użyj powitania po przykładowy dokument.

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
## <a name="where-can-i-run-sql-queries"></a>Gdzie można uruchomić zapytania SQL

Można uruchomić zapytania, używając hello Eksploratora danych w portalu Azure za pośrednictwem hello hello [interfejsu API REST i zestawy SDK](documentdb-sdk-dotnet.md)i nawet hello [Plac zabaw dla zapytań](https://www.documentdb.com/sql/demo), która działa na podstawie istniejącego zestawu danych przykładowych zapytań.

Aby uzyskać więcej informacji na temat kwerend SQL zobacz:
* [Zapytanie SQL i składni SQL](documentdb-sql-query.md)

## <a name="prerequisites"></a>Wymagania wstępne

W tym samouczku założono, że masz konto bazy danych Azure rozwiązania Cosmos i kolekcji. Nie masz żadnego z tych? Zakończenie hello [szybkiego startu 5-minutowy](create-mongodb-nodejs.md) lub hello [samouczek developer](tutorial-develop-mongodb.md) toocreate konto i kolekcji.

## <a name="example-query-1"></a>Przykładowe Zapytanie 1

Podana hello próbki rodziny dokumentu powyżej, następujące zapytanie SQL zwraca hello dokumenty Jeśli pole identyfikatora hello odpowiada `WakefieldFamily`. Ponieważ chodzi o `SELECT *` instrukcji, hello wyników kwerendy hello jest hello pełnego dokumentu JSON:

**Zapytanie**

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

**Wyniki**

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

## <a name="example-query-2"></a>Przykładowe zapytanie 2

Hello dalej zapytanie zwraca podanymi nazwami hello dzieci w rodzinie hello odpowiada o identyfikatorze `WakefieldFamily` uporządkowanych według ich klasy.

**Zapytanie**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

**Wyniki**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu hello następujące czynności:

> [!div class="checklist"]
> * Przedstawiono sposób tooquery przy użyciu programu SQL  

Można teraz kontynuować toohello następny samouczek toolearn jak toodistribute danych globalnie.

> [!div class="nextstepaction"]
> [Globalny dystrybucji danych](tutorial-global-distribution-documentdb.md)

