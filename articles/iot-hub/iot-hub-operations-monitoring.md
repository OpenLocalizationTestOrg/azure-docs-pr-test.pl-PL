---
title: monitorowanie operacji centrum IoT aaaAzure | Dokumentacja firmy Microsoft
description: "Sposób działania Centrum IoT Azure toouse monitorowania toomonitor hello stanu operacji w Centrum IoT w czasie rzeczywistym."
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a>Monitorowanie operacji centrum IoT

Monitorowanie operacji centrum IoT umożliwia toomonitor hello stanu operacji w Centrum IoT w czasie rzeczywistym. Centrum IoT śledzi zdarzenia przez różne kategorie działań. Można włączyć do wysyłania zdarzeń z jednego lub więcej kategorii tooan punktu końcowego Centrum IoT do przetwarzania. Możesz monitorować dane hello błędów lub konfigurowanie bardziej złożonych przetwarzania na podstawie wzorców danych.

Centrum IoT monitoruje sześć kategorii zdarzeń:

* Operacje tożsamości urządzenia
* Telemetrii urządzenia
* Komunikaty chmury do urządzenia
* Połączenia
* Przekazywania plików
* Rozsyłanie wiadomości

## <a name="how-tooenable-operations-monitoring"></a>Jak operacje tooenable monitorowania

1. Tworzenie Centrum IoT. Instrukcje można znaleźć na temat toocreate Centrum IoT w hello [wprowadzenie] [ lnk-get-started] przewodnik.

1. Otwiera blok hello Centrum IoT. Z tego miejsca, kliknij przycisk **operacje monitorowania**.

    ![Monitorowanie konfiguracji w portalu hello operacje związane z dostępem][1]

1. Wybierz hello monitorowania kategorii ma toomonitor, a następnie kliknij przycisk **zapisać**. Witaj zdarzenia są dostępne do odczytu z punktu końcowego hello zgodnego Centrum zdarzeń na liście **ustawienia monitorowania**. Witaj punktu końcowego Centrum IoT jest nazywany `messages/operationsmonitoringevents`.

    ![Skonfiguruj operacje monitorowania na Centrum IoT][2]

> [!NOTE]
> Wybieranie **pełne** monitorowania hello **połączeń** category powoduje, że Centrum IoT toogenerate komunikaty dodatkowych diagnostyczne. Dla wszystkich innych kategoriach hello **pełne** zawiera zmiany ustawień hello ilość informacji Centrum IoT w każdy komunikat o błędzie.

## <a name="event-categories-and-how-toouse-them"></a>Kategorie zdarzeń i w jaki sposób toouse ich

Każdy operacje monitorowania śledzi kategorii ma inny typ interakcji z Centrum IoT i każda kategoria monitorowania schematu definiującego struktury zdarzenia w tej kategorii.

### <a name="device-identity-operations"></a>Operacje tożsamości urządzenia

Kategoria operacje tożsamości urządzenia Hello śledzi błędów występujących podczas próby toocreate, zaktualizować lub usunąć wpis w rejestrze tożsamości Centrum IoT. Ta kategoria śledzenia jest przydatne w przypadku inicjowania obsługi scenariuszy.

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a>Telemetrii urządzenia

Kategoria telemetrii urządzenia Hello śledzi błędów, które występują w Centrum IoT hello a są powiązane toohello telemetrii potoku. Ta kategoria zawiera błędy występujące podczas wysyłania zdarzenia telemetrii (takie jak dławienie) i odbieranie zdarzeń telemetrii (np. czytnik nieautoryzowanych). Ta kategoria nie może przechwycić błędów spowodowanych przez kod działający na powitania urządzeniu.

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a>Polecenia chmury do urządzenia

Kategoria polecenia chmury do urządzenia Hello śledzi błędów, które występują w Centrum IoT hello a są powiązane toohello komunikatu chmura urządzenie potoku. Ta kategoria zawiera błędy występujące podczas wysyłania wiadomości chmury do urządzenia (takich jak nieautoryzowanego nadawcę), odbierania wiadomości chmury do urządzenia (takich jak przekroczona liczba dostarczania) i odbieranie komunikatu chmura urządzenie opinii (takie jak opinii wygasł). Ta kategoria nie przechwytuje błędy z urządzenia, które nieprawidłowo obsługuje komunikatu chmura urządzenie, jeśli został pomyślnie dostarczony wiadomości powitania chmury do urządzenia.

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a>Połączenia

Kategoria połączenia Hello śledzi błędów występujących podczas urządzeń Połącz lub Rozłącz z Centrum IoT. Śledzenie tej kategorii jest przydatne do identyfikowania próby nieautoryzowanego połączenia i śledzenia, gdy połączenie zostanie przerwane dla urządzeń w zakresie łączności niska.

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a>Przekazywania plików

Kategoria przekazywania pliku Hello śledzi błędów, które występują w Centrum IoT hello a są powiązane toofile funkcji przekazywania. Ta kategoria zawiera:

* Błędy, które występują w przypadku hello identyfikatora URI połączenia SAS, takie jak kiedy wygasa przed urządzenia powiadamia Centrum hello ukończone przekazywania.
* Zgłoszone przez urządzenie hello przekazywania nie powiodło się.
* Błędy występujące po plik nie zostanie znaleziony w magazynie podczas tworzenia komunikatu powiadomienia Centrum IoT.

Ta kategoria nie może przechwycić błędów, które są wykonywane bezpośrednio, gdy urządzenie hello jest przekazywanie toostorage pliku.

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a>Rozsyłanie wiadomości

Kategoria routingu wiadomość Hello śledzi błędów występujących podczas oceny trasy wiadomości i punktu końcowego kondycję postrzegane przez Centrum IoT. Ta kategoria zawiera zdarzenia, np. gdy reguła zwraca zbyt "undefined", gdy Centrum IoT oznacza punkt końcowy jako wiadomości i innych błędów, odbierane z punktu końcowego. Ta kategoria nie ma określonego błędy dotyczące wiadomości powitania się (na przykład urządzenie ograniczania błędy), które zostały zgłoszone w kategorii "telemetrii urządzenia" hello.

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a>Wyświetl wydarzenia

Można użyć hello *explorer Centrum iothub* tooquickly narzędzie test, że Centrum IoT generuje monitorowania zdarzeń. Witaj tooinstall narzędzie, zobacz instrukcje hello hello [explorer Centrum iothub] [ lnk-iothub-explorer] repozytorium GitHub.

1. Upewnij się, że hello **połączeń** monitorowania kategorii ustawiono zbyt**pełne** w portalu hello.

1. W wierszu polecenia Uruchom hello poniższych poleceń tooread z hello punkt końcowy monitorowania:

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. W innego wiersza polecenia Uruchom następujące polecenie toosimulate hello urządzenia wysyłania wiadomości urządzenia do chmury:

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. pierwszy wiersz polecenia Hello przedstawiono zdarzenia monitorowania hello hello symulowane urządzenie łączy tooyour Centrum IoT.

## <a name="connect-toohello-monitoring-endpoint"></a>Połącz toohello punkt końcowy monitorowania

Witaj, monitorowanie punktu końcowego w Centrum IoT jest punktem końcowym zgodnego Centrum zdarzeń. Można użyć dowolnego mechanizm, który współpracuje z usługi Event Hubs tooread monitorowania wiadomości z tego punktu końcowego. Witaj poniższy przykład tworzy podstawowe reader, który nie jest odpowiedni dla wdrożenia wysokiej przepływności. Aby uzyskać więcej informacji dotyczących sposobu tooprocess komunikaty z usługi Event Hubs, zobacz hello [Rozpoczynanie pracy z usługą Event Hubs] [ lnk-eventhubs-tutorial] samouczka.

tooconnect toohello punkt końcowy monitorowania, należy nazwa punktu końcowego i hello ciąg połączenia. Hello następujące kroki przedstawiają sposób toofind hello niezbędnych wartości w portalu hello:

1. W portalu hello Przejdź tooyour bloku zasobów Centrum IoT.

1. Wybierz **operacje monitorowania**i zanotuj hello **nazwę Centrum zdarzeń zgodnych** i **punktu końcowego Centrum zdarzeń zgodnych** wartości:

    ![Wartości punktu końcowego zgodnych z Centrum zdarzeń][img-endpoints]

1. Wybierz **zasady dostępu współużytkowanego**, a następnie wybierz **usługi**. Zanotuj hello **klucz podstawowy** wartość:

    ![Klucz podstawowy zasady dostępu współdzielonego usługi][img-service-key]

Witaj Poniższy przykładowy kod C# jest pobierana z programu Visual Studio **Windows Desktop klasycznego** aplikacji konsolowej C#. Projekt Hello ma hello **WindowsAzure.ServiceBus** zainstalowany pakiet NuGet.

* Zastąp symbol zastępczy parametrów połączenia hello ciąg połączenia, który używa hello **punktu końcowego Centrum zdarzeń zgodnych** i usługa **klucz podstawowy** wartości zanotowany wcześniej, jak pokazano poniżej hello przykład:

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* Zastąp hello monitorowania symbol zastępczy Nazwa punktu końcowego hello **nazwę Centrum zdarzeń zgodnych** wartość zanotowany wcześniej.

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a>Następne kroki
toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Przewodnik dewelopera Centrum IoT][lnk-devguide]
* [Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md