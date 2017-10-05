---
title: "Odbieranie zdarzeń z usługi Azure Event Hubs przy użyciu platformy .NET Standard | Dokumentacja firmy Microsoft"
description: "Rozpocząć odbieranie komunikatów z klasy EventProcessorHost w .NET Standard"
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
ms.openlocfilehash: cc62792dad0284f9514664795fdfb32e94a85943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-receiving-messages-with-the-event-processor-host-in-net-standard"></a><span data-ttu-id="131b2-103">Rozpocząć odbieranie komunikatów z hosta procesora zdarzeń w .NET Standard</span><span class="sxs-lookup"><span data-stu-id="131b2-103">Get started receiving messages with the Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="131b2-104">Ten przykład jest dostępny na [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="131b2-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="131b2-105">Ten samouczek przedstawia sposób zapisania odbierająca komunikaty od Centrum zdarzeń za pomocą aplikacji konsoli .NET Core **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="131b2-105">This tutorial shows how to write a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="131b2-106">Można uruchomić [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) rozwiązania jako — jest zastępowany ciągi wartości konta koncentratora i przechowywania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="131b2-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing the strings with your event hub and storage account values.</span></span> <span data-ttu-id="131b2-107">Lub może wykonaj kroki opisane w tym samouczku, aby utworzyć własny.</span><span class="sxs-lookup"><span data-stu-id="131b2-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="131b2-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="131b2-108">Prerequisites</span></span>

* <span data-ttu-id="131b2-109">[Microsoft Visual Studio 2015 lub 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="131b2-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="131b2-110">Obsługiwane jest również przykłady tego samouczka użyj Visual Studio 2017, ale programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="131b2-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="131b2-111">[.NET core Visual Studio 2015 lub narzędzia 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="131b2-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="131b2-112">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="131b2-112">An Azure subscription.</span></span>
* <span data-ttu-id="131b2-113">Przestrzeń nazw usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="131b2-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="131b2-114">Konto usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="131b2-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="131b2-115">Tworzenie przestrzeni nazw usługi Event Hubs i centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="131b2-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="131b2-116">Pierwszym krokiem jest użycie [portalu Azure](https://portal.azure.com) tworzenie przestrzeni nazw dla typu usługi Event Hubs i uzyskać poświadczenia zarządzania, które aplikacja musi łączyć się z Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="131b2-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the Event Hubs type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="131b2-117">Aby utworzyć przestrzeń nazw i zdarzenia koncentratora, postępuj zgodnie z procedurą w [w tym artykule](event-hubs-create.md), a następnie kontynuować następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="131b2-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="131b2-118">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="131b2-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="131b2-119">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="131b2-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="131b2-120">W okienku nawigacji po lewej stronie portalu kliknij **nowy**, kliknij przycisk **magazynu**, a następnie kliknij przycisk **konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="131b2-120">In the left navigation pane of the portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="131b2-121">Wypełnij pola w bloku konto magazynu, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="131b2-121">Complete the fields in the storage account blade, and then click **Create**.</span></span>

    ![Tworzenie konta magazynu][1]

4. <span data-ttu-id="131b2-123">Po **wdrożeń zakończyło się pomyślnie** komunikatów, kliknij nazwę nowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="131b2-123">After you see the **Deployments Succeeded** message, click the name of the new storage account.</span></span> <span data-ttu-id="131b2-124">W **Essentials** bloku, kliknij przycisk **obiekty BLOB**.</span><span class="sxs-lookup"><span data-stu-id="131b2-124">In the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="131b2-125">Gdy **usługa Blob** zostanie otwarty blok, kliknij przycisk **+ kontener** u góry.</span><span class="sxs-lookup"><span data-stu-id="131b2-125">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="131b2-126">Nadaj nazwę kontenera, a następnie Zamknij **usługa Blob** bloku.</span><span class="sxs-lookup"><span data-stu-id="131b2-126">Give the container a name, and then close the **Blob service** blade.</span></span>  
5. <span data-ttu-id="131b2-127">Kliknij przycisk **klucze dostępu** w lewym bloku i skopiuj nazwę kontenera magazynu, konta magazynu i wartości **klucz1**.</span><span class="sxs-lookup"><span data-stu-id="131b2-127">Click **Access keys** in the left blade and copy the name of the storage container, the storage account, and the value of **key1**.</span></span> <span data-ttu-id="131b2-128">Zapisz te wartości w Notatniku lub tymczasowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="131b2-128">Save these values to Notepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="131b2-129">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="131b2-129">Create a console application</span></span>

<span data-ttu-id="131b2-130">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="131b2-130">Start Visual Studio.</span></span> <span data-ttu-id="131b2-131">W menu **Plik** kliknij pozycję **Nowy**, a następnie kliknij pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="131b2-131">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="131b2-132">Tworzenie aplikacji konsoli .NET Core.</span><span class="sxs-lookup"><span data-stu-id="131b2-132">Create a .NET Core console application.</span></span>

![Nowy projekt][2]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="131b2-134">Dodaj pakiet NuGet centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="131b2-134">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="131b2-135">Dodaj [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) i [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) biblioteki .NET Standard NuGet pakietów do projektu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="131b2-135">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages to your project by following these steps:</span></span> 

1. <span data-ttu-id="131b2-136">Kliknij prawym przyciskiem myszy nowo utworzony projekt i wybierz pozycję **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="131b2-136">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="131b2-137">Kliknij przycisk **Przeglądaj** kartę, a następnie wyszukaj "Microsoft.Azure.EventHubs" i wybierz **Microsoft.Azure.EventHubs** pakietu.</span><span class="sxs-lookup"><span data-stu-id="131b2-137">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="131b2-138">Kliknij przycisk **Zainstaluj**, aby ukończyć instalację, a następnie zamknij to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="131b2-138">Click **Install** to complete the installation, then close this dialog box.</span></span>
3. <span data-ttu-id="131b2-139">Powtórz kroki 1 i 2, a następnie zainstaluj **Microsoft.Azure.EventHubs.Processor** pakietu.</span><span class="sxs-lookup"><span data-stu-id="131b2-139">Repeat steps 1 and 2, and install the **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-the-ieventprocessor-interface"></a><span data-ttu-id="131b2-140">Zaimplementuj interfejs IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="131b2-140">Implement the IEventProcessor interface</span></span>

1. <span data-ttu-id="131b2-141">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="131b2-141">In Solution Explorer, right-click the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="131b2-142">Nazwa nowej klasy **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="131b2-142">Name the new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="131b2-143">Otwórz plik SimpleEventProcessor.cs i dodaj następujące `using` instrukcje na początku pliku.</span><span class="sxs-lookup"><span data-stu-id="131b2-143">Open the SimpleEventProcessor.cs file and add the following `using` statements to the top of the file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="131b2-144">Implementowanie `IEventProcessor` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="131b2-144">Implement the `IEventProcessor` interface.</span></span> <span data-ttu-id="131b2-145">Zastąp całą zawartość `SimpleEventProcessor` klasy następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="131b2-145">Replace the entire contents of the `SimpleEventProcessor` class with the following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-the-simpleeventprocessor-class-to-receive-messages"></a><span data-ttu-id="131b2-146">Napisanie metody konsoli głównej, która używa klasy SimpleEventProcessor do odbierania wiadomości</span><span class="sxs-lookup"><span data-stu-id="131b2-146">Write a main console method that uses the SimpleEventProcessor class to receive messages</span></span>

1. <span data-ttu-id="131b2-147">Dodaj następujące instrukcje `using` w górnej części pliku Program.cs.</span><span class="sxs-lookup"><span data-stu-id="131b2-147">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="131b2-148">Dodaj, aby stałe `Program` klasy dla parametrów połączenia Centrum zdarzeń, nazwy Centrum zdarzeń, nazwa kontenera konta magazynu, nazwa konta magazynu i klucz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="131b2-148">Add constants to the `Program` class for the event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="131b2-149">Dodaj następujący kod, zastępując symbole zastępcze z odpowiednimi wartościami.</span><span class="sxs-lookup"><span data-stu-id="131b2-149">Add the following code, replacing the placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="131b2-150">Dodaj nową metodę o nazwie `MainAsync` do `Program` klasy, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="131b2-150">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

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

        // Registers the Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER to stop worker.");
        Console.ReadLine();

        // Disposes of the Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="131b2-151">Dodaj następujący wiersz kodu w celu `Main` metody:</span><span class="sxs-lookup"><span data-stu-id="131b2-151">Add the following line of code to the `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="131b2-152">Oto jak powinien wyglądać plik Program.cs:</span><span class="sxs-lookup"><span data-stu-id="131b2-152">Here is what your Program.cs file should look like:</span></span>

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

                // Registers the Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER to stop worker.");
                Console.ReadLine();

                // Disposes of the Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="131b2-153">Uruchom program i upewnij się, że nie ma w nim żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="131b2-153">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="131b2-154">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="131b2-154">Congratulations!</span></span> <span data-ttu-id="131b2-155">Możesz teraz otrzymali wiadomości z Centrum zdarzeń przy użyciu hosta procesora zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="131b2-155">You have now received messages from an event hub by using the Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="131b2-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="131b2-156">Next steps</span></span>
<span data-ttu-id="131b2-157">Następujące linki pozwalają dowiedzieć się więcej na temat usługi Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="131b2-157">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="131b2-158">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="131b2-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="131b2-159">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="131b2-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="131b2-160">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="131b2-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
