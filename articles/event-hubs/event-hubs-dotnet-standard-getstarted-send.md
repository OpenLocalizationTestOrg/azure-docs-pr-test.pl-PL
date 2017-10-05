---
title: "Wysyłanie zdarzeń do usługi Azure Event Hubs przy użyciu platformy .NET Standard | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do wysyłania zdarzeń do usługi Event Hubs w .NET Standard"
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
ms.openlocfilehash: 8af9d70965c1c9ad8c49b7d2bb04244fc207058d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-sending-messages-to-azure-event-hubs-in-net-standard"></a><span data-ttu-id="350ce-103">Rozpoczynanie pracy wysyłanie komunikatów do usługi Azure Event Hubs w .NET Standard</span><span class="sxs-lookup"><span data-stu-id="350ce-103">Get started sending messages to Azure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="350ce-104">Ten przykład jest dostępny na [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="350ce-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="350ce-105">W tym samouczku przedstawiono sposób tworzenia aplikacji konsoli .NET Core wysyłanej zestaw komunikatów do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="350ce-105">This tutorial shows how to write a .NET Core console application that sends a set of messages to an event hub.</span></span> <span data-ttu-id="350ce-106">Można uruchomić [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) rozwiązania jako-zastępuje `EhConnectionString` i `EhEntityPath` ciągów, wartościami Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="350ce-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing the `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="350ce-107">Lub może wykonaj kroki opisane w tym samouczku, aby utworzyć własny.</span><span class="sxs-lookup"><span data-stu-id="350ce-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="350ce-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="350ce-108">Prerequisites</span></span>

* <span data-ttu-id="350ce-109">[Microsoft Visual Studio 2015 lub 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="350ce-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="350ce-110">Obsługiwane jest również przykłady tego samouczka użyj Visual Studio 2017, ale programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="350ce-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="350ce-111">[.NET core Visual Studio 2015 lub narzędzia 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="350ce-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="350ce-112">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="350ce-112">An Azure subscription.</span></span>
* <span data-ttu-id="350ce-113">Koncentrator przestrzeni nazw zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="350ce-113">An event hub namespace.</span></span>

<span data-ttu-id="350ce-114">Do wysyłania komunikatów do Centrum zdarzeń, użyjemy programu Visual Studio do pisania aplikacji konsolowej C#.</span><span class="sxs-lookup"><span data-stu-id="350ce-114">To send messages to an event hub, we will use Visual Studio to write a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="350ce-115">Tworzenie przestrzeni nazw usługi Event Hubs i centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="350ce-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="350ce-116">Pierwszym krokiem jest użycie [portalu Azure](https://portal.azure.com) tworzenie przestrzeni nazw dla typu Centrum zdarzeń i uzyskać poświadczenia zarządzania, które aplikacja musi łączyć się z Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="350ce-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the event hub type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="350ce-117">Aby utworzyć przestrzeń nazw i Centrum zdarzeń, wykonaj procedurę opisaną w [w tym artykule](event-hubs-create.md), a następnie kontynuować następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="350ce-117">To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="350ce-118">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="350ce-118">Create a console application</span></span>

<span data-ttu-id="350ce-119">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="350ce-119">Start Visual Studio.</span></span> <span data-ttu-id="350ce-120">W menu **Plik** kliknij pozycję **Nowy**, a następnie kliknij pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="350ce-120">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="350ce-121">Tworzenie aplikacji konsoli .NET Core.</span><span class="sxs-lookup"><span data-stu-id="350ce-121">Create a .NET Core console application.</span></span>

![Nowy projekt][1]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="350ce-123">Dodaj pakiet NuGet centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="350ce-123">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="350ce-124">Dodaj [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard biblioteki pakiet NuGet do projektu, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="350ce-124">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package to your project by following these steps:</span></span> 

1. <span data-ttu-id="350ce-125">Kliknij prawym przyciskiem myszy nowo utworzony projekt i wybierz pozycję **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="350ce-125">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="350ce-126">Kliknij przycisk **Przeglądaj** kartę, a następnie wyszukaj "Microsoft.Azure.EventHubs" i wybierz **Microsoft.Azure.EventHubs** pakietu.</span><span class="sxs-lookup"><span data-stu-id="350ce-126">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="350ce-127">Kliknij przycisk **Zainstaluj**, aby ukończyć instalację, a następnie zamknij to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="350ce-127">Click **Install** to complete the installation, then close this dialog box.</span></span>

## <a name="write-some-code-to-send-messages-to-the-event-hub"></a><span data-ttu-id="350ce-128">Napisanie kodu do wysyłania komunikatów do Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="350ce-128">Write some code to send messages to the event hub</span></span>

1. <span data-ttu-id="350ce-129">Dodaj następujące instrukcje `using` w górnej części pliku Program.cs.</span><span class="sxs-lookup"><span data-stu-id="350ce-129">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="350ce-130">Dodaj, aby stałe `Program` klasy dla usługi Event Hubs połączenia ciągu i jednostek ścieżki (nazwa Centrum zdarzeń poszczególnych).</span><span class="sxs-lookup"><span data-stu-id="350ce-130">Add constants to the `Program` class for the Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="350ce-131">Zastąp symbole zastępcze w nawiasach odpowiednie wartości, które zostały uzyskane podczas tworzenia Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="350ce-131">Replace the placeholders in brackets with the proper values that were obtained when creating the event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="350ce-132">Dodaj nową metodę o nazwie `MainAsync` do `Program` klasy, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="350ce-132">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
        // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
        // we are using the connection string from the namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="350ce-133">Dodaj nową metodę o nazwie `SendMessagesToEventHub` do `Program` klasy, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="350ce-133">Add a new method named `SendMessagesToEventHub` to the `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages to the event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. <span data-ttu-id="350ce-134">Dodaj następujący kod do `Main` metoda `Program` klasy.</span><span class="sxs-lookup"><span data-stu-id="350ce-134">Add the following code to the `Main` method in the `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="350ce-135">Oto jak powinien wyglądać plik Program.cs.</span><span class="sxs-lookup"><span data-stu-id="350ce-135">Here is what your Program.cs should look like.</span></span>

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
                // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
                // we are using the connection string from the namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER to exit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages to the event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. <span data-ttu-id="350ce-136">Uruchom program i upewnij się, że nie ma w nim żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="350ce-136">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="350ce-137">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="350ce-137">Congratulations!</span></span> <span data-ttu-id="350ce-138">Wysłano komunikaty do centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="350ce-138">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="350ce-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="350ce-139">Next steps</span></span>
<span data-ttu-id="350ce-140">Następujące linki pozwalają dowiedzieć się więcej na temat usługi Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="350ce-140">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="350ce-141">Odbieranie zdarzeń z usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="350ce-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="350ce-142">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="350ce-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="350ce-143">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="350ce-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="350ce-144">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="350ce-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
