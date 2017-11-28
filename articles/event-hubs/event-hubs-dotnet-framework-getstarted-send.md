---
title: "aaaSend zdarzenia tooAzure usługi Event Hubs przy użyciu hello .NET Framework | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy wysyłanie zdarzeń tooEvent Hubs przy użyciu hello .NET Framework"
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
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="8dc3a-103">Wysyłanie zdarzeń tooAzure Event Hubs przy użyciu hello .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8dc3a-103">Send events tooAzure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="8dc3a-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="8dc3a-104">Introduction</span></span>

<span data-ttu-id="8dc3a-105">Event Hubs to usługa, która przetwarza duże ilości danych zdarzeń (danych telemetrycznych) z podłączonych urządzeń i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="8dc3a-106">Po zebraniu danych do usługi Event Hubs, można przechowywać dane hello przy użyciu klastra magazynu lub przekształcać je za pomocą dostawcy analiz w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="8dc3a-107">Ta możliwość zbierania i przetwarzania zdarzeń na dużą skalę jest kluczowym składnikiem architektur nowoczesnych aplikacji, w tym hello Internetu rzeczy (IoT).</span><span class="sxs-lookup"><span data-stu-id="8dc3a-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="8dc3a-108">Ten samouczek pokazuje, jak toouse hello [portalu Azure](https://portal.azure.com) toocreate Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-108">This tutorial shows how toouse hello [Azure portal](https://portal.azure.com) toocreate an event hub.</span></span> <span data-ttu-id="8dc3a-109">Pokazuje też, jak toosend zdarzenia tooan Centrum zdarzeń za pomocą aplikacji konsoli napisanych w języku C# przy użyciu hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-109">It also shows how toosend events tooan event hub using a console application written in C# using hello .NET Framework.</span></span> <span data-ttu-id="8dc3a-110">zdarzenia tooreceive przy użyciu hello .NET Framework, zobacz hello [zdarzenia są rejestrowane przy użyciu hello .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) artykułu, lub kliknij odpowiedni język odbierania hello w tabeli po lewej stronie powitania treści.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-110">tooreceive events using hello .NET Framework, see hello [Receive events using hello .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="8dc3a-111">toocomplete tego samouczka należy hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="8dc3a-111">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="8dc3a-112">[Program Microsoft Visual Studio w wersji 2015 lub nowszej](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="8dc3a-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="8dc3a-113">zrzuty ekranu Hello w tym samouczku za pomocą programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-113">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="8dc3a-114">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-114">An active Azure account.</span></span> <span data-ttu-id="8dc3a-115">Jeśli go nie masz, możesz utworzyć bezpłatne konto w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="8dc3a-116">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="8dc3a-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="8dc3a-117">Tworzenie przestrzeni nazw usługi Event Hubs i centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="8dc3a-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="8dc3a-118">pierwszym krokiem Hello jest toouse hello [portalu Azure](https://portal.azure.com) toocreate a przestrzeń nazw wpisz centra zdarzeń i uzyskać poświadczenia zarządzania aplikacja wymaga toocommunicate z Centrum zdarzeń hello hello.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-118">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="8dc3a-119">toocreate przestrzeni nazw i Centrum zdarzeń, wykonaj procedurę hello w [w tym artykule](event-hubs-create.md), następnie kontynuować hello, wykonaj następujące kroki w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-119">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="8dc3a-120">Tworzenie aplikacji konsolowej nadawcy</span><span class="sxs-lookup"><span data-stu-id="8dc3a-120">Create a sender console application</span></span>

<span data-ttu-id="8dc3a-121">W tej sekcji przedstawiono tworzenie aplikacji konsoli systemu Windows, która wysyła zdarzenia tooyour zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-121">In this section, you'll write a Windows console app that sends events tooyour event hub.</span></span>

1. <span data-ttu-id="8dc3a-122">W programie Visual Studio Utwórz nowy projekt Visual C# pulpitu aplikacji przy użyciu hello **aplikacji konsoli** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-122">In Visual Studio, create a new Visual C# Desktop App project using hello **Console Application** project template.</span></span> <span data-ttu-id="8dc3a-123">Nazwa projektu hello **nadawcy**.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-123">Name hello project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="8dc3a-124">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **nadawcy** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet dla rozwiązania**.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-124">In Solution Explorer, right-click hello **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="8dc3a-125">Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-125">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="8dc3a-126">Kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-126">Click **Install**, and accept hello terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="8dc3a-127">Pobieranie programu Visual Studio, instaluje i dodaje toohello odwołanie [pakiet NuGet biblioteki usługi Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="8dc3a-127">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="8dc3a-128">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="8dc3a-128">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="8dc3a-129">Dodaj następujące pola toohello hello **Program** klasy, zastępując symbole zastępcze hello o nazwie hello hello Centrum zdarzeń utworzonego w poprzedniej sekcji hello i zapisanymi wcześniej parametrami połączenia na poziomie przestrzeni nazw hello.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-129">Add hello following fields toohello **Program** class, substituting hello placeholder values with hello name of hello event hub you created in hello previous section, and hello namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="8dc3a-130">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="8dc3a-130">Add hello following method toohello **Program** class:</span></span>
   
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
   
  <span data-ttu-id="8dc3a-131">Ta metoda stale wysyła zdarzenia Centrum zdarzeń tooyour z opóźnieniem 200 ms.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-131">This method continuously sends events tooyour event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="8dc3a-132">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="8dc3a-132">Finally, add hello following lines toohello **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="8dc3a-133">Uruchom hello program i upewnij się, że nie ma żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-133">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="8dc3a-134">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="8dc3a-134">Congratulations!</span></span> <span data-ttu-id="8dc3a-135">Teraz zostały wysłane wiadomości tooan zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="8dc3a-135">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dc3a-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8dc3a-136">Next steps</span></span>
<span data-ttu-id="8dc3a-137">Teraz gdy masz utworzoną działającą aplikację, która tworzy Centrum zdarzeń i wysyła dane, możesz przejść na toohello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="8dc3a-137">Now that you've built a working application that creates an event hub and sends data, you can move on toohello following scenarios:</span></span>

* [<span data-ttu-id="8dc3a-138">Zdarzenia są rejestrowane przy użyciu hello hosta procesora zdarzeń</span><span class="sxs-lookup"><span data-stu-id="8dc3a-138">Receive events using hello Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="8dc3a-139">Dokumentacja hosta procesora zdarzeń</span><span class="sxs-lookup"><span data-stu-id="8dc3a-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="8dc3a-140">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8dc3a-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

