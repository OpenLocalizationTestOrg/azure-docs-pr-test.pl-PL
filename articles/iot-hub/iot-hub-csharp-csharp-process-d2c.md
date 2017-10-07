---
title: "komunikaty urządzenia do chmury Azure IoT Hub aaaProcess przy użyciu tras (.Net) | Dokumentacja firmy Microsoft"
description: "Jak tooprocess Centrum IoT wiadomości urządzenia do chmury przy użyciu reguł routingu oraz niestandardowe punkty końcowe toodispatch komunikatów tooother usług zaplecza."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a><span data-ttu-id="492d2-103">Przetwarzanie wiadomości urządzenia do chmury Centrum IoT przy użyciu tras (.NET)</span><span class="sxs-lookup"><span data-stu-id="492d2-103">Process IoT Hub device-to-cloud messages using routes (.NET)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="492d2-104">W tym samouczku opiera się na powitania [Rozpoczynanie pracy z Centrum IoT] samouczka.</span><span class="sxs-lookup"><span data-stu-id="492d2-104">This tutorial builds on hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="492d2-105">Samouczek Hello:</span><span class="sxs-lookup"><span data-stu-id="492d2-105">hello tutorial:</span></span>

* <span data-ttu-id="492d2-106">Pokazuje, jak toouse routing zasady toodispatch urządzenia do chmury wiadomości w sposób łatwy, na podstawie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="492d2-106">Shows you how toouse routing rules toodispatch device-to-cloud messages in an easy, configuration-based way.</span></span>
* <span data-ttu-id="492d2-107">Pokazuje, jak tooisolate interakcyjne komunikaty, które wymagają natychmiastowego działania z rozwiązania hello zaplecza dla dalszego przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="492d2-107">Illustrates how tooisolate interactive messages that require immediate action from hello solution back end for further processing.</span></span> <span data-ttu-id="492d2-108">Na przykład urządzenie może wysłać komunikat alarmu, które wyzwala Wstawianie biletu do systemu CRM.</span><span class="sxs-lookup"><span data-stu-id="492d2-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="492d2-109">Z kolei wiadomości punktu danych, takich jak telemetrii temperatury źródła danych do aparatu analizy.</span><span class="sxs-lookup"><span data-stu-id="492d2-109">In contrast, data-point messages, such as temperature telemetry, feed into an analytics engine.</span></span>

<span data-ttu-id="492d2-110">Na końcu hello tego samouczka możesz uruchomić trzech aplikacji konsoli .NET:</span><span class="sxs-lookup"><span data-stu-id="492d2-110">At hello end of this tutorial, you run three .NET console apps:</span></span>

* <span data-ttu-id="492d2-111">**SimulatedDevice**, zmodyfikowanej wersji aplikacji hello utworzone w hello [Rozpoczynanie pracy z Centrum IoT] samouczek wysyła komunikaty urządzenia do chmury punktu danych co sekundę i interaktywne urządzenia do chmury wiadomości co 10 Liczba sekund.</span><span class="sxs-lookup"><span data-stu-id="492d2-111">**SimulatedDevice**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span>
* <span data-ttu-id="492d2-112">**ReadDeviceToCloudMessages** czy wyświetla hello niekrytyczne telemetrii wysyłane przez aplikację na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="492d2-112">**ReadDeviceToCloudMessages** that displays hello non-critical telemetry sent by your device app.</span></span>
* <span data-ttu-id="492d2-113">**ReadCriticalQueue** usuwania kolejki hello krytycznych wiadomości wysyłane przez aplikację urządzenia z kolejki usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="492d2-113">**ReadCriticalQueue** de-queues hello critical messages sent by your device app from a Service Bus queue.</span></span> <span data-ttu-id="492d2-114">Kolejka jest dołączona toohello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="492d2-114">This queue is attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="492d2-115">Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków, w tym C, Java i JavaScript.</span><span class="sxs-lookup"><span data-stu-id="492d2-115">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="492d2-116">toolearn tooreplace hello symulowane urządzenie z tego samouczka z urządzenia fizycznego, zobacz hello [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="492d2-116">toolearn how tooreplace hello simulated device in this tutorial with a physical device, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="492d2-117">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="492d2-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="492d2-118">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="492d2-118">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="492d2-119">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="492d2-119">An active Azure account.</span></span> <br/><span data-ttu-id="492d2-120">Jeśli nie masz konta, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/) w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="492d2-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="492d2-121">Powinien mieć niektóre podstawową wiedzę na temat [usługi Azure Storage] i [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="492d2-121">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages"></a><span data-ttu-id="492d2-122">Wysyłanie komunikatów interakcyjne</span><span class="sxs-lookup"><span data-stu-id="492d2-122">Send interactive messages</span></span>

<span data-ttu-id="492d2-123">Modyfikowanie aplikacji urządzenia hello utworzony w hello [Rozpoczynanie pracy z Centrum IoT] toooccasionally samouczka wysyłać interaktywnego.</span><span class="sxs-lookup"><span data-stu-id="492d2-123">Modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send interactive messages.</span></span>

<span data-ttu-id="492d2-124">W programie Visual Studio w hello **SimulatedDevice** projekt, Zastąp hello `SendDeviceToCloudMessagesAsync` metody z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="492d2-124">In Visual Studio, in hello **SimulatedDevice** project, replace hello `SendDeviceToCloudMessagesAsync` method with hello following code:</span></span>

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

<span data-ttu-id="492d2-125">Ta metoda losowo dodaje właściwość hello `"level": "critical"` toomessages wysyłane przez urządzenie hello, która symuluje komunikat, który wymaga natychmiastowego działania przez hello zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="492d2-125">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello solution back-end.</span></span> <span data-ttu-id="492d2-126">aplikacji urządzenia Hello przekazuje informacje w oknie dialogowym właściwości wiadomość hello zamiast, w treści wiadomości powitania, dzięki tym Centrum IoT można kierować docelowy prawidłowego komunikatu toohello wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="492d2-126">hello device app passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>

> [!NOTE]
> <span data-ttu-id="492d2-127">Można użyć komunikatów właściwości tooroute komunikatów dla różnych scenariuszy, w tym przetwarzania dodatkowo toohello hot ścieżki przykładzie chłodni path.</span><span class="sxs-lookup"><span data-stu-id="492d2-127">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot-path example shown here.</span></span>

> [!NOTE]
> <span data-ttu-id="492d2-128">Dla zapewnienia hello prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="492d2-128">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="492d2-129">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania wykładniczego wycofywania, zgodnie z sugestią podaną w artykuł w witrynie MSDN hello np. [obsługi błędów przejściowych].</span><span class="sxs-lookup"><span data-stu-id="492d2-129">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a><span data-ttu-id="492d2-130">Kolejka tooa wiadomości trasy w Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="492d2-130">Route messages tooa queue in your IoT hub</span></span>

<span data-ttu-id="492d2-131">W tej sekcji omówiono następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="492d2-131">In this section, you:</span></span>

* <span data-ttu-id="492d2-132">Tworzenie kolejki usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="492d2-132">Create a Service Bus queue.</span></span>
* <span data-ttu-id="492d2-133">Podłącz je tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="492d2-133">Connect it tooyour IoT hub.</span></span>
* <span data-ttu-id="492d2-134">Skonfiguruj IoT Centrum toosend wiadomości toohello kolejki na podstawie obecności hello właściwości na wiadomość powitania.</span><span class="sxs-lookup"><span data-stu-id="492d2-134">Configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span>

<span data-ttu-id="492d2-135">Aby uzyskać więcej informacji o sposobie tooprocess komunikaty z kolejek usługi Service Bus, zobacz [Rozpoczynanie pracy z kolejkami][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="492d2-135">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][Service Bus queue].</span></span>

1. <span data-ttu-id="492d2-136">Tworzenie kolejki usługi Service Bus, zgodnie z opisem w [Rozpoczynanie pracy z kolejkami][Service Bus queue].</span><span class="sxs-lookup"><span data-stu-id="492d2-136">Create a Service Bus queue as described in [Get started with queues][Service Bus queue].</span></span> <span data-ttu-id="492d2-137">Kolejka Hello musi być w hello tej samej subskrypcji i regionu co Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="492d2-137">hello queue must be in hello same subscription and region as your IoT hub.</span></span> <span data-ttu-id="492d2-138">Zanotuj nazwę przestrzeni nazw i kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="492d2-138">Make a note of hello namespace and queue name.</span></span>

    > [!NOTE]
    > <span data-ttu-id="492d2-139">Tematy dotyczące używany jako punkty końcowe Centrum IoT nie może mieć i kolejek usługi Service Bus **sesji** lub **wykrywania duplikatów** włączone.</span><span class="sxs-lookup"><span data-stu-id="492d2-139">Service Bus queues and topics used as IoT Hub endpoints must not have **Sessions** or **Duplicate Detection** enabled.</span></span> <span data-ttu-id="492d2-140">Jeśli dowolna z tych opcji są włączone, hello punkt końcowy jest wyświetlany jako **informujący** w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="492d2-140">If either of those options are enabled, hello endpoint appears as **Unreachable** in hello Azure portal.</span></span>

2. <span data-ttu-id="492d2-141">Witaj w portalu Azure, Otwórz Centrum IoT i kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="492d2-141">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>
    
    ![Punkty końcowe Centrum IoT][30]

3. <span data-ttu-id="492d2-143">W hello **punkty końcowe** bloku, kliknij przycisk **Dodaj** na hello top tooadd Centrum IoT tooyour kolejki.</span><span class="sxs-lookup"><span data-stu-id="492d2-143">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="492d2-144">Punkt końcowy hello nazwa **CriticalQueue** i użyj hello listach rozwijanych tooselect **kolejki usługi Service Bus**hello przestrzeń nazw magistrali usług, w której znajduje się kolejki i hello nazwę kolejki.</span><span class="sxs-lookup"><span data-stu-id="492d2-144">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="492d2-145">Gdy wszystko będzie gotowe, kliknij przycisk **zapisać** u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="492d2-145">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Dodawanie punktu końcowego][31]
    
4. <span data-ttu-id="492d2-147">Teraz kliknij **tras** w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="492d2-147">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="492d2-148">Kliknij przycisk **Dodaj** u góry hello toocreate bloku hello reguły routingu kieruje komunikaty toohello kolejki można tylko dodać.</span><span class="sxs-lookup"><span data-stu-id="492d2-148">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="492d2-149">Wybierz **DeviceTelemetry** hello źródłem danych.</span><span class="sxs-lookup"><span data-stu-id="492d2-149">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="492d2-150">Wprowadź `level="critical"` hello warunkiem i wybierz polecenie kolejki hello właśnie został dodany jako punkt końcowy niestandardowych jako hello punkt końcowy reguły routingu.</span><span class="sxs-lookup"><span data-stu-id="492d2-150">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="492d2-151">Gdy wszystko będzie gotowe, kliknij przycisk **zapisać** u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="492d2-151">When you are done, click **Save** at hello bottom.</span></span>
    
    ![Dodawanie trasy][32]
    
    <span data-ttu-id="492d2-153">Upewnij się, że trasy rezerwowy hello ustawiono zbyt**ON**.</span><span class="sxs-lookup"><span data-stu-id="492d2-153">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="492d2-154">Ta wartość jest hello domyślną konfigurację Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="492d2-154">This value is hello default configuration for an IoT hub.</span></span>
    
    ![Trasy rezerwowej][33]

## <a name="read-from-hello-queue-endpoint"></a><span data-ttu-id="492d2-156">Odczyt z hello punkt końcowy z kolejki</span><span class="sxs-lookup"><span data-stu-id="492d2-156">Read from hello queue endpoint</span></span>

<span data-ttu-id="492d2-157">W tej sekcji można odczytywać wiadomości powitania hello punkt końcowy z kolejki.</span><span class="sxs-lookup"><span data-stu-id="492d2-157">In this section, you read hello messages from hello queue endpoint.</span></span>

1. <span data-ttu-id="492d2-158">W programie Visual Studio, Visual C# pulpitu systemu Windows klasycznego toohello bieżącego rozwiązania projektu, należy dodać przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="492d2-158">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="492d2-159">Nazwa projektu hello **ReadCriticalQueue**.</span><span class="sxs-lookup"><span data-stu-id="492d2-159">Name hello project **ReadCriticalQueue**.</span></span>

2. <span data-ttu-id="492d2-160">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ReadCriticalQueue** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="492d2-160">In Solution Explorer, right-click hello **ReadCriticalQueue** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="492d2-161">Ta operacja wyświetla hello **Menedżera pakietów NuGet** okna.</span><span class="sxs-lookup"><span data-stu-id="492d2-161">This operation displays hello **NuGet Package Manager** window.</span></span>

3. <span data-ttu-id="492d2-162">Wyszukaj **WindowsAzure.ServiceBus**, kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="492d2-162">Search for **WindowsAzure.ServiceBus**, click **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="492d2-163">Ta operacja pliki do pobrania, instaluje i dodaje toohello odwołanie do usługi Azure Service Bus ze wszystkimi zależnościami.</span><span class="sxs-lookup"><span data-stu-id="492d2-163">This operation downloads, installs, and adds a reference toohello Azure Service Bus, with all its dependencies.</span></span>

4. <span data-ttu-id="492d2-164">Dodaj następujące hello **przy użyciu** instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="492d2-164">Add hello following **using** statements at hello top of hello **Program.cs** file:</span></span>
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. <span data-ttu-id="492d2-165">Na koniec należy dodać następujące wiersze toohello hello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="492d2-165">Finally, add hello following lines toohello **Main** method.</span></span> <span data-ttu-id="492d2-166">Zastąp hello ciągu połączenia za pomocą **nasłuchiwania** uprawnień dla kolejki hello:</span><span class="sxs-lookup"><span data-stu-id="492d2-166">Substitute hello connection string with **Listen** permissions for hello queue:</span></span>
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="492d2-167">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="492d2-167">Run hello applications</span></span>
<span data-ttu-id="492d2-168">Teraz wszystko jest gotowe toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="492d2-168">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="492d2-169">W programie Visual Studio w Eksploratorze rozwiązań kliknij rozwiązanie prawym przyciskiem myszy i wybierz **Ustaw projekty startowe**.</span><span class="sxs-lookup"><span data-stu-id="492d2-169">In Visual Studio, in Solution Explorer, right-click your solution and select **Set StartUp Projects**.</span></span> <span data-ttu-id="492d2-170">Wybierz **wiele projektów startowych**, a następnie wybierz pozycję **Start** jako akcję hello hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, i **ReadCriticalQueue** projektów.</span><span class="sxs-lookup"><span data-stu-id="492d2-170">Select **Multiple startup projects**, then select **Start** as hello action for hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, and **ReadCriticalQueue** projects.</span></span>
2. <span data-ttu-id="492d2-171">Naciśnij klawisz **F5** toostart hello trzech aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="492d2-171">Press **F5** toostart hello three console apps.</span></span> <span data-ttu-id="492d2-172">Witaj **ReadDeviceToCloudMessages** aplikacja ma tylko niekrytyczne komunikatów wysyłanych z hello **SimulatedDevice** aplikacji i hello **ReadCriticalQueue** aplikacja ma tylko krytycznych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="492d2-172">hello **ReadDeviceToCloudMessages** app has only non-critical messages sent from hello **SimulatedDevice** application, and hello **ReadCriticalQueue** app has only critical messages.</span></span>
   
   ![Trzy aplikacje konsoli][50]

## <a name="next-steps"></a><span data-ttu-id="492d2-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="492d2-174">Next steps</span></span>
<span data-ttu-id="492d2-175">W tym samouczku przedstawiono sposób tooreliably wysyłania wiadomości urządzenia do chmury przy użyciu funkcji routingu wiadomość hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="492d2-175">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="492d2-176">Witaj [jak komunikaty toosend chmury do urządzenia z Centrum IoT] [ lnk-c2d] pokazuje, jak toosend wiadomości tooyour przez urządzenia z zaplecza rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="492d2-176">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="492d2-177">Przykłady toosee kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="492d2-177">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="492d2-178">toolearn więcej informacji na temat tworzenia rozwiązań z Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera].</span><span class="sxs-lookup"><span data-stu-id="492d2-178">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="492d2-179">Zobacz toolearn więcej informacji na temat routing komunikatów w Centrum IoT [wysyłania i odbierania wiadomości z Centrum IoT][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="492d2-179">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[usługi Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/
[Centrum IoT — przewodnik dewelopera]: iot-hub-devguide.md
[Rozpoczynanie pracy z Centrum IoT]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot
[obsługi błędów przejściowych]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
