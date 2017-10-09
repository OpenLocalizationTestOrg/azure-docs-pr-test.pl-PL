---
title: "aaaGet pracę z kolejek usługi Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Napisz aplikację konsolową w języku C#, która korzysta z kolejek komunikatów w usłudze Service Bus."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a>Wprowadzenie do kolejek usługi Service Bus
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a>Co zostanie osiągnięte?
Ten samouczek obejmuje hello następujące kroki:

1. Tworzenie przestrzeni nazw usługi Service Bus, przy użyciu hello portalu Azure.
2. Tworzenie kolejki usługi Service Bus, przy użyciu hello portalu Azure.
3. Napisz wiadomość toosend aplikacji konsoli.
4. Pisanie wiadomości wysłanych w poprzednim kroku hello hello tooreceive aplikacji konsoli.

## <a name="prerequisites"></a>Wymagania wstępne
1. [Program Visual Studio w wersji 2015 lub nowszej](http://www.visualstudio.com). Przykłady Hello w tym samouczku Użyj Visual Studio 2017 r.
2. Subskrypcja platformy Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Tworzenie przestrzeni nazw przy użyciu hello portalu Azure
Jeśli została już utworzona przestrzeń nazw usługi magistrali komunikatów, przejście toohello [Tworzenie kolejki przy użyciu portalu Azure hello](#2-create-a-queue-using-the-azure-portal) sekcji.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a>2. Tworzenie kolejki przy użyciu hello portalu Azure
Jeśli utworzono już kolejki usługi Service Bus, przejście toohello [wysyłania wiadomości toohello kolejki](#3-send-messages-to-the-queue) sekcji.

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a>3. Komunikaty toohello kolejki wysyłania
Kolejka toohello wiadomości toosend, możemy zapisać aplikacji konsolowej C# za pomocą programu Visual Studio.

### <a name="create-a-console-application"></a>Tworzenie aplikacji konsolowej

Uruchom program Visual Studio i utwórz nowy projekt **Aplikacja konsoli (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Dodaj pakiet NuGet usługi Service Bus hello
1. Kliknij prawym przyciskiem myszy hello nowo utworzonego projektu i wybierz **Zarządzaj pakietami NuGet**.
2. Kliknij hello **Przeglądaj** karcie, wyszukaj **Microsoft Azure Service Bus**, a następnie wybierz hello **WindowsAzure.ServiceBus** elementu. Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij to okno dialogowe.
   
    ![Wybieranie pakietu NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a>Zapis niektórych toosend kodu toohello kolejki komunikatów
1. Dodaj następujące hello `using` toohello instrukcji na początku pliku Program.cs hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Dodaj hello następującego kodu toohello `Main` metody. Zestaw hello `connectionString` połączenia toohello zmiennej ciągu uzyskane podczas tworzenia hello przestrzeni nazw i ustawić `queueName` toohello Nazwa kolejki, który został użyty podczas tworzenia kolejki hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Oto jak powinien wyglądać plik Program.cs:
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Uruchom hello program i sprawdź hello portalu Azure: kliknij nazwę swojej kolejki w przestrzeni nazw hello hello **omówienie** bloku. kolejki Hello **Essentials** bloku jest wyświetlany. Zwróć uwagę, że hello **liczby aktywnych komunikat** wartość powinna być teraz 1. Zawsze, gdy zostanie uruchomiony bez pobierania wiadomości powitania aplikację sender hello tej wartości zwiększa się o 1. Należy pamiętać, że bieżący rozmiar kolejki hello hello zwiększa każdej aplikacji hello czasu dodaje również toohello kolejki komunikatów.
   
      ![Rozmiar komunikatu][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a>4. Odbieranie komunikatów z kolejki hello

1. wiadomości powitania tooreceive właśnie wysłane, Utwórz nową aplikację konsoli i dodawanie pakietu NuGet usługi Service Bus toohello odwołania, podobne toohello poprzedniej aplikacji nadawcy.
2. Dodaj następujące hello `using` toohello instrukcji na początku pliku Program.cs hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Dodaj hello następującego kodu toohello `Main` metody. Zestaw hello `connectionString` toohello zmiennej ciąg połączenia, który został uzyskany podczas tworzenia hello przestrzeni nazw i ustaw `queueName` toohello Nazwa kolejki, który został użyty podczas tworzenia kolejki hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Oto jak powinien wyglądać plik Program.cs:
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. Uruchom hello program i ponownie sprawdzić hello portalu. Zwróć uwagę, że hello **liczby aktywnych komunikat** i **bieżącego** wartości są teraz 0.
   
    ![Długość kolejki][queue-message-receive]

Gratulacje! Utworzono kolejkę, wysłano komunikat i odebrano komunikat.

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z naszym [repozytorium GitHub i przykłady](https://github.com/Azure/azure-service-bus/tree/master/samples) który przedstawiono niektóre hello bardziej zaawansowane funkcje komunikatów usługi Service Bus.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
