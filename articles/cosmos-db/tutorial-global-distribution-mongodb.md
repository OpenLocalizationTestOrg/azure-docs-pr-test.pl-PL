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
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a><span data-ttu-id="93820-104">Jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello API bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="93820-104">How toosetup Azure Cosmos DB global distribution using hello MongoDB API</span></span>

<span data-ttu-id="93820-105">W tym artykule zostanie przedstawiony sposób toouse hello Azure toosetup portalu Azure DB rozwiązania Cosmos globalne dystrybucji, a następnie nawiąż połączenie przy użyciu hello API bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="93820-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello MongoDB API.</span></span>

<span data-ttu-id="93820-106">W tym artykule omówiono hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="93820-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="93820-107">Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="93820-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="93820-108">Skonfiguruj globalne dystrybucji przy użyciu hello [API bazy danych MongoDB](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="93820-108">Configure global distribution using hello [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a><span data-ttu-id="93820-109">Weryfikowanie ustawień regionalnych przy użyciu hello API bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="93820-109">Verifying your regional setup using hello MongoDB API</span></span>
<span data-ttu-id="93820-110">Najprostszym sposobem Hello o podwójnej precyzji sprawdzanie globalnej konfiguracji w obrębie interfejsu API dla bazy danych MongoDB jest toorun hello *isMaster()* polecenie hello powłoki Mongo.</span><span class="sxs-lookup"><span data-stu-id="93820-110">hello simplest way of double checking your global configuration within API for MongoDB is toorun hello *isMaster()* command from hello Mongo Shell.</span></span>

<span data-ttu-id="93820-111">Z powłoki Mongo:</span><span class="sxs-lookup"><span data-stu-id="93820-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="93820-112">Przykładowe wyniki:</span><span class="sxs-lookup"><span data-stu-id="93820-112">Example results:</span></span>

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

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a><span data-ttu-id="93820-113">Łączenie preferowanego regionu tooa przy użyciu hello API bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="93820-113">Connecting tooa preferred region using hello MongoDB API</span></span>

<span data-ttu-id="93820-114">Hello bazy danych MongoDB interfejsu API umożliwia toospecify możesz odczytu preferencji globalnie rozproszoną bazę danych z kolekcji.</span><span class="sxs-lookup"><span data-stu-id="93820-114">hello MongoDB API enables you toospecify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="93820-115">Dla obu małe opóźnienia odczytów, jak i globalnego wysokiej dostępności, firma Microsoft zaleca ustawienie zbyt preferencji odczytu kolekcji*najbliższej*.</span><span class="sxs-lookup"><span data-stu-id="93820-115">For both low latency reads and global high availability, we recommend setting your collection's read preference too*nearest*.</span></span> <span data-ttu-id="93820-116">Przeczytaj preferencję *najbliższej* jest skonfigurowany tooread z hello najbliżej regionu.</span><span class="sxs-lookup"><span data-stu-id="93820-116">A read preference of *nearest* is configured tooread from hello closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="93820-117">Dla aplikacji za pomocą podstawowego odczytu/zapisu regionu i regionu pomocniczego do odzyskiwania awaryjnego (DR) scenariuszy, firma Microsoft zaleca ustawienie zbyt preferencji odczytu kolekcji*pomocniczy preferowane*.</span><span class="sxs-lookup"><span data-stu-id="93820-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference too*secondary preferred*.</span></span> <span data-ttu-id="93820-118">Odczytu preferencję *pomocniczy preferowane* jest skonfigurowany tooread z regionu pomocniczego hello w przypadku regionu podstawowego hello jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="93820-118">A read preference of *secondary preferred* is configured tooread from hello secondary region when hello primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="93820-119">Ponadto jeśli takie jak toomanually Określ Twojej odczytu regionów.</span><span class="sxs-lookup"><span data-stu-id="93820-119">Lastly, if you would like toomanually specify your read regions.</span></span> <span data-ttu-id="93820-120">Można ustawić regionu hello tagu w swoich preferencji odczytu.</span><span class="sxs-lookup"><span data-stu-id="93820-120">You can set hello region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="93820-121">To wszystko, która kończy w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="93820-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="93820-122">Dowiedz się jak toomanage hello spójności konta globalnie replikowanych odczytując [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="93820-122">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="93820-123">I uzyskać więcej informacji na temat sposobu globalnej replikacji bazy danych działa w usłudze Azure DB rozwiązania Cosmos, zobacz [dystrybucji danych globalnie z bazy danych Azure rozwiązania Cosmos](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="93820-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="93820-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="93820-124">Next steps</span></span>

<span data-ttu-id="93820-125">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="93820-125">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="93820-126">Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="93820-126">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="93820-127">Skonfiguruj globalne dystrybucji przy użyciu hello interfejsów API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="93820-127">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="93820-128">Można teraz kontynuować toohello następny samouczek toolearn jak toodevelop lokalnie za pomocą hello emulatora lokalnej bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="93820-128">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="93820-129">Opracowywanie lokalnie emulatorze hello</span><span class="sxs-lookup"><span data-stu-id="93820-129">Develop locally with hello emulator</span></span>](local-emulator.md)
