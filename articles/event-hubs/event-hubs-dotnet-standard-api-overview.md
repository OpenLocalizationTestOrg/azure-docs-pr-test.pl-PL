---
title: "Omówienie usługi Azure Event hubs standardowych interfejsów API platformy .NET | Dokumentacja firmy Microsoft"
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
ms.date: 12/19/2017
ms.author: sethm
ms.openlocfilehash: 855f6e7f401621d7f923d68215ca880c05d38629
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/20/2017
---
# <a name="event-hubs-net-standard-api-overview"></a>Omówienie standardowy interfejs API .NET centra zdarzeń

W tym artykule przedstawiono niektóre kluczowe interfejsów API klienta Event Hubs .NET Standard. Obecnie nie istnieją dwie biblioteki klienta .NET Standard:

* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs): udostępnia wszystkie operacje podstawowego środowiska wykonawczego.
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor): dodaje dodatkowe funkcje, które umożliwia rejestrowanie informacji o przetworzonych zdarzeń i jest najprostszym sposobem odczytu z Centrum zdarzeń.

## <a name="event-hubs-client"></a>Klient centra zdarzeń

[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) jest podstawowym celem używane do wysyłania zdarzeń, tworzenie odbiorników i informacje czasu wykonywania. Ten klient jest połączony z koncentratorem konkretnego zdarzenia i tworzy nowe połączenie z punktem końcowym usługi Event Hubs.

### <a name="create-an-event-hubs-client"></a>Tworzenie klienta usługi Event Hubs

[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) obiekt jest tworzony z parametrów połączenia. W poniższym przykładzie przedstawiono to najprostszy sposób tworzenia wystąpienia nowego klienta:

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

Aby programowo Edytuj parametry połączenia, można użyć [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) klasy, a następnie przekazać ciąg połączenia jako parametr [EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a>Wysyłanie zdarzeń

Do wysyłania zdarzeń do Centrum zdarzeń, użyj [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) klasy. Treść musi być `byte` tablicy lub `byte` segmentu tablicy.

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a>Odbieranie zdarzeń

Zalecanym sposobem odbierania zdarzeń z usługi Event Hubs używa [hosta procesora zdarzeń](#event-processor-host-apis), który udostępnia funkcjonalność umożliwia automatyczne śledzenie informacji przesunięcia i partycji Centrum zdarzeń. Istnieją jednak pewne sytuacje, w których warto elastyczność podstawowej biblioteki usługi Event Hubs umożliwia odbieranie zdarzeń.

#### <a name="create-a-receiver"></a>Tworzenie odbiornika

Odbiorcy są również powiązane z określonymi partycjami, tak aby odbierać wszystkie zdarzenia w Centrum zdarzeń, należy utworzyć wiele wystąpień. Jest dobrym rozwiązaniem, aby uzyskać informacje o partycjach programowo, zamiast kodować identyfikatorów partycji. W tym celu można użyć [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) metody.

```csharp
// Create a list to keep track of the receivers
var receivers = new List<PartitionReceiver>();
// Use the eventHubClient created above to get the runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over the resulting partition IDs
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create the receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add the receiver to the list
    receivers.Add(receiver);
}
```

Ponieważ zdarzenia nigdy nie są usuwane z Centrum zdarzeń (i tylko wygaśnie), należy określić właściwego punktu początkowego. W poniższym przykładzie przedstawiono możliwe kombinacje:

```csharp
// partitionId is assumed to come from GetRuntimeInformationAsync()

// Using the constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a>Korzystanie ze zdarzeń

```csharp
// Receive a maximum of 100 messages in this call to ReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop to process
    foreach (var ehEvent in ehEvents)
    {
        // Decode the byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load the custom property that we set in the send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a>Interfejsy API hosta procesora zdarzeń

Te interfejsy API zapewniają odporność na procesach roboczych, które mogą stać się niedostępne, przekazując partycje dostępne pracowników.

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

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

// Disposes the Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

Poniżej przedstawiono przykładowe zastosowanie z [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).

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

## <a name="next-steps"></a>Kolejne kroki
Aby dowiedzieć się więcej o scenariuszach usługi Event Hubs, skorzystaj z następujących linków:

* [Co to jest usługa Azure Event Hubs?](event-hubs-what-is-event-hubs.md)
* [Interfejsy API centra zdarzeń dostępne](event-hubs-api-overview.md)

Odwołania .NET API są tutaj:

* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)