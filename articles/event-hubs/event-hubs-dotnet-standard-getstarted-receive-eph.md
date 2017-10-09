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
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a><span data-ttu-id="25eda-103">Rozpocząć odbieranie komunikatów z hello hosta procesora zdarzeń w .NET Standard</span><span class="sxs-lookup"><span data-stu-id="25eda-103">Get started receiving messages with hello Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="25eda-104">Ten przykład jest dostępny na [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="25eda-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="25eda-105">Ten samouczek pokazuje, jak toowrite .NET Core konsoli aplikacji, która odbiera komunikaty z Centrum zdarzeń za pomocą **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="25eda-105">This tutorial shows how toowrite a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="25eda-106">Możesz uruchomić hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) rozwiązania jako-zastępując hello ciągi wartości konta koncentratora i przechowywania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="25eda-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing hello strings with your event hub and storage account values.</span></span> <span data-ttu-id="25eda-107">Lub możesz wykonać hello czynnościach w ramach tego samouczka toocreate własnych.</span><span class="sxs-lookup"><span data-stu-id="25eda-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25eda-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="25eda-108">Prerequisites</span></span>

* <span data-ttu-id="25eda-109">[Microsoft Visual Studio 2015 lub 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="25eda-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="25eda-110">obsługiwane jest również Hello przykłady w tym samouczku 2017 usługi Visual Studio, ale programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="25eda-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="25eda-111">[.NET core Visual Studio 2015 lub narzędzia 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="25eda-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="25eda-112">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="25eda-112">An Azure subscription.</span></span>
* <span data-ttu-id="25eda-113">Przestrzeń nazw usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="25eda-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="25eda-114">Konto usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="25eda-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="25eda-115">Tworzenie przestrzeni nazw usługi Event Hubs i centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="25eda-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="25eda-116">Witaj pierwszym krokiem jest toouse hello [portalu Azure](https://portal.azure.com) toocreate obszaru nazw hello centra zdarzeń wpisz i uzyskać poświadczenia zarządzania, czy aplikacja wymaga toocommunicate z Centrum zdarzeń hello hello.</span><span class="sxs-lookup"><span data-stu-id="25eda-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello Event Hubs type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="25eda-117">toocreate przestrzeni nazw i Centrum zdarzeń, wykonaj procedurę hello w [w tym artykule](event-hubs-create.md), a następnie kontynuować hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="25eda-117">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="25eda-118">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="25eda-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="25eda-119">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="25eda-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="25eda-120">W okienku nawigacji po lewej stronie powitania hello portalu kliknij **nowy**, kliknij przycisk **magazynu**, a następnie kliknij przycisk **konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="25eda-120">In hello left navigation pane of hello portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="25eda-121">Wypełnij pola hello w bloku konto magazynu hello, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="25eda-121">Complete hello fields in hello storage account blade, and then click **Create**.</span></span>

    ![Tworzenie konta magazynu][1]

4. <span data-ttu-id="25eda-123">Po hello **wdrożeń zakończyło się pomyślnie** komunikatów, kliknij nazwę hello hello nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="25eda-123">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account.</span></span> <span data-ttu-id="25eda-124">W hello **Essentials** bloku, kliknij przycisk **obiekty BLOB**.</span><span class="sxs-lookup"><span data-stu-id="25eda-124">In hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="25eda-125">Gdy hello **usługa Blob** zostanie otwarty blok, kliknij przycisk **+ kontener** u góry hello.</span><span class="sxs-lookup"><span data-stu-id="25eda-125">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="25eda-126">Nadaj nazwę kontenera hello, a następnie zamknij hello **usługa Blob** bloku.</span><span class="sxs-lookup"><span data-stu-id="25eda-126">Give hello container a name, and then close hello **Blob service** blade.</span></span>  
5. <span data-ttu-id="25eda-127">Kliknij przycisk **klucze dostępu** hello po lewej stronie bloku i skopiuj hello nazwa kontenera magazynu hello, hello konta magazynu i wartości hello **klucz1**.</span><span class="sxs-lookup"><span data-stu-id="25eda-127">Click **Access keys** in hello left blade and copy hello name of hello storage container, hello storage account, and hello value of **key1**.</span></span> <span data-ttu-id="25eda-128">Zapisz te wartości tooNotepad lub tymczasowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="25eda-128">Save these values tooNotepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="25eda-129">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="25eda-129">Create a console application</span></span>

<span data-ttu-id="25eda-130">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="25eda-130">Start Visual Studio.</span></span> <span data-ttu-id="25eda-131">Z hello **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="25eda-131">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="25eda-132">Tworzenie aplikacji konsoli .NET Core.</span><span class="sxs-lookup"><span data-stu-id="25eda-132">Create a .NET Core console application.</span></span>

![Nowy projekt][2]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="25eda-134">Dodaj pakiet NuGet centra zdarzeń hello</span><span class="sxs-lookup"><span data-stu-id="25eda-134">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="25eda-135">Dodaj hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) i [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard NuGet pakiety tooyour projektu biblioteki wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="25eda-135">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="25eda-136">Kliknij prawym przyciskiem myszy hello nowo utworzonego projektu i wybierz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="25eda-136">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="25eda-137">Kliknij przycisk hello **Przeglądaj** kartę, a następnie wyszukaj "Microsoft.Azure.EventHubs" i wybierz hello **Microsoft.Azure.EventHubs** pakietu.</span><span class="sxs-lookup"><span data-stu-id="25eda-137">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="25eda-138">Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="25eda-138">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
3. <span data-ttu-id="25eda-139">Powtórz kroki 1 i 2, a następnie zainstaluj hello **Microsoft.Azure.EventHubs.Processor** pakietu.</span><span class="sxs-lookup"><span data-stu-id="25eda-139">Repeat steps 1 and 2, and install hello **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-hello-ieventprocessor-interface"></a><span data-ttu-id="25eda-140">Zaimplementuj interfejs IEventProcessor hello</span><span class="sxs-lookup"><span data-stu-id="25eda-140">Implement hello IEventProcessor interface</span></span>

1. <span data-ttu-id="25eda-141">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="25eda-141">In Solution Explorer, right-click hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="25eda-142">Nazwa nowej klasy hello **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="25eda-142">Name hello new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="25eda-143">Otwórz plik SimpleEventProcessor.cs hello i dodaj następujące hello `using` toohello instrukcje na początku pliku hello.</span><span class="sxs-lookup"><span data-stu-id="25eda-143">Open hello SimpleEventProcessor.cs file and add hello following `using` statements toohello top of hello file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="25eda-144">Implementowanie hello `IEventProcessor` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="25eda-144">Implement hello `IEventProcessor` interface.</span></span> <span data-ttu-id="25eda-145">Zastąp całą zawartość hello hello `SimpleEventProcessor` klasy z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="25eda-145">Replace hello entire contents of hello `SimpleEventProcessor` class with hello following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a><span data-ttu-id="25eda-146">Napisanie metody konsoli głównej, która używa hello SimpleEventProcessor klasy tooreceive komunikatów</span><span class="sxs-lookup"><span data-stu-id="25eda-146">Write a main console method that uses hello SimpleEventProcessor class tooreceive messages</span></span>

1. <span data-ttu-id="25eda-147">Dodaj następujące hello `using` toohello instrukcje na początku pliku Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="25eda-147">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="25eda-148">Dodaj toohello stałe `Program` klasy parametry połączenia Centrum zdarzeń hello, nazwy Centrum zdarzeń, nazwa kontenera konta magazynu, nazwa konta magazynu i klucza konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="25eda-148">Add constants toohello `Program` class for hello event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="25eda-149">Dodaj powitania po kod, zastępując symbole zastępcze hello z odpowiednimi wartościami.</span><span class="sxs-lookup"><span data-stu-id="25eda-149">Add hello following code, replacing hello placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="25eda-150">Dodaj nową metodę o nazwie `MainAsync` toohello `Program` klasy, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="25eda-150">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

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

3. <span data-ttu-id="25eda-151">Dodaj powitania po wierszu kodu toohello `Main` metody:</span><span class="sxs-lookup"><span data-stu-id="25eda-151">Add hello following line of code toohello `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="25eda-152">Oto jak powinien wyglądać plik Program.cs:</span><span class="sxs-lookup"><span data-stu-id="25eda-152">Here is what your Program.cs file should look like:</span></span>

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

4. <span data-ttu-id="25eda-153">Uruchom hello program i upewnij się, że nie ma żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="25eda-153">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="25eda-154">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="25eda-154">Congratulations!</span></span> <span data-ttu-id="25eda-155">Teraz Odebrano wiadomości z Centrum zdarzeń za pomocą hello hosta procesora zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="25eda-155">You have now received messages from an event hub by using hello Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25eda-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25eda-156">Next steps</span></span>
<span data-ttu-id="25eda-157">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="25eda-157">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="25eda-158">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="25eda-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="25eda-159">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="25eda-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="25eda-160">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="25eda-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
