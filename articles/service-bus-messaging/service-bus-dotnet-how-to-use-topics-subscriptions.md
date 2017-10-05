---
title: "Rozpoczynanie pracy z tematami i subskrypcjami usługi Azure Service Bus | Microsoft Docs"
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
ms.openlocfilehash: 9401ada519f600b0d2817f06a396e16607a24129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="5c5ce-103">Wprowadzenie do tematów usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="5c5ce-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="5c5ce-104">Co zostanie osiągnięte?</span><span class="sxs-lookup"><span data-stu-id="5c5ce-104">What will be accomplished</span></span>

<span data-ttu-id="5c5ce-105">Ten samouczek obejmuje następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5c5ce-105">This tutorial covers the following steps:</span></span>

1. <span data-ttu-id="5c5ce-106">Utworzenie przestrzeni nazw usługi Service Bus za pomocą usługi Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-106">Create a Service Bus namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="5c5ce-107">Utworzenie tematu usługi Service Bus przy użyciu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-107">Create a Service Bus topic, using the Azure portal.</span></span>
3. <span data-ttu-id="5c5ce-108">Utworzenie subskrypcji tego tematu usługi Service Bus przy użyciu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-108">Create a Service Bus subscription to that topic, using the Azure portal.</span></span>
4. <span data-ttu-id="5c5ce-109">Napisanie aplikacji konsolowej służącej do wysyłania komunikatu do tematu.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-109">Write a console application to send a message to the topic.</span></span>
5. <span data-ttu-id="5c5ce-110">Napisanie aplikacji konsolowej służącej do odbierania tego komunikatu z subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-110">Write a console application to receive that message from the subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c5ce-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5c5ce-111">Prerequisites</span></span>

1. <span data-ttu-id="5c5ce-112">[Program Visual Studio w wersji 2015 lub nowszej](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="5c5ce-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="5c5ce-113">W przykładach znajdujących się w tym samouczku używany jest program Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-113">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="5c5ce-114">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="5c5ce-115">1. Tworzenie przestrzeni nazw za pomocą usługi Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5c5ce-115">1. Create a namespace using the Azure portal</span></span>

<span data-ttu-id="5c5ce-116">Jeśli przestrzeń nazw obsługi komunikatów usługi Service Bus została już utworzona, przejdź do sekcji [Tworzenie tematu przy użyciu witryny Azure Portal](#2-create-a-topic-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="5c5ce-116">If you have already created a Service Bus Messaging namespace, jump to the [Create a topic using the Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-the-azure-portal"></a><span data-ttu-id="5c5ce-117">2. Tworzenie tematu przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5c5ce-117">2. Create a topic using the Azure portal</span></span>

1. <span data-ttu-id="5c5ce-118">Zaloguj się w witrynie [Azure Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="5c5ce-118">Log on to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="5c5ce-119">W lewym okienku nawigacji portalu kliknij pozycję **Service Bus** (jeśli pozycja **Service Bus** nie jest widoczna, kliknij pozycję **Więcej usług**).</span><span class="sxs-lookup"><span data-stu-id="5c5ce-119">In the left navigation pane of the portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="5c5ce-120">Kliknij przestrzeń nazw, w której chcesz utworzyć temat.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-120">Click the namespace in which you would like to create the topic.</span></span> <span data-ttu-id="5c5ce-121">Zostanie wyświetlony blok Przegląd przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="5c5ce-121">The namespace overview blade appears:</span></span>
   
    ![Tworzenie tematu][createtopic1]
4. <span data-ttu-id="5c5ce-123">W bloku **Przestrzeń nazw usługi Service Bus** kliknij pozycję **Tematy**, a następnie kliknij przycisk **Dodaj temat**.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-123">In the **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Wybieranie tematów][createtopic2]
5. <span data-ttu-id="5c5ce-125">Wprowadź nazwę tematu i usuń zaznaczenie opcji **Włącz partycjonowanie**.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-125">Enter a name for the topic, and uncheck the **Enable partitioning** option.</span></span> <span data-ttu-id="5c5ce-126">Pozostaw inne opcje z wartościami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-126">Leave the other options with their default values.</span></span>
   
    ![Wybieranie nowych kolejek][createtopic3]
6. <span data-ttu-id="5c5ce-128">W dolnej części bloku kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-128">At the bottom of the blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-to-the-topic"></a><span data-ttu-id="5c5ce-129">3. Tworzenie subskrypcji tematu</span><span class="sxs-lookup"><span data-stu-id="5c5ce-129">3. Create a subscription to the topic</span></span>

1. <span data-ttu-id="5c5ce-130">W okienku zasobów portalu kliknij przestrzeń nazw utworzoną w kroku 1, a następnie kliknij nazwę tematu utworzonego w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-130">In the portal resources pane, click the namespace you created in step 1, then click name of the topic you created in step 2.</span></span>
2. <span data-ttu-id="5c5ce-131">W górnej części okienka Przegląd kliknij znak plus obok pozycji **Subskrypcja**, aby dodać subskrypcję do tego tematu.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-131">A the top of the overview pane, click the plus sign next to **Subscription** to add a subscription to this topic.</span></span>

    ![Tworzenie subskrypcji][createtopic4]

3. <span data-ttu-id="5c5ce-133">Wprowadź nazwę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-133">Enter a name for the subscription.</span></span> <span data-ttu-id="5c5ce-134">Pozostaw inne opcje z wartościami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-134">Leave the other options with their default values.</span></span>

## <a name="4-send-messages-to-the-topic"></a><span data-ttu-id="5c5ce-135">4. Wysyłanie komunikatów do tematu</span><span class="sxs-lookup"><span data-stu-id="5c5ce-135">4. Send messages to the topic</span></span>

<span data-ttu-id="5c5ce-136">Aby wysyłać komunikaty do tematu, napiszemy aplikację konsolową w języku C# za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-136">To send messages to the topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="5c5ce-137">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="5c5ce-137">Create a console application</span></span>

<span data-ttu-id="5c5ce-138">Uruchom program Visual Studio i utwórz nowy projekt **Aplikacja konsoli (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-the-service-bus-nuget-package"></a><span data-ttu-id="5c5ce-139">Dodawanie pakietu NuGet usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="5c5ce-139">Add the Service Bus NuGet package</span></span>

1. <span data-ttu-id="5c5ce-140">Kliknij prawym przyciskiem myszy nowo utworzony projekt i wybierz pozycję **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-140">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="5c5ce-141">Kliknij kartę **Przeglądaj**, wyszukaj ciąg **Microsoft Azure Service Bus**, a następnie wybierz element **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-141">Click the **Browse** tab, search for **Microsoft Azure Service Bus**, and then select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="5c5ce-142">Kliknij przycisk **Zainstaluj**, aby ukończyć instalację, a następnie zamknij to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-142">Click **Install** to complete the installation, then close this dialog box.</span></span>
   
    ![Wybieranie pakietu NuGet][nuget-pkg]

### <a name="write-some-code-to-send-a-message-to-the-topic"></a><span data-ttu-id="5c5ce-144">Pisanie kodu służącego do wysyłania komunikatów do tematu</span><span class="sxs-lookup"><span data-stu-id="5c5ce-144">Write some code to send a message to the topic</span></span>

1. <span data-ttu-id="5c5ce-145">Dodaj następującą instrukcję `using` na początku pliku Program.cs.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-145">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="5c5ce-146">Dodaj następujący kod do metody `Main`:</span><span class="sxs-lookup"><span data-stu-id="5c5ce-146">Add the following code to the `Main` method.</span></span> <span data-ttu-id="5c5ce-147">Ustaw jako zmienną `connectionString` parametry połączenia, które zostały uzyskane podczas tworzenia przestrzeni nazw, a następnie ustaw jako zmienną `topicName` nazwę tematu użytą podczas tworzenia tematu.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-147">Set the `connectionString` variable to the connection string that you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="5c5ce-148">Oto jak powinien wyglądać plik Program.cs:</span><span class="sxs-lookup"><span data-stu-id="5c5ce-148">Here is what your Program.cs file should look like.</span></span>
   
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

                Console.WriteLine("Message successfully sent! Press ENTER to exit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="5c5ce-149">Uruchom program i sprawdź witrynę Azure Portal: kliknij nazwę swojego tematu w bloku **Przegląd** przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-149">Run the program, and check the Azure portal: click the name of your topic in the namespace **Overview** blade.</span></span> <span data-ttu-id="5c5ce-150">Zostanie wyświetlony blok **Podstawowe elementy** tematu.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-150">The topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="5c5ce-151">W subskrypcjach wyświetlanych w dolnej części bloku wartość pola **Liczba komunikatów** dla każdej subskrypcji powinna teraz wynosić 1.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-151">In the subscription(s) listed near the bottom of the blade, notice that the **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="5c5ce-152">Przy każdym uruchomieniu aplikacji nadawcy bez pobierania komunikatów (zgodnie z opisem w następnej sekcji) ta wartość zwiększa się o 1.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-152">Each time you run the sender application without retrieving the messages (as described in the next section), this value increases by 1.</span></span> <span data-ttu-id="5c5ce-153">Należy również zauważyć, że bieżący rozmiar tematu zwiększa wartość **Bieżące** w bloku **Podstawowe elementy** za każdym razem, kiedy aplikacja dodaje komunikat do tematu/subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-153">Also note that the current size of the topic increments the **Current** value on the **Essentials** blade each time the app adds a message to the topic/subscription.</span></span>
   
      ![Rozmiar komunikatu][topic-message]

## <a name="5-receive-messages-from-the-subscription"></a><span data-ttu-id="5c5ce-155">5. Odbieranie komunikatów z subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5c5ce-155">5. Receive messages from the subscription</span></span>

1. <span data-ttu-id="5c5ce-156">Aby odbierać komunikat (lub komunikaty) wysłane w poprzednim kroku, utwórz nową aplikację konsolową i dodaj odwołanie do pakietu NuGet usługi Service Bus, podobnie jak w przypadku poprzedniej aplikacji nadawcy.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-156">To receive the message or messages you just sent, create a new console application and add a reference to the Service Bus NuGet package, similar to the previous sender application.</span></span>
2. <span data-ttu-id="5c5ce-157">Dodaj następującą instrukcję `using` na początku pliku Program.cs.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-157">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="5c5ce-158">Dodaj następujący kod do metody `Main`:</span><span class="sxs-lookup"><span data-stu-id="5c5ce-158">Add the following code to the `Main` method.</span></span> <span data-ttu-id="5c5ce-159">Ustaw jako zmienną `connectionString` parametry połączenia, które zostały uzyskane podczas tworzenia przestrzeni nazw, a następnie ustaw jako zmienną `topicName` nazwę tematu użytą podczas tworzenia tematu.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-159">Set the `connectionString` variable to the connection string you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="5c5ce-160">Oto jak powinien wyglądać plik Program.cs:</span><span class="sxs-lookup"><span data-stu-id="5c5ce-160">Here is what your Program.cs file should look like:</span></span>
   
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

          Console.WriteLine("Press ENTER to exit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="5c5ce-161">Uruchom program i ponownie sprawdź portal.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-161">Run the program, and check the portal again.</span></span> <span data-ttu-id="5c5ce-162">Zauważ, że wartości **Liczba komunikatów** i **Bieżące** powinny teraz wynosić 0.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-162">Notice that the **Message Count** and **Current** values are now 0.</span></span>
   
    ![Długość tematu][topic-message-receive]

<span data-ttu-id="5c5ce-164">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="5c5ce-164">Congratulations!</span></span> <span data-ttu-id="5c5ce-165">Zostały utworzone temat i subskrypcja, wysłano komunikat i odebrano ten komunikat.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c5ce-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5c5ce-166">Next steps</span></span>

<span data-ttu-id="5c5ce-167">Zapoznaj się z naszym [repozytorium GitHub zawierającym przykłady](https://github.com/Azure/azure-service-bus/tree/master/samples), które pokazują niektóre bardziej zaawansowane funkcje obsługi komunikatów usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5c5ce-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of the more advanced features of Service Bus messaging.</span></span>

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
