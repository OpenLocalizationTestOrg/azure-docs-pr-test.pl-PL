---
title: "Samouczek globalne dystrybucji DB rozwiązania Cosmos aaaAzure tabeli interfejsu API | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello tabeli interfejsu API."
services: cosmos-db
keywords: globalne dystrybucji, tabeli
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
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a><span data-ttu-id="95654-104">Jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello tabeli interfejsu API</span><span class="sxs-lookup"><span data-stu-id="95654-104">How toosetup Azure Cosmos DB global distribution using hello Table API</span></span>

<span data-ttu-id="95654-105">W tym artykule zostanie przedstawiony sposób toouse hello dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup portalu Azure, a następnie nawiąż połączenie przy użyciu hello tabeli interfejsu API (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="95654-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Table API (preview).</span></span>

<span data-ttu-id="95654-106">W tym artykule omówiono hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="95654-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="95654-107">Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="95654-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="95654-108">Skonfiguruj globalne dystrybucji przy użyciu hello [tabeli interfejsu API](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="95654-108">Configure global distribution using hello [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a><span data-ttu-id="95654-109">Łączenie preferowanego regionu tooa przy użyciu hello tabeli interfejsu API</span><span class="sxs-lookup"><span data-stu-id="95654-109">Connecting tooa preferred region using hello Table API</span></span>

<span data-ttu-id="95654-110">W kolejności tootake zaletą [globalne dystrybucji](distribute-data-globally.md), aplikacje klienckie można określić hello uporządkowana lista preferencji toobe regionów używanych tooperform dokumentu operacji.</span><span class="sxs-lookup"><span data-stu-id="95654-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="95654-111">Można to zrobić przez ustawienie hello `TablePreferredLocations` wartości konfiguracji w pliku konfiguracyjnym aplikacji hello podglądu hello zestawu SDK usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="95654-111">This can be done by setting hello `TablePreferredLocations` configuration value in hello app config for hello preview Azure Storage SDK.</span></span> <span data-ttu-id="95654-112">Na podstawie konfiguracji konta bazy danych Azure rozwiązania Cosmos hello bieżącej dostępności regionalnych i hello preferencji listy jest określony, powitalne większości optymalne punkt końcowy zostanie wybrany przez tooperform zestawu SDK usługi Magazyn Azure hello zapisu i operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="95654-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello Azure Storage SDK tooperform write and read operations.</span></span>

<span data-ttu-id="95654-113">Witaj `TablePreferredLocations` powinien zawierać rozdzielaną przecinkami listę preferowanych lokalizacji (podłączonej do wielu sieci) dla operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="95654-113">hello `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="95654-114">Każde wystąpienie klienta można określić podzbiór tych regionów hello preferowane aby odczyty małe opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="95654-114">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="95654-115">regiony Hello muszą nosić przy użyciu ich [wyświetlane nazwy](https://msdn.microsoft.com/library/azure/gg441293.aspx), na przykład `West US`.</span><span class="sxs-lookup"><span data-stu-id="95654-115">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="95654-116">Wszystkie operacje odczytu zostaną wysłane jako pierwszy dostępny region toohello hello `TablePreferredLocations` listy.</span><span class="sxs-lookup"><span data-stu-id="95654-116">All reads will be sent toohello first available region in hello `TablePreferredLocations` list.</span></span> <span data-ttu-id="95654-117">W przypadku niepowodzenia żądania hello powitania klienta się nie powieść w dół listy hello toohello następny region i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="95654-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="95654-118">Hello SDK podejmie tylko tooread z określonych w regionów hello `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="95654-118">hello SDK will only attempt tooread from hello regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="95654-119">Tak, na przykład, jeśli hello konto bazy danych są dostępne w trzech regionów, ale powitania klienta określa tylko dwa hello regionów i do zapisu dla `TablePreferredLocations`, a następnie odczyty nie zostanie obsłużona poza region zapisu hello, nawet w przypadku hello pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="95654-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for `TablePreferredLocations`, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="95654-120">Witaj SDK będzie automatycznie wysyłać wszystkie zapisy toohello bieżącego zapisu regionu.</span><span class="sxs-lookup"><span data-stu-id="95654-120">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="95654-121">Jeśli hello `TablePreferredLocations` właściwość nie jest ustawiona, wszystkie żądania zostanie obsłużona z hello bieżący obszar zapisu.</span><span class="sxs-lookup"><span data-stu-id="95654-121">If hello `TablePreferredLocations` property is not set, all requests will be served from hello current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="95654-122">To wszystko, która kończy w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="95654-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="95654-123">Dowiedz się jak toomanage hello spójności konta globalnie replikowanych odczytując [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="95654-123">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="95654-124">I uzyskać więcej informacji na temat sposobu globalnej replikacji bazy danych działa w usłudze Azure DB rozwiązania Cosmos, zobacz [dystrybucji danych globalnie z bazy danych Azure rozwiązania Cosmos](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="95654-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="95654-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95654-125">Next steps</span></span>

<span data-ttu-id="95654-126">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="95654-126">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="95654-127">Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="95654-127">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="95654-128">Skonfiguruj globalne dystrybucji przy użyciu hello interfejsów API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="95654-128">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="95654-129">Można teraz kontynuować toohello następny samouczek toolearn jak toodevelop lokalnie za pomocą hello emulatora lokalnej bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="95654-129">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="95654-130">Opracowywanie lokalnie emulatorze hello</span><span class="sxs-lookup"><span data-stu-id="95654-130">Develop locally with hello emulator</span></span>](local-emulator.md)
