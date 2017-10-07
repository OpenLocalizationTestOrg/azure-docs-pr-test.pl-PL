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
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="d1c33-103">Wyślij środowiska czasu serii Insights tooa zdarzeń przy użyciu Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="d1c33-103">Send events tooa Time Series Insights environment using event hub</span></span>

<span data-ttu-id="d1c33-104">Ten samouczek wyjaśnia sposób toocreate i konfigurowania Centrum zdarzeń i uruchamiania toopush aplikacji przykładowej zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d1c33-104">This tutorial explains how toocreate and configure event hub and run a sample application toopush events.</span></span> <span data-ttu-id="d1c33-105">Jeśli masz już centrum zdarzeń, które zawiera zdarzenia w formacie JSON, możesz pominąć ten samouczek i wyświetlić swoje środowisko, korzystając z [wglądu w dane szeregów czasowych](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d1c33-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="d1c33-106">Konfigurowanie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="d1c33-106">Configure an event hub</span></span>
1. <span data-ttu-id="d1c33-107">toocreate Centrum zdarzeń, wykonaj instrukcje z hello Centrum zdarzeń [dokumentacji](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span><span class="sxs-lookup"><span data-stu-id="d1c33-107">toocreate an event hub, follow instructions from hello Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="d1c33-108">Upewnij się, że utworzona grupa odbiorców jest używana wyłącznie przez źródło zdarzeń usługi Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="d1c33-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d1c33-109">Sprawdź, czy ta grupa odbiorców nie jest używana przez żadną inną usługę (np. zadanie usługi Stream Analytics lub drugie środowisko usługi Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="d1c33-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="d1c33-110">Jeśli grupy odbiorców jest używany przez inne usługi, odczytać negatywny wpływ na operację dla tego środowiska i hello innych usług.</span><span class="sxs-lookup"><span data-stu-id="d1c33-110">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="d1c33-111">Jeśli używasz "$Default" jako grupy odbiorców hello, połączenie może prowadzić ponownemu toopotential przez inne czytników.</span><span class="sxs-lookup"><span data-stu-id="d1c33-111">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

  ![Wybieranie grupy odbiorców centrum zdarzeń](media/send-events/consumer-group.png)

3. <span data-ttu-id="d1c33-113">Utwórz "MySendPolicy" na powitania Centrum zdarzeń, czyli toosend używane zdarzenia w przykładowym csharp hello.</span><span class="sxs-lookup"><span data-stu-id="d1c33-113">On hello event hub, create “MySendPolicy” that is used toosend events in hello csharp sample.</span></span>

  ![Wybieranie zasad dostępu współdzielonego i klikanie przycisku Dodaj](media/send-events/shared-access-policy.png)  

  ![Dodawanie nowej zasady dostępu współdzielonego](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="d1c33-116">Tworzenie źródła zdarzeń usługi Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="d1c33-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="d1c33-117">Jeśli nie utworzono źródło zdarzeń, wykonaj [tych instrukcji](time-series-insights-add-event-source.md) toocreate źródła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d1c33-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) toocreate an event source.</span></span>

2. <span data-ttu-id="d1c33-118">Określ "deviceTimestamp" jako nazwy właściwości sygnatury czasowej hello — ta właściwość jest używana jako hello rzeczywiste sygnatury czasowej w przykładowym csharp hello.</span><span class="sxs-lookup"><span data-stu-id="d1c33-118">Specify “deviceTimestamp” as hello timestamp property name – this property is used as hello actual timestamp in hello csharp sample.</span></span> <span data-ttu-id="d1c33-119">Nazwa właściwości sygnatury czasowej Hello jest rozróżniana wielkość liter i wartości musi być zgodny hello format __RRRR-MM-Ddtgg. FFFFFFFK__ wysłany jako koncentrator tooevent JSON.</span><span class="sxs-lookup"><span data-stu-id="d1c33-119">hello timestamp property name is case-sensitive and values must follow hello format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON tooevent hub.</span></span> <span data-ttu-id="d1c33-120">Jeśli właściwość hello nie istnieje w przypadku hello, następnie hello czasu umieszczonych w kolejce Centrum zdarzeń jest używany.</span><span class="sxs-lookup"><span data-stu-id="d1c33-120">If hello property does not exist in hello event, then hello event hub enqueued time is used.</span></span>

  ![Tworzenie źródła zdarzeń](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a><span data-ttu-id="d1c33-122">Przykładowy kod toopush zdarzeń</span><span class="sxs-lookup"><span data-stu-id="d1c33-122">Sample code toopush events</span></span>
1. <span data-ttu-id="d1c33-123">Przejdź zasady Centrum zdarzeń toohello "MySendPolicy" i skopiuj parametry połączenia hello kluczem hello zasad.</span><span class="sxs-lookup"><span data-stu-id="d1c33-123">Go toohello event hub policy “MySendPolicy” and copy hello connection string with hello policy key.</span></span>

  ![Kopiowanie parametrów połączenia Moja_zasada_wysyłania](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="d1c33-125">Uruchom hello następującego kodu tego zdarzenia toosend 600 każdego z trzech hello urządzeń.</span><span class="sxs-lookup"><span data-stu-id="d1c33-125">Run hello following code that toosend 600 events per each of hello three devices.</span></span> <span data-ttu-id="d1c33-126">Zaktualizuj zmienną `eventHubConnectionString` przy użyciu parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="d1c33-126">Update `eventHubConnectionString` with your connection string.</span></span>

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
## <a name="supported-json-shapes"></a><span data-ttu-id="d1c33-127">Obsługiwane kształty JSON</span><span class="sxs-lookup"><span data-stu-id="d1c33-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="d1c33-128">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="d1c33-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="d1c33-129">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="d1c33-129">Input</span></span>

<span data-ttu-id="d1c33-130">Prosty obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="d1c33-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="d1c33-131">Dane wyjściowe — jedno zdarzenie</span><span class="sxs-lookup"><span data-stu-id="d1c33-131">Output - 1 event</span></span>

|<span data-ttu-id="d1c33-132">id</span><span class="sxs-lookup"><span data-stu-id="d1c33-132">id</span></span>|<span data-ttu-id="d1c33-133">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="d1c33-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="d1c33-134">device1</span><span class="sxs-lookup"><span data-stu-id="d1c33-134">device1</span></span>|<span data-ttu-id="d1c33-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="d1c33-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="d1c33-136">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="d1c33-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="d1c33-137">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="d1c33-137">Input</span></span>
<span data-ttu-id="d1c33-138">Tablica JSON z dwoma obiektami JSON.</span><span class="sxs-lookup"><span data-stu-id="d1c33-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="d1c33-139">Poszczególne obiekty JSON będą przekonwertowane tooan zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d1c33-139">Each JSON object will be converted tooan event.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="d1c33-140">Dane wyjściowe — dwa zdarzenia</span><span class="sxs-lookup"><span data-stu-id="d1c33-140">Output - 2 Events</span></span>

|<span data-ttu-id="d1c33-141">id</span><span class="sxs-lookup"><span data-stu-id="d1c33-141">id</span></span>|<span data-ttu-id="d1c33-142">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="d1c33-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="d1c33-143">device1</span><span class="sxs-lookup"><span data-stu-id="d1c33-143">device1</span></span>|<span data-ttu-id="d1c33-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="d1c33-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="d1c33-145">device2</span><span class="sxs-lookup"><span data-stu-id="d1c33-145">device2</span></span>|<span data-ttu-id="d1c33-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="d1c33-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="d1c33-147">Przykład 3</span><span class="sxs-lookup"><span data-stu-id="d1c33-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="d1c33-148">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="d1c33-148">Input</span></span>

<span data-ttu-id="d1c33-149">Obiekt JSON z zagnieżdżoną tablicą JSON zawierającą dwa obiekty JSON.</span><span class="sxs-lookup"><span data-stu-id="d1c33-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="d1c33-150">Dane wyjściowe — dwa zdarzenia</span><span class="sxs-lookup"><span data-stu-id="d1c33-150">Output - 2 Events</span></span>
<span data-ttu-id="d1c33-151">Należy pamiętać, że właściwość hello "Lokalizacja" jest kopiowana za pośrednictwem tooeach hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d1c33-151">Note that hello property "location" is copied over tooeach of hello event.</span></span>

|<span data-ttu-id="d1c33-152">location</span><span class="sxs-lookup"><span data-stu-id="d1c33-152">location</span></span>|<span data-ttu-id="d1c33-153">events.id</span><span class="sxs-lookup"><span data-stu-id="d1c33-153">events.id</span></span>|<span data-ttu-id="d1c33-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="d1c33-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="d1c33-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="d1c33-155">WestUs</span></span>|<span data-ttu-id="d1c33-156">device1</span><span class="sxs-lookup"><span data-stu-id="d1c33-156">device1</span></span>|<span data-ttu-id="d1c33-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="d1c33-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="d1c33-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="d1c33-158">WestUs</span></span>|<span data-ttu-id="d1c33-159">device2</span><span class="sxs-lookup"><span data-stu-id="d1c33-159">device2</span></span>|<span data-ttu-id="d1c33-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="d1c33-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="d1c33-161">Przykład 4</span><span class="sxs-lookup"><span data-stu-id="d1c33-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="d1c33-162">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="d1c33-162">Input</span></span>

<span data-ttu-id="d1c33-163">Obiekt JSON z zagnieżdżoną tablicą JSON zawierającą dwa obiekty JSON.</span><span class="sxs-lookup"><span data-stu-id="d1c33-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="d1c33-164">Tych danych wejściowych pokazuje, że hello globalnych właściwości mogą być reprezentowane przez obiekt JSON złożony hello.</span><span class="sxs-lookup"><span data-stu-id="d1c33-164">This input demonstrates that hello global properties may be represented by hello complex JSON object.</span></span>

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
#### <a name="output---2-events"></a><span data-ttu-id="d1c33-165">Dane wyjściowe — dwa zdarzenia</span><span class="sxs-lookup"><span data-stu-id="d1c33-165">Output - 2 Events</span></span>

|<span data-ttu-id="d1c33-166">location</span><span class="sxs-lookup"><span data-stu-id="d1c33-166">location</span></span>|<span data-ttu-id="d1c33-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="d1c33-167">manufacturer.name</span></span>|<span data-ttu-id="d1c33-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="d1c33-168">manufacturer.location</span></span>|<span data-ttu-id="d1c33-169">events.id</span><span class="sxs-lookup"><span data-stu-id="d1c33-169">events.id</span></span>|<span data-ttu-id="d1c33-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="d1c33-170">events.timestamp</span></span>|<span data-ttu-id="d1c33-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="d1c33-171">events.data.type</span></span>|<span data-ttu-id="d1c33-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="d1c33-172">events.data.units</span></span>|<span data-ttu-id="d1c33-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="d1c33-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="d1c33-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="d1c33-174">WestUs</span></span>|<span data-ttu-id="d1c33-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="d1c33-175">manufacturer1</span></span>|<span data-ttu-id="d1c33-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="d1c33-176">EastUs</span></span>|<span data-ttu-id="d1c33-177">device1</span><span class="sxs-lookup"><span data-stu-id="d1c33-177">device1</span></span>|<span data-ttu-id="d1c33-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="d1c33-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="d1c33-179">pressure</span><span class="sxs-lookup"><span data-stu-id="d1c33-179">pressure</span></span>|<span data-ttu-id="d1c33-180">psi</span><span class="sxs-lookup"><span data-stu-id="d1c33-180">psi</span></span>|<span data-ttu-id="d1c33-181">108.09</span><span class="sxs-lookup"><span data-stu-id="d1c33-181">108.09</span></span>|
|<span data-ttu-id="d1c33-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="d1c33-182">WestUs</span></span>|<span data-ttu-id="d1c33-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="d1c33-183">manufacturer1</span></span>|<span data-ttu-id="d1c33-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="d1c33-184">EastUs</span></span>|<span data-ttu-id="d1c33-185">device2</span><span class="sxs-lookup"><span data-stu-id="d1c33-185">device2</span></span>|<span data-ttu-id="d1c33-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="d1c33-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="d1c33-187">vibration</span><span class="sxs-lookup"><span data-stu-id="d1c33-187">vibration</span></span>|<span data-ttu-id="d1c33-188">abs G</span><span class="sxs-lookup"><span data-stu-id="d1c33-188">abs G</span></span>|<span data-ttu-id="d1c33-189">217.09</span><span class="sxs-lookup"><span data-stu-id="d1c33-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="d1c33-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1c33-190">Next steps</span></span>

* <span data-ttu-id="d1c33-191">Wyświetlanie środowiska w [Portalu usługi Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d1c33-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
