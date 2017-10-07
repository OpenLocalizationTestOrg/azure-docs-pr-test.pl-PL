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
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a>Wysyłanie zdarzeń tooAzure Event Hubs przy użyciu hello .NET Framework

## <a name="introduction"></a>Wprowadzenie

Event Hubs to usługa, która przetwarza duże ilości danych zdarzeń (danych telemetrycznych) z podłączonych urządzeń i aplikacji. Po zebraniu danych do usługi Event Hubs, można przechowywać dane hello przy użyciu klastra magazynu lub przekształcać je za pomocą dostawcy analiz w czasie rzeczywistym. Ta możliwość zbierania i przetwarzania zdarzeń na dużą skalę jest kluczowym składnikiem architektur nowoczesnych aplikacji, w tym hello Internetu rzeczy (IoT).

Ten samouczek pokazuje, jak toouse hello [portalu Azure](https://portal.azure.com) toocreate Centrum zdarzeń. Pokazuje też, jak toosend zdarzenia tooan Centrum zdarzeń za pomocą aplikacji konsoli napisanych w języku C# przy użyciu hello .NET Framework. zdarzenia tooreceive przy użyciu hello .NET Framework, zobacz hello [zdarzenia są rejestrowane przy użyciu hello .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) artykułu, lub kliknij odpowiedni język odbierania hello w tabeli po lewej stronie powitania treści.

toocomplete tego samouczka należy hello następujące wymagania wstępne:

* [Program Microsoft Visual Studio w wersji 2015 lub nowszej](http://visualstudio.com). zrzuty ekranu Hello w tym samouczku za pomocą programu Visual Studio 2017 r.
* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Tworzenie przestrzeni nazw usługi Event Hubs i centrum zdarzeń

pierwszym krokiem Hello jest toouse hello [portalu Azure](https://portal.azure.com) toocreate a przestrzeń nazw wpisz centra zdarzeń i uzyskać poświadczenia zarządzania aplikacja wymaga toocommunicate z Centrum zdarzeń hello hello. toocreate przestrzeni nazw i Centrum zdarzeń, wykonaj procedurę hello w [w tym artykule](event-hubs-create.md), następnie kontynuować hello, wykonaj następujące kroki w tym samouczku.

## <a name="create-a-sender-console-application"></a>Tworzenie aplikacji konsolowej nadawcy

W tej sekcji przedstawiono tworzenie aplikacji konsoli systemu Windows, która wysyła zdarzenia tooyour zdarzenia koncentratora.

1. W programie Visual Studio Utwórz nowy projekt Visual C# pulpitu aplikacji przy użyciu hello **aplikacji konsoli** szablonu projektu. Nazwa projektu hello **nadawcy**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **nadawcy** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet dla rozwiązania**. 
3. Kliknij przycisk hello **Przeglądaj** , a następnie wyszukaj `Microsoft Azure Service Bus`. Kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello. 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    Pobieranie programu Visual Studio, instaluje i dodaje toohello odwołanie [pakiet NuGet biblioteki usługi Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).
4. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. Dodaj następujące pola toohello hello **Program** klasy, zastępując symbole zastępcze hello o nazwie hello hello Centrum zdarzeń utworzonego w poprzedniej sekcji hello i zapisanymi wcześniej parametrami połączenia na poziomie przestrzeni nazw hello.
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. Dodaj następujące metody toohello hello **Program** klasy:
   
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
   
  Ta metoda stale wysyła zdarzenia Centrum zdarzeń tooyour z opóźnieniem 200 ms.
7. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. Uruchom hello program i upewnij się, że nie ma żadnych błędów.
  
Gratulacje! Teraz zostały wysłane wiadomości tooan zdarzenia koncentratora.

## <a name="next-steps"></a>Następne kroki
Teraz gdy masz utworzoną działającą aplikację, która tworzy Centrum zdarzeń i wysyła dane, możesz przejść na toohello następujące scenariusze:

* [Zdarzenia są rejestrowane przy użyciu hello hosta procesora zdarzeń](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [Dokumentacja hosta procesora zdarzeń](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

