---
title: "Samouczek usługi Azure globalne dystrybucji rozwiązania Cosmos DB dla bazy danych MongoDB interfejsu API | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować bazy danych Azure rozwiązania Cosmos dystrybucji globalnego przy użyciu interfejsu API bazy danych MongoDB."
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
ms.openlocfilehash: a2747102f4d8cac412b67abc3fd07cfa3661bcee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-mongodb-api"></a><span data-ttu-id="7f5ef-104">Konfigurowanie bazy danych Azure rozwiązania Cosmos dystrybucji globalnego przy użyciu interfejsu API bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="7f5ef-104">How to setup Azure Cosmos DB global distribution using the MongoDB API</span></span>

<span data-ttu-id="7f5ef-105">W tym artykule zostanie przedstawiony sposób użycia portalu Azure do instalacji bazy danych Azure rozwiązania Cosmos globalne dystrybucji, a następnie nawiąż połączenie przy użyciu interfejsu API bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7f5ef-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the MongoDB API.</span></span>

<span data-ttu-id="7f5ef-106">W tym artykule opisano następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="7f5ef-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="7f5ef-107">Skonfiguruj globalne dystrybucji przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7f5ef-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="7f5ef-108">Skonfigurować globalne dystrybucji za pomocą [API bazy danych MongoDB](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="7f5ef-108">Configure global distribution using the [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-the-mongodb-api"></a><span data-ttu-id="7f5ef-109">Weryfikowanie ustawień regionalnych przy użyciu interfejsu API bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="7f5ef-109">Verifying your regional setup using the MongoDB API</span></span>
<span data-ttu-id="7f5ef-110">Najprostszym sposobem sprawdzanie globalnej konfiguracji w obrębie interfejsu API dla bazy danych MongoDB ma być uruchamiany o podwójnej precyzji *isMaster()* polecenie z poziomu powłoki Mongo.</span><span class="sxs-lookup"><span data-stu-id="7f5ef-110">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span></span>

<span data-ttu-id="7f5ef-111">Z powłoki Mongo:</span><span class="sxs-lookup"><span data-stu-id="7f5ef-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="7f5ef-112">Przykładowe wyniki:</span><span class="sxs-lookup"><span data-stu-id="7f5ef-112">Example results:</span></span>

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

## <a name="connecting-to-a-preferred-region-using-the-mongodb-api"></a><span data-ttu-id="7f5ef-113">Łączenie z preferowanego regionu przy użyciu interfejsu API bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="7f5ef-113">Connecting to a preferred region using the MongoDB API</span></span>

<span data-ttu-id="7f5ef-114">Interfejs API bazy danych MongoDB umożliwia określenie preferencji odczytu kolekcji globalnie rozproszone bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7f5ef-114">The MongoDB API enables you to specify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="7f5ef-115">Dla obu małe opóźnienia odczytów, jak i globalnego wysokiej dostępności, firma Microsoft zaleca ustawienie preferencji odczytu kolekcji *najbliższej*.</span><span class="sxs-lookup"><span data-stu-id="7f5ef-115">For both low latency reads and global high availability, we recommend setting your collection's read preference to *nearest*.</span></span> <span data-ttu-id="7f5ef-116">Przeczytaj preferencję *najbliższej* jest skonfigurowany do odczytu z najbliżej regionu.</span><span class="sxs-lookup"><span data-stu-id="7f5ef-116">A read preference of *nearest* is configured to read from the closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="7f5ef-117">Dla aplikacji za pomocą podstawowego odczytu/zapisu regionu i regionu pomocniczego do odzyskiwania awaryjnego (DR) scenariuszy, firma Microsoft zaleca ustawienie preferencji odczytu kolekcji *pomocniczy preferowane*.</span><span class="sxs-lookup"><span data-stu-id="7f5ef-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference to *secondary preferred*.</span></span> <span data-ttu-id="7f5ef-118">Odczytu preferencję *pomocniczy preferowane* jest skonfigurowany do odczytu z regionu pomocniczego, gdy region podstawowy jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="7f5ef-118">A read preference of *secondary preferred* is configured to read from the secondary region when the primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="7f5ef-119">Ponadto jeśli chcesz ręcznie określić Twojej odczytu regionów.</span><span class="sxs-lookup"><span data-stu-id="7f5ef-119">Lastly, if you would like to manually specify your read regions.</span></span> <span data-ttu-id="7f5ef-120">Można ustawić regionu tagu w swoich preferencji odczytu.</span><span class="sxs-lookup"><span data-stu-id="7f5ef-120">You can set the region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="7f5ef-121">To wszystko, która kończy w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="7f5ef-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="7f5ef-122">Znajdują się informacje dotyczące zarządzania spójności konta globalnie replikowanych odczytując [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="7f5ef-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="7f5ef-123">I uzyskać więcej informacji na temat sposobu globalnej replikacji bazy danych działa w usłudze Azure DB rozwiązania Cosmos, zobacz [dystrybucji danych globalnie z bazy danych Azure rozwiązania Cosmos](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="7f5ef-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f5ef-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7f5ef-124">Next steps</span></span>

<span data-ttu-id="7f5ef-125">W tym samouczku wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="7f5ef-125">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7f5ef-126">Skonfiguruj globalne dystrybucji przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7f5ef-126">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="7f5ef-127">Skonfiguruj globalne dystrybucji przy użyciu interfejsów API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="7f5ef-127">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="7f5ef-128">Możesz teraz przejść do następnym samouczku, aby dowiedzieć się, jak opracowywać lokalnie przy użyciu emulatora lokalnej bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7f5ef-128">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f5ef-129">Opracowywanie lokalnie w emulatorze</span><span class="sxs-lookup"><span data-stu-id="7f5ef-129">Develop locally with the emulator</span></span>](local-emulator.md)