---
title: "Rozpoczynanie pracy z usługą Azure IoT Hub (.NET) | Microsoft Docs"
description: "Dowiedz się, jak wysyłać komunikaty urządzenie-chmura do usługi Azure IoT Hub za pomocą zestawów SDK usługi IoT dla platformy .NET. Utwórz symulowane aplikacje urządzenia i usługi, aby zarejestrować urządzenie, wysyłać wiadomości i odczytywać wiadomości z usługi IoT Hub."
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
ms.openlocfilehash: 69296eb9ac2a74a97b632d27733a6a06500b4abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-net"></a><span data-ttu-id="c3993-104">Podłączanie urządzenia do usługi IoT Hub za pomocą środowiska .NET</span><span class="sxs-lookup"><span data-stu-id="c3993-104">Connect your device to your IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="c3993-105">Na końcu tego samouczka będziesz mieć trzy aplikacje konsolowe .NET:</span><span class="sxs-lookup"><span data-stu-id="c3993-105">At the end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="c3993-106">**CreateDeviceIdentity** tworzy tożsamość urządzenia i skojarzony klucz zabezpieczeń w celu podłączenia aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c3993-106">**CreateDeviceIdentity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="c3993-107">**ReadDeviceToCloudMessages** powoduje wyświetlenie telemetrii wysyłanej przez aplikację urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c3993-107">**ReadDeviceToCloudMessages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="c3993-108">Projekt **SimulatedDevice** łączy się z usługą IoT Hub przy użyciu utworzonej wcześniej tożsamości urządzenia i wysyła komunikat telemetrii co sekundę przy użyciu protokołu MQTT.</span><span class="sxs-lookup"><span data-stu-id="c3993-108">**SimulatedDevice**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second by using the MQTT protocol.</span></span>

<span data-ttu-id="c3993-109">Rozwiązanie Visual Studio z tymi trzema aplikacjami można pobrać lub sklonować z usługi Github.</span><span class="sxs-lookup"><span data-stu-id="c3993-109">You can download or clone the Visual Studio solution, which contains the three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="c3993-110">Artykuł [Azure IoT SDKs][lnk-hub-sdks] (Zestawy SDK usługi Azure IoT) zawiera informacje dotyczące zestawów SDK usługi Azure IoT, przy użyciu których można tworzyć aplikacje zarówno do uruchamiania na urządzaniach, jak i w zapleczu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c3993-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="c3993-111">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c3993-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="c3993-112">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c3993-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="c3993-113">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c3993-113">An active Azure account.</span></span> <span data-ttu-id="c3993-114">(Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).</span><span class="sxs-lookup"><span data-stu-id="c3993-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="c3993-115">Centrum IoT zostało już utworzone i masz nazwę hosta oraz parametry połączenia usługi IoT Hub potrzebne do ukończenia pozostałej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="c3993-115">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="c3993-116">Odbieranie komunikatów z urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="c3993-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="c3993-117">W tej sekcji opisano tworzenie aplikacji konsolowej .NET, która odczytuje komunikaty z urządzenia do chmury z usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3993-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="c3993-118">Usługa IoT Hub udostępnia punkt końcowy zgodny z usługą [Azure Event Hubs][lnk-event-hubs-overview], aby umożliwić odczytywanie komunikatów z urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="c3993-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="c3993-119">W celu uproszczenia informacji instrukcje w samouczku dotyczą tworzenia czytnika podstawowego, który nie jest odpowiedni do wdrożenia z użyciem dużej przepustowości.</span><span class="sxs-lookup"><span data-stu-id="c3993-119">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="c3993-120">W samouczku [Process device-to-cloud messages][lnk-process-d2c-tutorial] (Przetwarzanie komunikatów przesyłanych z urządzeń do chmury) przedstawiono sposób przetwarzania komunikatów z urządzenia do chmury na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="c3993-120">To learn how to process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="c3993-121">Więcej informacji na temat przetwarzania komunikatów z usługi Event Hubs znajduje się w samouczku [Rozpoczynanie pracy z usługą Event Hubs][lnk-eventhubs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="c3993-121">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="c3993-122">(Ten samouczek dotyczy punktów końcowych usługi IoT Hub zgodnych z centrum zdarzeń).</span><span class="sxs-lookup"><span data-stu-id="c3993-122">(This tutorial is applicable to the IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="c3993-123">Punkt końcowy zgodny z centrum zdarzeń przeznaczony do odczytywania komunikatów z urządzenia do chmury zawsze korzysta z protokołu AMQP.</span><span class="sxs-lookup"><span data-stu-id="c3993-123">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="c3993-124">W programie Visual Studio dodaj projekt Visual C# Windows Classic Desktop do bieżącego rozwiązania, używając szablonu projektu **Aplikacja konsoli (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="c3993-124">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="c3993-125">Upewnij się, że program .NET Framework jest w wersji 4.5.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c3993-125">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="c3993-126">Nazwij projekt **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="c3993-126">Name the project **ReadDeviceToCloudMessages**.</span></span>

    ![Nowy projekt Visual C# Windows Classic Desktop][10a]

2. <span data-ttu-id="c3993-128">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **ReadDeviceToCloudMessages**, a następnie kliknij pozycję **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c3993-128">In Solution Explorer, right-click the **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="c3993-129">W oknie **Menedżer pakietów NuGet** wyszukaj **WindowsAzure.ServiceBus**, wybierz opcję **Zainstaluj** i zaakceptuj warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="c3993-129">In the **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept the terms of use.</span></span> <span data-ttu-id="c3993-130">Ta procedura spowoduje pobranie, zainstalowanie i dodanie odniesienia do usługi [Azure Service Bus][lnk-servicebus-nuget] ze wszystkimi jej zależnościami.</span><span class="sxs-lookup"><span data-stu-id="c3993-130">This procedure downloads, installs, and adds a reference to [Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="c3993-131">Ten pakiet umożliwia aplikacji połączenie się z punktem końcowym zgodnym z centrum zdarzeń w centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c3993-131">This package enables the application to connect to the Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="c3993-132">Dodaj następujące instrukcje `using` w górnej części pliku **Program.cs**:</span><span class="sxs-lookup"><span data-stu-id="c3993-132">Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="c3993-133">Dodaj następujące pola do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="c3993-133">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="c3993-134">Zastąp wartość symbolu zastępczego parametrami połączenia usługi IoT Hub dla centrum utworzonego w sekcji „Tworzenie centrum IoT”.</span><span class="sxs-lookup"><span data-stu-id="c3993-134">Replace the placeholder value with the IoT Hub connection string for the hub you created in the "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="c3993-135">Dodaj następującą metodę do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="c3993-135">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="c3993-136">W metodzie tej używane jest wystąpienie **EventHubReceiver** do odbierania komunikatów ze wszystkich partycji odbioru z urządzenia do chmury centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c3993-136">This method uses an **EventHubReceiver** instance to receive messages from all the IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="c3993-137">Zwróć uwagę na sposób przekazywania parametru `DateTime.Now` podczas tworzenia obiektu **EventHubReceiver** w taki sposób, aby odbierał komunikaty wysłane tylko po jego uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="c3993-137">Notice how you pass a `DateTime.Now` parameter when you create the **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="c3993-138">Ten filtr jest przydatny w środowisku testowym, gdyż umożliwia wyświetlenie bieżącego zestawu komunikatów.</span><span class="sxs-lookup"><span data-stu-id="c3993-138">This filter is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="c3993-139">W środowisku produkcyjnym kod powinien sprawdzać, czy przetwarzane są wszystkie komunikaty.</span><span class="sxs-lookup"><span data-stu-id="c3993-139">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="c3993-140">Więcej informacji znajduje się w samouczku [How to process IoT Hub device-to-cloud messages (Jak przetwarzać komunikaty z urządzenia do chmury w usłudze IoT Hub)][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="c3993-140">For more information, see the tutorial [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="c3993-141">Na koniec dodaj następujące wiersze do metody **Główne**:</span><span class="sxs-lookup"><span data-stu-id="c3993-141">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C to exit.\n");
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

## <a name="create-a-device-app"></a><span data-ttu-id="c3993-142">Tworzenie aplikacji urządzenia</span><span class="sxs-lookup"><span data-stu-id="c3993-142">Create a device app</span></span>

<span data-ttu-id="c3993-143">Ta sekcja zawiera instrukcje dotyczące tworzenia aplikacji konsolowej .NET, która symuluje urządzenie wysyłające komunikaty z urządzenia do chmury do usługi IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3993-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="c3993-144">W programie Visual Studio dodaj projekt Visual C# Windows Classic Desktop do bieżącego rozwiązania, używając szablonu projektu **Aplikacja konsoli (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="c3993-144">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="c3993-145">Upewnij się, że program .NET Framework jest w wersji 4.5.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c3993-145">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="c3993-146">Nazwij projekt **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="c3993-146">Name the project **SimulatedDevice**.</span></span>

    ![Nowy projekt Visual C# Windows Classic Desktop][10b]

2. <span data-ttu-id="c3993-148">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **SimulatedDevice**, a następnie kliknij pozycję **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c3993-148">In Solution Explorer, right-click the **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="c3993-149">W oknie **Menedżera pakietów NuGet** wybierz opcję **Przeglądaj**, wyszukaj pozycję **Microsoft.Azure.Devices.Client**, wybierz opcję **Zainstaluj**, aby zainstalować pakiet **Microsoft.Azure.Devices.Client**, i zaakceptuj warunki użytkowania.</span><span class="sxs-lookup"><span data-stu-id="c3993-149">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="c3993-150">Ta procedura spowoduje pobranie, zainstalowanie i dodanie odwołania do [pakietu NuGet zestawu SDK urządzenia w usłudze Azure IoT][lnk-device-nuget] oraz jego zależności.</span><span class="sxs-lookup"><span data-stu-id="c3993-150">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="c3993-151">Dodaj następującą instrukcję `using` w górnej części pliku **Program.cs**:</span><span class="sxs-lookup"><span data-stu-id="c3993-151">Add the following `using` statement at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="c3993-152">Dodaj następujące pola do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="c3993-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="c3993-153">Zastąp element `{iot hub hostname}` nazwą hosta centrum IoT pozyskaną w sekcji „Tworzenie centrum IoT”.</span><span class="sxs-lookup"><span data-stu-id="c3993-153">Substitute `{iot hub hostname}` with the IoT hub host name you retrieved in the "Create an IoT hub" section.</span></span> <span data-ttu-id="c3993-154">Zastąp element `{device key}` kluczem urządzenia pozyskanym w sekcji „Tworzenie tożsamości urządzenia”.</span><span class="sxs-lookup"><span data-stu-id="c3993-154">Substitute `{device key}` with the device key you retrieved in the "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="c3993-155">Dodaj następującą metodę do klasy **Program**:</span><span class="sxs-lookup"><span data-stu-id="c3993-155">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="c3993-156">Ta metoda wysyła nowy komunikat z urządzenia do chmury co sekundę.</span><span class="sxs-lookup"><span data-stu-id="c3993-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="c3993-157">Komunikat zawiera obiekt serializacji JSON z identyfikatorem urządzenia i generowanymi losowo numerami do symulacji czujników temperatury i wilgotności.</span><span class="sxs-lookup"><span data-stu-id="c3993-157">The message contains a JSON-serialized object, with the device ID and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="c3993-158">Na koniec dodaj następujące wiersze do metody **Główne**:</span><span class="sxs-lookup"><span data-stu-id="c3993-158">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="c3993-159">Domyślnie metoda **Utwórz** w aplikacji .NET Framework tworzy wystąpienie **DeviceClient**, które używa protokołu AMQP do komunikowania się z usługą IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3993-159">By default, the **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses the AMQP protocol to communicate with IoT Hub.</span></span> <span data-ttu-id="c3993-160">Aby skorzystać z protokołu MQTT lub HTTP, użyj zastępowania metody **Create**, która pozwala na określenie protokołu.</span><span class="sxs-lookup"><span data-stu-id="c3993-160">To use the MQTT or HTTP protocol, use the override of the **Create** method that enables you to specify the protocol.</span></span> <span data-ttu-id="c3993-161">Platforma uniwersalna systemu Windows oraz klienci PCL domyślnie używają protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="c3993-161">UWP and PCL clients use the HTTP protocol by default.</span></span> <span data-ttu-id="c3993-162">Jeśli używasz protokołu HTTP, dodaj również do projektu pakiet NuGet **Microsoft.AspNet.WebApi.Client**, aby dołączyć przestrzeń nazw **System.Net.Http.Formatting**.</span><span class="sxs-lookup"><span data-stu-id="c3993-162">If you use the HTTP protocol, you should also add the **Microsoft.AspNet.WebApi.Client** NuGet package to your project to include the **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="c3993-163">Ten samouczek zawiera instrukcje tworzenia aplikacji urządzenia w usłudze IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3993-163">This tutorial takes you through the steps to create an IoT Hub device app.</span></span> <span data-ttu-id="c3993-164">Możesz również użyć rozszerzenia programu Visual Studio [Connected Service for Azure IoT Hub][lnk-connected-service], aby dodać niezbędny kod do aplikacji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c3993-164">You can also use the [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension to add the necessary code to your device app.</span></span>

> [!NOTE]
> <span data-ttu-id="c3993-165">Dla uproszczenia ten samouczek nie zawiera opisu wdrożenia żadnych zasad ponawiania.</span><span class="sxs-lookup"><span data-stu-id="c3993-165">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="c3993-166">W kodzie produkcyjnym należy wdrożyć zasady ponawiania (np. wycofywanie wykładnicze) zgodnie z sugestią w artykule z witryny MSDN [Transient Fault Handling][lnk-transient-faults] (Obsługa przejściowych błędów).</span><span class="sxs-lookup"><span data-stu-id="c3993-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="c3993-167">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="c3993-167">Run the apps</span></span>

<span data-ttu-id="c3993-168">Teraz można przystąpić do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c3993-168">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="c3993-169">W programie Visual Studio w Eksploratorze rozwiązań kliknij rozwiązanie prawym przyciskiem myszy, a następnie kliknij przycisk **Ustaw projekty startowe**.</span><span class="sxs-lookup"><span data-stu-id="c3993-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="c3993-170">Wybierz opcję **Wiele projektów startowych**, a następnie wybierz opcję **Uruchom** jako akcję dla projektów **ReadDeviceToCloudMessages** i **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="c3993-170">Select **Multiple startup projects**, and then select **Start** as the action for both the **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Właściwości projektu startowego][41]

2. <span data-ttu-id="c3993-172">Naciśnij klawisz **F5**, aby uruchomić obie aplikacje.</span><span class="sxs-lookup"><span data-stu-id="c3993-172">Press **F5** to start both apps running.</span></span> <span data-ttu-id="c3993-173">Dane wyjściowe konsoli z aplikacji **SimulatedDevice** zawierają komunikaty, które aplikacja urządzenia wysyła do centrum IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3993-173">The console output from the **SimulatedDevice** app shows the messages your device app sends to your IoT hub.</span></span> <span data-ttu-id="c3993-174">Dane wyjściowe konsoli z aplikacji **ReadDeviceToCloudMessages** zawierają komunikaty odbierane przez centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c3993-174">The console output from the **ReadDeviceToCloudMessages** app shows the messages that your IoT hub receives.</span></span>

    ![Dane wyjściowe konsoli z aplikacji][42]

3. <span data-ttu-id="c3993-176">Na kafelku **Użycie** w [witrynie Azure Portal][lnk-portal] wyświetlana jest liczba komunikatów wysłanych do centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="c3993-176">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![Kafelek Użycie portalu Azure][43]

## <a name="next-steps"></a><span data-ttu-id="c3993-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3993-178">Next steps</span></span>

<span data-ttu-id="c3993-179">W tym samouczku opisano konfigurowanie centrum IoT Hub w witrynie Azure Portal, a następnie tworzenie tożsamości urządzenia w rejestrze tożsamości centrum IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3993-179">In this tutorial, you configured an IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="c3993-180">Tożsamość urządzenia została użyta, aby włączyć w aplikacji urządzenia funkcję wysyłania komunikatów z urządzenia do chmury do centrum IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3993-180">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="c3993-181">Utworzono również aplikację, która wyświetla komunikaty odbierane przez centrum IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c3993-181">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="c3993-182">Aby kontynuować wprowadzenie do usługi IoT Hub i zapoznać się z innymi scenariuszami IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="c3993-182">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="c3993-183">[Łączenie urządzenia][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="c3993-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="c3993-184">[Wprowadzenie do zarządzania urządzeniami][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="c3993-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="c3993-185">[Getting started with IoT Edge][lnk-iot-edge] (Wprowadzenie do usługi IoT Edge)</span><span class="sxs-lookup"><span data-stu-id="c3993-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="c3993-186">Aby dowiedzieć się, jak rozszerzyć rozwiązanie IoT i przetwarzać komunikaty z urządzenia do chmury na dużą skalę, zobacz samouczek [Przetwarzanie komunikatów przesyłanych z urządzeń do chmury][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="c3993-186">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

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
