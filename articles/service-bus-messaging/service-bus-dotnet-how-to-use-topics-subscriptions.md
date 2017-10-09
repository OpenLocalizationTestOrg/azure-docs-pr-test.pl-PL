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
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="2c0b5-103">Wprowadzenie do tematów usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="2c0b5-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="2c0b5-104">Co zostanie osiągnięte?</span><span class="sxs-lookup"><span data-stu-id="2c0b5-104">What will be accomplished</span></span>

<span data-ttu-id="2c0b5-105">Ten samouczek obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2c0b5-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="2c0b5-106">Tworzenie przestrzeni nazw usługi Service Bus, przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="2c0b5-107">Tworzenie tematu usługi Service Bus, przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-107">Create a Service Bus topic, using hello Azure portal.</span></span>
3. <span data-ttu-id="2c0b5-108">Utwórz temat toothat subskrypcji usługi Service Bus, przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-108">Create a Service Bus subscription toothat topic, using hello Azure portal.</span></span>
4. <span data-ttu-id="2c0b5-109">Zapis temat toohello wiadomość toosend aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-109">Write a console application toosend a message toohello topic.</span></span>
5. <span data-ttu-id="2c0b5-110">Zapis tooreceive aplikacji konsoli tę wiadomość hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-110">Write a console application tooreceive that message from hello subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c0b5-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2c0b5-111">Prerequisites</span></span>

1. <span data-ttu-id="2c0b5-112">[Program Visual Studio w wersji 2015 lub nowszej](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="2c0b5-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="2c0b5-113">Przykłady Hello w tym samouczku Użyj Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-113">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="2c0b5-114">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="2c0b5-115">1. Tworzenie przestrzeni nazw przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2c0b5-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="2c0b5-116">Jeśli utworzono już przestrzeń nazw usługi magistrali komunikatów, przejście toohello [utworzyć temat przy użyciu portalu Azure hello](#2-create-a-topic-using-the-azure-portal) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-116">If you have already created a Service Bus Messaging namespace, jump toohello [Create a topic using hello Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a><span data-ttu-id="2c0b5-117">2. Tworzenie tematu przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2c0b5-117">2. Create a topic using hello Azure portal</span></span>

1. <span data-ttu-id="2c0b5-118">Zaloguj się na toohello [portalu Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="2c0b5-118">Log on toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="2c0b5-119">W okienku nawigacji po lewej stronie powitania hello portalu kliknij **usługi Service Bus** (Jeśli nie widzisz **usługi Service Bus**, kliknij przycisk **więcej usług**).</span><span class="sxs-lookup"><span data-stu-id="2c0b5-119">In hello left navigation pane of hello portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="2c0b5-120">Kliknij przestrzeń nazw hello, w którym chcesz toocreate hello tematu.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-120">Click hello namespace in which you would like toocreate hello topic.</span></span> <span data-ttu-id="2c0b5-121">zostanie wyświetlony blok Omówienie przestrzeni nazw Hello:</span><span class="sxs-lookup"><span data-stu-id="2c0b5-121">hello namespace overview blade appears:</span></span>
   
    ![Tworzenie tematu][createtopic1]
4. <span data-ttu-id="2c0b5-123">W hello **przestrzeni nazw usługi Service Bus** bloku, kliknij przycisk **tematy**, następnie kliknij przycisk **tematu Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-123">In hello **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Wybieranie tematów][createtopic2]
5. <span data-ttu-id="2c0b5-125">Wprowadź nazwę dla tematu hello i usuń zaznaczenie pola wyboru hello **włączyć partycjonowania** opcji.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-125">Enter a name for hello topic, and uncheck hello **Enable partitioning** option.</span></span> <span data-ttu-id="2c0b5-126">Pozostaw hello inne opcje z wartościami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-126">Leave hello other options with their default values.</span></span>
   
    ![Wybieranie nowych kolejek][createtopic3]
6. <span data-ttu-id="2c0b5-128">U dołu hello hello bloku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-128">At hello bottom of hello blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-toohello-topic"></a><span data-ttu-id="2c0b5-129">3. Tworzenie tematu toohello subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2c0b5-129">3. Create a subscription toohello topic</span></span>

1. <span data-ttu-id="2c0b5-130">W okienku portalu zasobów hello kliknij hello przestrzeni nazw, który został utworzony w kroku 1, a następnie kliknij nazwę hello temat, który został utworzony w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-130">In hello portal resources pane, click hello namespace you created in step 1, then click name of hello topic you created in step 2.</span></span>
2. <span data-ttu-id="2c0b5-131">Hello początku hello okienku przeglądu, kliknij hello plus obok Zaloguj za**subskrypcji** tooadd temat toothis subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-131">A hello top of hello overview pane, click hello plus sign next too**Subscription** tooadd a subscription toothis topic.</span></span>

    ![Tworzenie subskrypcji][createtopic4]

3. <span data-ttu-id="2c0b5-133">Wprowadź nazwę hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-133">Enter a name for hello subscription.</span></span> <span data-ttu-id="2c0b5-134">Pozostaw hello inne opcje z wartościami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-134">Leave hello other options with their default values.</span></span>

## <a name="4-send-messages-toohello-topic"></a><span data-ttu-id="2c0b5-135">4. Wysyłanie wiadomości toohello tematu</span><span class="sxs-lookup"><span data-stu-id="2c0b5-135">4. Send messages toohello topic</span></span>

<span data-ttu-id="2c0b5-136">toosend wiadomości toohello tematu, możemy zapisać aplikacji konsolowej C# za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-136">toosend messages toohello topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="2c0b5-137">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="2c0b5-137">Create a console application</span></span>

<span data-ttu-id="2c0b5-138">Uruchom program Visual Studio i utwórz nowy projekt **Aplikacja konsoli (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="2c0b5-139">Dodaj pakiet NuGet usługi Service Bus hello</span><span class="sxs-lookup"><span data-stu-id="2c0b5-139">Add hello Service Bus NuGet package</span></span>

1. <span data-ttu-id="2c0b5-140">Kliknij prawym przyciskiem myszy hello nowo utworzonego projektu i wybierz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-140">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="2c0b5-141">Kliknij hello **Przeglądaj** karcie, wyszukaj **Microsoft Azure Service Bus**, a następnie wybierz hello **WindowsAzure.ServiceBus** elementu.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-141">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="2c0b5-142">Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-142">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Wybieranie pakietu NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a><span data-ttu-id="2c0b5-144">Zapis niektórych toosend kodu temat toohello wiadomość</span><span class="sxs-lookup"><span data-stu-id="2c0b5-144">Write some code toosend a message toohello topic</span></span>

1. <span data-ttu-id="2c0b5-145">Dodaj następujące hello `using` toohello instrukcji na początku pliku Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-145">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="2c0b5-146">Dodaj hello następującego kodu toohello `Main` metody.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-146">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="2c0b5-147">Zestaw hello `connectionString` połączenia toohello zmiennej ciągu uzyskane podczas tworzenia hello przestrzeni nazw i ustawić `topicName` nazwa toohello, który został użyty podczas tworzenia tematu hello.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-147">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
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
   
    <span data-ttu-id="2c0b5-148">Oto jak powinien wyglądać plik Program.cs:</span><span class="sxs-lookup"><span data-stu-id="2c0b5-148">Here is what your Program.cs file should look like.</span></span>
   
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
3. <span data-ttu-id="2c0b5-149">Uruchom hello program i sprawdź hello portalu Azure: kliknij nazwę hello tematu w przestrzeni nazw hello **omówienie** bloku.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-149">Run hello program, and check hello Azure portal: click hello name of your topic in hello namespace **Overview** blade.</span></span> <span data-ttu-id="2c0b5-150">temat Hello **Essentials** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-150">hello topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="2c0b5-151">W subskrypcji hello wymienione na dole bloku hello hello, zwróć uwagę, że hello **liczba komunikatów** wartość dla każdej subskrypcji teraz powinna wynosić 1.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-151">In hello subscription(s) listed near hello bottom of hello blade, notice that hello **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="2c0b5-152">Każdym uruchomieniu aplikacji nadawcy hello bez pobierania wiadomości powitania (zgodnie z opisem w następnej sekcji hello), wartość ta zwiększa się o 1.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-152">Each time you run hello sender application without retrieving hello messages (as described in hello next section), this value increases by 1.</span></span> <span data-ttu-id="2c0b5-153">Należy również zauważyć, bieżący rozmiar hello tego hello tematu zwiększa hello **bieżącego** wartości na powitania **Essentials** bloku zawsze aplikacji hello dodaje toohello komunikat tematu/subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-153">Also note that hello current size of hello topic increments hello **Current** value on hello **Essentials** blade each time hello app adds a message toohello topic/subscription.</span></span>
   
      ![Rozmiar komunikatu][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a><span data-ttu-id="2c0b5-155">5. Odbieranie komunikatów z subskrypcji hello</span><span class="sxs-lookup"><span data-stu-id="2c0b5-155">5. Receive messages from hello subscription</span></span>

1. <span data-ttu-id="2c0b5-156">wiadomość hello tooreceive lub wysłanych wiadomości tak, Utwórz nową aplikację konsoli, a następnie dodaj pakiet NuGet usługi Service Bus toohello odwołania, podobne toohello poprzedniej aplikacji nadawcy.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-156">tooreceive hello message or messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="2c0b5-157">Dodaj następujące hello `using` toohello instrukcji na początku pliku Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-157">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="2c0b5-158">Dodaj hello następującego kodu toohello `Main` metody.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-158">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="2c0b5-159">Zestaw hello `connectionString` połączenia toohello zmiennej ciągu uzyskane podczas tworzenia hello przestrzeni nazw i ustawić `topicName` nazwa toohello, który został użyty podczas tworzenia tematu hello.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-159">Set hello `connectionString` variable toohello connection string you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
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
   
    <span data-ttu-id="2c0b5-160">Oto jak powinien wyglądać plik Program.cs:</span><span class="sxs-lookup"><span data-stu-id="2c0b5-160">Here is what your Program.cs file should look like:</span></span>
   
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
4. <span data-ttu-id="2c0b5-161">Uruchom hello program i ponownie sprawdzić hello portalu.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-161">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="2c0b5-162">Zwróć uwagę, że hello **liczba komunikatów** i **bieżącego** wartości są teraz 0.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-162">Notice that hello **Message Count** and **Current** values are now 0.</span></span>
   
    ![Długość tematu][topic-message-receive]

<span data-ttu-id="2c0b5-164">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="2c0b5-164">Congratulations!</span></span> <span data-ttu-id="2c0b5-165">Zostały utworzone temat i subskrypcja, wysłano komunikat i odebrano ten komunikat.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c0b5-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2c0b5-166">Next steps</span></span>

<span data-ttu-id="2c0b5-167">Zapoznaj się z naszym [repozytorium GitHub i przykłady](https://github.com/Azure/azure-service-bus/tree/master/samples) który przedstawiono niektóre hello bardziej zaawansowane funkcje komunikatów usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2c0b5-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

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
