---
title: "Azure komunikatów usługi Service Bus przykłady omówienie | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano wiadomości próbki z łączami do każdej usługi Service Bus"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0b420343-2d2a-4c65-98f1-ee0e39ef55c8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: sethm
ms.openlocfilehash: 0cf21ea9a820de0396b54dd26a625a046de39291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="service-bus-messaging-samples"></a><span data-ttu-id="5bfb5-103">Przykłady obsługi komunikatów usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="5bfb5-103">Service Bus messaging samples</span></span>

<span data-ttu-id="5bfb5-104">Przykłady obsługi komunikatów usługi Service Bus pokazują kluczowe funkcje [komunikatów usługi Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="5bfb5-104">The Service Bus messaging samples demonstrate key features in [Service Bus messaging](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="5bfb5-105">Obecnie można znaleźć przykłady w dwóch miejscach:</span><span class="sxs-lookup"><span data-stu-id="5bfb5-105">Currently, you can find the samples in two places:</span></span>

- <span data-ttu-id="5bfb5-106">[Przykłady komunikatów usługi Service Bus w serwisie GitHub](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet): nowszej zestaw przykładów, w usłudze GitHub.</span><span class="sxs-lookup"><span data-stu-id="5bfb5-106">[Service Bus messaging samples on GitHub](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet): a newer set of samples, hosted on GitHub.</span></span> <span data-ttu-id="5bfb5-107">Zobacz [plik readme](https://github.com/Azure/azure-service-bus/blob/master/samples/DotNet/Microsoft.ServiceBus.Messaging/README.md) w repozytorium, aby uzyskać opis tych przykładów .NET.</span><span class="sxs-lookup"><span data-stu-id="5bfb5-107">See the [readme file](https://github.com/Azure/azure-service-bus/blob/master/samples/DotNet/Microsoft.ServiceBus.Messaging/README.md) in the repo for descriptions of these .NET samples.</span></span> <span data-ttu-id="5bfb5-108">Przykłady są stale aktualizowane, tak sprawdzać, czy często aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="5bfb5-108">The samples are continuously updated, so check back often for updates.</span></span>
- <span data-ttu-id="5bfb5-109">[Strona przykłady MSDN](https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=5): starsze przykłady, które znajdują się w galerii kodu MSDN.</span><span class="sxs-lookup"><span data-stu-id="5bfb5-109">[MSDN samples page](https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=5): older samples that live in the MSDN code gallery.</span></span> <span data-ttu-id="5bfb5-110">Mimo że te przykłady nadal działać, nie są obsługiwane i mogą być nieaktualne względem bieżącego rozwiązania programowania.</span><span class="sxs-lookup"><span data-stu-id="5bfb5-110">Although these samples still work, they are not maintained and may be outdated with respect to current recommended programming practices.</span></span>
 
## <a name="service-bus-explorer"></a><span data-ttu-id="5bfb5-111">Eksplorator usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="5bfb5-111">Service Bus Explorer</span></span>

<span data-ttu-id="5bfb5-112">Ponadto [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer) przykładowe w usłudze GitHub, umożliwiające nawiązywanie przestrzeni nazw usługi Service Bus i łatwe zarządzanie jednostek obsługi komunikatów.</span><span class="sxs-lookup"><span data-stu-id="5bfb5-112">In addition, the [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer) is a sample hosted on GitHub that enables you to connect to a Service Bus service namespace and easily manage messaging entities.</span></span> <span data-ttu-id="5bfb5-113">To narzędzie zawiera funkcje zaawansowane, takich jak funkcje importowania i eksportowania oraz możliwość testowania jednostek obsługi komunikatów i usług przekazywania.</span><span class="sxs-lookup"><span data-stu-id="5bfb5-113">The tool provides advanced features such as import/export functionality, and the ability to test messaging entities and relay services.</span></span> <span data-ttu-id="5bfb5-114">Pełne źródła Eksploratora magistrali usług i dokumentację można znaleźć w [GitHub](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="5bfb5-114">You can find the full Service Bus Explorer source and documentation on [GitHub](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bfb5-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5bfb5-115">Next steps</span></span>

<span data-ttu-id="5bfb5-116">Lokalizacje próbki są tutaj:</span><span class="sxs-lookup"><span data-stu-id="5bfb5-116">Sample locations are here:</span></span>

- [<span data-ttu-id="5bfb5-117">Przykłady GitHub</span><span class="sxs-lookup"><span data-stu-id="5bfb5-117">GitHub samples</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples)
- [<span data-ttu-id="5bfb5-118">Eksplorator usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="5bfb5-118">Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer)

<span data-ttu-id="5bfb5-119">Zobacz poniższe tematy zawierają omówienie pojęć związanych z usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5bfb5-119">See the following topics for conceptual overviews of Service Bus.</span></span>

* [<span data-ttu-id="5bfb5-120">Omówienie obsługi komunikatów w usłudze Service Bus</span><span class="sxs-lookup"><span data-stu-id="5bfb5-120">Service Bus messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="5bfb5-121">Architektura usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="5bfb5-121">Service Bus architecture</span></span>](service-bus-architecture.md)
* [<span data-ttu-id="5bfb5-122">Podstawy usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="5bfb5-122">Service Bus fundamentals</span></span>](service-bus-fundamentals-hybrid-solutions.md)

