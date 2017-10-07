---
title: "aaaSend zdarzenia tooAzure Insights serii czasu środowiska | Dokumentacja firmy Microsoft"
description: "Ten samouczek obejmuje hello kroki toopush zdarzenia tooyour Insights serii czasu środowiska"
keywords: 
services: tsi
documentationcenter: 
author: venkatgct
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: venkatja
ms.openlocfilehash: dbccc23f61351a0033cd48c1a02fb3841b45d560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a>Wyślij środowiska czasu serii Insights tooa zdarzeń przy użyciu Centrum zdarzeń

Ten samouczek wyjaśnia sposób toocreate i konfigurowania Centrum zdarzeń i uruchamiania toopush aplikacji przykładowej zdarzenia. Jeśli masz już centrum zdarzeń, które zawiera zdarzenia w formacie JSON, możesz pominąć ten samouczek i wyświetlić swoje środowisko, korzystając z [wglądu w dane szeregów czasowych](https://insights.timeseries.azure.com).

## <a name="configure-an-event-hub"></a>Konfigurowanie centrum zdarzeń
1. toocreate Centrum zdarzeń, wykonaj instrukcje z hello Centrum zdarzeń [dokumentacji](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).

2. Upewnij się, że utworzona grupa odbiorców jest używana wyłącznie przez źródło zdarzeń usługi Time Series Insights.

  > [!IMPORTANT]
  > Sprawdź, czy ta grupa odbiorców nie jest używana przez żadną inną usługę (np. zadanie usługi Stream Analytics lub drugie środowisko usługi Time Series Insights). Jeśli grupy odbiorców jest używany przez inne usługi, odczytać negatywny wpływ na operację dla tego środowiska i hello innych usług. Jeśli używasz "$Default" jako grupy odbiorców hello, połączenie może prowadzić ponownemu toopotential przez inne czytników.

  ![Wybieranie grupy odbiorców centrum zdarzeń](media/send-events/consumer-group.png)

3. Utwórz "MySendPolicy" na powitania Centrum zdarzeń, czyli toosend używane zdarzenia w przykładowym csharp hello.

  ![Wybieranie zasad dostępu współdzielonego i klikanie przycisku Dodaj](media/send-events/shared-access-policy.png)  

  ![Dodawanie nowej zasady dostępu współdzielonego](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a>Tworzenie źródła zdarzeń usługi Time Series Insights
1. Jeśli nie utworzono źródło zdarzeń, wykonaj [tych instrukcji](time-series-insights-add-event-source.md) toocreate źródła zdarzenia.

2. Określ "deviceTimestamp" jako nazwy właściwości sygnatury czasowej hello — ta właściwość jest używana jako hello rzeczywiste sygnatury czasowej w przykładowym csharp hello. Nazwa właściwości sygnatury czasowej Hello jest rozróżniana wielkość liter i wartości musi być zgodny hello format __RRRR-MM-Ddtgg. FFFFFFFK__ wysłany jako koncentrator tooevent JSON. Jeśli właściwość hello nie istnieje w przypadku hello, następnie hello czasu umieszczonych w kolejce Centrum zdarzeń jest używany.

  ![Tworzenie źródła zdarzeń](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a>Przykładowy kod toopush zdarzeń
1. Przejdź zasady Centrum zdarzeń toohello "MySendPolicy" i skopiuj parametry połączenia hello kluczem hello zasad.

  ![Kopiowanie parametrów połączenia Moja_zasada_wysyłania](media/send-events/sample-code-connection-string.png)

2. Uruchom hello następującego kodu tego zdarzenia toosend 600 każdego z trzech hello urządzeń. Zaktualizuj zmienną `eventHubConnectionString` przy użyciu parametrów połączenia.

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using Microsoft.ServiceBus.Messaging;

namespace Microsoft.Rdx.DataGenerator
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var from = new DateTime(2017, 4, 20, 15, 0, 0, DateTimeKind.Utc);
            Random r = new Random();
            const int numberOfEvents = 600;

            var deviceIds = new[] { "device1", "device2", "device3" };

            var events = new List<string>();
            for (int i = 0; i < numberOfEvents; ++i)
            {
                for (int device = 0; device < deviceIds.Length; ++device)
                {
                    // Generate event and serialize as JSON object:
                    // { "deviceTimestamp": "utc timestamp", "deviceId": "guid", "value": 123.456 }
                    events.Add(
                        String.Format(
                            CultureInfo.InvariantCulture,
                            @"{{ ""deviceTimestamp"": ""{0}"", ""deviceId"": ""{1}"", ""value"": {2} }}",
                            (from + TimeSpan.FromSeconds(i * 30)).ToString("o"),
                            deviceIds[device],
                            r.NextDouble()));
                }
            }

            // Create event hub connection.
            var eventHubConnectionString = @"Endpoint=sb://...";
            var eventHubClient = EventHubClient.CreateFromConnectionString(eventHubConnectionString);

            using (var ms = new MemoryStream())
            using (var sw = new StreamWriter(ms))
            {
                // Wrap events into JSON array:
                sw.Write("[");
                for (int i = 0; i < events.Count; ++i)
                {
                    if (i > 0)
                    {
                        sw.Write(',');
                    }
                    sw.Write(events[i]);
                }
                sw.Write("]");

                sw.Flush();
                ms.Position = 0;

                // Send JSON tooevent hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a>Obsługiwane kształty JSON
### <a name="sample-1"></a>Przykład 1

#### <a name="input"></a>Dane wejściowe

Prosty obiekt JSON.

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a>Dane wyjściowe — jedno zdarzenie

|id|sygnatura czasowa|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|

### <a name="sample-2"></a>Przykład 2

#### <a name="input"></a>Dane wejściowe
Tablica JSON z dwoma obiektami JSON. Poszczególne obiekty JSON będą przekonwertowane tooan zdarzeń.
```json
[
    {
        "id":"device1",
        "timestamp":"2016-01-08T01:08:00Z"
    },
    {
        "id":"device2",
        "timestamp":"2016-01-17T01:17:00Z"
    }
]
```
#### <a name="output---2-events"></a>Dane wyjściowe — dwa zdarzenia

|id|sygnatura czasowa|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|
|device2|2016-01-08T01:17:00Z|
### <a name="sample-3"></a>Przykład 3

#### <a name="input"></a>Dane wejściowe

Obiekt JSON z zagnieżdżoną tablicą JSON zawierającą dwa obiekty JSON.
```json
{
    "location":"WestUs",
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z"
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z"
        }
    ]
}

```
#### <a name="output---2-events"></a>Dane wyjściowe — dwa zdarzenia
Należy pamiętać, że właściwość hello "Lokalizacja" jest kopiowana za pośrednictwem tooeach hello zdarzenia.

|location|events.id|events.timestamp|
|--------|---------------|----------------------|
|WestUs|device1|2016-01-08T01:08:00Z|
|WestUs|device2|2016-01-08T01:17:00Z|

### <a name="sample-4"></a>Przykład 4

#### <a name="input"></a>Dane wejściowe

Obiekt JSON z zagnieżdżoną tablicą JSON zawierającą dwa obiekty JSON. Tych danych wejściowych pokazuje, że hello globalnych właściwości mogą być reprezentowane przez obiekt JSON złożony hello.

```json
{
    "location":"WestUs",
    "manufacturer":{
        "name":"manufacturer1",
        "location":"EastUs"
    },
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z",
            "data":{
                "type":"pressure",
                "units":"psi",
                "value":108.09
            }
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z",
            "data":{
                "type":"vibration",
                "units":"abs G",
                "value":217.09
            }
        }
    ]
}
```
#### <a name="output---2-events"></a>Dane wyjściowe — dwa zdarzenia

|location|manufacturer.name|manufacturer.location|events.id|events.timestamp|events.data.type|events.data.units|events.data.value|
|---|---|---|---|---|---|---|---|
|WestUs|manufacturer1|EastUs|device1|2016-01-08T01:08:00Z|pressure|psi|108.09|
|WestUs|manufacturer1|EastUs|device2|2016-01-08T01:17:00Z|vibration|abs G|217.09|

## <a name="next-steps"></a>Następne kroki

* Wyświetlanie środowiska w [Portalu usługi Time Series Insights](https://insights.timeseries.azure.com)
