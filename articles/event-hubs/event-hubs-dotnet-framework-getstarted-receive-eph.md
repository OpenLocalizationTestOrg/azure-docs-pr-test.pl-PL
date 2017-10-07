---
title: ".NET Framework hello aaaReceive zdarzenia z usługi Azure Event Hubs przy użyciu | Dokumentacja firmy Microsoft"
description: "Wykonaj ten samouczek tooreceive zdarzenia z usługi Azure Event Hubs przy użyciu hello .NET Framework."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: a88c3feeacfd3de9622dbb86e25222e861750204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a>Odbieranie zdarzeń z usługi Azure Event Hubs przy użyciu hello .NET Framework

## <a name="introduction"></a>Wprowadzenie

Event Hubs to usługa, która przetwarza duże ilości danych zdarzeń (danych telemetrycznych) z podłączonych urządzeń i aplikacji. Po zebraniu danych do usługi Event Hubs, można przechowywać dane hello przy użyciu klastra magazynu lub przekształcać je za pomocą dostawcy analiz w czasie rzeczywistym. Ta możliwość zbierania i przetwarzania zdarzeń na dużą skalę jest kluczowym składnikiem architektur nowoczesnych aplikacji, w tym hello Internetu rzeczy (IoT).

Ten samouczek pokazuje, jak toowrite .NET Framework konsoli aplikacji, która odbiera komunikaty z Centrum zdarzeń za pomocą hello  **[hosta procesora zdarzeń][EventProcessorHost]**. zdarzenia toosend przy użyciu hello .NET Framework, zobacz hello [wysyłać zdarzenia tooAzure Event Hubs przy użyciu hello .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) artykułu, lub kliknij odpowiedni język wysyłania hello w tabeli po lewej stronie powitania treści.

Witaj [hosta procesora zdarzeń] [ EventProcessorHost] jest klasą .NET, która upraszcza odbieranie zdarzeń z usługi event hubs przez zarządzanie trwałymi punktami kontrolnymi i równoległymi odbiorami z tych usług. Przy użyciu hello [hosta procesora zdarzeń][Event Processor Host], można podzielić zdarzenia między wieloma odbiornikami, nawet w przypadku hostowania w różnych węzłach. W tym przykładzie pokazano sposób toouse hello [hosta procesora zdarzeń] [ EventProcessorHost] dla jednego odbiornika. Witaj [skalowania przetwarzania zdarzeń] [ Scale out Event Processing with Event Hubs] przykładowe pokazuje, jak toouse hello [hosta procesora zdarzeń] [ EventProcessorHost] z wieloma odbiornikami.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka należy hello następujące wymagania wstępne:

* [Program Microsoft Visual Studio w wersji 2015 lub nowszej](http://visualstudio.com). zrzuty ekranu Hello w tym samouczku za pomocą programu Visual Studio 2017 r.
* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Tworzenie przestrzeni nazw usługi Event Hubs i centrum zdarzeń

pierwszym krokiem Hello jest toouse hello [portalu Azure](https://portal.azure.com) toocreate a przestrzeń nazw wpisz centra zdarzeń i uzyskać poświadczenia zarządzania aplikacja wymaga toocommunicate z Centrum zdarzeń hello hello. toocreate przestrzeni nazw i Centrum zdarzeń, wykonaj procedurę hello w [w tym artykule](event-hubs-create.md), następnie kontynuować hello, wykonaj następujące kroki w tym samouczku.

## <a name="create-an-azure-storage-account"></a>Tworzenie konta usługi Azure Storage

Witaj toouse [hosta procesora zdarzeń][EventProcessorHost], musi mieć [konta magazynu Azure][Azure Storage account]:

1. Zaloguj się na toohello [portalu Azure][Azure portal]i kliknij przycisk **nowy** na powitania lewym górnym rogu ekranu hello.
2. Kliknij pozycję **Magazyn**, a następnie pozycję **Konto magazynu**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. W hello **utworzyć konto magazynu** bloku, wpisz nazwę konta magazynu hello. Wybierz subskrypcję platformy Azure, lokalizacji i grupy zasobów w toocreate hello zasobów. Następnie kliknij pozycję **Utwórz**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. Na liście hello kont magazynu kliknij hello nowo utworzone konto magazynu.
5. W bloku konto magazynu hello, kliknij przycisk **klucze dostępu**. Skopiuj wartość hello **klucz1** toouse w dalszej części tego samouczka.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a>Tworzenie aplikacji konsolowej odbiorcy

1. W programie Visual Studio Utwórz nowy projekt Visual C# pulpitu aplikacji przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **odbiornika**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **odbiornika** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet dla rozwiązania**.
3. Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus Event Hub - EventProcessorHost`. Kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    Pobieranie programu Visual Studio, instaluje i dodaje toohello odwołanie [Centrum zdarzeń usługi Azure Service Bus — pakiet EventProcessorHost NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), ze wszystkimi zależnościami.
4. Powitania kliknij prawym przyciskiem myszy **odbiornika** projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**. Nazwa nowej klasy hello **SimpleEventProcessor**, a następnie kliknij przycisk **Dodaj** toocreate hello klasy.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. Dodaj następujące instrukcje u góry pliku SimpleEventProcessor.cs hello hello hello:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  Następnie zastąp hello następującego kodu dla treści hello hello klasy:
    
  ```csharp
  class SimpleEventProcessor : IEventProcessor
  {
    Stopwatch checkpointStopWatch;
    
    async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
    
    Task IEventProcessor.OpenAsync(PartitionContext context)
    {
        Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
        this.checkpointStopWatch = new Stopwatch();
        this.checkpointStopWatch.Start();
        return Task.FromResult<object>(null);
    }
    
    async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData eventData in messages)
        {
            string data = Encoding.UTF8.GetString(eventData.GetBytes());
    
            Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                context.Lease.PartitionId, data));
        }
    
        //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
        if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
        {
            await context.CheckpointAsync();
            this.checkpointStopWatch.Restart();
        }
    }
  }
  ```
    
  Ta klasa jest wywoływana przez hello **EventProcessorHost** tooprocess zdarzeń odebranych z Centrum zdarzeń hello. Witaj `SimpleEventProcessor` klasy używa stopera tooperiodically wywołania hello punktu kontrolnego metody na powitania **EventProcessorHost** kontekstu. To przetwarzanie gwarantuje, że jeśli odbiornik hello zostanie ponownie uruchomiony, utraci nie więcej niż pięć minut operacji przetwarzania.
6. W hello **Program** klasy, Dodaj następujące hello `using` instrukcji u góry pliku hello hello:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  Następnie zastąp hello `Main` metoda hello `Program` klas z następującego kodu hello, zastępując nazwę Centrum zdarzeń hello i hello poziomie przestrzeni nazw połączenia tego zostanie zapisane wcześniej ciągu, a hello konto magazynu i klucz skopiowane w hello przedstawione w poprzednich sekcjach. 
    
  ```csharp
  static void Main(string[] args)
  {
    string eventHubConnectionString = "{Event Hubs namespace connection string}";
    string eventHubName = "{Event Hub name}";
    string storageAccountName = "{storage account name}";
    string storageAccountKey = "{storage account key}";
    string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);
    
    string eventProcessorHostName = Guid.NewGuid().ToString();
    EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
    Console.WriteLine("Registering EventProcessor...");
    var options = new EventProcessorOptions();
    options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
    eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();
    
    Console.WriteLine("Receiving. Press enter key toostop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. Uruchom hello program i upewnij się, że nie ma żadnych błędów.
  
Gratulacje! Teraz otrzymali wiadomości z Centrum zdarzeń za pomocą hello hosta procesora zdarzeń.


> [!NOTE]
> Instrukcje w tym samouczku obejmują użycie pojedynczego wystąpienia klasy [EventProcessorHost][EventProcessorHost]. Przepływność tooincrease, zaleca się uruchomienie wielu wystąpień [EventProcessorHost][EventProcessorHost], jak pokazano w hello [skalowany w poziomie przetwarzania zdarzeń] [skalowany w poziomie przetwarzania zdarzeń] próbki. W takich przypadkach hello różne wystąpienia automatycznie koordynują ze sobą tooload saldo hello odebranych zdarzeń. Jeśli chcesz, aby wiele odbiorników tooeach procesu *wszystkie* hello zdarzenia, należy użyć hello **grupy konsumentów** koncepcji. Podczas odbierania zdarzeń z różnych komputerów, może być przydatne toospecify nazwy [EventProcessorHost] [ EventProcessorHost] wystąpień na podstawie hello maszyny (lub role), w których są one wdrażane. Aby uzyskać więcej informacji dotyczących tych tematów, zobacz hello [Przegląd usługi Event Hubs] [ Event Hubs overview] i hello [Podręcznik programowania usługi Event Hubs] [ Event Hubs Programming Guide] tematów.
> 
> 

## <a name="next-steps"></a>Następne kroki

Teraz gdy masz utworzoną działającą aplikację, która tworzy Centrum zdarzeń oraz wysyła i odbiera dane, można dowiedzieć się więcej, przechodząc na stronę hello następującego łącza:

* [Host procesora zdarzeń][Event Processor Host]
* [Przegląd usługi Event Hubs][Event Hubs overview]
* [Event Hubs — często zadawane pytania](event-hubs-faq.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]:../storage/common/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com
