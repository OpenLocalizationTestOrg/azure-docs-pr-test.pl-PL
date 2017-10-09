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
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="6f401-103">Wprowadzenie do kolejek usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="6f401-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="6f401-104">Co zostanie osiągnięte?</span><span class="sxs-lookup"><span data-stu-id="6f401-104">What will be accomplished</span></span>
<span data-ttu-id="6f401-105">Ten samouczek obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6f401-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="6f401-106">Tworzenie przestrzeni nazw usługi Service Bus, przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6f401-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="6f401-107">Tworzenie kolejki usługi Service Bus, przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6f401-107">Create a Service Bus queue, using hello Azure portal.</span></span>
3. <span data-ttu-id="6f401-108">Napisz wiadomość toosend aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="6f401-108">Write a console application toosend a message.</span></span>
4. <span data-ttu-id="6f401-109">Pisanie wiadomości wysłanych w poprzednim kroku hello hello tooreceive aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="6f401-109">Write a console application tooreceive hello messages sent in hello previous step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f401-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6f401-110">Prerequisites</span></span>
1. <span data-ttu-id="6f401-111">[Program Visual Studio w wersji 2015 lub nowszej](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="6f401-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="6f401-112">Przykłady Hello w tym samouczku Użyj Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="6f401-112">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="6f401-113">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f401-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="6f401-114">1. Tworzenie przestrzeni nazw przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6f401-114">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="6f401-115">Jeśli została już utworzona przestrzeń nazw usługi magistrali komunikatów, przejście toohello [Tworzenie kolejki przy użyciu portalu Azure hello](#2-create-a-queue-using-the-azure-portal) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6f401-115">If you've already created a Service Bus Messaging namespace, jump toohello [Create a queue using hello Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a><span data-ttu-id="6f401-116">2. Tworzenie kolejki przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6f401-116">2. Create a queue using hello Azure portal</span></span>
<span data-ttu-id="6f401-117">Jeśli utworzono już kolejki usługi Service Bus, przejście toohello [wysyłania wiadomości toohello kolejki](#3-send-messages-to-the-queue) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6f401-117">If you have already created a Service Bus queue, jump toohello [Send messages toohello queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a><span data-ttu-id="6f401-118">3. Komunikaty toohello kolejki wysyłania</span><span class="sxs-lookup"><span data-stu-id="6f401-118">3. Send messages toohello queue</span></span>
<span data-ttu-id="6f401-119">Kolejka toohello wiadomości toosend, możemy zapisać aplikacji konsolowej C# za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6f401-119">toosend messages toohello queue, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="6f401-120">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="6f401-120">Create a console application</span></span>

<span data-ttu-id="6f401-121">Uruchom program Visual Studio i utwórz nowy projekt **Aplikacja konsoli (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="6f401-121">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="6f401-122">Dodaj pakiet NuGet usługi Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="6f401-122">Add hello Service Bus NuGet package</span></span>
1. <span data-ttu-id="6f401-123">Kliknij prawym przyciskiem myszy hello nowo utworzonego projektu i wybierz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6f401-123">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="6f401-124">Kliknij hello **Przeglądaj** karcie, wyszukaj **Microsoft Azure Service Bus**, a następnie wybierz hello **WindowsAzure.ServiceBus** elementu.</span><span class="sxs-lookup"><span data-stu-id="6f401-124">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="6f401-125">Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="6f401-125">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Wybieranie pakietu NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a><span data-ttu-id="6f401-127">Zapis niektórych toosend kodu toohello kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="6f401-127">Write some code toosend a message toohello queue</span></span>
1. <span data-ttu-id="6f401-128">Dodaj następujące hello `using` toohello instrukcji na początku pliku Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="6f401-128">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="6f401-129">Dodaj hello następującego kodu toohello `Main` metody.</span><span class="sxs-lookup"><span data-stu-id="6f401-129">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="6f401-130">Zestaw hello `connectionString` połączenia toohello zmiennej ciągu uzyskane podczas tworzenia hello przestrzeni nazw i ustawić `queueName` toohello Nazwa kolejki, który został użyty podczas tworzenia kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="6f401-130">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
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
   
    <span data-ttu-id="6f401-131">Oto jak powinien wyglądać plik Program.cs:</span><span class="sxs-lookup"><span data-stu-id="6f401-131">Here is what your Program.cs file should look like.</span></span>
   
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
3. <span data-ttu-id="6f401-132">Uruchom hello program i sprawdź hello portalu Azure: kliknij nazwę swojej kolejki w przestrzeni nazw hello hello **omówienie** bloku.</span><span class="sxs-lookup"><span data-stu-id="6f401-132">Run hello program, and check hello Azure portal: click hello name of your queue in hello namespace **Overview** blade.</span></span> <span data-ttu-id="6f401-133">kolejki Hello **Essentials** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="6f401-133">hello queue **Essentials** blade is displayed.</span></span> <span data-ttu-id="6f401-134">Zwróć uwagę, że hello **liczby aktywnych komunikat** wartość powinna być teraz 1.</span><span class="sxs-lookup"><span data-stu-id="6f401-134">Notice that hello **Active Message Count** value should now be 1.</span></span> <span data-ttu-id="6f401-135">Zawsze, gdy zostanie uruchomiony bez pobierania wiadomości powitania aplikację sender hello tej wartości zwiększa się o 1.</span><span class="sxs-lookup"><span data-stu-id="6f401-135">Each time you run hello sender application without retrieving hello messages, this value increases by 1.</span></span> <span data-ttu-id="6f401-136">Należy pamiętać, że bieżący rozmiar kolejki hello hello zwiększa każdej aplikacji hello czasu dodaje również toohello kolejki komunikatów.</span><span class="sxs-lookup"><span data-stu-id="6f401-136">Also note that hello current size of hello queue increments each time hello app adds a message toohello queue.</span></span>
   
      ![Rozmiar komunikatu][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a><span data-ttu-id="6f401-138">4. Odbieranie komunikatów z kolejki hello</span><span class="sxs-lookup"><span data-stu-id="6f401-138">4. Receive messages from hello queue</span></span>

1. <span data-ttu-id="6f401-139">wiadomości powitania tooreceive właśnie wysłane, Utwórz nową aplikację konsoli i dodawanie pakietu NuGet usługi Service Bus toohello odwołania, podobne toohello poprzedniej aplikacji nadawcy.</span><span class="sxs-lookup"><span data-stu-id="6f401-139">tooreceive hello messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="6f401-140">Dodaj następujące hello `using` toohello instrukcji na początku pliku Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="6f401-140">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="6f401-141">Dodaj hello następującego kodu toohello `Main` metody.</span><span class="sxs-lookup"><span data-stu-id="6f401-141">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="6f401-142">Zestaw hello `connectionString` toohello zmiennej ciąg połączenia, który został uzyskany podczas tworzenia hello przestrzeni nazw i ustaw `queueName` toohello Nazwa kolejki, który został użyty podczas tworzenia kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="6f401-142">Set hello `connectionString` variable toohello connection string that was obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
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
   
    <span data-ttu-id="6f401-143">Oto jak powinien wyglądać plik Program.cs:</span><span class="sxs-lookup"><span data-stu-id="6f401-143">Here is what your Program.cs file should look like:</span></span>
   
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
4. <span data-ttu-id="6f401-144">Uruchom hello program i ponownie sprawdzić hello portalu.</span><span class="sxs-lookup"><span data-stu-id="6f401-144">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="6f401-145">Zwróć uwagę, że hello **liczby aktywnych komunikat** i **bieżącego** wartości są teraz 0.</span><span class="sxs-lookup"><span data-stu-id="6f401-145">Notice that hello **Active Message Count** and **Current** values are now 0.</span></span>
   
    ![Długość kolejki][queue-message-receive]

<span data-ttu-id="6f401-147">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="6f401-147">Congratulations!</span></span> <span data-ttu-id="6f401-148">Utworzono kolejkę, wysłano komunikat i odebrano komunikat.</span><span class="sxs-lookup"><span data-stu-id="6f401-148">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f401-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f401-149">Next steps</span></span>

<span data-ttu-id="6f401-150">Zapoznaj się z naszym [repozytorium GitHub i przykłady](https://github.com/Azure/azure-service-bus/tree/master/samples) który przedstawiono niektóre hello bardziej zaawansowane funkcje komunikatów usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6f401-150">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
