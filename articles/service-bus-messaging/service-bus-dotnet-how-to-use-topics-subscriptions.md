---
title: "aaaGet pracę z tematów i subskrypcji Azure Service Bus | Dokumentacja firmy Microsoft"
description: "Napisz aplikację konsolową w języku C#, która korzysta z tematów i subskrypcji komunikatów usługi Service Bus."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a>Wprowadzenie do tematów usługi Service Bus

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a>Co zostanie osiągnięte?

Ten samouczek obejmuje hello następujące kroki:

1. Tworzenie przestrzeni nazw usługi Service Bus, przy użyciu hello portalu Azure.
2. Tworzenie tematu usługi Service Bus, przy użyciu hello portalu Azure.
3. Utwórz temat toothat subskrypcji usługi Service Bus, przy użyciu hello portalu Azure.
4. Zapis temat toohello wiadomość toosend aplikacji konsoli.
5. Zapis tooreceive aplikacji konsoli tę wiadomość hello subskrypcji.

## <a name="prerequisites"></a>Wymagania wstępne

1. [Program Visual Studio w wersji 2015 lub nowszej](http://www.visualstudio.com). Przykłady Hello w tym samouczku Użyj Visual Studio 2017 r.
2. Subskrypcja platformy Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Tworzenie przestrzeni nazw przy użyciu hello portalu Azure

Jeśli utworzono już przestrzeń nazw usługi magistrali komunikatów, przejście toohello [utworzyć temat przy użyciu portalu Azure hello](#2-create-a-topic-using-the-azure-portal) sekcji.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a>2. Tworzenie tematu przy użyciu hello portalu Azure

1. Zaloguj się na toohello [portalu Azure][azure-portal].
2. W okienku nawigacji po lewej stronie powitania hello portalu kliknij **usługi Service Bus** (Jeśli nie widzisz **usługi Service Bus**, kliknij przycisk **więcej usług**).
3. Kliknij przestrzeń nazw hello, w którym chcesz toocreate hello tematu. zostanie wyświetlony blok Omówienie przestrzeni nazw Hello:
   
    ![Tworzenie tematu][createtopic1]
4. W hello **przestrzeni nazw usługi Service Bus** bloku, kliknij przycisk **tematy**, następnie kliknij przycisk **tematu Dodaj**.
   
    ![Wybieranie tematów][createtopic2]
5. Wprowadź nazwę dla tematu hello i usuń zaznaczenie pola wyboru hello **włączyć partycjonowania** opcji. Pozostaw hello inne opcje z wartościami domyślnymi.
   
    ![Wybieranie nowych kolejek][createtopic3]
6. U dołu hello hello bloku, kliknij przycisk **Utwórz**.

## <a name="3-create-a-subscription-toohello-topic"></a>3. Tworzenie tematu toohello subskrypcji

1. W okienku portalu zasobów hello kliknij hello przestrzeni nazw, który został utworzony w kroku 1, a następnie kliknij nazwę hello temat, który został utworzony w kroku 2.
2. Hello początku hello okienku przeglądu, kliknij hello plus obok Zaloguj za**subskrypcji** tooadd temat toothis subskrypcji.

    ![Tworzenie subskrypcji][createtopic4]

3. Wprowadź nazwę hello subskrypcji. Pozostaw hello inne opcje z wartościami domyślnymi.

## <a name="4-send-messages-toohello-topic"></a>4. Wysyłanie wiadomości toohello tematu

toosend wiadomości toohello tematu, możemy zapisać aplikacji konsolowej C# za pomocą programu Visual Studio.

### <a name="create-a-console-application"></a>Tworzenie aplikacji konsolowej

Uruchom program Visual Studio i utwórz nowy projekt **Aplikacja konsoli (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Dodaj pakiet NuGet usługi Service Bus hello

1. Kliknij prawym przyciskiem myszy hello nowo utworzonego projektu i wybierz **Zarządzaj pakietami NuGet**.
2. Kliknij hello **Przeglądaj** karcie, wyszukaj **Microsoft Azure Service Bus**, a następnie wybierz hello **WindowsAzure.ServiceBus** elementu. Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij to okno dialogowe.
   
    ![Wybieranie pakietu NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a>Zapis niektórych toosend kodu temat toohello wiadomość

1. Dodaj następujące hello `using` toohello instrukcji na początku pliku Program.cs hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Dodaj hello następującego kodu toohello `Main` metody. Zestaw hello `connectionString` połączenia toohello zmiennej ciągu uzyskane podczas tworzenia hello przestrzeni nazw i ustawić `topicName` nazwa toohello, który został użyty podczas tworzenia tematu hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
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

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Uruchom hello program i sprawdź hello portalu Azure: kliknij nazwę hello tematu w przestrzeni nazw hello **omówienie** bloku. temat Hello **Essentials** bloku jest wyświetlany. W subskrypcji hello wymienione na dole bloku hello hello, zwróć uwagę, że hello **liczba komunikatów** wartość dla każdej subskrypcji teraz powinna wynosić 1. Każdym uruchomieniu aplikacji nadawcy hello bez pobierania wiadomości powitania (zgodnie z opisem w następnej sekcji hello), wartość ta zwiększa się o 1. Należy również zauważyć, bieżący rozmiar hello tego hello tematu zwiększa hello **bieżącego** wartości na powitania **Essentials** bloku zawsze aplikacji hello dodaje toohello komunikat tematu/subskrypcji.
   
      ![Rozmiar komunikatu][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a>5. Odbieranie komunikatów z subskrypcji hello

1. wiadomość hello tooreceive lub wysłanych wiadomości tak, Utwórz nową aplikację konsoli, a następnie dodaj pakiet NuGet usługi Service Bus toohello odwołania, podobne toohello poprzedniej aplikacji nadawcy.
2. Dodaj następujące hello `using` toohello instrukcji na początku pliku Program.cs hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Dodaj hello następującego kodu toohello `Main` metody. Zestaw hello `connectionString` połączenia toohello zmiennej ciągu uzyskane podczas tworzenia hello przestrzeni nazw i ustawić `topicName` nazwa toohello, który został użyty podczas tworzenia tematu hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
4. Uruchom hello program i ponownie sprawdzić hello portalu. Zwróć uwagę, że hello **liczba komunikatów** i **bieżącego** wartości są teraz 0.
   
    ![Długość tematu][topic-message-receive]

Gratulacje! Zostały utworzone temat i subskrypcja, wysłano komunikat i odebrano ten komunikat.

## <a name="next-steps"></a>Następne kroki

Zapoznaj się z naszym [repozytorium GitHub i przykłady](https://github.com/Azure/azure-service-bus/tree/master/samples) który przedstawiono niektóre hello bardziej zaawansowane funkcje komunikatów usługi Service Bus.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
