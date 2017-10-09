---
title: "aaaReceive zdarzenia z usługi Azure Event Hubs przy użyciu platformy .NET Standard | Dokumentacja firmy Microsoft"
description: "Rozpocząć odbieranie komunikatów z hello EventProcessorHost w .NET Standard"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a>Rozpocząć odbieranie komunikatów z hello hosta procesora zdarzeń w .NET Standard

> [!NOTE]
> Ten przykład jest dostępny na [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).

Ten samouczek pokazuje, jak toowrite .NET Core konsoli aplikacji, która odbiera komunikaty z Centrum zdarzeń za pomocą **EventProcessorHost**. Możesz uruchomić hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) rozwiązania jako-zastępując hello ciągi wartości konta koncentratora i przechowywania zdarzeń. Lub możesz wykonać hello czynnościach w ramach tego samouczka toocreate własnych.

## <a name="prerequisites"></a>Wymagania wstępne

* [Microsoft Visual Studio 2015 lub 2017](http://www.visualstudio.com). obsługiwane jest również Hello przykłady w tym samouczku 2017 usługi Visual Studio, ale programu Visual Studio 2015.
* [.NET core Visual Studio 2015 lub narzędzia 2017](http://www.microsoft.com/net/core).
* Subskrypcja platformy Azure.
* Przestrzeń nazw usługi Azure Event Hubs.
* Konto usługi Azure Storage.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Tworzenie przestrzeni nazw usługi Event Hubs i centrum zdarzeń  

Witaj pierwszym krokiem jest toouse hello [portalu Azure](https://portal.azure.com) toocreate obszaru nazw hello centra zdarzeń wpisz i uzyskać poświadczenia zarządzania, czy aplikacja wymaga toocommunicate z Centrum zdarzeń hello hello. toocreate przestrzeni nazw i Centrum zdarzeń, wykonaj procedurę hello w [w tym artykule](event-hubs-create.md), a następnie kontynuować hello następujące kroki.  

## <a name="create-an-azure-storage-account"></a>Tworzenie konta usługi Azure Storage  

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).  
2. W okienku nawigacji po lewej stronie powitania hello portalu kliknij **nowy**, kliknij przycisk **magazynu**, a następnie kliknij przycisk **konta magazynu**.  
3. Wypełnij pola hello w bloku konto magazynu hello, a następnie kliknij przycisk **Utwórz**.

    ![Tworzenie konta magazynu][1]

4. Po hello **wdrożeń zakończyło się pomyślnie** komunikatów, kliknij nazwę hello hello nowe konto magazynu. W hello **Essentials** bloku, kliknij przycisk **obiekty BLOB**. Gdy hello **usługa Blob** zostanie otwarty blok, kliknij przycisk **+ kontener** u góry hello. Nadaj nazwę kontenera hello, a następnie zamknij hello **usługa Blob** bloku.  
5. Kliknij przycisk **klucze dostępu** hello po lewej stronie bloku i skopiuj hello nazwa kontenera magazynu hello, hello konta magazynu i wartości hello **klucz1**. Zapisz te wartości tooNotepad lub tymczasowej lokalizacji.  

## <a name="create-a-console-application"></a>Tworzenie aplikacji konsolowej

Uruchom program Visual Studio. Z hello **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**. Tworzenie aplikacji konsoli .NET Core.

![Nowy projekt][2]

## <a name="add-hello-event-hubs-nuget-package"></a>Dodaj pakiet NuGet centra zdarzeń hello

Dodaj hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) i [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard NuGet pakiety tooyour projektu biblioteki wykonaj następujące czynności: 

1. Kliknij prawym przyciskiem myszy hello nowo utworzonego projektu i wybierz **Zarządzaj pakietami NuGet**.
2. Kliknij przycisk hello **Przeglądaj** kartę, a następnie wyszukaj "Microsoft.Azure.EventHubs" i wybierz hello **Microsoft.Azure.EventHubs** pakietu. Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij to okno dialogowe.
3. Powtórz kroki 1 i 2, a następnie zainstaluj hello **Microsoft.Azure.EventHubs.Processor** pakietu.

## <a name="implement-hello-ieventprocessor-interface"></a>Zaimplementuj interfejs IEventProcessor hello

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**. Nazwa nowej klasy hello **SimpleEventProcessor**.

2. Otwórz plik SimpleEventProcessor.cs hello i dodaj następujące hello `using` toohello instrukcje na początku pliku hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. Implementowanie hello `IEventProcessor` interfejsu. Zastąp całą zawartość hello hello `SimpleEventProcessor` klasy z hello następującego kodu:

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

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a>Napisanie metody konsoli głównej, która używa hello SimpleEventProcessor klasy tooreceive komunikatów

1. Dodaj następujące hello `using` toohello instrukcje na początku pliku Program.cs hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. Dodaj toohello stałe `Program` klasy parametry połączenia Centrum zdarzeń hello, nazwy Centrum zdarzeń, nazwa kontenera konta magazynu, nazwa konta magazynu i klucza konta magazynu. Dodaj powitania po kod, zastępując symbole zastępcze hello z odpowiednimi wartościami.

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. Dodaj nową metodę o nazwie `MainAsync` toohello `Program` klasy, w następujący sposób:

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. Dodaj powitania po wierszu kodu toohello `Main` metody:

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    Oto jak powinien wyglądać plik Program.cs:

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. Uruchom hello program i upewnij się, że nie ma żadnych błędów.

Gratulacje! Teraz Odebrano wiadomości z Centrum zdarzeń za pomocą hello hosta procesora zdarzeń.

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md)
* [Tworzenie centrum zdarzeń](event-hubs-create.md)
* [Event Hubs — często zadawane pytania](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
