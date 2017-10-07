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
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a>Przetwarzanie wiadomości urządzenia do chmury Centrum IoT przy użyciu tras (.NET)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

W tym samouczku opiera się na powitania [Rozpoczynanie pracy z Centrum IoT] samouczka. Samouczek Hello:

* Pokazuje, jak toouse routing zasady toodispatch urządzenia do chmury wiadomości w sposób łatwy, na podstawie konfiguracji.
* Pokazuje, jak tooisolate interakcyjne komunikaty, które wymagają natychmiastowego działania z rozwiązania hello zaplecza dla dalszego przetwarzania. Na przykład urządzenie może wysłać komunikat alarmu, które wyzwala Wstawianie biletu do systemu CRM. Z kolei wiadomości punktu danych, takich jak telemetrii temperatury źródła danych do aparatu analizy.

Na końcu hello tego samouczka możesz uruchomić trzech aplikacji konsoli .NET:

* **SimulatedDevice**, zmodyfikowanej wersji aplikacji hello utworzone w hello [Rozpoczynanie pracy z Centrum IoT] samouczek wysyła komunikaty urządzenia do chmury punktu danych co sekundę i interaktywne urządzenia do chmury wiadomości co 10 Liczba sekund.
* **ReadDeviceToCloudMessages** czy wyświetla hello niekrytyczne telemetrii wysyłane przez aplikację na urządzeniu.
* **ReadCriticalQueue** usuwania kolejki hello krytycznych wiadomości wysyłane przez aplikację urządzenia z kolejki usługi Service Bus. Kolejka jest dołączona toohello Centrum IoT.

> [!NOTE]
> Centrum IoT obsługuje zestawu SDK dla wielu platform urządzeń i języków, w tym C, Java i JavaScript. toolearn tooreplace hello symulowane urządzenie z tego samouczka z urządzenia fizycznego, zobacz hello [Azure IoT Developer Center].

toocomplete tego samouczka należy hello następujące:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Aktywne konto platformy Azure. <br/>Jeśli nie masz konta, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/) w zaledwie kilka minut.

Powinien mieć niektóre podstawową wiedzę na temat [usługi Azure Storage] i [Azure Service Bus].

## <a name="send-interactive-messages"></a>Wysyłanie komunikatów interakcyjne

Modyfikowanie aplikacji urządzenia hello utworzony w hello [Rozpoczynanie pracy z Centrum IoT] toooccasionally samouczka wysyłać interaktywnego.

W programie Visual Studio w hello **SimulatedDevice** projekt, Zastąp hello `SendDeviceToCloudMessagesAsync` metody z hello następującego kodu:

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

Ta metoda losowo dodaje właściwość hello `"level": "critical"` toomessages wysyłane przez urządzenie hello, która symuluje komunikat, który wymaga natychmiastowego działania przez hello zaplecza rozwiązania. aplikacji urządzenia Hello przekazuje informacje w oknie dialogowym właściwości wiadomość hello zamiast, w treści wiadomości powitania, dzięki tym Centrum IoT można kierować docelowy prawidłowego komunikatu toohello wiadomość hello.

> [!NOTE]
> Można użyć komunikatów właściwości tooroute komunikatów dla różnych scenariuszy, w tym przetwarzania dodatkowo toohello hot ścieżki przykładzie chłodni path.

> [!NOTE]
> Dla zapewnienia hello prostotę w tym samouczku nie implementuje wszystkie zasady ponawiania. W kodzie produkcyjnym, należy zaimplementować zasady ponawiania wykładniczego wycofywania, zgodnie z sugestią podaną w artykuł w witrynie MSDN hello np. [obsługi błędów przejściowych].

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a>Kolejka tooa wiadomości trasy w Centrum IoT

W tej sekcji omówiono następujące zagadnienia:

* Tworzenie kolejki usługi Service Bus.
* Podłącz je tooyour Centrum IoT.
* Skonfiguruj IoT Centrum toosend wiadomości toohello kolejki na podstawie obecności hello właściwości na wiadomość powitania.

Aby uzyskać więcej informacji o sposobie tooprocess komunikaty z kolejek usługi Service Bus, zobacz [Rozpoczynanie pracy z kolejkami][Service Bus queue].

1. Tworzenie kolejki usługi Service Bus, zgodnie z opisem w [Rozpoczynanie pracy z kolejkami][Service Bus queue]. Kolejka Hello musi być w hello tej samej subskrypcji i regionu co Centrum IoT. Zanotuj nazwę przestrzeni nazw i kolejki hello.

    > [!NOTE]
    > Tematy dotyczące używany jako punkty końcowe Centrum IoT nie może mieć i kolejek usługi Service Bus **sesji** lub **wykrywania duplikatów** włączone. Jeśli dowolna z tych opcji są włączone, hello punkt końcowy jest wyświetlany jako **informujący** w hello portalu Azure.

2. Witaj w portalu Azure, Otwórz Centrum IoT i kliknij przycisk **punkty końcowe**.
    
    ![Punkty końcowe Centrum IoT][30]

3. W hello **punkty końcowe** bloku, kliknij przycisk **Dodaj** na hello top tooadd Centrum IoT tooyour kolejki. Punkt końcowy hello nazwa **CriticalQueue** i użyj hello listach rozwijanych tooselect **kolejki usługi Service Bus**hello przestrzeń nazw magistrali usług, w której znajduje się kolejki i hello nazwę kolejki. Gdy wszystko będzie gotowe, kliknij przycisk **zapisać** u dołu hello.
    
    ![Dodawanie punktu końcowego][31]
    
4. Teraz kliknij **tras** w Centrum IoT. Kliknij przycisk **Dodaj** u góry hello toocreate bloku hello reguły routingu kieruje komunikaty toohello kolejki można tylko dodać. Wybierz **DeviceTelemetry** hello źródłem danych. Wprowadź `level="critical"` hello warunkiem i wybierz polecenie kolejki hello właśnie został dodany jako punkt końcowy niestandardowych jako hello punkt końcowy reguły routingu. Gdy wszystko będzie gotowe, kliknij przycisk **zapisać** u dołu hello.
    
    ![Dodawanie trasy][32]
    
    Upewnij się, że trasy rezerwowy hello ustawiono zbyt**ON**. Ta wartość jest hello domyślną konfigurację Centrum IoT.
    
    ![Trasy rezerwowej][33]

## <a name="read-from-hello-queue-endpoint"></a>Odczyt z hello punkt końcowy z kolejki

W tej sekcji można odczytywać wiadomości powitania hello punkt końcowy z kolejki.

1. W programie Visual Studio, Visual C# pulpitu systemu Windows klasycznego toohello bieżącego rozwiązania projektu, należy dodać przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu. Nazwa projektu hello **ReadCriticalQueue**.

2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **ReadCriticalQueue** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**. Ta operacja wyświetla hello **Menedżera pakietów NuGet** okna.

3. Wyszukaj **WindowsAzure.ServiceBus**, kliknij przycisk **zainstalować**i zaakceptuj warunki użytkowania hello. Ta operacja pliki do pobrania, instaluje i dodaje toohello odwołanie do usługi Azure Service Bus ze wszystkimi zależnościami.

4. Dodaj następujące hello **przy użyciu** instrukcji u góry hello hello **Program.cs** pliku:
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. Na koniec należy dodać następujące wiersze toohello hello **Main** metody. Zastąp hello ciągu połączenia za pomocą **nasłuchiwania** uprawnień dla kolejki hello:
   
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

## <a name="run-hello-applications"></a>Uruchamianie aplikacji hello
Teraz wszystko jest gotowe toorun hello aplikacji.

1. W programie Visual Studio w Eksploratorze rozwiązań kliknij rozwiązanie prawym przyciskiem myszy i wybierz **Ustaw projekty startowe**. Wybierz **wiele projektów startowych**, a następnie wybierz pozycję **Start** jako akcję hello hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, i **ReadCriticalQueue** projektów.
2. Naciśnij klawisz **F5** toostart hello trzech aplikacji konsoli. Witaj **ReadDeviceToCloudMessages** aplikacja ma tylko niekrytyczne komunikatów wysyłanych z hello **SimulatedDevice** aplikacji i hello **ReadCriticalQueue** aplikacja ma tylko krytycznych wiadomości.
   
   ![Trzy aplikacje konsoli][50]

## <a name="next-steps"></a>Następne kroki
W tym samouczku przedstawiono sposób tooreliably wysyłania wiadomości urządzenia do chmury przy użyciu funkcji routingu wiadomość hello Centrum IoT.

Witaj [jak komunikaty toosend chmury do urządzenia z Centrum IoT] [ lnk-c2d] pokazuje, jak toosend wiadomości tooyour przez urządzenia z zaplecza rozwiązania.

Przykłady toosee kompletnych rozwiązań end-to-end korzystających z Centrum IoT, zobacz [pakiet IoT Azure][lnk-suite].

toolearn więcej informacji na temat tworzenia rozwiązań z Centrum IoT, zobacz hello [Centrum IoT — przewodnik dewelopera].

Zobacz toolearn więcej informacji na temat routing komunikatów w Centrum IoT [wysyłania i odbierania wiadomości z Centrum IoT][lnk-devguide-messaging].

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
