---
title: aaaGet pracy z Centrum IoT Azure (.NET) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak urządzenia chmury toosend wiadomości tooAzure Centrum IoT przy użyciu IoT zestawy SDK dla platformy .NET. Utworzyć symulowane urządzenie i tooregister aplikacji usługi, urządzenia, wysyłania wiadomości i odczytywać wiadomości z Centrum IoT."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a><span data-ttu-id="d56d9-104">Połącz z Centrum IoT tooyour urządzenia przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="d56d9-104">Connect your device tooyour IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="d56d9-105">Na końcu hello tego samouczka dostępne są trzy aplikacji konsoli .NET:</span><span class="sxs-lookup"><span data-stu-id="d56d9-105">At hello end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="d56d9-106">**CreateDeviceIdentity**, co powoduje tożsamości urządzenia i skojarzony klucz tooconnect aplikacją urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d56d9-106">**CreateDeviceIdentity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="d56d9-107">**ReadDeviceToCloudMessages**, który zawiera dane telemetryczne hello wysyłane przez aplikację na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="d56d9-107">**ReadDeviceToCloudMessages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="d56d9-108">**SimulatedDevice**, która łączy się tooyour Centrum IoT z tożsamości urządzenia hello utworzony wcześniej i wysyła komunikat telemetrii w ciągu sekundy przy użyciu protokołu MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="d56d9-108">**SimulatedDevice**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second by using hello MQTT protocol.</span></span>

<span data-ttu-id="d56d9-109">Można pobrać lub sklonować hello rozwiązania Visual Studio, które zawiera trzy aplikacji hello z usługi Github.</span><span class="sxs-lookup"><span data-stu-id="d56d9-109">You can download or clone hello Visual Studio solution, which contains hello three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="d56d9-110">Informacji o hello Azure IoT SDK, w których można używać toobuild toorun aplikacji na urządzeniach i z zaplecza rozwiązania, zobacz [Azure IoT SDK][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="d56d9-110">For information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="d56d9-111">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="d56d9-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="d56d9-112">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d56d9-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="d56d9-113">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d56d9-113">An active Azure account.</span></span> <span data-ttu-id="d56d9-114">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="d56d9-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="d56d9-115">Teraz utworzeniu Centrum IoT i masz hello nazwy hosta i parametry połączenia Centrum IoT należy toocomplete hello pozostałej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="d56d9-115">You have now created your IoT hub, and you have hello host name and IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="d56d9-116">Odbieranie komunikatów z urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="d56d9-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="d56d9-117">W tej sekcji opisano tworzenie aplikacji konsolowej .NET, która odczytuje komunikaty z urządzenia do chmury z usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d56d9-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="d56d9-118">Przedstawia Centrum IoT [Azure Event Hubs][lnk-event-hubs-overview]-tooenable zgodne punktu końcowego można tooread wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="d56d9-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="d56d9-119">elementy tookeep proste, w tym samouczku tworzy podstawowe reader, który nie jest odpowiedni dla wdrożenia wysokiej przepływności.</span><span class="sxs-lookup"><span data-stu-id="d56d9-119">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="d56d9-120">toolearn jak tooprocess urządzenia do chmury komunikatów na dużą skalę, zobacz hello [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="d56d9-120">toolearn how tooprocess device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="d56d9-121">Aby uzyskać więcej informacji dotyczących sposobu tooprocess komunikaty z usługi Event Hubs, zobacz hello [Rozpoczynanie pracy z usługą Event Hubs] [ lnk-eventhubs-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="d56d9-121">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="d56d9-122">(W tym samouczku jest punkty końcowe dotyczy toohello zgodnego Centrum zdarzeń Centrum IoT).</span><span class="sxs-lookup"><span data-stu-id="d56d9-122">(This tutorial is applicable toohello IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="d56d9-123">Hello punktu końcowego Centrum zdarzeń zgodnych do odczytywania wiadomości urządzenia do chmury zawsze używa protokołu AMQP hello.</span><span class="sxs-lookup"><span data-stu-id="d56d9-123">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="d56d9-124">W programie Visual Studio, Visual C# pulpitu systemu Windows klasycznego toohello bieżącego rozwiązania projektu, należy dodać przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="d56d9-124">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="d56d9-125">Upewnij się, że wersja platformy .NET hello jest 4.5.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d56d9-125">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="d56d9-126">Nazwa projektu hello **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="d56d9-126">Name hello project **ReadDeviceToCloudMessages**.</span></span>

    ![Nowy projekt Visual C# Windows Classic Desktop][10a]

2. <span data-ttu-id="d56d9-128">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ReadDeviceToCloudMessages** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d56d9-128">In Solution Explorer, right-click hello **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="d56d9-129">W hello **Menedżera pakietów NuGet** okna, wyszukiwanie **WindowsAzure.ServiceBus**, wybierz pozycję **zainstalować**i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="d56d9-129">In hello **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="d56d9-130">Ta procedura pliki do pobrania, instaluje i dodaje odwołanie za[Azure Service Bus][lnk-servicebus-nuget], ze wszystkimi zależnościami.</span><span class="sxs-lookup"><span data-stu-id="d56d9-130">This procedure downloads, installs, and adds a reference too[Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="d56d9-131">Ten pakiet umożliwia hello tooconnect toohello zgodnego Centrum zdarzeń punkt końcowy aplikacji w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d56d9-131">This package enables hello application tooconnect toohello Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="d56d9-132">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="d56d9-132">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="d56d9-133">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="d56d9-133">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d56d9-134">Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w sekcji "Utwórz Centrum IoT" hello parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d56d9-134">Replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="d56d9-135">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="d56d9-135">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    <span data-ttu-id="d56d9-136">Ta metoda używa **EventHubReceiver** partycje odbierać komunikaty tooreceive wystąpienia z wszystkich hello IoT hub urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="d56d9-136">This method uses an **EventHubReceiver** instance tooreceive messages from all hello IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="d56d9-137">Zwróć uwagę, jak przekazać `DateTime.Now` parametru podczas tworzenia hello **EventHubReceiver** obiektu, tak aby tylko odbiera komunikaty wysyłane po jego uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="d56d9-137">Notice how you pass a `DateTime.Now` parameter when you create hello **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="d56d9-138">Ten filtr jest przydatne w środowisku testowym, dzięki czemu hello bieżący zestaw komunikatów.</span><span class="sxs-lookup"><span data-stu-id="d56d9-138">This filter is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="d56d9-139">W środowisku produkcyjnym kodu upewnij się, przetwarza wszystkie wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="d56d9-139">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="d56d9-140">Aby uzyskać więcej informacji, zobacz samouczek hello [jak tooprocess Centrum IoT urządzenia do chmury wiadomości][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="d56d9-140">For more information, see hello tutorial [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="d56d9-141">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="d56d9-141">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="d56d9-142">Tworzenie aplikacji urządzenia</span><span class="sxs-lookup"><span data-stu-id="d56d9-142">Create a device app</span></span>

<span data-ttu-id="d56d9-143">W tej sekcji służy do tworzenia aplikacji konsoli .NET, która symuluje urządzenia, które wysyła Centrum IoT tooan wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="d56d9-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="d56d9-144">W programie Visual Studio, Visual C# pulpitu systemu Windows klasycznego toohello bieżącego rozwiązania projektu, należy dodać przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="d56d9-144">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="d56d9-145">Upewnij się, że wersja platformy .NET hello jest 4.5.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d56d9-145">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="d56d9-146">Nazwa projektu hello **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="d56d9-146">Name hello project **SimulatedDevice**.</span></span>

    ![Nowy projekt Visual C# Windows Classic Desktop][10b]

2. <span data-ttu-id="d56d9-148">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **SimulatedDevice** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d56d9-148">In Solution Explorer, right-click hello **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="d56d9-149">W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **Microsoft.Azure.Devices.Client**, wybierz pozycję **zainstalować** Witaj tooinstall **Microsoft.Azure.Devices.Client** pakietu i zaakceptuj warunki użytkowania hello.</span><span class="sxs-lookup"><span data-stu-id="d56d9-149">In hello **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="d56d9-150">Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [pakiet SDK NuGet urządzenia Azure IoT] [ lnk-device-nuget] i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="d56d9-150">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="d56d9-151">Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:</span><span class="sxs-lookup"><span data-stu-id="d56d9-151">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="d56d9-152">Dodaj następujące pola toohello hello **Program** klasy.</span><span class="sxs-lookup"><span data-stu-id="d56d9-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="d56d9-153">SUBSTITUTE `{iot hub hostname}` hello IoT hub nazwą hosta pobierane w sekcji "Tworzenie Centrum IoT" hello.</span><span class="sxs-lookup"><span data-stu-id="d56d9-153">Substitute `{iot hub hostname}` with hello IoT hub host name you retrieved in hello "Create an IoT hub" section.</span></span> <span data-ttu-id="d56d9-154">SUBSTITUTE `{device key}` kluczem hello urządzenia pobierane w sekcji "Tworzenie tożsamości urządzenia" hello.</span><span class="sxs-lookup"><span data-stu-id="d56d9-154">Substitute `{device key}` with hello device key you retrieved in hello "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="d56d9-155">Dodaj następujące metody toohello hello **Program** klasy:</span><span class="sxs-lookup"><span data-stu-id="d56d9-155">Add hello following method toohello **Program** class:</span></span>

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    <span data-ttu-id="d56d9-156">Ta metoda wysyła nowy komunikat z urządzenia do chmury co sekundę.</span><span class="sxs-lookup"><span data-stu-id="d56d9-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="d56d9-157">wiadomości powitania zawiera obiekt serializacji JSON z Identyfikatorem urządzenia hello i losowo wygenerowane numery toosimulate czujnik temperatury i wilgotności czujnika.</span><span class="sxs-lookup"><span data-stu-id="d56d9-157">hello message contains a JSON-serialized object, with hello device ID and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="d56d9-158">Na koniec należy dodać następujące wiersze toohello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="d56d9-158">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="d56d9-159">Domyślnie program hello **Utwórz** metoda w aplikacji .NET Framework tworzy **DeviceClient** wystąpienia, która używa toocommunicate protokołu AMQP hello z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d56d9-159">By default, hello **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses hello AMQP protocol toocommunicate with IoT Hub.</span></span> <span data-ttu-id="d56d9-160">toouse hello protokołu HTTP lub MQTT, użyj hello zastępowania hello **Utwórz** metodę, która umożliwia toospecify hello protokołu.</span><span class="sxs-lookup"><span data-stu-id="d56d9-160">toouse hello MQTT or HTTP protocol, use hello override of hello **Create** method that enables you toospecify hello protocol.</span></span> <span data-ttu-id="d56d9-161">Platformy uniwersalnej systemu Windows i PCL klienci używają protokołu HTTP hello domyślnie.</span><span class="sxs-lookup"><span data-stu-id="d56d9-161">UWP and PCL clients use hello HTTP protocol by default.</span></span> <span data-ttu-id="d56d9-162">Jeśli używasz protokołu hello HTTP należy również dodać hello **Microsoft.AspNet.WebApi.Client** NuGet pakietu tooyour projektu tooinclude hello **System.Net.Http.Formatting** przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="d56d9-162">If you use hello HTTP protocol, you should also add hello **Microsoft.AspNet.WebApi.Client** NuGet package tooyour project tooinclude hello **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="d56d9-163">Ten samouczek przedstawia hello kroki toocreate Centrum IoT aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d56d9-163">This tutorial takes you through hello steps toocreate an IoT Hub device app.</span></span> <span data-ttu-id="d56d9-164">Można również użyć hello [połączone usługi dla usługi Azure IoT Hub] [ lnk-connected-service] tooadd rozszerzenia programu Visual Studio hello aplikacji urządzenia tooyour wymagany kod.</span><span class="sxs-lookup"><span data-stu-id="d56d9-164">You can also use hello [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension tooadd hello necessary code tooyour device app.</span></span>

> [!NOTE]
> <span data-ttu-id="d56d9-165">rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania.</span><span class="sxs-lookup"><span data-stu-id="d56d9-165">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d56d9-166">W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="d56d9-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="d56d9-167">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="d56d9-167">Run hello apps</span></span>

<span data-ttu-id="d56d9-168">Wszystko jest teraz gotowy toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d56d9-168">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="d56d9-169">W programie Visual Studio w Eksploratorze rozwiązań kliknij rozwiązanie prawym przyciskiem myszy, a następnie kliknij przycisk **Ustaw projekty startowe**.</span><span class="sxs-lookup"><span data-stu-id="d56d9-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="d56d9-170">Wybierz **wiele projektów startowych**, a następnie wybierz **Start** hello akcji dla obu hello **ReadDeviceToCloudMessages** i **SimulatedDevice** projektów.</span><span class="sxs-lookup"><span data-stu-id="d56d9-170">Select **Multiple startup projects**, and then select **Start** as hello action for both hello **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Właściwości projektu startowego][41]

2. <span data-ttu-id="d56d9-172">Naciśnij klawisz **F5** toostart obie aplikacje uruchomione.</span><span class="sxs-lookup"><span data-stu-id="d56d9-172">Press **F5** toostart both apps running.</span></span> <span data-ttu-id="d56d9-173">Witaj dane wyjściowe konsoli hello **SimulatedDevice** wiadomości powitania pokazuje aplikacji aplikacją urządzenia wysyła tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d56d9-173">hello console output from hello **SimulatedDevice** app shows hello messages your device app sends tooyour IoT hub.</span></span> <span data-ttu-id="d56d9-174">Witaj dane wyjściowe konsoli hello **ReadDeviceToCloudMessages** aplikacji zawiera wiadomości powitania, które otrzymuje Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d56d9-174">hello console output from hello **ReadDeviceToCloudMessages** app shows hello messages that your IoT hub receives.</span></span>

    ![Dane wyjściowe konsoli z aplikacji][42]

3. <span data-ttu-id="d56d9-176">Witaj **użycia** kafelka w hello [portalu Azure] [ lnk-portal] pokazuje hello liczbę komunikatów wysłanych toohello Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="d56d9-176">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Kafelek Użycie portalu Azure][43]

## <a name="next-steps"></a><span data-ttu-id="d56d9-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d56d9-178">Next steps</span></span>

<span data-ttu-id="d56d9-179">W tym samouczku został skonfigurowany Centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d56d9-179">In this tutorial, you configured an IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="d56d9-180">Użyto tego urządzenia tożsamości tooenable hello urządzenia aplikacji toosend wiadomości urządzenia do chmury toohello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d56d9-180">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="d56d9-181">Utworzono aplikację, która wyświetla hello komunikatów odebranych przez Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="d56d9-181">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="d56d9-182">toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="d56d9-182">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="d56d9-183">[Łączenie urządzenia][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="d56d9-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="d56d9-184">[Wprowadzenie do zarządzania urządzeniami][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="d56d9-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="d56d9-185">[Getting started with IoT Edge][lnk-iot-edge] (Wprowadzenie do usługi IoT Edge)</span><span class="sxs-lookup"><span data-stu-id="d56d9-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="d56d9-186">toolearn tooextend IoT rozwiązanie i procesu urządzenia do chmury wiadomości na dużą skalę, zobacz temat hello [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczka.</span><span class="sxs-lookup"><span data-stu-id="d56d9-186">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
