---
title: "Samouczek usługi Azure globalne dystrybucji rozwiązania Cosmos bazy danych dla tabeli interfejsu API | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować bazy danych Azure rozwiązania Cosmos dystrybucji globalnego przy użyciu interfejsu API tabeli."
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
ms.openlocfilehash: 63c9e530a4982e2e6e478fea56e015fc77851e1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-table-api"></a><span data-ttu-id="c8b1b-104">Konfigurowanie bazy danych Azure rozwiązania Cosmos dystrybucji globalnego przy użyciu interfejsu API tabeli</span><span class="sxs-lookup"><span data-stu-id="c8b1b-104">How to setup Azure Cosmos DB global distribution using the Table API</span></span>

<span data-ttu-id="c8b1b-105">W tym artykule zostanie przedstawiony sposób korzystać z portalu Azure do instalacji bazy danych Azure rozwiązania Cosmos globalne dystrybucji, a następnie nawiąż połączenie przy użyciu interfejsu API tabeli (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="c8b1b-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Table API (preview).</span></span>

<span data-ttu-id="c8b1b-106">W tym artykule opisano następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="c8b1b-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c8b1b-107">Skonfiguruj globalne dystrybucji przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c8b1b-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="c8b1b-108">Skonfigurować globalne dystrybucji za pomocą [tabeli interfejsu API](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c8b1b-108">Configure global distribution using the [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-table-api"></a><span data-ttu-id="c8b1b-109">Łączenie z preferowanego regionu przy użyciu interfejsu API tabeli</span><span class="sxs-lookup"><span data-stu-id="c8b1b-109">Connecting to a preferred region using the Table API</span></span>

<span data-ttu-id="c8b1b-110">Aby korzystać z [globalne dystrybucji](distribute-data-globally.md), aplikacje klienckie można określić listy uporządkowanej preferencji regionów ma być używany do wykonywania operacji dokumentu.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="c8b1b-111">Można to zrobić przez ustawienie `TablePreferredLocations` wartości konfiguracji w pliku konfiguracyjnym aplikacji dla zestawu SDK usługi Magazyn Azure w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-111">This can be done by setting the `TablePreferredLocations` configuration value in the app config for the preview Azure Storage SDK.</span></span> <span data-ttu-id="c8b1b-112">Na podstawie konfiguracji konta bazy danych Azure rozwiązania Cosmos, bieżącej dostępności regionalnych i na liście preferencji określone, optymalny punkt końcowy zostanie wybrany przez zestaw SDK magazynu Azure do wykonywania zapisu i operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the Azure Storage SDK to perform write and read operations.</span></span>

<span data-ttu-id="c8b1b-113">`TablePreferredLocations` Powinien zawierać rozdzielaną przecinkami listę preferowanych lokalizacji (podłączonej do wielu sieci) dla operacji odczytu.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-113">The `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="c8b1b-114">Każde wystąpienie klienta można określić podzbiór tych regionów, w preferowanej kolejności dla odczytów małe opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-114">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="c8b1b-115">Regionów muszą nosić przy użyciu ich [wyświetlane nazwy](https://msdn.microsoft.com/library/azure/gg441293.aspx), na przykład `West US`.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-115">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="c8b1b-116">Wszystkie operacje odczytu, które zostaną wysłane do pierwszy dostępny region w `TablePreferredLocations` listy.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-116">All reads will be sent to the first available region in the `TablePreferredLocations` list.</span></span> <span data-ttu-id="c8b1b-117">Jeśli żądanie kończy się niepowodzeniem, klient się nie powieść w dół na liście, aby następny region i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="c8b1b-118">Zestawu SDK podejmie próbę odczytu z określonych w regionów `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-118">The SDK will only attempt to read from the regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="c8b1b-119">Tak, na przykład, jeśli konto bazy danych jest dostępne w trzech regionów, ale klient określa tylko dwóch regionach i do zapisu dla `TablePreferredLocations`, a następnie odczyty nie zostanie obsłużona poza region zapisu, nawet w przypadku pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for `TablePreferredLocations`, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="c8b1b-120">Zestaw SDK będzie automatycznie wysyłać zapisuje wszystkie dane w bieżącej zapisu regionu.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-120">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="c8b1b-121">Jeśli `TablePreferredLocations` właściwość nie jest ustawiona, zostanie obsłużona wszystkie żądania z bieżącego obszaru zapisu.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-121">If the `TablePreferredLocations` property is not set, all requests will be served from the current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="c8b1b-122">To wszystko, która kończy w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="c8b1b-123">Znajdują się informacje dotyczące zarządzania spójności konta globalnie replikowanych odczytując [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="c8b1b-123">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="c8b1b-124">I uzyskać więcej informacji na temat sposobu globalnej replikacji bazy danych działa w usłudze Azure DB rozwiązania Cosmos, zobacz [dystrybucji danych globalnie z bazy danych Azure rozwiązania Cosmos](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="c8b1b-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8b1b-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c8b1b-125">Next steps</span></span>

<span data-ttu-id="c8b1b-126">W tym samouczku wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="c8b1b-126">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c8b1b-127">Skonfiguruj globalne dystrybucji przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c8b1b-127">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="c8b1b-128">Skonfiguruj globalne dystrybucji przy użyciu interfejsów API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c8b1b-128">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="c8b1b-129">Możesz teraz przejść do następnym samouczku, aby dowiedzieć się, jak opracowywać lokalnie przy użyciu emulatora lokalnej bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c8b1b-129">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c8b1b-130">Opracowywanie lokalnie w emulatorze</span><span class="sxs-lookup"><span data-stu-id="c8b1b-130">Develop locally with the emulator</span></span>](local-emulator.md)