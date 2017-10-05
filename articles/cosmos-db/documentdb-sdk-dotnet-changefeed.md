---
title: "Usługa Azure DocumentDB .NET zmienić zasoby & źródła procesora zestawu SDK | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o interfejsie API procesora źródła danych zmian i zestawu SDK, w tym daty wydania, daty wycofania i zmiany wprowadzone od każda wersja programu .NET zmiany źródła procesora zestawu SDK usługi DocumentDB."
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
ms.openlocfilehash: 40c796bc5af1220c46950a6fac062ffdd243e59f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="documentdb-net-change-feed-processor-sdk-download-and-release-notes"></a><span data-ttu-id="71bea-103">Usługa DocumentDB .NET zmiany źródła strumieniowego procesora zestawu SDK: Pobierz i informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="71bea-103">DocumentDB .NET Change Feed Processor SDK: Download and release notes</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71bea-104">.NET</span><span class="sxs-lookup"><span data-stu-id="71bea-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="71bea-105">Źródła danych zmian .NET</span><span class="sxs-lookup"><span data-stu-id="71bea-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="71bea-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="71bea-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="71bea-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="71bea-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="71bea-108">Java</span><span class="sxs-lookup"><span data-stu-id="71bea-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="71bea-109">Python</span><span class="sxs-lookup"><span data-stu-id="71bea-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="71bea-110">REST</span><span class="sxs-lookup"><span data-stu-id="71bea-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="71bea-111">Dostawca zasobów REST</span><span class="sxs-lookup"><span data-stu-id="71bea-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="71bea-112">SQL</span><span class="sxs-lookup"><span data-stu-id="71bea-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="71bea-113">**Pobierz zestaw SDK**</span><span class="sxs-lookup"><span data-stu-id="71bea-113">**SDK download**</span></span></td><td>[<span data-ttu-id="71bea-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="71bea-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)</td></tr>

<tr><td><span data-ttu-id="71bea-115">**Dokumentacja interfejsu API**</span><span class="sxs-lookup"><span data-stu-id="71bea-115">**API documentation**</span></span></td><td>[<span data-ttu-id="71bea-116">Zmień dokumentacji interfejsu API biblioteki procesora źródła danych</span><span class="sxs-lookup"><span data-stu-id="71bea-116">Change Feed Processor library API reference documentation</span></span>](/dotnet/api/microsoft.azure.documents.changefeedprocessor?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="71bea-117">**Wprowadzenie**</span><span class="sxs-lookup"><span data-stu-id="71bea-117">**Get started**</span></span></td><td>[<span data-ttu-id="71bea-118">Wprowadzenie do usługi DocumentDB zmiany źródła procesora zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="71bea-118">Get started with the DocumentDB Change Feed Processor .NET SDK</span></span>](change-feed.md)</td></tr>

<tr><td><span data-ttu-id="71bea-119">**Bieżąca platforma obsługiwane**</span><span class="sxs-lookup"><span data-stu-id="71bea-119">**Current supported framework**</span></span></td><td>[<span data-ttu-id="71bea-120">Microsoft .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="71bea-120">Microsoft .NET Framework 4.5</span></span>](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="71bea-121">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="71bea-121">Release notes</span></span>

### <a name="a-name110110"></a><span data-ttu-id="71bea-122"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="71bea-122"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="71bea-123">Dodaje metody uzyskać szacunkową Praca pozostała na przetworzenie w źródła danych zmian.</span><span class="sxs-lookup"><span data-stu-id="71bea-123">Added a method to obtain an estimate of remaining work to be processed in the Change Feed.</span></span>
* <span data-ttu-id="71bea-124">Zgodny z [zestawu SDK .NET usługi DocumentDB](documentdb-sdk-dotnet.md) wersji 1.13.2 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="71bea-124">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.13.2 and above.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="71bea-125"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="71bea-125"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="71bea-126">GA SDK</span><span class="sxs-lookup"><span data-stu-id="71bea-126">GA SDK</span></span>
* <span data-ttu-id="71bea-127">Zgodny z [zestawu SDK .NET usługi DocumentDB](documentdb-sdk-dotnet.md) wersji 1.14.1 i poniżej.</span><span class="sxs-lookup"><span data-stu-id="71bea-127">Compatible with [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) versions 1.14.1 and below.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="71bea-128">Wersja & wycofania dat</span><span class="sxs-lookup"><span data-stu-id="71bea-128">Release & Retirement dates</span></span>
<span data-ttu-id="71bea-129">Firma Microsoft udostępni powiadomienia co najmniej **12 miesięcy** klienta z wyprzedzeniem wycofanie SDK w celu złagodzenia przejścia do nowszej/nieobsługiwaną wersję.</span><span class="sxs-lookup"><span data-stu-id="71bea-129">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="71bea-130">Nowe funkcje i funkcjonalność i optymalizację, które są dodawane tylko do bieżącego zestawu SDK, w związku jest zalecane, zawsze Uaktualnij zestaw SDK najnowszą tak szybko jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="71bea-130">New features and functionality and optimizations are only added to the current SDK, as such it is recommended that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="71bea-131">Każde żądanie do rozwiązania Cosmos bazy danych przy użyciu wycofane zestawu SDK będą odrzucane przez usługę.</span><span class="sxs-lookup"><span data-stu-id="71bea-131">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="71bea-132">Wersja</span><span class="sxs-lookup"><span data-stu-id="71bea-132">Version</span></span> | <span data-ttu-id="71bea-133">Data wydania</span><span class="sxs-lookup"><span data-stu-id="71bea-133">Release Date</span></span> | <span data-ttu-id="71bea-134">Dacie wycofania</span><span class="sxs-lookup"><span data-stu-id="71bea-134">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="71bea-135">1.1.0</span><span class="sxs-lookup"><span data-stu-id="71bea-135">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="71bea-136">13 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="71bea-136">August 13, 2017</span></span> |--- |
| [<span data-ttu-id="71bea-137">1.0.0</span><span class="sxs-lookup"><span data-stu-id="71bea-137">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="71bea-138">07 lipca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="71bea-138">July 07, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="71bea-139">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="71bea-139">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="71bea-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="71bea-140">See also</span></span>
<span data-ttu-id="71bea-141">Aby dowiedzieć się więcej na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi.</span><span class="sxs-lookup"><span data-stu-id="71bea-141">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

