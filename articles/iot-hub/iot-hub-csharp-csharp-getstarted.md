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
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a>Połącz z Centrum IoT tooyour urządzenia przy użyciu platformy .NET

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Na końcu hello tego samouczka dostępne są trzy aplikacji konsoli .NET:

* **CreateDeviceIdentity**, co powoduje tożsamości urządzenia i skojarzony klucz tooconnect aplikacją urządzenia.
* **ReadDeviceToCloudMessages**, który zawiera dane telemetryczne hello wysyłane przez aplikację na urządzeniu.
* **SimulatedDevice**, która łączy się tooyour Centrum IoT z tożsamości urządzenia hello utworzony wcześniej i wysyła komunikat telemetrii w ciągu sekundy przy użyciu protokołu MQTT hello.

Można pobrać lub sklonować hello rozwiązania Visual Studio, które zawiera trzy aplikacji hello z usługi Github.

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> Informacji o hello Azure IoT SDK, w których można używać toobuild toorun aplikacji na urządzeniach i z zaplecza rozwiązania, zobacz [Azure IoT SDK][lnk-hub-sdks].

toocomplete tego samouczka należy hello następujące:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Aktywne konto platformy Azure. (Jeśli go nie masz, możesz utworzyć [bezpłatne konto próbne][lnk-free-trial] w zaledwie kilka minut).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Teraz utworzeniu Centrum IoT i masz hello nazwy hosta i parametry połączenia Centrum IoT należy toocomplete hello pozostałej części tego samouczka.

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a>Odbieranie komunikatów z urządzenia do chmury
W tej sekcji opisano tworzenie aplikacji konsolowej .NET, która odczytuje komunikaty z urządzenia do chmury z usługi IoT Hub. Przedstawia Centrum IoT [Azure Event Hubs][lnk-event-hubs-overview]-tooenable zgodne punktu końcowego można tooread wiadomości urządzenia do chmury. elementy tookeep proste, w tym samouczku tworzy podstawowe reader, który nie jest odpowiedni dla wdrożenia wysokiej przepływności. toolearn jak tooprocess urządzenia do chmury komunikatów na dużą skalę, zobacz hello [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczka. Aby uzyskać więcej informacji dotyczących sposobu tooprocess komunikaty z usługi Event Hubs, zobacz hello [Rozpoczynanie pracy z usługą Event Hubs] [ lnk-eventhubs-tutorial] samouczka. (W tym samouczku jest punkty końcowe dotyczy toohello zgodnego Centrum zdarzeń Centrum IoT).

> [!NOTE]
> Hello punktu końcowego Centrum zdarzeń zgodnych do odczytywania wiadomości urządzenia do chmury zawsze używa protokołu AMQP hello.

1. W programie Visual Studio, Visual C# pulpitu systemu Windows klasycznego toohello bieżącego rozwiązania projektu, należy dodać przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu. Upewnij się, że wersja platformy .NET hello jest 4.5.1 lub nowszej. Nazwa projektu hello **ReadDeviceToCloudMessages**.

    ![Nowy projekt Visual C# Windows Classic Desktop][10a]

2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ReadDeviceToCloudMessages** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.

3. W hello **Menedżera pakietów NuGet** okna, wyszukiwanie **WindowsAzure.ServiceBus**, wybierz pozycję **zainstalować**i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje odwołanie za[Azure Service Bus][lnk-servicebus-nuget], ze wszystkimi zależnościami. Ten pakiet umożliwia hello tooconnect toohello zgodnego Centrum zdarzeń punkt końcowy aplikacji w Centrum IoT.

4. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. Dodaj następujące pola toohello hello **Program** klasy. Zastąp wartość symbolu zastępczego hello hello hello koncentratora, który został utworzony w sekcji "Utwórz Centrum IoT" hello parametry połączenia Centrum IoT.

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. Dodaj następujące metody toohello hello **Program** klasy:

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

    Ta metoda używa **EventHubReceiver** partycje odbierać komunikaty tooreceive wystąpienia z wszystkich hello IoT hub urządzenia do chmury. Zwróć uwagę, jak przekazać `DateTime.Now` parametru podczas tworzenia hello **EventHubReceiver** obiektu, tak aby tylko odbiera komunikaty wysyłane po jego uruchomieniu. Ten filtr jest przydatne w środowisku testowym, dzięki czemu hello bieżący zestaw komunikatów. W środowisku produkcyjnym kodu upewnij się, przetwarza wszystkie wiadomości powitania. Aby uzyskać więcej informacji, zobacz samouczek hello [jak tooprocess Centrum IoT urządzenia do chmury wiadomości][lnk-process-d2c-tutorial].

7. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:

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

## <a name="create-a-device-app"></a>Tworzenie aplikacji urządzenia

W tej sekcji służy do tworzenia aplikacji konsoli .NET, która symuluje urządzenia, które wysyła Centrum IoT tooan wiadomości urządzenia do chmury.

1. W programie Visual Studio, Visual C# pulpitu systemu Windows klasycznego toohello bieżącego rozwiązania projektu, należy dodać przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu. Upewnij się, że wersja platformy .NET hello jest 4.5.1 lub nowszej. Nazwa projektu hello **SimulatedDevice**.

    ![Nowy projekt Visual C# Windows Classic Desktop][10b]

2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **SimulatedDevice** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.

3. W hello **Menedżera pakietów NuGet** wybierz **Przeglądaj**, wyszukaj **Microsoft.Azure.Devices.Client**, wybierz pozycję **zainstalować** Witaj tooinstall **Microsoft.Azure.Devices.Client** pakietu i zaakceptuj warunki użytkowania hello. Ta procedura pliki do pobrania, instaluje i dodaje toohello odwołanie [pakiet SDK NuGet urządzenia Azure IoT] [ lnk-device-nuget] i jego zależności.

4. Dodaj następujące hello `using` instrukcji u góry hello hello **Program.cs** pliku:

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. Dodaj następujące pola toohello hello **Program** klasy. SUBSTITUTE `{iot hub hostname}` hello IoT hub nazwą hosta pobierane w sekcji "Tworzenie Centrum IoT" hello. SUBSTITUTE `{device key}` kluczem hello urządzenia pobierane w sekcji "Tworzenie tożsamości urządzenia" hello.

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. Dodaj następujące metody toohello hello **Program** klasy:

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

    Ta metoda wysyła nowy komunikat z urządzenia do chmury co sekundę. wiadomości powitania zawiera obiekt serializacji JSON z Identyfikatorem urządzenia hello i losowo wygenerowane numery toosimulate czujnik temperatury i wilgotności czujnika.

7. Na koniec należy dodać następujące wiersze toohello hello **Main** metody:

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    Domyślnie program hello **Utwórz** metoda w aplikacji .NET Framework tworzy **DeviceClient** wystąpienia, która używa toocommunicate protokołu AMQP hello z Centrum IoT. toouse hello protokołu HTTP lub MQTT, użyj hello zastępowania hello **Utwórz** metodę, która umożliwia toospecify hello protokołu. Platformy uniwersalnej systemu Windows i PCL klienci używają protokołu HTTP hello domyślnie. Jeśli używasz protokołu hello HTTP należy również dodać hello **Microsoft.AspNet.WebApi.Client** NuGet pakietu tooyour projektu tooinclude hello **System.Net.Http.Formatting** przestrzeni nazw.

Ten samouczek przedstawia hello kroki toocreate Centrum IoT aplikacji urządzenia. Można również użyć hello [połączone usługi dla usługi Azure IoT Hub] [ lnk-connected-service] tooadd rozszerzenia programu Visual Studio hello aplikacji urządzenia tooyour wymagany kod.

> [!NOTE]
> rzeczy tookeep proste, w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania (na przykład wykładniczego wycofywania), zgodnie z sugestią podaną w artykuł w witrynie MSDN hello [obsługi błędów przejściowych][lnk-transient-faults].

## <a name="run-hello-apps"></a>Uruchamianie aplikacji hello

Wszystko jest teraz gotowy toorun hello aplikacji.

1. W programie Visual Studio w Eksploratorze rozwiązań kliknij rozwiązanie prawym przyciskiem myszy, a następnie kliknij przycisk **Ustaw projekty startowe**. Wybierz **wiele projektów startowych**, a następnie wybierz **Start** hello akcji dla obu hello **ReadDeviceToCloudMessages** i **SimulatedDevice** projektów.

    ![Właściwości projektu startowego][41]

2. Naciśnij klawisz **F5** toostart obie aplikacje uruchomione. Witaj dane wyjściowe konsoli hello **SimulatedDevice** wiadomości powitania pokazuje aplikacji aplikacją urządzenia wysyła tooyour Centrum IoT. Witaj dane wyjściowe konsoli hello **ReadDeviceToCloudMessages** aplikacji zawiera wiadomości powitania, które otrzymuje Centrum IoT.

    ![Dane wyjściowe konsoli z aplikacji][42]

3. Witaj **użycia** kafelka w hello [portalu Azure] [ lnk-portal] pokazuje hello liczbę komunikatów wysłanych toohello Centrum IoT:

    ![Kafelek Użycie portalu Azure][43]

## <a name="next-steps"></a>Następne kroki

W tym samouczku został skonfigurowany Centrum IoT w portalu Azure hello i w rejestrze tożsamości Centrum IoT hello zostanie utworzona tożsamość urządzenia. Użyto tego urządzenia tożsamości tooenable hello urządzenia aplikacji toosend wiadomości urządzenia do chmury toohello Centrum IoT. Utworzono aplikację, która wyświetla hello komunikatów odebranych przez Centrum IoT hello.

toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:

* [Łączenie urządzenia][lnk-connect-device]
* [Wprowadzenie do zarządzania urządzeniami][lnk-device-management]
* [Getting started with IoT Edge][lnk-iot-edge] (Wprowadzenie do usługi IoT Edge)

toolearn tooextend IoT rozwiązanie i procesu urządzenia do chmury wiadomości na dużą skalę, zobacz temat hello [przetwarzania komunikatów urządzenia do chmury] [ lnk-process-d2c-tutorial] samouczka.

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
