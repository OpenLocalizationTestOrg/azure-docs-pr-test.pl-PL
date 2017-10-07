---
title: "aaaAzure zasoby & .NET zmiany źródła procesora zestawu SDK usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o hello API procesora źródła danych zmian i zestawu SDK, w tym daty wydania, daty wycofania i zmiany między poszczególnymi wersjami hello .NET zmiany źródła procesora zestawu SDK usługi DocumentDB."
services: cosmos-db
documentationcenter: .net
author: ealsur
manager: kirillg
editor: mimig1
ms.assetid: f2dd9438-8879-4f74-bb6c-e1efc2cd0157
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: maquaran
ms.openlocfilehash: 7c001cc77f41c01445fb53328e9d99fd3d312c58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="dfdf9-103">Usługa DocumentDB .NET zmiany źródła strumieniowego procesora zestawu SDK: Pobierz i informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="dfdf9-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dfdf9-104">.NET</span><span class="sxs-lookup"><span data-stu-id="dfdf9-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="dfdf9-105">Źródła danych zmian .NET</span><span class="sxs-lookup"><span data-stu-id="dfdf9-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="dfdf9-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="dfdf9-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="dfdf9-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="dfdf9-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="dfdf9-108">Java</span><span class="sxs-lookup"><span data-stu-id="dfdf9-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="dfdf9-109">Python</span><span class="sxs-lookup"><span data-stu-id="dfdf9-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="dfdf9-110">REST</span><span class="sxs-lookup"><span data-stu-id="dfdf9-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="dfdf9-111">Dostawca zasobów REST</span><span class="sxs-lookup"><span data-stu-id="dfdf9-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="dfdf9-112">SQL</span><span class="sxs-lookup"><span data-stu-id="dfdf9-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="dfdf9-113">**Pobierz zestaw SDK**</span><span class="sxs-lookup"><span data-stu-id="dfdf9-113">**SDK download**</span></span></td><td>[<span data-ttu-id="dfdf9-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="dfdf9-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="dfdf9-115">**Dokumentacja interfejsu API**</span><span class="sxs-lookup"><span data-stu-id="dfdf9-115">**API documentation**</span></span></td><td>[<span data-ttu-id="dfdf9-116">Zmień dokumentacji interfejsu API biblioteki procesora źródła danych</span><span class="sxs-lookup"><span data-stu-id="dfdf9-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="dfdf9-117">**Wprowadzenie**</span><span class="sxs-lookup"><span data-stu-id="dfdf9-117">**Get started**</span></span></td><td>[<span data-ttu-id="dfdf9-118">Rozpoczynanie pracy z hello zmiany źródła procesora .NET zestawu SDK usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="dfdf9-118">Get started with hello DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="dfdf9-119">**Bieżąca platforma obsługiwane**</span><span class="sxs-lookup"><span data-stu-id="dfdf9-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="dfdf9-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="dfdf9-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="dfdf9-121">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="dfdf9-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="dfdf9-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="dfdf9-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="dfdf9-123">Dodaje metody tooobtain szacowania pozostała toobe pracy przetwarzane w hello zmiany źródła danych.</span><span class="sxs-lookup"><span data-stu-id="dfdf9-123">Added a method tooobtain an estimate of remaining work toobe processed in hello Change Feed.</span></span>
* <span data-ttu-id="dfdf9-124">Zgodny z [zestawu SDK .NET usługi DocumentDB](documentdb-sdk-dotnet.md) wersji 1.13.2 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="dfdf9-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="dfdf9-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="dfdf9-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="dfdf9-126">GA SDK</span><span class="sxs-lookup"><span data-stu-id="dfdf9-126">GA SDK</span></span>
* <span data-ttu-id="dfdf9-127">Zgodny z [zestawu SDK .NET usługi DocumentDB](documentdb-sdk-dotnet.md) wersji 1.14.1 i poniżej.</span><span class="sxs-lookup"><span data-stu-id="dfdf9-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="dfdf9-128">Wersja & wycofania dat</span><span class="sxs-lookup"><span data-stu-id="dfdf9-128">Release & Retirement dates</span></span>
<span data-ttu-id="dfdf9-129">Firma Microsoft udostępni powiadomienia co najmniej **12 miesięcy** klienta z wyprzedzeniem wycofanie SDK w kolejności toosmooth hello przejścia tooa nowszej/nieobsługiwaną wersję.</span><span class="sxs-lookup"><span data-stu-id="dfdf9-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="dfdf9-130">Nowe funkcje i funkcjonalność i optymalizację, które są dodawane tylko toohello bieżącego zestawu SDK, w związku zaleca się tego należy zawsze uaktualnienia toohello najnowszego zestawu SDK w wersji możliwie jak najszybciej.</span><span class="sxs-lookup"><span data-stu-id="dfdf9-130">New features and functionality and optimizations are only added toohello current SDK, as such it is recommended that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="dfdf9-131">Wszystkie żądania tooCosmos bazy danych przy użyciu wycofane zestawu SDK będą odrzucane przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="dfdf9-131">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="dfdf9-132">Wersja</span><span class="sxs-lookup"><span data-stu-id="dfdf9-132">Version</span></span> | <span data-ttu-id="dfdf9-133">Data wydania</span><span class="sxs-lookup"><span data-stu-id="dfdf9-133">Release Date</span></span> | <span data-ttu-id="dfdf9-134">Dacie wycofania</span><span class="sxs-lookup"><span data-stu-id="dfdf9-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="dfdf9-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="dfdf9-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="dfdf9-136">13 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="dfdf9-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="dfdf9-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="dfdf9-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="dfdf9-138">07 lipca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="dfdf9-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="dfdf9-139">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="dfdf9-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="dfdf9-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="dfdf9-140">See also</span></span>
<span data-ttu-id="dfdf9-141">toolearn więcej informacji na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi.</span><span class="sxs-lookup"><span data-stu-id="dfdf9-141">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

