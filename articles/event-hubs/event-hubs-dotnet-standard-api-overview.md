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
# <a name="event-hubs-net-standard-api-overview"></a>Omówienie standardowy interfejs API .NET centra zdarzeń
Ten artykuł zawiera podsumowanie klucza hello interfejsów API klienta Event Hubs .NET Standard. Obecnie nie istnieją dwie biblioteki klienta .NET Standard:
* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
  *  Ta biblioteka zawiera wszystkie operacje podstawowego środowiska wykonawczego.
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)
  * Ta biblioteka dodaje dodatkowe funkcje, które umożliwia rejestrowanie informacji o przetworzonych zdarzeń i jest hello Najprostszym sposobem tooread z Centrum zdarzeń.

## <a name="event-hubs-client"></a>Klient centra zdarzeń
[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) jest hello obiektu podstawowego można użyć zdarzenia toosend tworzenie odbiorników i tooget informacje czasu wykonywania. Ten klient jest tooa połączonego Centrum zdarzeń określonego i tworzy nowy punkt końcowy usługi Event Hubs toohello połączenia.

### <a name="create-an-event-hubs-client"></a>Tworzenie klienta usługi Event Hubs
[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) obiekt jest tworzony z parametrów połączenia. Hello najprostszy sposób tooinstantiate nowy klient jest wyświetlany w hello poniższy przykład:

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

tooprogrammatically Edytuj parametry połączenia hello, możesz użyć hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) klasy, a następnie przekazać ciąg połączenia hello jako parametr zbyt[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a>Wysyłanie zdarzeń
Centrum zdarzeń tooan toosend zdarzenia, użyj hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) klasy. Treść Hello musi być `byte` tablicy lub `byte` segmentu tablicy.

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a>Odbieranie zdarzeń
Witaj zalecany sposób tooreceive zdarzenia z usługi Event Hubs używa hello [hosta procesora zdarzeń](#event-processor-host-apis), zapewniające tooautomatically funkcji śledzić przesunięcie i informacji o partycji. Istnieją jednak pewne sytuacje, w których można toouse elastyczność hello hello podstawowe usługi Event Hubs biblioteki tooreceive zdarzenia.

#### <a name="create-a-receiver"></a>Tworzenie odbiornika
Odbiorcy są wiązanej toospecific partycji, dlatego w celu tooreceive wszystkich zdarzeń w Centrum zdarzeń, konieczne będzie toocreate wiele wystąpień. Ogólnie rzecz biorąc jest informacji o partycji hello tooget dobrym rozwiązaniem programowo, zamiast kodować hello identyfikatorów partycji. Kolejność toodo, tak, można użyć hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) metody.

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

Ponieważ zdarzenia nigdy nie są usuwane z Centrum zdarzeń (i tylko wygaśnie), należy toospecify hello właściwy punkt początkowy. Witaj poniższy przykład przedstawia możliwych kombinacji.

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a>Korzystanie ze zdarzeń
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

## <a name="event-processor-host-apis"></a>Interfejsy API hosta procesora zdarzeń
Te interfejsy API zapewniają odporność tooworker procesów, które mogą stać się niedostępne, przekazując partycje dostępne pracowników.

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

Witaj poniżej znajduje się Przykładowa implementacja hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).

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

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji o scenariuszach usługi Event Hubs, odwiedź te linki:

* [Co to jest usługa Azure Event Hubs?](event-hubs-what-is-event-hubs.md)
* [Interfejsy API centra zdarzeń dostępne](event-hubs-api-overview.md)

odwołania .NET API Hello są tutaj:

* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)