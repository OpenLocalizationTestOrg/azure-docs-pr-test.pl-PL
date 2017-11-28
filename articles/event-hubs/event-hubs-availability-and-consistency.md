---
title: "aaaAvailability i spójność Azure Event Hubs | Dokumentacja firmy Microsoft"
description: "Jak partycje tooprovide hello maksymalną ilość dostępności i spójności z przy użyciu usługi Azure Event Hubs."
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
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="7cfd6-103">Dostępność i spójności w usłudze Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7cfd6-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="7cfd6-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7cfd6-104">Overview</span></span>
<span data-ttu-id="7cfd6-105">Usługa Azure Event Hubs używa [partycjonowania modelu](event-hubs-features.md#partitions) tooimprove dostępności i paralelizacja w obrębie jednego zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) tooimprove availability and parallelization within a single event hub.</span></span> <span data-ttu-id="7cfd6-106">Na przykład jeśli Centrum zdarzeń zawiera cztery partycje, a jeden z tych partycji jest przenoszone z jednego serwera tooanother w operacji z równoważeniem obciążenia, użytkownik może nadal wysyłania i odbierania z trzech innych partycji.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server tooanother in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="7cfd6-107">Ponadto posiadanie więcej partycji umożliwia toohave więcej jednoczesnych czytników przetwarzania danych, poprawy z łącznej przepływności.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-107">Additionally, having more partitions enables you toohave more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="7cfd6-108">Opis skutków hello partycjonowanie i kolejność w rozproszonym systemie jest krytyczne aspektów projektu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-108">Understanding hello implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="7cfd6-109">toohelp wyjaśnić hello kompromis między porządkowania i dostępności, zobacz hello [Newtona zakończenia](https://en.wikipedia.org/wiki/CAP_theorem), znanej również jako Newtona Brewera firmy.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-109">toohelp explain hello trade-off between ordering and availability, see hello [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="7cfd6-110">Ta Newtona omówiono hello wybór między spójności, dostępności i tolerancję partycji.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-110">This theorem discusses hello choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="7cfd6-111">Newtona firmy Brewera definiuje spójności i dostępności w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="7cfd6-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="7cfd6-112">Partycji tolerancji: hello możliwości toocontinue systemu przetwarzania danych, przetwarzanie danych, nawet jeśli wystąpi błąd partycji.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-112">Partition tolerance: hello ability of a data processing system toocontinue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="7cfd6-113">Dostępność: węzłem z systemem innym niż niepowodzenie zwraca odpowiedź uzasadnione w rozsądnym czasie (z nie błędów lub przekroczenia limitu czasu).</span><span class="sxs-lookup"><span data-stu-id="7cfd6-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="7cfd6-114">Spójności: odczytu jest gwarantowana tooreturn hello ostatniego zapisu dla danego klienta.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-114">Consistency: a read is guaranteed tooreturn hello most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="7cfd6-115">Tolerancja partycji</span><span class="sxs-lookup"><span data-stu-id="7cfd6-115">Partition tolerance</span></span>
<span data-ttu-id="7cfd6-116">Centra zdarzeń jest oparty na modelu danych podzielonej na partycje.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="7cfd6-117">Witaj liczby partycji w Centrum zdarzeń można skonfigurować podczas instalacji, ale nie można później zmienić tę wartość.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-117">You can configure hello number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="7cfd6-118">Ponieważ partycje musi korzystać z usługą Event Hubs, masz toomake decyzji o dostępności i spójności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-118">Since you must use partitions with Event Hubs, you have toomake a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="7cfd6-119">Dostępność</span><span class="sxs-lookup"><span data-stu-id="7cfd6-119">Availability</span></span>
<span data-ttu-id="7cfd6-120">Hello najprostszy sposób tooget wprowadzenie do usługi Event Hubs jest toouse hello domyślne zachowanie.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-120">hello simplest way tooget started with Event Hubs is toouse hello default behavior.</span></span> <span data-ttu-id="7cfd6-121">Jeśli tworzysz nową `EventHubClient` obiektu i użyj hello `Send` metody zdarzeń są automatycznie dystrybuowane między partycji w Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-121">If you create a new `EventHubClient` object and use hello `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="7cfd6-122">Takie zachowanie umożliwia hello największą ilość czasu.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-122">This behavior allows for hello greatest amount of up time.</span></span>

<span data-ttu-id="7cfd6-123">Dla przypadków użycia, które wymagają hello maksymalny czas działania ten model jest preferowany.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-123">For use cases that require hello maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="7cfd6-124">Spójność</span><span class="sxs-lookup"><span data-stu-id="7cfd6-124">Consistency</span></span>
<span data-ttu-id="7cfd6-125">W niektórych scenariuszach hello uporządkowania zdarzeń może być istotne.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-125">In some scenarios, hello ordering of events can be important.</span></span> <span data-ttu-id="7cfd6-126">Na przykład można tooprocess Twojego systemu zaplecza polecenie aktualizacji przed polecenia delete.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-126">For example, you may want your back-end system tooprocess an update command before a delete command.</span></span> <span data-ttu-id="7cfd6-127">W takim przypadku można ustawić klucz partycji hello na zdarzenie, lub użyj `PartitionSender` tooonly obiektu wysyłania zdarzeń tooa partycji.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-127">In this instance, you can either set hello partition key on an event, or use a `PartitionSender` object tooonly send events tooa certain partition.</span></span> <span data-ttu-id="7cfd6-128">Daje to gwarancję, że gdy zdarzenia te są odczytywane z hello partycji, są one odczytu w kolejności.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-128">Doing so ensures that when these events are read from hello partition, they are read in order.</span></span>

<span data-ttu-id="7cfd6-129">W tej konfiguracji należy pamiętać, że jeśli hello toowhich określonej partycji, który jest wysyłany jest niedostępny, zostanie wyświetlony błąd odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-129">With this configuration, keep in mind that if hello particular partition toowhich you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="7cfd6-130">Jako punkt odniesienia Jeśli nie masz jednej partycji tooa koligacji hello usługi Event Hubs wysyła zdarzenia toohello dalej partycja dostępne.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-130">As a point of comparison, if you do not have an affinity tooa single partition, hello Event Hubs service sends your event toohello next available partition.</span></span>

<span data-ttu-id="7cfd6-131">Jeden tooensure możliwe rozwiązanie porządkowanie zwiększają również czasu, będzie tooaggregate zdarzenia w ramach wydarzenia przetwarzania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-131">One possible solution tooensure ordering, while also maximizing up time, would be tooaggregate events as part of your event processing application.</span></span> <span data-ttu-id="7cfd6-132">Najprostszym sposobem tooaccomplish Witaj, to jest zdarzenie z właściwością numer sekwencji niestandardowych toostamp.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-132">hello easiest way tooaccomplish this is toostamp your event with a custom sequence number property.</span></span> <span data-ttu-id="7cfd6-133">przykład Hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="7cfd6-133">hello following code shows an example:</span></span>

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="7cfd6-134">W tym przykładzie wysyła tooone Twojego zdarzeń hello dostępnych partycji w Centrum zdarzeń i ustawia jej numer sekwencji hello z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-134">This example sends your event tooone of hello available partitions in your event hub, and sets hello corresponding sequence number from your application.</span></span> <span data-ttu-id="7cfd6-135">To rozwiązanie wymaga toobe stanu zachowana przez aplikację przetwarzania, ale zapewnia Twojej nadawców punktu końcowego, który jest bardziej prawdopodobne toobe dostępne.</span><span class="sxs-lookup"><span data-stu-id="7cfd6-135">This solution requires state toobe kept by your processing application, but gives your senders an endpoint that is more likely toobe available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cfd6-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7cfd6-136">Next steps</span></span>
<span data-ttu-id="7cfd6-137">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="7cfd6-137">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="7cfd6-138">Omówienie usługi Event Hubs usługi</span><span class="sxs-lookup"><span data-stu-id="7cfd6-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="7cfd6-139">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="7cfd6-139">Create an event hub</span></span>](event-hubs-create.md)
