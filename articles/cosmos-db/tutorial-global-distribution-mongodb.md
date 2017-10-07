---
title: "Samouczek globalne dystrybucji DB rozwiązania Cosmos aaaAzure dla bazy danych MongoDB interfejsu API | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello API bazy danych MongoDB."
services: cosmos-db
keywords: globalne dystrybucji, bazy danych MongoDB
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a>Jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello API bazy danych MongoDB

W tym artykule zostanie przedstawiony sposób toouse hello Azure toosetup portalu Azure DB rozwiązania Cosmos globalne dystrybucji, a następnie nawiąż połączenie przy użyciu hello API bazy danych MongoDB.

W tym artykule omówiono hello następujące zadania: 

> [!div class="checklist"]
> * Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure
> * Skonfiguruj globalne dystrybucji przy użyciu hello [API bazy danych MongoDB](mongodb-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a>Weryfikowanie ustawień regionalnych przy użyciu hello API bazy danych MongoDB
Najprostszym sposobem Hello o podwójnej precyzji sprawdzanie globalnej konfiguracji w obrębie interfejsu API dla bazy danych MongoDB jest toorun hello *isMaster()* polecenie hello powłoki Mongo.

Z powłoki Mongo:

   ```
      db.isMaster()
   ```
   
Przykładowe wyniki:

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a>Łączenie preferowanego regionu tooa przy użyciu hello API bazy danych MongoDB

Hello bazy danych MongoDB interfejsu API umożliwia toospecify możesz odczytu preferencji globalnie rozproszoną bazę danych z kolekcji. Dla obu małe opóźnienia odczytów, jak i globalnego wysokiej dostępności, firma Microsoft zaleca ustawienie zbyt preferencji odczytu kolekcji*najbliższej*. Przeczytaj preferencję *najbliższej* jest skonfigurowany tooread z hello najbliżej regionu.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

Dla aplikacji za pomocą podstawowego odczytu/zapisu regionu i regionu pomocniczego do odzyskiwania awaryjnego (DR) scenariuszy, firma Microsoft zaleca ustawienie zbyt preferencji odczytu kolekcji*pomocniczy preferowane*. Odczytu preferencję *pomocniczy preferowane* jest skonfigurowany tooread z regionu pomocniczego hello w przypadku regionu podstawowego hello jest niedostępny.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

Ponadto jeśli takie jak toomanually Określ Twojej odczytu regionów. Można ustawić regionu hello tagu w swoich preferencji odczytu.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

To wszystko, która kończy w tym samouczku. Dowiedz się jak toomanage hello spójności konta globalnie replikowanych odczytując [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md). I uzyskać więcej informacji na temat sposobu globalnej replikacji bazy danych działa w usłudze Azure DB rozwiązania Cosmos, zobacz [dystrybucji danych globalnie z bazy danych Azure rozwiązania Cosmos](distribute-data-globally.md).

## <a name="next-steps"></a>Następne kroki

W tym samouczku wykonaniu hello następujące czynności:

> [!div class="checklist"]
> * Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure
> * Skonfiguruj globalne dystrybucji przy użyciu hello interfejsów API usługi DocumentDB

Można teraz kontynuować toohello następny samouczek toolearn jak toodevelop lokalnie za pomocą hello emulatora lokalnej bazy danych Azure rozwiązania Cosmos.

> [!div class="nextstepaction"]
> [Opracowywanie lokalnie emulatorze hello](local-emulator.md)
