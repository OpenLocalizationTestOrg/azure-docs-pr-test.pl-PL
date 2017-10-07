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
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="b1e38-103">Odbieranie zdarzeń z usługi Azure Event Hubs przy użyciu hello .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b1e38-103">Receive events from Azure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="b1e38-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="b1e38-104">Introduction</span></span>

<span data-ttu-id="b1e38-105">Event Hubs to usługa, która przetwarza duże ilości danych zdarzeń (danych telemetrycznych) z podłączonych urządzeń i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b1e38-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="b1e38-106">Po zebraniu danych do usługi Event Hubs, można przechowywać dane hello przy użyciu klastra magazynu lub przekształcać je za pomocą dostawcy analiz w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="b1e38-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="b1e38-107">Ta możliwość zbierania i przetwarzania zdarzeń na dużą skalę jest kluczowym składnikiem architektur nowoczesnych aplikacji, w tym hello Internetu rzeczy (IoT).</span><span class="sxs-lookup"><span data-stu-id="b1e38-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="b1e38-108">Ten samouczek pokazuje, jak toowrite .NET Framework konsoli aplikacji, która odbiera komunikaty z Centrum zdarzeń za pomocą hello  **[hosta procesora zdarzeń][EventProcessorHost]**.</span><span class="sxs-lookup"><span data-stu-id="b1e38-108">This tutorial shows how toowrite a .NET Framework console application that receives messages from an event hub using hello **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="b1e38-109">zdarzenia toosend przy użyciu hello .NET Framework, zobacz hello [wysyłać zdarzenia tooAzure Event Hubs przy użyciu hello .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) artykułu, lub kliknij odpowiedni język wysyłania hello w tabeli po lewej stronie powitania treści.</span><span class="sxs-lookup"><span data-stu-id="b1e38-109">toosend events using hello .NET Framework, see hello [Send events tooAzure Event Hubs using hello .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click hello appropriate sending language in hello left-hand table of contents.</span></span>

<span data-ttu-id="b1e38-110">Witaj [hosta procesora zdarzeń] [ EventProcessorHost] jest klasą .NET, która upraszcza odbieranie zdarzeń z usługi event hubs przez zarządzanie trwałymi punktami kontrolnymi i równoległymi odbiorami z tych usług.</span><span class="sxs-lookup"><span data-stu-id="b1e38-110">hello [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="b1e38-111">Przy użyciu hello [hosta procesora zdarzeń][Event Processor Host], można podzielić zdarzenia między wieloma odbiornikami, nawet w przypadku hostowania w różnych węzłach.</span><span class="sxs-lookup"><span data-stu-id="b1e38-111">Using hello [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="b1e38-112">W tym przykładzie pokazano sposób toouse hello [hosta procesora zdarzeń] [ EventProcessorHost] dla jednego odbiornika.</span><span class="sxs-lookup"><span data-stu-id="b1e38-112">This example shows how toouse hello [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="b1e38-113">Witaj [skalowania przetwarzania zdarzeń] [ Scale out Event Processing with Event Hubs] przykładowe pokazuje, jak toouse hello [hosta procesora zdarzeń] [ EventProcessorHost] z wieloma odbiornikami.</span><span class="sxs-lookup"><span data-stu-id="b1e38-113">hello [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how toouse hello [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1e38-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b1e38-114">Prerequisites</span></span>

<span data-ttu-id="b1e38-115">toocomplete tego samouczka należy hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="b1e38-115">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="b1e38-116">[Program Microsoft Visual Studio w wersji 2015 lub nowszej](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="b1e38-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="b1e38-117">zrzuty ekranu Hello w tym samouczku za pomocą programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="b1e38-117">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="b1e38-118">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b1e38-118">An active Azure account.</span></span> <span data-ttu-id="b1e38-119">Jeśli go nie masz, możesz utworzyć bezpłatne konto w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="b1e38-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="b1e38-120">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b1e38-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="b1e38-121">Tworzenie przestrzeni nazw usługi Event Hubs i centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b1e38-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="b1e38-122">pierwszym krokiem Hello jest toouse hello [portalu Azure](https://portal.azure.com) toocreate a przestrzeń nazw wpisz centra zdarzeń i uzyskać poświadczenia zarządzania aplikacja wymaga toocommunicate z Centrum zdarzeń hello hello.</span><span class="sxs-lookup"><span data-stu-id="b1e38-122">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="b1e38-123">toocreate przestrzeni nazw i Centrum zdarzeń, wykonaj procedurę hello w [w tym artykule](event-hubs-create.md), następnie kontynuować hello, wykonaj następujące kroki w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b1e38-123">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="b1e38-124">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b1e38-124">Create an Azure Storage account</span></span>

<span data-ttu-id="b1e38-125">Witaj toouse [hosta procesora zdarzeń][EventProcessorHost], musi mieć [konta magazynu Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="b1e38-125">toouse hello [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="b1e38-126">Zaloguj się na toohello [portalu Azure][Azure portal]i kliknij przycisk **nowy** na powitania lewym górnym rogu ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="b1e38-126">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
2. <span data-ttu-id="b1e38-127">Kliknij pozycję **Magazyn**, a następnie pozycję **Konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="b1e38-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="b1e38-128">W hello **utworzyć konto magazynu** bloku, wpisz nazwę konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="b1e38-128">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="b1e38-129">Wybierz subskrypcję platformy Azure, lokalizacji i grupy zasobów w toocreate hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="b1e38-129">Choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="b1e38-130">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b1e38-130">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="b1e38-131">Na liście hello kont magazynu kliknij hello nowo utworzone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="b1e38-131">In hello list of storage accounts, click hello newly created storage account.</span></span>
5. <span data-ttu-id="b1e38-132">W bloku konto magazynu hello, kliknij przycisk **klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="b1e38-132">In hello storage account blade, click **Access keys**.</span></span> <span data-ttu-id="b1e38-133">Skopiuj wartość hello **klucz1** toouse w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="b1e38-133">Copy hello value of **key1** toouse later in this tutorial.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a><span data-ttu-id="b1e38-134">Tworzenie aplikacji konsolowej odbiorcy</span><span class="sxs-lookup"><span data-stu-id="b1e38-134">Create a receiver console application</span></span>

1. <span data-ttu-id="b1e38-135">W programie Visual Studio Utwórz nowy projekt Visual C# pulpitu aplikacji przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="b1e38-135">In Visual Studio, create a new Visual C# Desktop App project using hello **Console  Application** project template.</span></span> <span data-ttu-id="b1e38-136">Nazwa projektu hello **odbiornika**.</span><span class="sxs-lookup"><span data-stu-id="b1e38-136">Name hello project **Receiver**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. <span data-ttu-id="b1e38-137">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **odbiornika** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet dla rozwiązania**.</span><span class="sxs-lookup"><span data-stu-id="b1e38-137">In Solution Explorer, right-click hello **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
3. <span data-ttu-id="b1e38-138">Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="b1e38-138">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="b1e38-139">Kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="b1e38-139">Click **Install**, and accept hello terms of use.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="b1e38-140">Pobieranie programu Visual Studio, instaluje i dodaje toohello odwołanie [Centrum zdarzeń usługi Azure Service Bus — pakiet EventProcessorHost NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), ze wszystkimi zależnościami.</span><span class="sxs-lookup"><span data-stu-id="b1e38-140">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
4. <span data-ttu-id="b1e38-141">Powitania kliknij prawym przyciskiem myszy **odbiornika** projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="b1e38-141">Right-click hello **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="b1e38-142">Nazwa nowej klasy hello **SimpleEventProcessor**, a następnie kliknij przycisk **Dodaj** toocreate hello klasy.</span><span class="sxs-lookup"><span data-stu-id="b1e38-142">Name hello new class **SimpleEventProcessor**, and then click **Add** toocreate hello class.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. <span data-ttu-id="b1e38-143">Dodaj następujące instrukcje u góry pliku SimpleEventProcessor.cs hello hello hello:</span><span class="sxs-lookup"><span data-stu-id="b1e38-143">Add hello following statements at hello top of hello SimpleEventProcessor.cs file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  <span data-ttu-id="b1e38-144">Następnie zastąp hello następującego kodu dla treści hello hello klasy:</span><span class="sxs-lookup"><span data-stu-id="b1e38-144">Then, substitute hello following code for hello body of hello class:</span></span>
    
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
    
  <span data-ttu-id="b1e38-145">Ta klasa jest wywoływana przez hello **EventProcessorHost** tooprocess zdarzeń odebranych z Centrum zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="b1e38-145">This class is called by hello **EventProcessorHost** tooprocess events received from hello event hub.</span></span> <span data-ttu-id="b1e38-146">Witaj `SimpleEventProcessor` klasy używa stopera tooperiodically wywołania hello punktu kontrolnego metody na powitania **EventProcessorHost** kontekstu.</span><span class="sxs-lookup"><span data-stu-id="b1e38-146">hello `SimpleEventProcessor` class uses a stopwatch tooperiodically call hello checkpoint method on hello **EventProcessorHost** context.</span></span> <span data-ttu-id="b1e38-147">To przetwarzanie gwarantuje, że jeśli odbiornik hello zostanie ponownie uruchomiony, utraci nie więcej niż pięć minut operacji przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="b1e38-147">This processing ensures that, if hello receiver is restarted, it loses no more than five minutes of processing work.</span></span>
6. <span data-ttu-id="b1e38-148">W hello **Program** klasy, Dodaj następujące hello `using` instrukcji u góry pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="b1e38-148">In hello **Program** class, add hello following `using` statement at hello top of hello file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  <span data-ttu-id="b1e38-149">Następnie zastąp hello `Main` metoda hello `Program` klas z następującego kodu hello, zastępując nazwę Centrum zdarzeń hello i hello poziomie przestrzeni nazw połączenia tego zostanie zapisane wcześniej ciągu, a hello konto magazynu i klucz skopiowane w hello przedstawione w poprzednich sekcjach.</span><span class="sxs-lookup"><span data-stu-id="b1e38-149">Then, replace hello `Main` method in hello `Program` class with hello following code, substituting hello event hub name and hello namespace-level connection string that you saved previously, and hello storage account and key that you copied in hello previous sections.</span></span> 
    
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

7. <span data-ttu-id="b1e38-150">Uruchom hello program i upewnij się, że nie ma żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="b1e38-150">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="b1e38-151">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="b1e38-151">Congratulations!</span></span> <span data-ttu-id="b1e38-152">Teraz otrzymali wiadomości z Centrum zdarzeń za pomocą hello hosta procesora zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="b1e38-152">You have now received messages from an event hub using hello Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="b1e38-153">Instrukcje w tym samouczku obejmują użycie pojedynczego wystąpienia klasy [EventProcessorHost][EventProcessorHost].</span><span class="sxs-lookup"><span data-stu-id="b1e38-153">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="b1e38-154">Przepływność tooincrease, zaleca się uruchomienie wielu wystąpień [EventProcessorHost][EventProcessorHost], jak pokazano w hello [skalowany w poziomie przetwarzania zdarzeń] [skalowany w poziomie przetwarzania zdarzeń] próbki.</span><span class="sxs-lookup"><span data-stu-id="b1e38-154">tooincrease throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in hello [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="b1e38-155">W takich przypadkach hello różne wystąpienia automatycznie koordynują ze sobą tooload saldo hello odebranych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="b1e38-155">In those cases, hello various instances automatically coordinate with each other tooload balance hello received events.</span></span> <span data-ttu-id="b1e38-156">Jeśli chcesz, aby wiele odbiorników tooeach procesu *wszystkie* hello zdarzenia, należy użyć hello **grupy konsumentów** koncepcji.</span><span class="sxs-lookup"><span data-stu-id="b1e38-156">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="b1e38-157">Podczas odbierania zdarzeń z różnych komputerów, może być przydatne toospecify nazwy [EventProcessorHost] [ EventProcessorHost] wystąpień na podstawie hello maszyny (lub role), w których są one wdrażane.</span><span class="sxs-lookup"><span data-stu-id="b1e38-157">When receiving events from different machines, it might be useful toospecify names for [EventProcessorHost][EventProcessorHost] instances based on hello machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="b1e38-158">Aby uzyskać więcej informacji dotyczących tych tematów, zobacz hello [Przegląd usługi Event Hubs] [ Event Hubs overview] i hello [Podręcznik programowania usługi Event Hubs] [ Event Hubs Programming Guide] tematów.</span><span class="sxs-lookup"><span data-stu-id="b1e38-158">For more information about these topics, see hello [Event Hubs overview][Event Hubs overview] and hello [Event Hubs programming guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b1e38-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1e38-159">Next steps</span></span>

<span data-ttu-id="b1e38-160">Teraz gdy masz utworzoną działającą aplikację, która tworzy Centrum zdarzeń oraz wysyła i odbiera dane, można dowiedzieć się więcej, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="b1e38-160">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting hello following links:</span></span>

* <span data-ttu-id="b1e38-161">[Host procesora zdarzeń][Event Processor Host]</span><span class="sxs-lookup"><span data-stu-id="b1e38-161">[Event Processor Host][Event Processor Host]</span></span>
* <span data-ttu-id="b1e38-162">[Przegląd usługi Event Hubs][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="b1e38-162">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="b1e38-163">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="b1e38-163">Event Hubs FAQ</span></span>](event-hubs-faq.md)

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
