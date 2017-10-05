---
title: "Wysyłanie zdarzeń do środowiska usługi Azure Time Series Insights | Microsoft Docs"
description: "Ten samouczek przedstawia kroki wypychania zdarzeń do środowiska usługi Time Series Insights"
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
ms.openlocfilehash: b4ef96a045393f28b3cd750068fe82a5a8411afa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="send-events-to-a-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="9c8ab-103">Wysyłanie zdarzeń do środowiska usługi Time Series Insights za pomocą centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="9c8ab-103">Send events to a Time Series Insights environment using event hub</span></span>

<span data-ttu-id="9c8ab-104">W tym samouczku wyjaśniono, jak utworzyć i skonfigurować centrum zdarzeń oraz jak uruchomić przykładową aplikację do wypychania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-104">This tutorial explains how to create and configure event hub and run a sample application to push events.</span></span> <span data-ttu-id="9c8ab-105">Jeśli masz już centrum zdarzeń, które zawiera zdarzenia w formacie JSON, możesz pominąć ten samouczek i wyświetlić swoje środowisko, korzystając z [wglądu w dane szeregów czasowych](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9c8ab-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="9c8ab-106">Konfigurowanie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="9c8ab-106">Configure an event hub</span></span>
1. <span data-ttu-id="9c8ab-107">Aby utworzyć centrum zdarzeń, wykonaj instrukcje zawarte w [dokumentacji](https://docs.microsoft.com/azure/event-hubs/event-hubs-create) centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-107">To create an event hub, follow instructions from the Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="9c8ab-108">Upewnij się, że utworzona grupa odbiorców jest używana wyłącznie przez źródło zdarzeń usługi Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9c8ab-109">Sprawdź, czy ta grupa odbiorców nie jest używana przez żadną inną usługę (np. zadanie usługi Stream Analytics lub drugie środowisko usługi Time Series Insights).</span><span class="sxs-lookup"><span data-stu-id="9c8ab-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="9c8ab-110">Używanie grupy odbiorców przez inne usługi ma negatywny wpływ na operacje odczytu w bieżącym środowisku i tych usługach.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-110">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="9c8ab-111">Użycie grupy odbiorców „$Default” może potencjalnie spowodować jej ponowne użycie przez inne czytniki.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-111">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

  ![Wybieranie grupy odbiorców centrum zdarzeń](media/send-events/consumer-group.png)

3. <span data-ttu-id="9c8ab-113">W centrum zdarzeń utwórz zasady „Moje_zasady_wysyłania”, które w poniższym przykładzie w języku csharp będą używane do wysyłania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-113">On the event hub, create “MySendPolicy” that is used to send events in the csharp sample.</span></span>

  ![Wybieranie zasad dostępu współdzielonego i klikanie przycisku Dodaj](media/send-events/shared-access-policy.png)  

  ![Dodawanie nowej zasady dostępu współdzielonego](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="9c8ab-116">Tworzenie źródła zdarzeń usługi Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="9c8ab-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="9c8ab-117">Jeśli nie utworzono źródła zdarzeń, postępuj zgodnie z [tymi instrukcjami](time-series-insights-add-event-source.md), aby je utworzyć.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) to create an event source.</span></span>

2. <span data-ttu-id="9c8ab-118">Wpisz „deviceTimestamp” jako nazwę właściwości sygnatury czasowej — właściwość ta jest używana w przykładzie w języku csharp jako rzeczywista sygnatura czasowa.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-118">Specify “deviceTimestamp” as the timestamp property name – this property is used as the actual timestamp in the csharp sample.</span></span> <span data-ttu-id="9c8ab-119">W nazwie właściwości sygnatury czasowej jest uwzględniana wielkość liter. Wartości wysyłane do centrum zdarzeń jako dane JSON muszą mieć format __rrrr-MM-ddTGG:mm:ss.FFFFFFFK__.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-119">The timestamp property name is case-sensitive and values must follow the format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON to event hub.</span></span> <span data-ttu-id="9c8ab-120">Jeśli w zdarzeniu nie ma tej właściwości, używany jest czas umieszczenia zdarzenia w kolejce w centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-120">If the property does not exist in the event, then the event hub enqueued time is used.</span></span>

  ![Tworzenie źródła zdarzeń](media/send-events/event-source-1.png)

## <a name="sample-code-to-push-events"></a><span data-ttu-id="9c8ab-122">Przykładowy kod umożliwiający wypychanie zdarzeń</span><span class="sxs-lookup"><span data-stu-id="9c8ab-122">Sample code to push events</span></span>
1. <span data-ttu-id="9c8ab-123">Przejdź do zasad centrum zdarzeń „Moje_zasady_wysyłania” i skopiuj parametry połączenia z kluczem zasad.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-123">Go to the event hub policy “MySendPolicy” and copy the connection string with the policy key.</span></span>

  ![Kopiowanie parametrów połączenia Moja_zasada_wysyłania](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="9c8ab-125">Uruchom poniższy kod, który umożliwia wysyłanie 600 zdarzeń do każdego z trzech urządzeń.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-125">Run the following code that to send 600 events per each of the three devices.</span></span> <span data-ttu-id="9c8ab-126">Zaktualizuj zmienną `eventHubConnectionString` przy użyciu parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-126">Update `eventHubConnectionString` with your connection string.</span></span>

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

                // Send JSON to event hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="9c8ab-127">Obsługiwane kształty JSON</span><span class="sxs-lookup"><span data-stu-id="9c8ab-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="9c8ab-128">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="9c8ab-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="9c8ab-129">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="9c8ab-129">Input</span></span>

<span data-ttu-id="9c8ab-130">Prosty obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="9c8ab-131">Dane wyjściowe — jedno zdarzenie</span><span class="sxs-lookup"><span data-stu-id="9c8ab-131">Output - 1 event</span></span>

|<span data-ttu-id="9c8ab-132">id</span><span class="sxs-lookup"><span data-stu-id="9c8ab-132">id</span></span>|<span data-ttu-id="9c8ab-133">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="9c8ab-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="9c8ab-134">device1</span><span class="sxs-lookup"><span data-stu-id="9c8ab-134">device1</span></span>|<span data-ttu-id="9c8ab-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="9c8ab-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="9c8ab-136">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="9c8ab-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="9c8ab-137">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="9c8ab-137">Input</span></span>
<span data-ttu-id="9c8ab-138">Tablica JSON z dwoma obiektami JSON.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="9c8ab-139">Każdy obiekt JSON zostanie przekształcony na zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-139">Each JSON object will be converted to an event.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="9c8ab-140">Dane wyjściowe — dwa zdarzenia</span><span class="sxs-lookup"><span data-stu-id="9c8ab-140">Output - 2 Events</span></span>

|<span data-ttu-id="9c8ab-141">id</span><span class="sxs-lookup"><span data-stu-id="9c8ab-141">id</span></span>|<span data-ttu-id="9c8ab-142">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="9c8ab-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="9c8ab-143">device1</span><span class="sxs-lookup"><span data-stu-id="9c8ab-143">device1</span></span>|<span data-ttu-id="9c8ab-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="9c8ab-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="9c8ab-145">device2</span><span class="sxs-lookup"><span data-stu-id="9c8ab-145">device2</span></span>|<span data-ttu-id="9c8ab-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="9c8ab-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="9c8ab-147">Przykład 3</span><span class="sxs-lookup"><span data-stu-id="9c8ab-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="9c8ab-148">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="9c8ab-148">Input</span></span>

<span data-ttu-id="9c8ab-149">Obiekt JSON z zagnieżdżoną tablicą JSON zawierającą dwa obiekty JSON.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="9c8ab-150">Dane wyjściowe — dwa zdarzenia</span><span class="sxs-lookup"><span data-stu-id="9c8ab-150">Output - 2 Events</span></span>
<span data-ttu-id="9c8ab-151">Zwróć uwagę na to, że właściwość „location” jest kopiowana do każdego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-151">Note that the property "location" is copied over to each of the event.</span></span>

|<span data-ttu-id="9c8ab-152">location</span><span class="sxs-lookup"><span data-stu-id="9c8ab-152">location</span></span>|<span data-ttu-id="9c8ab-153">events.id</span><span class="sxs-lookup"><span data-stu-id="9c8ab-153">events.id</span></span>|<span data-ttu-id="9c8ab-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="9c8ab-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="9c8ab-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="9c8ab-155">WestUs</span></span>|<span data-ttu-id="9c8ab-156">device1</span><span class="sxs-lookup"><span data-stu-id="9c8ab-156">device1</span></span>|<span data-ttu-id="9c8ab-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="9c8ab-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="9c8ab-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="9c8ab-158">WestUs</span></span>|<span data-ttu-id="9c8ab-159">device2</span><span class="sxs-lookup"><span data-stu-id="9c8ab-159">device2</span></span>|<span data-ttu-id="9c8ab-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="9c8ab-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="9c8ab-161">Przykład 4</span><span class="sxs-lookup"><span data-stu-id="9c8ab-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="9c8ab-162">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="9c8ab-162">Input</span></span>

<span data-ttu-id="9c8ab-163">Obiekt JSON z zagnieżdżoną tablicą JSON zawierającą dwa obiekty JSON.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="9c8ab-164">Te dane wejściowe pokazują, że globalne właściwości mogą być reprezentowane przez złożony obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="9c8ab-164">This input demonstrates that the global properties may be represented by the complex JSON object.</span></span>

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
#### <a name="output---2-events"></a><span data-ttu-id="9c8ab-165">Dane wyjściowe — dwa zdarzenia</span><span class="sxs-lookup"><span data-stu-id="9c8ab-165">Output - 2 Events</span></span>

|<span data-ttu-id="9c8ab-166">location</span><span class="sxs-lookup"><span data-stu-id="9c8ab-166">location</span></span>|<span data-ttu-id="9c8ab-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="9c8ab-167">manufacturer.name</span></span>|<span data-ttu-id="9c8ab-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="9c8ab-168">manufacturer.location</span></span>|<span data-ttu-id="9c8ab-169">events.id</span><span class="sxs-lookup"><span data-stu-id="9c8ab-169">events.id</span></span>|<span data-ttu-id="9c8ab-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="9c8ab-170">events.timestamp</span></span>|<span data-ttu-id="9c8ab-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="9c8ab-171">events.data.type</span></span>|<span data-ttu-id="9c8ab-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="9c8ab-172">events.data.units</span></span>|<span data-ttu-id="9c8ab-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="9c8ab-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="9c8ab-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="9c8ab-174">WestUs</span></span>|<span data-ttu-id="9c8ab-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="9c8ab-175">manufacturer1</span></span>|<span data-ttu-id="9c8ab-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="9c8ab-176">EastUs</span></span>|<span data-ttu-id="9c8ab-177">device1</span><span class="sxs-lookup"><span data-stu-id="9c8ab-177">device1</span></span>|<span data-ttu-id="9c8ab-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="9c8ab-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="9c8ab-179">pressure</span><span class="sxs-lookup"><span data-stu-id="9c8ab-179">pressure</span></span>|<span data-ttu-id="9c8ab-180">psi</span><span class="sxs-lookup"><span data-stu-id="9c8ab-180">psi</span></span>|<span data-ttu-id="9c8ab-181">108.09</span><span class="sxs-lookup"><span data-stu-id="9c8ab-181">108.09</span></span>|
|<span data-ttu-id="9c8ab-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="9c8ab-182">WestUs</span></span>|<span data-ttu-id="9c8ab-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="9c8ab-183">manufacturer1</span></span>|<span data-ttu-id="9c8ab-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="9c8ab-184">EastUs</span></span>|<span data-ttu-id="9c8ab-185">device2</span><span class="sxs-lookup"><span data-stu-id="9c8ab-185">device2</span></span>|<span data-ttu-id="9c8ab-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="9c8ab-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="9c8ab-187">vibration</span><span class="sxs-lookup"><span data-stu-id="9c8ab-187">vibration</span></span>|<span data-ttu-id="9c8ab-188">abs G</span><span class="sxs-lookup"><span data-stu-id="9c8ab-188">abs G</span></span>|<span data-ttu-id="9c8ab-189">217.09</span><span class="sxs-lookup"><span data-stu-id="9c8ab-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="9c8ab-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9c8ab-190">Next steps</span></span>

* <span data-ttu-id="9c8ab-191">Wyświetlanie środowiska w [Portalu usługi Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="9c8ab-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
