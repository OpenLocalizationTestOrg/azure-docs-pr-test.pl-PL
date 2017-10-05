---
title: "Wysyłanie zdarzeń do usługi Azure Event Hubs za pomocą programu .NET Framework | Microsoft Docs"
description: "Rozpocznij wysyłanie zdarzeń do usługi Event Hubs przy użyciu programu .NET Framework"
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
ms.openlocfilehash: 4eb0e7bcc14722010121c2a5945509d6ed736f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="send-events-to-azure-event-hubs-using-the-net-framework"></a><span data-ttu-id="ad97b-103">Wysyłanie zdarzeń do usługi Azure Event Hubs za pomocą programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="ad97b-103">Send events to Azure Event Hubs using the .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="ad97b-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="ad97b-104">Introduction</span></span>

<span data-ttu-id="ad97b-105">Event Hubs to usługa, która przetwarza duże ilości danych zdarzeń (danych telemetrycznych) z podłączonych urządzeń i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ad97b-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="ad97b-106">Po zebraniu danych w usłudze Event Hubs można przechowywać dane przy użyciu klastra magazynu lub przekształcać je za pomocą dostawcy analiz w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="ad97b-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="ad97b-107">Ta możliwość zbierania i przetwarzania zdarzeń na wielką skalę jest kluczowym składnikiem architektur nowoczesnych aplikacji, w tym Internetu rzeczy (IoT).</span><span class="sxs-lookup"><span data-stu-id="ad97b-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span></span>

<span data-ttu-id="ad97b-108">W tym samouczku pokazano, jak utworzyć centrum zdarzeń za pomocą witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad97b-108">This tutorial shows how to use the [Azure portal](https://portal.azure.com) to create an event hub.</span></span> <span data-ttu-id="ad97b-109">Pokazano w nim także, jak wysyłać zdarzenia do centrum zdarzeń za pomocą aplikacji konsoli napisanej w języku C# w programie .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="ad97b-109">It also shows how to send events to an event hub using a console application written in C# using the .NET Framework.</span></span> <span data-ttu-id="ad97b-110">Aby odbierać zdarzenia przy użyciu programu .NET Framework, zobacz artykuł [Receive events using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) (Odbieranie zdarzeń za pomocą programu .NET Framework) lub kliknij odpowiedni język odbierający w spisie treści po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="ad97b-110">To receive events using the .NET Framework, see the [Receive events using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="ad97b-111">Do wykonania kroków tego samouczka niezbędne jest spełnienie następujących wymagań wstępnych:</span><span class="sxs-lookup"><span data-stu-id="ad97b-111">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="ad97b-112">[Program Microsoft Visual Studio w wersji 2015 lub nowszej](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="ad97b-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="ad97b-113">Na zrzutach ekranów przedstawionych w tym samouczku używany jest program Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ad97b-113">The screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="ad97b-114">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ad97b-114">An active Azure account.</span></span> <span data-ttu-id="ad97b-115">Jeśli go nie masz, możesz utworzyć bezpłatne konto w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="ad97b-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="ad97b-116">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="ad97b-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="ad97b-117">Tworzenie przestrzeni nazw usługi Event Hubs i centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ad97b-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="ad97b-118">Pierwszym krokiem jest skorzystanie z witryny [Azure Portal](https://portal.azure.com) w celu utworzenia przestrzeni nazw typu Event Hubs i uzyskania poświadczeń zarządzania wymaganych przez aplikację do komunikacji z centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ad97b-118">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span></span> <span data-ttu-id="ad97b-119">Aby utworzyć obszar nazw i centrum zdarzeń, wykonaj procedurę opisaną w [tym artykule](event-hubs-create.md), a następnie wykonaj następujące czynności z tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="ad97b-119">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="ad97b-120">Tworzenie aplikacji konsolowej nadawcy</span><span class="sxs-lookup"><span data-stu-id="ad97b-120">Create a sender console application</span></span>

<span data-ttu-id="ad97b-121">W tej sekcji przedstawiono tworzenie aplikacji konsoli systemu Windows, która wysyła zdarzenia do centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ad97b-121">In this section, you'll write a Windows console app that sends events to your event hub.</span></span>

1. <span data-ttu-id="ad97b-122">W programie Visual Studio utwórz nowy projekt aplikacji klasycznej Visual C# za pomocą szablonu projektu **Aplikacja konsoli**.</span><span class="sxs-lookup"><span data-stu-id="ad97b-122">In Visual Studio, create a new Visual C# Desktop App project using the **Console Application** project template.</span></span> <span data-ttu-id="ad97b-123">Nazwij projekt **Nadawca**.</span><span class="sxs-lookup"><span data-stu-id="ad97b-123">Name the project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="ad97b-124">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **Nadawca**, a następnie kliknij pozycję **Zarządzaj pakietami NuGet rozwiązania**.</span><span class="sxs-lookup"><span data-stu-id="ad97b-124">In Solution Explorer, right-click the **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="ad97b-125">Kliknij kartę **Przeglądanie**, a następnie wyszukaj ciąg `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="ad97b-125">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="ad97b-126">Kliknij pozycję **Zainstaluj** i zaakceptuj warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="ad97b-126">Click **Install**, and accept the terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="ad97b-127">Program Visual Studio pobierze, zainstaluje i doda odniesienia do [pakietu NuGet biblioteki usługi Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="ad97b-127">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="ad97b-128">Dodaj następujące instrukcje `using` w górnej części pliku **Program.cs**:</span><span class="sxs-lookup"><span data-stu-id="ad97b-128">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="ad97b-129">Dodaj następujące pola do klasy **Program**, zastępując symbole zastępcze nazwą centrum zdarzeń utworzonego w poprzedniej sekcji oraz zapisanymi wcześniej parametrami połączenia na poziomie przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="ad97b-129">Add the following fields to the **Program** class, substituting the placeholder values with the name of the event hub you created in the previous section, and the namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="ad97b-130">Dodaj następującą metodę do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="ad97b-130">Add the following method to the **Program** class:</span></span>
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  <span data-ttu-id="ad97b-131">Ta metoda stale wysyła zdarzenia do centrum zdarzeń z opóźnieniem 200 ms.</span><span class="sxs-lookup"><span data-stu-id="ad97b-131">This method continuously sends events to your event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="ad97b-132">Na koniec dodaj następujące wiersze do metody **Główne**:</span><span class="sxs-lookup"><span data-stu-id="ad97b-132">Finally, add the following lines to the **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C to stop the sender process");
  Console.WriteLine("Press Enter to start now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="ad97b-133">Uruchom program i upewnij się, że nie ma w nim żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="ad97b-133">Run the program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="ad97b-134">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="ad97b-134">Congratulations!</span></span> <span data-ttu-id="ad97b-135">Wysłano komunikaty do centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ad97b-135">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad97b-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ad97b-136">Next steps</span></span>
<span data-ttu-id="ad97b-137">Teraz, gdy masz utworzoną działającą aplikację, która tworzy centrum zdarzeń i wysyła dane, możesz przejść do następujących scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="ad97b-137">Now that you've built a working application that creates an event hub and sends data, you can move on to the following scenarios:</span></span>

* [<span data-ttu-id="ad97b-138">Odbieranie zdarzeń za pomocą hosta procesora zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ad97b-138">Receive events using the Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="ad97b-139">Dokumentacja hosta procesora zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ad97b-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="ad97b-140">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ad97b-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

