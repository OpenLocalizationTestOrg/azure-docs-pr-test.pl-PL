---
title: "aaaOverview hello Azure Event Hubs .NET standardowych interfejsów API | Dokumentacja firmy Microsoft"
description: "Omówienie standardowy interfejs API .NET"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a173f8e4-556c-42b8-b856-838189f7e636
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: c97acecb35b69039e06ded7203c75fca41ce98f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="38a8b-103">Omówienie standardowy interfejs API .NET centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="38a8b-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="38a8b-104">Ten artykuł zawiera podsumowanie klucza hello interfejsów API klienta Event Hubs .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="38a8b-104">This article summarizes some of hello key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="38a8b-105">Obecnie nie istnieją dwie biblioteki klienta .NET Standard:</span><span class="sxs-lookup"><span data-stu-id="38a8b-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="38a8b-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="38a8b-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="38a8b-107">Ta biblioteka zawiera wszystkie operacje podstawowego środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="38a8b-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="38a8b-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="38a8b-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="38a8b-109">Ta biblioteka dodaje dodatkowe funkcje, które umożliwia rejestrowanie informacji o przetworzonych zdarzeń i jest hello Najprostszym sposobem tooread z Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="38a8b-109">This library adds additional functionality that allows for keeping track of processed events, and is hello easiest way tooread from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="38a8b-110">Klient centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="38a8b-110">Event Hubs client</span></span>
<span data-ttu-id="38a8b-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) jest hello obiektu podstawowego można użyć zdarzenia toosend tworzenie odbiorników i tooget informacje czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="38a8b-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is hello primary object you use toosend events, create receivers, and tooget run-time information.</span></span> <span data-ttu-id="38a8b-112">Ten klient jest tooa połączonego Centrum zdarzeń określonego i tworzy nowy punkt końcowy usługi Event Hubs toohello połączenia.</span><span class="sxs-lookup"><span data-stu-id="38a8b-112">This client is linked tooa particular event hub, and creates a new connection toohello Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="38a8b-113">Tworzenie klienta usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="38a8b-113">Create an Event Hubs client</span></span>
<span data-ttu-id="38a8b-114">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) obiekt jest tworzony z parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="38a8b-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="38a8b-115">Hello najprostszy sposób tooinstantiate nowy klient jest wyświetlany w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="38a8b-115">hello simplest way tooinstantiate a new client is shown in hello following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="38a8b-116">tooprogrammatically Edytuj parametry połączenia hello, możesz użyć hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) klasy, a następnie przekazać ciąg połączenia hello jako parametr zbyt[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="38a8b-116">tooprogrammatically edit hello connection string, you can use hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass hello connection string as a parameter too[EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="38a8b-117">Wysyłanie zdarzeń</span><span class="sxs-lookup"><span data-stu-id="38a8b-117">Send events</span></span>
<span data-ttu-id="38a8b-118">Centrum zdarzeń tooan toosend zdarzenia, użyj hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) klasy.</span><span class="sxs-lookup"><span data-stu-id="38a8b-118">toosend events tooan event hub, use hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="38a8b-119">Treść Hello musi być `byte` tablicy lub `byte` segmentu tablicy.</span><span class="sxs-lookup"><span data-stu-id="38a8b-119">hello body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="38a8b-120">Odbieranie zdarzeń</span><span class="sxs-lookup"><span data-stu-id="38a8b-120">Receive events</span></span>
<span data-ttu-id="38a8b-121">Witaj zalecany sposób tooreceive zdarzenia z usługi Event Hubs używa hello [hosta procesora zdarzeń](#event-processor-host-apis), zapewniające tooautomatically funkcji śledzić przesunięcie i informacji o partycji.</span><span class="sxs-lookup"><span data-stu-id="38a8b-121">hello recommended way tooreceive events from Event Hubs is using hello [Event Processor Host](#event-processor-host-apis), which provides functionality tooautomatically keep track of offset, and partition information.</span></span> <span data-ttu-id="38a8b-122">Istnieją jednak pewne sytuacje, w których można toouse elastyczność hello hello podstawowe usługi Event Hubs biblioteki tooreceive zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="38a8b-122">However, there are certain situations in which you may want toouse hello flexibility of hello core Event Hubs library tooreceive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="38a8b-123">Tworzenie odbiornika</span><span class="sxs-lookup"><span data-stu-id="38a8b-123">Create a receiver</span></span>
<span data-ttu-id="38a8b-124">Odbiorcy są wiązanej toospecific partycji, dlatego w celu tooreceive wszystkich zdarzeń w Centrum zdarzeń, konieczne będzie toocreate wiele wystąpień.</span><span class="sxs-lookup"><span data-stu-id="38a8b-124">Receivers are tied toospecific partitions, so in order tooreceive all events in an event hub, you will need toocreate multiple instances.</span></span> <span data-ttu-id="38a8b-125">Ogólnie rzecz biorąc jest informacji o partycji hello tooget dobrym rozwiązaniem programowo, zamiast kodować hello identyfikatorów partycji.</span><span class="sxs-lookup"><span data-stu-id="38a8b-125">Generally speaking, it is a good practice tooget hello partition information programatically, rather than hard-coding hello partition ids.</span></span> <span data-ttu-id="38a8b-126">Kolejność toodo, tak, można użyć hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) metody.</span><span class="sxs-lookup"><span data-stu-id="38a8b-126">In order toodo so, you can use hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list tookeep track of hello receivers
var receivers = new List<PartitionReceiver>();
// Use hello eventHubClient created above tooget hello runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over hello resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create hello receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add hello receiver toohello list
    receivers.Add(receiver);
}
```

<span data-ttu-id="38a8b-127">Ponieważ zdarzenia nigdy nie są usuwane z Centrum zdarzeń (i tylko wygaśnie), należy toospecify hello właściwy punkt początkowy.</span><span class="sxs-lookup"><span data-stu-id="38a8b-127">Since events are never removed from an event hub (and only expire), you need toospecify hello proper starting point.</span></span> <span data-ttu-id="38a8b-128">Witaj poniższy przykład przedstawia możliwych kombinacji.</span><span class="sxs-lookup"><span data-stu-id="38a8b-128">hello following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="38a8b-129">Korzystanie ze zdarzeń</span><span class="sxs-lookup"><span data-stu-id="38a8b-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call tooReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop tooprocess
    foreach (var ehEvent in ehEvents)
    {
        // Decode hello byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load hello custom property that we set in hello send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="38a8b-130">Interfejsy API hosta procesora zdarzeń</span><span class="sxs-lookup"><span data-stu-id="38a8b-130">Event Processor Host APIs</span></span>
<span data-ttu-id="38a8b-131">Te interfejsy API zapewniają odporność tooworker procesów, które mogą stać się niedostępne, przekazując partycje dostępne pracowników.</span><span class="sxs-lookup"><span data-stu-id="38a8b-131">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{event hub path/name}";
var storageConnectionString = "{Storage connection string}";
var storageContainerName = "{Storage account container name}";

var eventProcessorHost = new EventProcessorHost(
    ehEntityPath,
    PartitionReceiver.DefaultConsumerGroupName,
    ehConnectionString,
    storageConnectionString,
    storageContainerName);

// Start/register an EventProcessorHost
await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

// Disposes of hello Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="38a8b-132">Witaj poniżej znajduje się Przykładowa implementacja hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span><span class="sxs-lookup"><span data-stu-id="38a8b-132">hello following is a sample implementation of hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    public Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
        return Task.CompletedTask;
    }

    public Task OpenAsync(PartitionContext context)
    {
        Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
        return Task.CompletedTask;
    }

    public Task ProcessErrorAsync(PartitionContext context, Exception error)
    {
        Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
        return Task.CompletedTask;
    }

    public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (var eventData in messages)
        {
            var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
            Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
        }

        return context.CheckpointAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="38a8b-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="38a8b-133">Next steps</span></span>
<span data-ttu-id="38a8b-134">toolearn więcej informacji o scenariuszach usługi Event Hubs, odwiedź te linki:</span><span class="sxs-lookup"><span data-stu-id="38a8b-134">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="38a8b-135">Co to jest usługa Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="38a8b-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="38a8b-136">Interfejsy API centra zdarzeń dostępne</span><span class="sxs-lookup"><span data-stu-id="38a8b-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="38a8b-137">odwołania .NET API Hello są tutaj:</span><span class="sxs-lookup"><span data-stu-id="38a8b-137">hello .NET API references are here:</span></span>

* [<span data-ttu-id="38a8b-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="38a8b-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="38a8b-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="38a8b-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)