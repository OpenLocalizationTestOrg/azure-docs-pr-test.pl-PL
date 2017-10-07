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
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a>Wprowadzenie do wysyłania wiadomości tooAzure centra zdarzeń w programie .NET Standard

> [!NOTE]
> Ten przykład jest dostępny na [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).

Ten samouczek pokazuje, jak toowrite aplikacji konsoli .NET Core, która wysyła zestaw komunikatów tooan Centrum zdarzeń. Możesz uruchomić hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) rozwiązania jako-zastępuje hello `EhConnectionString` i `EhEntityPath` ciągów, wartościami Centrum zdarzeń. Lub możesz wykonać hello czynnościach w ramach tego samouczka toocreate własnych.

## <a name="prerequisites"></a>Wymagania wstępne

* [Microsoft Visual Studio 2015 lub 2017](http://www.visualstudio.com). obsługiwane jest również Hello przykłady w tym samouczku 2017 usługi Visual Studio, ale programu Visual Studio 2015.
* [.NET core Visual Studio 2015 lub narzędzia 2017](http://www.microsoft.com/net/core).
* Subskrypcja platformy Azure.
* Koncentrator przestrzeni nazw zdarzenia.

Centrum zdarzeń tooan wiadomości toosend, użyjemy toowrite Visual Studio aplikacji konsolowej C#.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Tworzenie przestrzeni nazw usługi Event Hubs i centrum zdarzeń

pierwszym krokiem Hello jest toouse hello [portalu Azure](https://portal.azure.com) toocreate przestrzeni nazw dla typu Centrum zdarzeń hello i uzyskać poświadczenia zarządzania, czy aplikacja wymaga toocommunicate z Centrum zdarzeń hello hello. toocreate przestrzeni nazw i Centrum zdarzeń, wykonaj procedurę hello w [w tym artykule](event-hubs-create.md), a następnie kontynuować hello następujące kroki.

## <a name="create-a-console-application"></a>Tworzenie aplikacji konsolowej

Uruchom program Visual Studio. Z hello **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**. Tworzenie aplikacji konsoli .NET Core.

![Nowy projekt][1]

## <a name="add-hello-event-hubs-nuget-package"></a>Dodaj pakiet NuGet centra zdarzeń hello

Dodaj hello [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard NuGet pakietu tooyour projektu biblioteki wykonaj następujące czynności: 

1. Kliknij prawym przyciskiem myszy hello nowo utworzonego projektu i wybierz **Zarządzaj pakietami NuGet**.
2. Kliknij przycisk hello **Przeglądaj** kartę, a następnie wyszukaj "Microsoft.Azure.EventHubs" i wybierz hello **Microsoft.Azure.EventHubs** pakietu. Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij to okno dialogowe.

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a>Niektóre Centrum zdarzeń kodu toosend wiadomości toohello zapisu

1. Dodaj następujące hello `using` toohello instrukcje na początku pliku Program.cs hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. Dodaj toohello stałe `Program` klasy hello usługi Event Hubs połączenia ciągu i jednostek ścieżki (nazwa Centrum zdarzeń poszczególnych). Zastąp symbole zastępcze hello w nawiasach hello odpowiednie wartości, które zostały uzyskane podczas tworzenia Centrum zdarzeń hello.

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. Dodaj nową metodę o nazwie `MainAsync` toohello `Program` klasy, w następujący sposób:

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

4. Dodaj nową metodę o nazwie `SendMessagesToEventHub` toohello `Program` klasy, w następujący sposób:

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

5. Dodaj hello następującego kodu toohello `Main` w hello metody `Program` klasy.

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   Oto jak powinien wyglądać plik Program.cs.

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

6. Uruchom hello program i upewnij się, że nie ma żadnych błędów.

Gratulacje! Teraz zostały wysłane wiadomości tooan zdarzenia koncentratora.

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Odbieranie zdarzeń z usługi Event Hubs](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md)
* [Tworzenie centrum zdarzeń](event-hubs-create.md)
* [Event Hubs — często zadawane pytania](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
