---
title: "aaaWhat to Azure Event Hubs i dlaczego warto jej używać | Dokumentacja firmy Microsoft"
description: "Omówienie i wprowadzenie tooAzure usługi Event Hubs — wprowadzanie danych telemetrycznych skali chmury z witryn sieci Web, aplikacji i urządzeń"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a><span data-ttu-id="e49e2-103">Co to jest usługa Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="e49e2-103">What is Event Hubs?</span></span>

<span data-ttu-id="e49e2-104">Azure Event Hubs to wysoce skalowalna platforma do pobierania zdarzeń i strumieniowego przesyłania danych, która umożliwia odbieranie i przetwarzanie milionów zdarzeń na sekundę.</span><span class="sxs-lookup"><span data-stu-id="e49e2-104">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service capable of receiving and processing millions of events per second.</span></span> <span data-ttu-id="e49e2-105">Usługa Event Hubs pozwala przetwarzać i przechowywać zdarzenia, dane lub dane telemetryczne generowane przez rozproszone oprogramowanie i urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e49e2-105">Event Hubs can process and store events, data, or telemetry produced by distributed software and devices.</span></span> <span data-ttu-id="e49e2-106">Dane wysyłane tooan Centrum zdarzeń można je przekształcać i przechowywać za pomocą dowolnego dostawcy analiz w czasie rzeczywistym lub kart przetwarzania wsadowego i magazynowania.</span><span class="sxs-lookup"><span data-stu-id="e49e2-106">Data sent tooan event hub can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="e49e2-107">Z hello możliwości tooprovide [możliwości publikowania / subskrypcji](https://msdn.microsoft.com/library/aa560414.aspx) z małych opóźnień i bardzo dużej skali, usługa Event Hubs służy jako hello "na narastania" dla danych Big Data.</span><span class="sxs-lookup"><span data-stu-id="e49e2-107">With hello ability tooprovide [publish-subscribe capabilities](https://msdn.microsoft.com/library/aa560414.aspx) with low latency and at massive scale, Event Hubs serves as hello "on ramp" for Big Data.</span></span>

## <a name="why-use-event-hubs"></a><span data-ttu-id="e49e2-108">Dlaczego warto korzystać z usługi Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="e49e2-108">Why use Event Hubs?</span></span>

<span data-ttu-id="e49e2-109">Możliwości obsługi zdarzeń i telemetrii w usłudze Event Hubs czynią ją szczególnie użyteczną do:</span><span class="sxs-lookup"><span data-stu-id="e49e2-109">Event Hubs event and telemetry handling capabilities make it especially useful for:</span></span>

* <span data-ttu-id="e49e2-110">instrumentacji aplikacji</span><span class="sxs-lookup"><span data-stu-id="e49e2-110">Application instrumentation</span></span>
* <span data-ttu-id="e49e2-111">przetwarzania czynności użytkownika lub przepływów pracy</span><span class="sxs-lookup"><span data-stu-id="e49e2-111">User experience or workflow processing</span></span>
* <span data-ttu-id="e49e2-112">scenariuszy Internetu rzeczy (IoT)</span><span class="sxs-lookup"><span data-stu-id="e49e2-112">Internet of Things (IoT) scenarios</span></span>

<span data-ttu-id="e49e2-113">Usługa Event Hubs umożliwia na przykład śledzenie zachowania w aplikacjach mobilnych, gromadzenie informacji o ruchu z farmy serwerów w Internecie, przechwytywanie zdarzeń w grach na konsole i zbieranie danych telemetrycznych z maszyn przemysłowych, podłączonych pojazdów lub innych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="e49e2-113">For example, Event Hubs enables behavior tracking in mobile apps, traffic information from web farms, in-game event capture in console games, or telemetry collected from industrial machines, connected vehicles, or other devices.</span></span>

## <a name="azure-event-hubs-overview"></a><span data-ttu-id="e49e2-114">Omówienie usługi Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e49e2-114">Azure Event Hubs overview</span></span>

<span data-ttu-id="e49e2-115">Witaj typową rolą usługi Event hubs w architekturze rozwiązań jest hello "drzwi wejściowe" dla potoku zdarzeń, często nazywane *systemem zbierania zdarzeń*.</span><span class="sxs-lookup"><span data-stu-id="e49e2-115">hello common role that Event Hubs plays in solution architectures is hello "front door" for an event pipeline, often called an *event ingestor*.</span></span> <span data-ttu-id="e49e2-116">Systemem zbierania zdarzeń to składnik lub usługa, która znajduje się między wydawcami zdarzeń, a zdarzenie konsumentów toodecouple hello Wytwarzanie strumienia zdarzeń od użycia tych zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="e49e2-116">An event ingestor is a component or service that sits between event publishers and event consumers toodecouple hello production of an event stream from hello consumption of those events.</span></span> <span data-ttu-id="e49e2-117">Witaj poniższym rysunku przedstawiono tej architektury:</span><span class="sxs-lookup"><span data-stu-id="e49e2-117">hello following figure depicts this architecture:</span></span>

![Usługa Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

<span data-ttu-id="e49e2-119">Usługa Event Hubs umożliwia obsługę strumienia komunikatów, ale jej właściwości różnią się od tradycyjnych metod przesyłania komunikatów w przedsiębiorstwie.</span><span class="sxs-lookup"><span data-stu-id="e49e2-119">Event Hubs provides message stream handling capability but has characteristics that are different from traditional enterprise messaging.</span></span> <span data-ttu-id="e49e2-120">Możliwości usługi Event Hubs są zbudowane wokół scenariuszy wysokiej przepływności i przetwarzania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="e49e2-120">Event Hubs capabilities are built around high throughput and event processing scenarios.</span></span> <span data-ttu-id="e49e2-121">W efekcie Usługa Event Hubs różni się od [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) wiadomości, a nie implementuje niektórych możliwości hello, które są dostępne dla [komunikatów usługi Service Bus](/azure/service-bus-messaging/) jednostki, na przykład tematów.</span><span class="sxs-lookup"><span data-stu-id="e49e2-121">As such, Event Hubs is different from [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) messaging, and does not implement some of hello capabilities that are available for [Service Bus messaging](/azure/service-bus-messaging/) entities, such as topics.</span></span>

## <a name="event-hubs-features"></a><span data-ttu-id="e49e2-122">Funkcje usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e49e2-122">Event Hubs features</span></span>

<span data-ttu-id="e49e2-123">Centra zdarzeń zawiera następujące kluczowe elementy hello:</span><span class="sxs-lookup"><span data-stu-id="e49e2-123">Event Hubs contains hello following key elements:</span></span>

- <span data-ttu-id="e49e2-124">[**Wydawcy producentów zdarzeń**](event-hubs-features.md#event-publishers): jednostki, która wysyła Centrum zdarzeń tooan danych.</span><span class="sxs-lookup"><span data-stu-id="e49e2-124">[**Event producers/publishers**](event-hubs-features.md#event-publishers): An entity that sends data tooan event hub.</span></span> <span data-ttu-id="e49e2-125">Zdarzenia są publikowane za pośrednictwem protokołu AMQP 1.0 lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e49e2-125">An event is published via AMQP 1.0 or HTTPS.</span></span>
- <span data-ttu-id="e49e2-126">[**Przechwyć**](event-hubs-features.md#capture): umożliwia toocapture Event Hubs strumieniowego przesyłania danych i zapisze go na koncie magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e49e2-126">[**Capture**](event-hubs-features.md#capture): Enables you toocapture Event Hubs streaming data and store it in an Azure Blob storage account.</span></span>
- <span data-ttu-id="e49e2-127">[**Partycje**](event-hubs-features.md#partitions): włącza tooonly każdego konsumenta odczyt konkretny podzbiór, lub partycję, hello strumienia zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="e49e2-127">[**Partitions**](event-hubs-features.md#partitions): Enables each consumer tooonly read a specific subset, or partition, of hello event stream.</span></span>
- <span data-ttu-id="e49e2-128">[**Tokeny sygnatury dostępu Współdzielonego**](event-hubs-features.md#sas-tokens): identyfikuje i uwierzytelnia hello wydawca zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="e49e2-128">[**SAS tokens**](event-hubs-features.md#sas-tokens): Identifies and authenticates hello event publisher.</span></span>
- <span data-ttu-id="e49e2-129">[**Odbiorca zdarzenia**](event-hubs-features.md#event-consumers): jednostka, która odczytuje dane zdarzenia z centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="e49e2-129">[**Event consumers**](event-hubs-features.md#event-consumers): An entity that reads event data from an event hub.</span></span> <span data-ttu-id="e49e2-130">Odbiorcy zdarzenia nawiązują połączenia za pomocą protokołu AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="e49e2-130">Event consumers connect via AMQP 1.0.</span></span> 
- <span data-ttu-id="e49e2-131">[**Grupy konsumentów**](event-hubs-features.md#consumer-groups): zapewnia każdego wielu korzystanie z aplikacji przy użyciu osobny widok strumienia zdarzeń hello, włączanie tych tooact konsumentów niezależnie.</span><span class="sxs-lookup"><span data-stu-id="e49e2-131">[**Consumer groups**](event-hubs-features.md#consumer-groups): Provides each multiple consuming application with a separate view of hello event stream, enabling those consumers tooact independently.</span></span>
- <span data-ttu-id="e49e2-132">[**Jednostki przepływności**](event-hubs-features.md#capacity): zakupione wcześniej jednostki wydajności.</span><span class="sxs-lookup"><span data-stu-id="e49e2-132">[**Throughput units**](event-hubs-features.md#capacity): Pre-purchased units of capacity.</span></span> <span data-ttu-id="e49e2-133">Jedna partycja ma maksymalną skalę wynoszącą jedną jednostkę przepływności.</span><span class="sxs-lookup"><span data-stu-id="e49e2-133">A single partition has a maximum scale of 1 throughput unit.</span></span>

<span data-ttu-id="e49e2-134">Aby uzyskać szczegółowe informacje techniczne na temat tych i innych funkcji usługi Event Hubs, zobacz hello [Przegląd funkcji usługi Event Hubs](event-hubs-features.md).</span><span class="sxs-lookup"><span data-stu-id="e49e2-134">For technical details about these and other Event Hubs features, see hello [Event Hubs features overview](event-hubs-features.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e49e2-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e49e2-135">Next steps</span></span>

<span data-ttu-id="e49e2-136">Aby uzyskać szczegółowe informacje o cenach za korzystanie z usługi Event Hubs, zobacz [Usługa Event Hubs — cennik](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="e49e2-136">For detailed Event Hubs pricing information, see [Event Hubs Pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span>

<span data-ttu-id="e49e2-137">Aby uzyskać więcej informacji na temat usługi Event Hubs odwiedź hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="e49e2-137">For more information about Event Hubs, visit hello following links:</span></span>

* <span data-ttu-id="e49e2-138">Rozpocznij pracę od [samouczka dotyczącego usługi Event Hubs](event-hubs-dotnet-standard-getstarted-send.md)</span><span class="sxs-lookup"><span data-stu-id="e49e2-138">Get started with an [Event Hubs tutorial](event-hubs-dotnet-standard-getstarted-send.md)</span></span>
* [<span data-ttu-id="e49e2-139">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="e49e2-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)
* [<span data-ttu-id="e49e2-140">Przykładowe aplikacje korzystające z usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e49e2-140">Sample applications that use Event Hubs</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

