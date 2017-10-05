---
title: "Dostępność i spójność Azure Event Hubs | Dokumentacja firmy Microsoft"
description: "Jak zapewnić maksymalną ilość dostępności i spójności z usługi Azure Event Hubs przy użyciu partycji."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 681a9d1636d547492f6f827461c6b2494b918778
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="52790-103">Dostępność i spójności w usłudze Event Hubs</span><span class="sxs-lookup"><span data-stu-id="52790-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="52790-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="52790-104">Overview</span></span>
<span data-ttu-id="52790-105">Usługa Azure Event Hubs używa [partycjonowania modelu](event-hubs-features.md#partitions) do zwiększenia dostępności i paralelizacja w obrębie jednego zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="52790-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) to improve availability and parallelization within a single event hub.</span></span> <span data-ttu-id="52790-106">Na przykład jeśli Centrum zdarzeń ma cztery partycje i jedną z tych partycji jest przenoszone z jednego serwera do drugiego w operacji z równoważeniem obciążenia, użytkownik może nadal wysyłania i odbierania z trzech innych partycji.</span><span class="sxs-lookup"><span data-stu-id="52790-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server to another in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="52790-107">Ponadto posiadanie więcej partycji pozwala mieć więcej jednoczesnych czytników przetwarzania danych, poprawy z łącznej przepływności.</span><span class="sxs-lookup"><span data-stu-id="52790-107">Additionally, having more partitions enables you to have more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="52790-108">Opis skutków partycjonowanie i kolejność w rozproszonym systemie jest krytyczne aspektów projektu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="52790-108">Understanding the implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="52790-109">Aby wyjaśnić równowagę między porządkowania i dostępności, zobacz [Newtona zakończenia](https://en.wikipedia.org/wiki/CAP_theorem), znanej również jako Newtona Brewera firmy.</span><span class="sxs-lookup"><span data-stu-id="52790-109">To help explain the trade-off between ordering and availability, see the [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="52790-110">Ta Newtona omówiono wybór między spójności, dostępności i tolerancję partycji.</span><span class="sxs-lookup"><span data-stu-id="52790-110">This theorem discusses the choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="52790-111">Newtona firmy Brewera definiuje spójności i dostępności w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="52790-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="52790-112">Partycji tolerancji: możliwość dalszego przetwarzania danych, nawet jeśli wystąpi błąd partycji systemu przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="52790-112">Partition tolerance: the ability of a data processing system to continue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="52790-113">Dostępność: węzłem z systemem innym niż niepowodzenie zwraca odpowiedź uzasadnione w rozsądnym czasie (z nie błędów lub przekroczenia limitu czasu).</span><span class="sxs-lookup"><span data-stu-id="52790-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="52790-114">Spójności: odczytu gwarancji zwrócić ostatniego zapisu dla danego klienta.</span><span class="sxs-lookup"><span data-stu-id="52790-114">Consistency: a read is guaranteed to return the most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="52790-115">Tolerancja partycji</span><span class="sxs-lookup"><span data-stu-id="52790-115">Partition tolerance</span></span>
<span data-ttu-id="52790-116">Centra zdarzeń jest oparty na modelu danych podzielonej na partycje.</span><span class="sxs-lookup"><span data-stu-id="52790-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="52790-117">Liczba partycji w Centrum zdarzeń można skonfigurować podczas instalacji, ale nie można później zmienić tę wartość.</span><span class="sxs-lookup"><span data-stu-id="52790-117">You can configure the number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="52790-118">Ponieważ partycji musi być używany z usługą Event Hubs, trzeba podjąć decyzję o dostępności i spójności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="52790-118">Since you must use partitions with Event Hubs, you have to make a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="52790-119">Dostępność</span><span class="sxs-lookup"><span data-stu-id="52790-119">Availability</span></span>
<span data-ttu-id="52790-120">Najprostszym sposobem, aby rozpocząć pracę z usługą Event Hubs jest zachowanie domyślne.</span><span class="sxs-lookup"><span data-stu-id="52790-120">The simplest way to get started with Event Hubs is to use the default behavior.</span></span> <span data-ttu-id="52790-121">Jeśli tworzysz nową `EventHubClient` obiektu i użyj `Send` metody zdarzeń są automatycznie dystrybuowane między partycji w Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="52790-121">If you create a new `EventHubClient` object and use the `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="52790-122">Takie zachowanie umożliwia największą ilość czasu.</span><span class="sxs-lookup"><span data-stu-id="52790-122">This behavior allows for the greatest amount of up time.</span></span>

<span data-ttu-id="52790-123">Dla przypadków użycia, które wymagają maksymalny czas działania ten model jest preferowany.</span><span class="sxs-lookup"><span data-stu-id="52790-123">For use cases that require the maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="52790-124">Spójność</span><span class="sxs-lookup"><span data-stu-id="52790-124">Consistency</span></span>
<span data-ttu-id="52790-125">W niektórych scenariuszach uporządkowania zdarzeń może być istotne.</span><span class="sxs-lookup"><span data-stu-id="52790-125">In some scenarios, the ordering of events can be important.</span></span> <span data-ttu-id="52790-126">Na przykład możesz systemie zaplecza, aby przetworzyć polecenia aktualizacji przed polecenia delete.</span><span class="sxs-lookup"><span data-stu-id="52790-126">For example, you may want your back-end system to process an update command before a delete command.</span></span> <span data-ttu-id="52790-127">W takim przypadku można ustawić klucza partycji dla zdarzenia, lub użyj `PartitionSender` obiektu tylko do wysyłania zdarzeń do danej partycji.</span><span class="sxs-lookup"><span data-stu-id="52790-127">In this instance, you can either set the partition key on an event, or use a `PartitionSender` object to only send events to a certain partition.</span></span> <span data-ttu-id="52790-128">Daje to gwarancję, że kiedy te zdarzenia są odczytywane z partycji, są one odczytu w kolejności.</span><span class="sxs-lookup"><span data-stu-id="52790-128">Doing so ensures that when these events are read from the partition, they are read in order.</span></span>

<span data-ttu-id="52790-129">W tej konfiguracji należy pamiętać, że jeśli określonej partycji, do którego są wysyłane jest niedostępny, zostanie wyświetlony błąd odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="52790-129">With this configuration, keep in mind that if the particular partition to which you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="52790-130">Jako punkt odniesienia Jeśli nie masz koligacji do jednej partycji, usługę Event Hubs wysyła zdarzenie do następnej dostępnej partycji.</span><span class="sxs-lookup"><span data-stu-id="52790-130">As a point of comparison, if you do not have an affinity to a single partition, the Event Hubs service sends your event to the next available partition.</span></span>

<span data-ttu-id="52790-131">Agregowania zdarzeń jest możliwe rozwiązanie zapewniające porządkowanie zwiększają również czasu, w ramach wydarzenia przetwarzania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="52790-131">One possible solution to ensure ordering, while also maximizing up time, would be to aggregate events as part of your event processing application.</span></span> <span data-ttu-id="52790-132">Najprostszym sposobem, w tym celu jest sygnatury zdarzenie z właściwością numer sekwencji niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="52790-132">The easiest way to accomplish this is to stamp your event with a custom sequence number property.</span></span> <span data-ttu-id="52790-133">Poniższy kod przedstawia przykład:</span><span class="sxs-lookup"><span data-stu-id="52790-133">The following code shows an example:</span></span>

```csharp
// Get the latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="52790-134">W tym przykładzie wysyła zdarzenie do jednej z dostępnych partycji w Centrum zdarzeń i ustawia jej numer sekwencji z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="52790-134">This example sends your event to one of the available partitions in your event hub, and sets the corresponding sequence number from your application.</span></span> <span data-ttu-id="52790-135">To rozwiązanie wymaga stanu, które mają być przechowywane przez aplikację przetwarzania, ale zapewnia Twojej nadawców punktu końcowego, który jest mogą być dostępne.</span><span class="sxs-lookup"><span data-stu-id="52790-135">This solution requires state to be kept by your processing application, but gives your senders an endpoint that is more likely to be available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52790-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="52790-136">Next steps</span></span>
<span data-ttu-id="52790-137">Następujące linki pozwalają dowiedzieć się więcej na temat usługi Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="52790-137">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="52790-138">Omówienie usługi Event Hubs usługi</span><span class="sxs-lookup"><span data-stu-id="52790-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="52790-139">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="52790-139">Create an event hub</span></span>](event-hubs-create.md)
