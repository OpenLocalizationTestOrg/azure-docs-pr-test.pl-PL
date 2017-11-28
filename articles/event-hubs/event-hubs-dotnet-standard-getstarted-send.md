---
title: "aaaSend zdarzenia tooAzure Event Hubs przy użyciu platformy .NET Standard | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy wysyłanie tooEvent centra zdarzeń w programie .NET Standard"
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
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a><span data-ttu-id="5cb4f-103">Wprowadzenie do wysyłania wiadomości tooAzure centra zdarzeń w programie .NET Standard</span><span class="sxs-lookup"><span data-stu-id="5cb4f-103">Get started sending messages tooAzure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="5cb4f-104">Ten przykład jest dostępny na [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="5cb4f-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="5cb4f-105">Ten samouczek pokazuje, jak toowrite aplikacji konsoli .NET Core, która wysyła zestaw komunikatów tooan Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-105">This tutorial shows how toowrite a .NET Core console application that sends a set of messages tooan event hub.</span></span> <span data-ttu-id="5cb4f-106">Możesz uruchomić hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) rozwiązania jako-zastępuje hello `EhConnectionString` i `EhEntityPath` ciągów, wartościami Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing hello `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="5cb4f-107">Lub możesz wykonać hello czynnościach w ramach tego samouczka toocreate własnych.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cb4f-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5cb4f-108">Prerequisites</span></span>

* <span data-ttu-id="5cb4f-109">[Microsoft Visual Studio 2015 lub 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="5cb4f-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="5cb4f-110">obsługiwane jest również Hello przykłady w tym samouczku 2017 usługi Visual Studio, ale programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="5cb4f-111">[.NET core Visual Studio 2015 lub narzędzia 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="5cb4f-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="5cb4f-112">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-112">An Azure subscription.</span></span>
* <span data-ttu-id="5cb4f-113">Koncentrator przestrzeni nazw zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-113">An event hub namespace.</span></span>

<span data-ttu-id="5cb4f-114">Centrum zdarzeń tooan wiadomości toosend, użyjemy toowrite Visual Studio aplikacji konsolowej C#.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-114">toosend messages tooan event hub, we will use Visual Studio toowrite a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="5cb4f-115">Tworzenie przestrzeni nazw usługi Event Hubs i centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="5cb4f-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="5cb4f-116">pierwszym krokiem Hello jest toouse hello [portalu Azure](https://portal.azure.com) toocreate przestrzeni nazw dla typu Centrum zdarzeń hello i uzyskać poświadczenia zarządzania, czy aplikacja wymaga toocommunicate z Centrum zdarzeń hello hello.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello event hub type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="5cb4f-117">toocreate przestrzeni nazw i Centrum zdarzeń, wykonaj procedurę hello w [w tym artykule](event-hubs-create.md), a następnie kontynuować hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-117">toocreate a namespace and an event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="5cb4f-118">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="5cb4f-118">Create a console application</span></span>

<span data-ttu-id="5cb4f-119">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-119">Start Visual Studio.</span></span> <span data-ttu-id="5cb4f-120">Z hello **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-120">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="5cb4f-121">Tworzenie aplikacji konsoli .NET Core.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-121">Create a .NET Core console application.</span></span>

![Nowy projekt][1]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="5cb4f-123">Dodaj pakiet NuGet centra zdarzeń hello</span><span class="sxs-lookup"><span data-stu-id="5cb4f-123">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="5cb4f-124">Dodaj hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard NuGet pakietu tooyour projektu biblioteki wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5cb4f-124">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="5cb4f-125">Kliknij prawym przyciskiem myszy hello nowo utworzonego projektu i wybierz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-125">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="5cb4f-126">Kliknij przycisk hello **Przeglądaj** kartę, a następnie wyszukaj "Microsoft.Azure.EventHubs" i wybierz hello **Microsoft.Azure.EventHubs** pakietu.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-126">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="5cb4f-127">Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-127">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a><span data-ttu-id="5cb4f-128">Niektóre Centrum zdarzeń kodu toosend wiadomości toohello zapisu</span><span class="sxs-lookup"><span data-stu-id="5cb4f-128">Write some code toosend messages toohello event hub</span></span>

1. <span data-ttu-id="5cb4f-129">Dodaj następujące hello `using` toohello instrukcje na początku pliku Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-129">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="5cb4f-130">Dodaj toohello stałe `Program` klasy hello usługi Event Hubs połączenia ciągu i jednostek ścieżki (nazwa Centrum zdarzeń poszczególnych).</span><span class="sxs-lookup"><span data-stu-id="5cb4f-130">Add constants toohello `Program` class for hello Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="5cb4f-131">Zastąp symbole zastępcze hello w nawiasach hello odpowiednie wartości, które zostały uzyskane podczas tworzenia Centrum zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-131">Replace hello placeholders in brackets with hello proper values that were obtained when creating hello event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="5cb4f-132">Dodaj nową metodę o nazwie `MainAsync` toohello `Program` klasy, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5cb4f-132">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="5cb4f-133">Dodaj nową metodę o nazwie `SendMessagesToEventHub` toohello `Program` klasy, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5cb4f-133">Add a new method named `SendMessagesToEventHub` toohello `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
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

5. <span data-ttu-id="5cb4f-134">Dodaj hello następującego kodu toohello `Main` w hello metody `Program` klasy.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-134">Add hello following code toohello `Main` method in hello `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="5cb4f-135">Oto jak powinien wyglądać plik Program.cs.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-135">Here is what your Program.cs should look like.</span></span>

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
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
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

6. <span data-ttu-id="5cb4f-136">Uruchom hello program i upewnij się, że nie ma żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-136">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="5cb4f-137">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="5cb4f-137">Congratulations!</span></span> <span data-ttu-id="5cb4f-138">Teraz zostały wysłane wiadomości tooan zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="5cb4f-138">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cb4f-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5cb4f-139">Next steps</span></span>
<span data-ttu-id="5cb4f-140">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="5cb4f-140">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="5cb4f-141">Odbieranie zdarzeń z usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="5cb4f-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="5cb4f-142">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="5cb4f-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="5cb4f-143">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="5cb4f-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="5cb4f-144">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="5cb4f-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
