---
title: "aaaAzure rozwiązania Cosmos bazy danych dystrybucji globalne samouczek dotyczący interfejsu API programu Graph | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello interfejsu API programu Graph."
services: cosmos-db
keywords: globalne dystrybucji, wykres, gremlin
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a><span data-ttu-id="50c6d-104">Jak przy użyciu dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup hello interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="50c6d-104">How toosetup Azure Cosmos DB global distribution using hello Graph API</span></span>

<span data-ttu-id="50c6d-105">W tym artykule zostanie przedstawiony sposób toouse hello dystrybucji globalnej bazy danych Azure rozwiązania Cosmos toosetup portalu Azure, a następnie nawiąż połączenie przy użyciu hello interfejsu API programu Graph (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="50c6d-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Graph API (preview).</span></span>

<span data-ttu-id="50c6d-106">W tym artykule omówiono hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="50c6d-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="50c6d-107">Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="50c6d-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="50c6d-108">Skonfiguruj globalne dystrybucji przy użyciu hello [API Graph](graph-introduction.md) (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="50c6d-108">Configure global distribution using hello [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a><span data-ttu-id="50c6d-109">Łączenie tooa przy użyciu interfejsu API programu Graph hello przy użyciu zestawu .NET SDK hello preferowanego regionu.</span><span class="sxs-lookup"><span data-stu-id="50c6d-109">Connecting tooa preferred region using hello Graph API using hello .NET SDK</span></span>

<span data-ttu-id="50c6d-110">Interfejs API programu Graph Hello jest ujawniona jako biblioteki rozszerzenia na powitania zestawu SDK usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="50c6d-110">hello Graph API is exposed as an extension library on top of hello DocumentDB SDK.</span></span>

<span data-ttu-id="50c6d-111">W kolejności tootake zaletą [globalne dystrybucji](distribute-data-globally.md), aplikacje klienckie można określić hello uporządkowana lista preferencji toobe regionów używanych tooperform dokumentu operacji.</span><span class="sxs-lookup"><span data-stu-id="50c6d-111">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="50c6d-112">Można to zrobić przez ustawienie hello zasad połączenia.</span><span class="sxs-lookup"><span data-stu-id="50c6d-112">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="50c6d-113">Na podstawie konfiguracji konta bazy danych Azure rozwiązania Cosmos hello bieżącej dostępności regionalnych i hello preferencji listy określone, hello większości optymalne punktu końcowego zostanie wybrany przez hello SDK tooperform zapisu i operacje odczytu.</span><span class="sxs-lookup"><span data-stu-id="50c6d-113">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello SDK tooperform write and read operations.</span></span>

<span data-ttu-id="50c6d-114">Ta lista preferencji został określony podczas inicjowania połączenia przy użyciu hello zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="50c6d-114">This preference list is specified when initializing a connection using hello SDKs.</span></span> <span data-ttu-id="50c6d-115">Witaj zestawów SDK zaakceptować opcjonalny parametr "PreferredLocations" oznacza to uporządkowana lista regionów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="50c6d-115">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="50c6d-116">**Zapisuje**: hello SDK będzie automatycznie wysyłać wszystkie zapisuje toohello bieżący obszar zapisu.</span><span class="sxs-lookup"><span data-stu-id="50c6d-116">**Writes**: hello SDK will automatically send all writes toohello current write region.</span></span>
* <span data-ttu-id="50c6d-117">**Odczytuje**: wszystkie operacje odczytu zostaną wysłane jako pierwszy dostępny region toohello hello PreferredLocations listy.</span><span class="sxs-lookup"><span data-stu-id="50c6d-117">**Reads**: All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="50c6d-118">W przypadku niepowodzenia żądania hello powitania klienta się nie powieść w dół listy hello toohello następny region i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="50c6d-118">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span> <span data-ttu-id="50c6d-119">tylko tooread z określonych w PreferredLocations regionów hello zostanie podjęta próba Hello zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="50c6d-119">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="50c6d-120">Tak na przykład, jeśli hello konto rozwiązania Cosmos bazy danych jest dostępne w trzech regionów, ale powitania klienta tylko określa dwa regiony i do zapisu hello PreferredLocations, następnie odczyty nie zostanie obsłużona poza region zapisu hello, nawet w przypadku hello pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="50c6d-120">So, for example, if hello Cosmos DB account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="50c6d-121">aplikacji Hello można Sprawdź hello bieżący punkt końcowy zapisu i odczytu punktu końcowego wybierany przez hello zestawu SDK przez sprawdzanie, czy dwie właściwości WriteEndpoint i ReadEndpoint dostępne w wersji zestawu SDK 1.8 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="50c6d-121">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="50c6d-122">Jeśli nie ustawiono właściwości PreferredLocations hello, wszystkie żądania będą udostępniane przez hello bieżący obszar zapisu.</span><span class="sxs-lookup"><span data-stu-id="50c6d-122">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

### <a name="using-hello-sdk"></a><span data-ttu-id="50c6d-123">Przy użyciu hello zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="50c6d-123">Using hello SDK</span></span>

<span data-ttu-id="50c6d-124">Na przykład w hello zestawu .NET SDK hello `ConnectionPolicy` parametr hello `DocumentClient` Konstruktor ma właściwość o nazwie `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="50c6d-124">For example, in hello .NET SDK, hello `ConnectionPolicy` parameter for hello `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="50c6d-125">Tej właściwości można ustawić tooa lista obszaru nazw.</span><span class="sxs-lookup"><span data-stu-id="50c6d-125">This property can be set tooa list of region names.</span></span> <span data-ttu-id="50c6d-126">Nazwa wyświetlana Hello [regiony platformy Azure] [ regions] może być określona jako część `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="50c6d-126">hello display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="50c6d-127">nie należy traktować jako długotrwałe stałe adresy URL Hello hello punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="50c6d-127">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="50c6d-128">Usługa Hello może zaktualizować je w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="50c6d-128">hello service may update these at any point.</span></span> <span data-ttu-id="50c6d-129">Witaj SDK automatycznie obsługuje tę zmianę.</span><span class="sxs-lookup"><span data-stu-id="50c6d-129">hello SDK handles this change automatically.</span></span>
>
>

```cs
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;

ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="50c6d-130">To wszystko, która kończy w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="50c6d-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="50c6d-131">Dowiedz się jak toomanage hello spójności konta globalnie replikowanych odczytując [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="50c6d-131">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="50c6d-132">I uzyskać więcej informacji na temat sposobu globalnej replikacji bazy danych działa w usłudze Azure DB rozwiązania Cosmos, zobacz [dystrybucji danych globalnie z bazy danych Azure rozwiązania Cosmos](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="50c6d-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="50c6d-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="50c6d-133">Next steps</span></span>

<span data-ttu-id="50c6d-134">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="50c6d-134">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="50c6d-135">Skonfiguruj globalne dystrybucji przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="50c6d-135">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="50c6d-136">Skonfiguruj globalne dystrybucji przy użyciu hello interfejsów API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="50c6d-136">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="50c6d-137">Można teraz kontynuować toohello następny samouczek toolearn jak toodevelop lokalnie za pomocą hello emulatora lokalnej bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="50c6d-137">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="50c6d-138">Opracowywanie lokalnie emulatorze hello</span><span class="sxs-lookup"><span data-stu-id="50c6d-138">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

